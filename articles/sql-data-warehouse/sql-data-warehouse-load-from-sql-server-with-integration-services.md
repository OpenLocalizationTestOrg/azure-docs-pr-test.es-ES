---
title: datos de aaaLoad de SQL Server en almacenamiento de datos de SQL Azure (SSIS) | Documentos de Microsoft
description: "Muestra cómo toocreate datos de toomove paquete SQL Server Integration Services (SSIS) desde una gran variedad de datos de orígenes tooSQL almacenamiento de datos."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: cakarst;douglasl;barbkess
ms.openlocfilehash: bb28a08807a5b07832b85f2f074c2acf912c1dc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a>Carga de datos de SQL Server en Almacenamiento de datos SQL de Azure (SSIS)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

Crear datos de SQL Server Integration Services (SSIS) paquete tooload de SQL Server en almacenamiento de datos de SQL Azure. Si lo desea puede reestructurar, transformar y limpiar los datos de hello cuando pasan a través del flujo de datos SSIS Hola.

En este tutorial, aprenderá lo siguiente:

* Crear un proyecto de Integration Services en Visual Studio.
* Conectar orígenes de toodata, como SQL Server (como un origen) y almacenamiento de datos de SQL (como un destino).
* Diseñar un paquete SSIS que carga datos de origen de hello en destino Hola.
* Hola SSIS paquete tooload Hola datos de ejecución.

Este tutorial utiliza SQL Server como origen de datos de Hola. SQL Server se puede estar ejecutando en el entorno local o en una máquina virtual de Azure.

## <a name="basic-concepts"></a>Conceptos básicos
paquete de Hello es Hola unidad de trabajo en SSIS. Los paquetes relacionados se agrupan en proyectos. Los proyectos se crean y los paquetes se diseñan en Visual Studio con SQL Server Data Tools. diseño de Hello es un proceso visual en el que arrastrar y colocar los componentes de la superficie de diseño de toohello de cuadro de herramientas de hello, conectarlos y establecer sus propiedades. Después de finalizar el paquete, puede, opcionalmente, implementarla tooSQL servidor de administración completa, la supervisión y la seguridad.

## <a name="options-for-loading-data-with-ssis"></a>Opciones para cargar datos con SSIS
SQL Server Integration Services (SSIS) es un conjunto flexible de herramientas que proporciona un abanico de opciones para conectarse a datos y cargarlos en Almacenamiento de datos SQL.

1. Utilice un tooSQL de tooconnect almacenamiento de datos de destino de ADO NET. Este tutorial usa un destino de ADO NET porque tiene Hola menor número de opciones de configuración.
2. Utilice un tooSQL de tooconnect almacenamiento de datos de destino de OLE DB. Esta opción puede proporcionar un rendimiento ligeramente mejor que Hola destino de ADO NET.
3. Usar datos de Hola de toostage de hello tarea de carga de blobs de Azure en almacenamiento de blobs de Azure. A continuación, utilice Hola SSIS ejecutar SQL tarea toolaunch una secuencia de comandos de Polybase que carga datos de hello en almacenamiento de datos SQL. Esta opción proporciona mejor rendimiento de Hola de hello tres opciones se muestran aquí. Hola tooget tarea carga de blobs de Azure, descargue hello [Microsoft SQL Server 2016 Integration Services Feature Pack para Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]. toolearn más información acerca de Polybase, consulte [Guía de PolyBase][PolyBase Guide].

## <a name="before-you-start"></a>Antes de comenzar
toostep a través de este tutorial, necesitará:

