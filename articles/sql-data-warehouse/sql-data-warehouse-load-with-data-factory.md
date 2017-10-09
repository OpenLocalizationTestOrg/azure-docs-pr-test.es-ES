---
title: "datos de aaaLoad en almacenamiento de datos de SQL Azure: factoría de datos | Documentos de Microsoft"
description: Este tutorial carga datos en almacenamiento de datos de SQL Azure mediante Data Factory de Azure y utiliza una base de datos de SQL Server como origen de datos de Hola.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a>Carga de datos en SQL Data Warehouse con Data Factory

Puede usar datos de tooload de Data Factory de Azure en almacenamiento de datos de SQL Azure desde cualquiera de hello [admite almacenes de datos de origen](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats). Por ejemplo, puede cargar datos desde una base de datos SQL de Azure o una base de datos de Oracle en una instancia de SQL Data Warehouse mediante Data Factory. Tutorial en este artículo muestra cómo tooload datos desde un servidor local de SQL base de datos en un almacén de datos SQL.

**Estimación del tiempo**: este tutorial tarda aproximadamente 10-15 minutos toocomplete una vez que se cumplen los requisitos previos de Hola.

## <a name="prerequisites"></a>Requisitos previos

- Necesita un **base de datos de SQL Server** con tablas que contienen datos de hello toobe copió toohello almacenamiento de datos SQL.  

- Necesita una instancia en línea de **SQL Data Warehouse**. Si no dispone de un almacén de datos, obtenga información acerca de cómo demasiado[para crear un almacén de datos de SQL Azure](sql-data-warehouse-get-started-provision.md).

- Debe tener una **cuenta de Azure Storage**. Si no dispone de una cuenta de almacenamiento, obtenga información acerca de cómo demasiado[crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md). Para mejorar el rendimiento, busque la cuenta de almacenamiento de Hola y almacenamiento de datos de Hola Hola misma región de Azure.

