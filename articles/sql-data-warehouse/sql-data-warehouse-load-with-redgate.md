---
title: almacenamiento de datos de Azure de aaaUse Redgate tooload datos tooyour | Documentos de Microsoft
description: "Obtenga información acerca de cómo Studio del toouse Redgate de plataforma de datos para escenarios de almacenamiento de datos."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a>Carga de datos con Redgate's Data Platform Studio
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)
> * [Factoría de datos](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

Este tutorial muestra cómo toouse [datos plataforma Studio del Redgate](http://www.red-gate.com/products/azure-development/data-platform-studio/) datos de toomove (DP) desde un tooAzure de SQL Server local almacenamiento de datos SQL. Studio de la plataforma de datos aplica correcciones de compatibilidad más adecuadas de Hola y optimizaciones, por lo que tiene más rápido Hola tooget de manera que se inició con almacenamiento de datos de SQL.

> [!NOTE]
> [Redgate](http://www.red-gate.com) es un experimentado asociado de Microsoft que ofrece diversas herramientas de SQL Server. Esta característica de Data Platform Studio está disponible gratuitamente para uso comercial y no comercial.
> 
> 

## <a name="before-you-begin"></a>Antes de empezar
### <a name="create-or-identify-resources"></a>Creación o identificación de recursos
Antes de iniciar este tutorial, necesita toohave:

* **base de datos de SQL Server local**: Hola datos que desea tooimport tooSQL almacenamiento de datos necesita toocome desde un servidor local de SQL (versión 2008R2 o superior). Data Platform Studio no puede importar datos directamente desde Azure SQL Database ni desde archivos de texto.
* **Cuenta de almacenamiento de Azure**: datos de hello en el almacenamiento de blobs de Azure cree etapas en Studio de la plataforma de datos antes de cargarlos en el almacén de datos SQL. cuenta de almacenamiento de Hello debe utilizar modelo de implementación de "Administrador de recursos" hello (valor predeterminado de Hola) en lugar del modelo de implementación "Clásico" Hola. Si no tienes una cuenta de almacenamiento, obtenga información acerca de cómo tooCreate una cuenta de almacenamiento. 
* **Almacenamiento de datos SQL**: este tutorial mueve datos Hola de tooSQL de SQL Server local almacenamiento de datos, por lo que necesita toohave un almacenamiento de datos en línea. Si no dispone de un almacén de datos, obtenga información acerca de cómo tooCreate un almacenamiento de datos de SQL Azure.

> [!NOTE]
> El rendimiento mejora si la cuenta de almacenamiento de Hola y Hola data warehouse se crean en hello misma región.
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a>Paso 1: Iniciar sesión en tooData Studio plataforma con su cuenta de Azure
Abra el explorador web y navegue toohello [Studio de la plataforma de datos](https://www.dataplatformstudio.com/) sitio Web. Inicio de sesión con Hola misma cuenta de Azure que le toocreate usado Hola almacenamiento cuenta de almacenamiento de datos. Si su dirección de correo electrónico está asociado con un trabajo o a la cuenta del centro educativo y una cuenta de Microsoft, ser cuenta de hello toochoose seguro de que tiene acceso a los recursos de tooyour.

> [!NOTE]
> Si se trata de la primera vez que usa Studio de la plataforma de datos, son más frecuentes toogrant Hola aplicación permiso toomanage los recursos de Azure.
> 
> 

## <a name="step-2-start-hello-import-wizard"></a>Paso 2: Iniciar el Asistente para la importación de Hola
Desde la pantalla principal de DP de bienvenida, seleccione a hello tooAzure almacenamiento de datos SQL vínculo toostart Hola importación Asistente para la importación.

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a>Paso 3: Instalar la puerta de enlace de datos plataforma Studio Hola
tooconnect tooyour en SQL Server base de datos local, deberá tooinstall Hola DP puerta de enlace. puerta de enlace de Hello es un agente de cliente que proporciona acceso tooyour entorno local extrae datos de Hola y lo carga en la cuenta de almacenamiento de tooyour. Los datos nunca pasan a través de los servidores de Redgate. Hola tooinstall puerta de enlace:

1. Haga clic en hello **crear puerta de enlace** vínculo
2. Descarga e instalación Hola puerta de enlace con Hola el instalador proporcionado

![][2]

> [!NOTE]
> Hola puerta de enlace puede instalarse en cualquier equipo con la base de datos de SQL Server de origen de toohello de red acceso. Tiene acceso a la base de datos de SQL Server de hello mediante la autenticación de Windows con credenciales de saludo del usuario actual de Hola.
> 
> 

Una vez instalado, Hola tooConnected de cambios de estado de puerta de enlace y puede seleccionar siguiente.

## <a name="step-4-identify-hello-source-database"></a>Paso 4: Identificar la base de datos de origen de Hola
Hola *escriba el nombre del servidor* cuadro de texto, escriba Hola nombre de hello servidor que hospeda la base de datos y seleccione **siguiente**. A continuación, desde el menú desplegable de hello, seleccione base de datos de hello de que desea tooimport datos.

![][3]

DP inspecciona la base de datos seleccionada de Hola para tablas tooimport. De forma predeterminada, DP importa todas las tablas de hello en la base de datos de Hola. Puede seleccionar o anular la selección de tablas expandiendo Hola todas las tablas de vínculo. Seleccione toomove siguiente de botón Hola al día.

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a>Paso 5: Elija un almacenamiento cuenta toostage Hola de datos
DP le solicitará una ubicación toostage Hola de datos. Elija una cuenta de almacenamiento existente de la suscripción y seleccione **Siguiente**.

> [!NOTE]
> DP creará un nuevo contenedor de blob en hello elegido cuenta de almacenamiento y utilizar una carpeta distinta para cada importación.
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a>Paso 6: Selección del almacenamiento de datos
A continuación, seleccione en línea [almacenamiento de datos de SQL Azure](http://aka.ms/sqldw) tooimport datos de hello en la base de datos. Una vez que haya seleccionado la base de datos, necesita tooenter Hola credenciales tooconnect toohello la base de datos y seleccione **siguiente**.

![][5]

> [!NOTE]
> DP combina tablas de datos de origen de hello en almacenamiento de datos de Hola. DP le advierte si el nombre de tabla Hola requiere toooverwrite tablas existentes en almacenamiento de datos de Hola. Opcionalmente, puede eliminar los objetos existentes en almacenamiento de datos de hello haciendo clic en eliminar todos los objetos existentes antes de la importación.
> 
> 

## <a name="step-7-import-hello-data"></a>Paso 7: Importar datos de Hola
DP confirma que desea incluir los datos de hello tooimport. Simplemente haga clic en la importación de datos de hello inicio importación botón toobegin Hola.

![][6]

DP muestra una visualización que muestra el progreso de Hola de extracción y carga de datos Hola Hola local SQL Server y Hola del progreso de la importación de hello en almacenamiento de datos de SQL.

![][7]

Una vez completada la importación de hello, DP muestra un resumen de importación de datos de Hola y Hola de correcciones de compatibilidad que se han realizado un informe de cambios.

![][8]

## <a name="next-steps"></a>Pasos siguientes
tooexplore sus datos en almacenamiento de datos de SQL, iniciar, consulte:

* [Consultas en Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]
* [Visualización de datos con Power BI][Visualize data with Power BI]

toolearn más información acerca datos plataforma Studio del Redgate:

* [Visite la página principal de DP de Hola](http://www.dataplatformstudio.com/)
* [Vea una demostración de DPS en Channel9](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

Para obtener información general de otras maneras toomigrate y carga los datos en el almacén de datos de SQL consulte:

* [Migrar el almacenamiento de datos de solución tooSQL][Migrate your solution tooSQL Data Warehouse]
* [Carga de datos en Almacenamiento de datos SQL de Azure](sql-data-warehouse-overview-load.md)

Para más sugerencias de desarrollo, vea hello [Introducción al desarrollo de almacenamiento de datos de SQL](sql-data-warehouse-overview-develop.md).

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