1. **SQL Server Integration Services (SSIS)**. SSIS es un componente de SQL Server y requiere una versión de evaluación o una versión con licencia de SQL Server. tooget una versión de evaluación de SQL Server 2016 Preview, consulte [SQL Server evaluaciones][SQL Server Evaluations].
2. **Visual Studio**. tooget Hola edición gratuita de Visual Studio Community, consulte [Visual Studio Community][Visual Studio Community].
3. **SQL Server Data Tools para Visual Studio (SSDT)**. tooget SQL Server Data Tools para Visual Studio, vea [descargar SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].
4. **Datos de ejemplo**. Este tutorial usa datos de ejemplo que se almacenan en SQL Server en la base de datos de ejemplo de AdventureWorks de hello como Hola toobe de datos de origen cargado en el almacén de datos de SQL. Hola tooget base de datos de ejemplo de AdventureWorks, vea [bases de datos de ejemplo de AdventureWorks 2014][AdventureWorks 2014 Sample Databases].
5. **Una base de datos de Almacenamiento de datos SQL y permisos**. Este tutorial conecta la instancia de almacenamiento de datos SQL de tooa y carga datos en él. Tiene una tabla y tooload datos toohave permisos toocreate.
6. **Una regla de firewall**. Tiene toocreate una regla de firewall en el almacén de datos de SQL con la dirección IP de hello del equipo local antes de cargar datos toohello almacenamiento de datos SQL.

## <a name="step-1-create-a-new-integration-services-project"></a>Paso 1: Creación de un proyecto de Integration Services
1. Inicie Visual Studio.
2. En hello **archivo** menú, seleccione **nuevo | Proyecto**.
3. Navegue toohello **instalado | Plantillas | Business Intelligence | Servicios de integración** tipos de proyecto.
4. Seleccione **Proyecto de Integration Services**. Proporcione los valores de **Nombre** y **Ubicación**, y seleccione **Aceptar**.

Se abre Visual Studio y se crea un proyecto de Integration Services (SSIS). A continuación, Visual Studio abre diseñador Hola Hola único nuevo paquete de SSIS (Package.dtsx) en proyecto Hola. Vea Hola siguientes áreas de la pantalla:

* Hola izquierda, Hola **cuadro de herramientas** de componentes SSIS.
* En el centro de hello, Hola superficie de diseño, con múltiples fichas. Normalmente se utiliza al menos hello **flujo de Control** hello y **de flujo de datos** pestañas.
* En Hola derecho Hola **el Explorador de soluciones** hello y **propiedades** paneles.
  
    ![][01]

## <a name="step-2-create-hello-basic-data-flow"></a>Paso 2: Crear el flujo de datos básicos de Hola
1. Arrastre una tarea de flujo de datos desde el centro de toohello de cuadro de herramientas de Hola de superficie de diseño de hello (en hello **flujo de Control** ficha).
   
    ![][02]
2. Haga doble clic en la pestaña flujo de datos de hello tarea flujo de datos tooswitch toohello.
3. En lista de otros orígenes de Hola Hola cuadro de herramientas, arrastre una superficie de diseño de toohello de origen de ADO.NET. Con el adaptador de origen de hello aún seleccionado, cambie su nombre demasiado**origen de SQL Server** en hello **propiedades** panel.
4. En lista de otros destinos de Hola Hola cuadro de herramientas, arrastre una superficie de diseño de ADO.NET, destino toohello en hello origen ADO.NET. Con el adaptador de destino de hello aún seleccionado, cambie su nombre demasiado**destino de almacenamiento de datos de SQL** en hello **propiedades** panel.
   
    ![][09]

## <a name="step-3-configure-hello-source-adapter"></a>Paso 3: Configurar el adaptador de origen de Hola
1. Haga doble clic en Hola de hello origen adaptador tooopen **Editor de origen de ADO.NET**.
   
    ![][03]
2. En hello **Connection Manager** ficha de hello **Editor de origen de ADO.NET**, haga clic en hello **New** toohello siguiente botón **Administrador de conexiones de ADO.NET**Hola de lista tooopen **configurar el Administrador de conexión de ADO.NET** diálogo cuadro y crear la configuración de conexión de base de datos de SQL Server de Hola desde el que este tutorial carga los datos.
   
    ![][04]