## <a name="configure-a-data-factory"></a>Configuración de una factoría de datos
1. Inicie sesión en toohello [portal de Azure][].
2. Localice el almacén de datos y haga clic en tooopen se.
3. En la hoja principal de hello, haga clic en **carga datos** > **Data Factory de Azure**.

    ![Inicio del Asistente para cargar datos](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. Si no tiene una factoría de datos en su suscripción de Azure, verá un **factoría de datos** cuadro de diálogo en una pestaña independiente del explorador de Hola. Hola, rellene la información solicitada y haga clic en **crear**. Después de crea la factoría de datos de hello, Hola **factoría de datos** cierra el cuadro de diálogo y ver hello **factoría de datos seleccione** cuadro de diálogo.

    Si tiene una o varias fábricas de datos ya se encuentran en hello suscripción de Azure, vea hello **factoría de datos seleccione** cuadro de diálogo. En este cuadro de diálogo, puede seleccionar un generador de datos existente o haga clic en **crear nuevo generador de datos** toocreate uno nuevo.

    ![Configurar Data Factory](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. Hola **factoría de datos seleccione** cuadro de diálogo, hello **cargar datos** opción está activada de forma predeterminada. Haga clic en **siguiente** toostart crear una tarea de carga de datos.

## <a name="configure-hello-data-factory-properties"></a>Configurar las propiedades de generador de datos de Hola
Ahora que ha creado una factoría de datos, paso siguiente hello es programación al cargar los datos tooconfigure Hola.

1. En **Nombre de la tarea**, escriba **DWLoadData-fromSQLServer**.
2. Usar valor predeterminado de hello **ejecutar una vez ahora** opción, haga clic en **siguiente**.

    ![Configuración de la programación de carga](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a>Configurar el almacén de datos de origen de Hola y puerta de enlace
Ahora, saber la factoría de datos acerca de la base de datos SQL de hello local desde el que desea que los datos de tooload.

1. Elija **SQL Server** de datos de origen de hello admitida almacenar catálogo y haga clic en **siguiente**.

    ![Selección del origen de SQL Server](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. A **base de datos de SQL Server de especificar Hola local** aparece el cuadro de diálogo. Hola primero **nombre de la conexión** campo está rellenado automático. segundo campo de Hello pide nombre Hola de hello **puerta de enlace**. Si está utilizando un generador de datos existente que ya tiene una puerta de enlace, puede volver a usar la puerta de enlace de hello, selecciónelo en la lista desplegable de Hola. Haga clic en hello **crear puerta de enlace** vincular toocreate Data Management Gateway.  

    > [!NOTE]
    > Si el almacén de datos de origen de hello es local o en una máquina virtual de IaaS de Azure, se requiere una puerta de enlace de administración de datos. Una puerta de enlace tiene una relación de 1 a 1 con una factoría de datos. No se puede usar desde otro generador de datos, pero se puede utilizar por varias tareas con Hola de carga de datos misma factoría de datos. Una puerta de enlace puede ser usado tooconnect toomultiple los almacenes de datos cuando se ejecuta tareas de carga de datos.
    >
    > Para obtener información detallada acerca de la puerta de enlace de hello, consulte [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) artículo.

3. Se mostrará el cuadro de diálogo **Crear puerta de enlace**. En Nombre, escriba **GatewayForDWLoading**y haga clic en **Crear**.

4. Se mostrará el cuadro de diálogo **Configure Gateway** (Configurar puerta de enlace). Haga clic en **iniciar el programa de instalación rápida en este equipo** tooautomatically descargar, instalar y registrar Data Management Gateway en el equipo actual. Hola progreso se muestra en una ventana emergente. Si la máquina de hello no puede conectar el almacén de datos de toohello, puede preparar manualmente [descargar e instalar la puerta de enlace de hello](https://www.microsoft.com/download/details.aspx?id=39717) en un equipo que se puede conectar datos toohello almacenar y, a continuación, usar tooregister clave Hola.
    > [!NOTE]
    > el programa de instalación rápida de Hello funciona de forma nativa con Microsoft Edge e Internet Explorer. Si está usando Google Chrome, instale primero la extensión de ClickOnce de Hola de almacén web de Chrome.

    ![Inicio de la configuración rápida](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. Espere a que toocomplete de instalación de puerta de enlace de Hola. Una vez que la puerta de enlace de Hola se ha registrado correctamente y está en línea, se cierra la ventana emergente de Hola y nueva puerta de enlace de hello aparece en el campo de la puerta de enlace de Hola. A continuación, rellene el resto de hello campos obligatorios como se indica a continuación, a continuación, haga clic en **siguiente**.
    - **Nombre del servidor**: nombre del programa Hola a SQL Server local.
    - **Nombre de la base de datos**: la base de datos de SQL Server.
    - **Cifrado de credenciales**: usar valor predeterminado de hello "por el explorador web".
    - **Tipo de autenticación**: elija Hola tipo de autenticación que usa.
    - **Nombre de usuario** y **contraseña**: escriba Hola nombre de usuario y una contraseña para un usuario que tiene permiso toocopy Hola datos.

    ![Inicio de la configuración rápida](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. Hola siguiente paso es tablas de hello toochoose de los datos de hello toocopy. Puede filtrar las tablas de hello mediante palabras clave. Y puede obtener una vista previa de esquema de datos y tabla de hello en el panel inferior Hola. Después de finalizar la selección, haga clic en **Siguiente**.

    ![Selección de tablas](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a>Configurar el destino de hello, el almacenamiento de datos de SQL

Ahora se explíquenos factoría de datos de información de destino de Hola.

1. La información de conexión de SQL Data Warehouse se rellenará automáticamente. Escriba la contraseña de Hola Hola nombre de usuario. y haga clic en **Siguiente**.

    ![Configuración del destino](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. Una asignación de tabla inteligente aparece que asigna origen toodestination, basándose en los nombres de tabla. Si no existe la tabla de hello en el destino de hello, de forma predeterminada ADF creará uno con hello mismo nombre (Esto aplica tooSQL servidor o base de datos de SQL de Azure como origen). También puede elegir tabla de toomap tooan existente. Revise la información y haga clic en **Siguiente**.

    ![Asignación de tablas](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. Revise la asignación de esquema de Hola y busque mensajes de error o advertencia. La asignación inteligente se basa en el nombre de las columnas. Si se produce una conversión de tipo de datos no compatibles entre la columna de origen y destino de hello, verá un mensaje de error junto a la tabla correspondiente de Hola. Si elige automático de la factoría de datos de toolet crear tablas de hello, conversión de tipos de datos apropiados puede ocurrir si es necesario incompatibilidad de hello toofix entre los almacenes de origen y de destino.

    ![Esquema de asignación](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. Haga clic en **Siguiente**.

## <a name="configure-hello-performance-settings"></a>Configurar opciones de rendimiento de Hola
En configuraciones de rendimiento de hello, configure una cuenta de almacenamiento de Azure utilizada para almacenar provisionalmente los datos de hello antes de que se carga en el modo más eficaz de almacenamiento de datos SQL usando [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly). Después de realiza la copia de hello, datos provisionales de hello en el almacenamiento se limpiarán automáticamente.

Seleccione una cuenta de Azure Storage y haga clic en **Siguiente**.

![Configuración del blob de almacenamiento provisional](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a>Revise la información de resumen e implementar la canalización de Hola

Revise la configuración de Hola y haga clic en **finalizar** canalización de botón toodeploy Hola.

![Implementación de la factoría de datos](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a>Supervisión del progreso de carga de datos

Puede ver el progreso de la implementación de Hola y resultados en hello **implementación** página.

1. Una vez que se realice la implementación de hello, haga clic en el vínculo Hola que dice **haga clic aquí canalización de copia de toomonitor** toomonitor progreso al cargar los datos.

    ![Supervisión de la canalización](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. Hola recién creado **DWLoadData fromSQLServer** canalización de carga de datos es automático seleccionado de hello izquierdo **Resource Explorer**.

    ![Visualización de la canalización](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. Haga clic en la canalización de hello en medio de Hola Hola de toosee panel Estado detallado de cada tabla que asigna tooan actividad.

    ![Visualización de la actividad de tabla](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. Haga clic en más de una actividad y ver detalles en el panel derecho de hello incluido el tamaño de los datos, filas, rendimiento, etcetera la carga de datos de Hola.

    ![Visualización de la información de actividad de tabla](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. toolaunch esta supervisión vista posterior, vaya tooyour almacenamiento de datos de SQL, haga clic en ejecutar **carga datos > Data Factory de Azure**, seleccione la fábrica y elija **supervisar existente cargar tareas**.

## <a name="next-steps"></a>Pasos siguientes

toomigrate su tooSQL base de datos del almacén de datos, vea [información general de migración](sql-data-warehouse-overview-migrate.md).

toolearn más información acerca de Data Factory de Azure y sus capacidades de movimiento de datos, vea Hola siguientes artículos:

- [Introducción tooAzure factoría de datos](../data-factory/data-factory-introduction.md)
- [Movimiento de datos con la actividad de copia](../data-factory/data-factory-data-movement-activities.md)
- [Mover datos tooand de almacenamiento de datos de SQL Azure mediante Data Factory de Azure](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

tooexplore los datos en el almacén de datos de SQL, vea Hola siguientes artículos:

- [Conectar tooSQL almacenamiento de datos con Visual Studio como SSDT](sql-data-warehouse-query-visual-studio.md)
- [Datos visuales con Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).

<!-- Azure references -->
[portal de Azure]: https://portal.azure.com