3. Hola **configurar el Administrador de conexión de ADO.NET** diálogo cuadro, haga clic en hello **nuevo** Hola de botón tooopen **Connection Manager** diálogo cuadro y crear una nueva conexión de datos.
   
    ![][05]
4. Hola **Connection Manager** diálogo cuadro, Hola siguientes cosas.
   
   1. Para **proveedor**, seleccione Hola SqlClient Data Provider.
   2. Para **nombre del servidor**, escriba el nombre de SQL Server de Hola.
   3. Hola **toohello servidor de inicio de sesión** sección, seleccione o escriba la información de autenticación.
   4. Hola **base de datos de Connect tooa** sección, seleccione la base de datos de ejemplo de AdventureWorks de Hola.
   5. Haga clic en **Probar conexión**.
      
       ![][06]
   6. En el cuadro de diálogo de Hola que informa sobre los resultados de Hola de prueba de conexión de hello, haga clic en **Aceptar** tooreturn toohello **Connection Manager** cuadro de diálogo.
   7. Hola **Connection Manager** cuadro de diálogo, haga clic en **Aceptar** tooreturn toohello **configurar el Administrador de conexión de ADO.NET** cuadro de diálogo.
5. Hola **configurar el Administrador de conexión de ADO.NET** cuadro de diálogo, haga clic en **Aceptar** tooreturn toohello **Editor de origen de ADO.NET**.
6. Hola **Editor de origen de ADO.NET**, Hola **nombre de tabla de Hola o vista de hello** lista, seleccione hello **Sales.SalesOrderDetail** tabla.
   
    ![][07]
7. Haga clic en **vista previa** toosee Hola 200 primeras filas de datos de tabla de origen de Hola Hola **vista previa Query Results** cuadro de diálogo.
   
    ![][08]
8. Hola **vista previa Query Results** cuadro de diálogo, haga clic en **cerrar** tooreturn toohello **Editor de origen de ADO.NET**.
9. Hola **Editor de origen de ADO.NET**, haga clic en **Aceptar** toofinish Configurar origen de datos de Hola.

## <a name="step-4-connect-hello-source-adapter-toohello-destination-adapter"></a>Paso 4: Conecte el adaptador de destino de hello origen adaptador toohello
1. Seleccione el adaptador de origen de hello en la superficie de diseño de Hola.
2. Seleccione la flecha azul Hola que abarca desde el adaptador de origen de Hola y arrástrelo toohello editor de destino hasta que ajuste en su lugar.
   
    ![][10]
   
    En un paquete SSIS típico, use un número de otros componentes de hello cuadro de herramientas de SSIS entre el origen de Hola y Hola destino toorestructure, transformación y limpiar los datos cuando pasan a través del flujo de datos SSIS Hola. tookeep este ejemplo tan simple como sea posible, se estamos conexión Hola directamente origen toohello destino.

## <a name="step-5-configure-hello-destination-adapter"></a>Paso 5: Configurar el adaptador de destino de Hola
1. Haga doble clic en Hola Hola de tooopen de adaptador de destino **Editor de destino de ADO.NET**.
   
    ![][11]
2. En hello **Connection Manager** ficha de hello **Editor de destino de ADO.NET**, haga clic en hello **New** toohello siguiente botón **Administrador de conexiones**Hola de lista tooopen **configurar el Administrador de conexión de ADO.NET** diálogo cuadro y crear la configuración de conexión de base de datos de almacenamiento de datos de SQL Azure de hello en el que este tutorial carga los datos.
3. Hola **configurar el Administrador de conexión de ADO.NET** diálogo cuadro, haga clic en hello **nuevo** Hola de botón tooopen **Connection Manager** diálogo cuadro y crear una nueva conexión de datos.
4. Hola **Connection Manager** diálogo cuadro, Hola siguientes cosas.
   1. Para **proveedor**, seleccione Hola SqlClient Data Provider.
   2. Para **nombre del servidor**, escriba el nombre de almacén de datos SQL de Hola.
   3. Hola **toohello servidor de inicio de sesión** sección, seleccione **autenticación de uso de SQL Server** y escriba la información de autenticación.
   4. Hola **base de datos de Connect tooa** sección, seleccione una base de datos de almacenamiento de datos SQL existente.
   5. Haga clic en **Probar conexión**.
   6. En el cuadro de diálogo de Hola que informa sobre los resultados de Hola de prueba de conexión de hello, haga clic en **Aceptar** tooreturn toohello **Connection Manager** cuadro de diálogo.
   7. Hola **Connection Manager** cuadro de diálogo, haga clic en **Aceptar** tooreturn toohello **configurar el Administrador de conexión de ADO.NET** cuadro de diálogo.
5. Hola **configurar el Administrador de conexión de ADO.NET** cuadro de diálogo, haga clic en **Aceptar** tooreturn toohello **Editor de destino de ADO.NET**.
6. Hola **Editor de destino de ADO.NET**, haga clic en **New** toohello siguiente **usan una tabla o vista** Hola de lista tooopen **Create Table** cuadro de diálogo toocreate una nueva tabla de destino con una lista de columnas que coincide con la tabla de origen de Hola.
   
    ![][12a]
7. Hola **Create Table** diálogo cuadro, Hola siguientes cosas.
   
   1. Cambiar nombre de Hola de tabla de destino de hello demasiado**SalesOrderDetail**.
   2. Quitar hello **rowguid** columna. Hola **uniqueidentifier** no se admite el tipo de datos en el almacén de datos de SQL.
   3. Cambiar tipo de datos de Hola de hello **LineTotal** columna demasiado**dinero**. Hola **decimal** no se admite el tipo de datos en el almacén de datos de SQL. Para información sobre los tipos de datos compatibles, consulte [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)] [CREATE TABLE (SQL Data Warehouse de Azure, Almacenamiento de datos paralelos)].
      
       ![][12b]
   4. Haga clic en **Aceptar** toocreate Hola tabla y devuelven toohello **Editor de destino de ADO.NET**.
8. Hola **Editor de destino de ADO.NET**, seleccione hello **asignaciones** ficha toosee cómo las columnas de origen de hello asignan toocolumns en destino Hola.
   
    ![][13]
9. Haga clic en **Aceptar** toofinish Configurar origen de datos de Hola.

## <a name="step-6-run-hello-package-tooload-hello-data"></a>Paso 6: Ejecutar Hola paquete tooload Hola de datos
Paquete de hello ejecución haciendo clic en hello **iniciar** botón de barra de herramientas de Hola o seleccionando una de hello **ejecutar** opciones en hello **depurar** menú.

Paquete de hello comienza toorun, ve amarillo ruedas de giro tooindicate actividad, así como número de Hola de filas procesadas hasta ahora.

![][14]

Cuando el paquete de hello ha terminado de ejecutarse, se vea marcas de verificación verdes tooindicate correcto así como Hola número total de filas de datos cargados desde origen toohello destino de Hola.

![][15]

¡Enhorabuena! Ha usado correctamente datos de SQL Server Integration Services tooload en almacenamiento de datos de SQL Azure.

## <a name="next-steps"></a>Pasos siguientes
* Más información acerca del flujo de datos SSIS Hola. Comience aquí: [Flujo de datos][Data Flow].
* Obtenga información acerca de cómo toodebug y solucionar problemas de la derecha de paquetes en el entorno de diseño de Hola. Comience aquí: [Herramientas para solucionar problemas con el desarrollo de paquetes][Troubleshooting Tools for Package Development].
* Obtenga información acerca de cómo la toodeploy su SSIS proyectos y paquetes tooIntegration tooanother o servidor de servicios de ubicación de almacenamiento. Comience aquí: [Implementación de proyectos y paquetes][Deployment of Projects and Packages].

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
