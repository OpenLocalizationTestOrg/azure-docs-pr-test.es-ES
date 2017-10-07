---
title: "aaaReport entre bases de datos de escala horizontal en la nube (creación de particiones horizontales) | Documentos de Microsoft"
description: "¿Cómo toouse entre las consultas de base de datos de base de datos"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a>Informes de bases de datos escaladas horizontalmente en la nube (versión preliminar)
Puede crear informes de varias bases de datos SQL de Azure desde un único punto de conexión mediante una [consulta elástica](sql-database-elastic-query-overview.md). las bases de datos de Hello deben crear particiones horizontalmente (también conocida como "particionadas").

Si tiene una base de datos existente, vea [existente migrar bases de datos de las bases de datos fuera de tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).

los objetos SQL de hello toounderstand necesarios tooquery, consulte [consulta entre bases de datos con particiones horizontales](sql-database-elastic-query-horizontal-partitioning.md).

## <a name="prerequisites"></a>Requisitos previos
Descargue y ejecute hello [cómo empezar a usar el ejemplo de herramientas de la base de datos elástica](sql-database-elastic-scale-get-started.md).

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>Crear un mapa de particiones administrador mediante la aplicación de ejemplo de Hola
A continuación creará un mapa de particiones administrador junto con varias particiones, seguido por la inserción de datos en particiones de Hola. Si se encontrara tooalready tienen el programa de instalación de particiones con datos particionados en ellos, puede omitir Hola pasos y mover toohello siguiente sección.

1. Compile y ejecute hello **Introducción a las herramientas de base de datos elástica** aplicación de ejemplo. Siga los pasos de hello hasta el paso 7 de la sección de hello [descargue y ejecute la aplicación de ejemplo de Hola](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app). Al final de saludo del paso 7, verá Hola después de símbolo del sistema:

    ![símbolo del sistema][1]
2. En la ventana de comandos de hello, escriba "1" y presione **ENTRAR**. Esto crea el Administrador de mapa de particiones de Hola y agrega dos particiones toohello servidor. A continuación, escriba "3" y presione **ENTRAR**; repita la acción de hello cuatro veces. De esta forma, se insertan las filas de datos de ejemplo en sus particiones.
3. Hola [portal de Azure](https://portal.azure.com) debe mostrar tres nuevas bases de datos en el servidor:

   ![Confirmación de Visual Studio][2]

   En este momento, se admiten las consultas entre bases de datos a través de bibliotecas de cliente de base de datos elástica Hola. Por ejemplo, utilice la opción 4 en la ventana de comandos de Hola. Hola resultados de una consulta de varias particiones siempre son un **UNION ALL** resultados de Hola de todas las particiones.

   En la siguiente sección hello, creamos un punto de conexión de base de datos de ejemplo que admite las consultas más completa de los datos de hello entre las particiones.

## <a name="create-an-elastic-query-database"></a>Creación una base de datos de consulta elástica
1. Abra hello [portal de Azure](https://portal.azure.com) e inicie sesión.
2. Crear una nueva base de datos de SQL Azure en hello mismo servidor que el programa de instalación de la partición. Base de datos de nombres Hola "ElasticDBQuery."

    ![Portal de Azure y nivel de precios][3]

    > [!NOTE]
    > puede usar una base de datos existente. Si puede hacerlo, no debe ser una de las particiones de Hola que desearía tooexecute las consultas en. Esta base de datos se usará para crear objetos de metadatos para una consulta de base de datos elástica de Hola.
    >

## <a name="create-database-objects"></a>Creación de objetos de base de datos
### <a name="database-scoped-master-key-and-credentials"></a>Clave maestra y credenciales de ámbito de base de datos
Se trata de administrador de asignación de tooconnect usado toohello particiones y las particiones de hello:

1. Abra SQL Server Management Studio o SQL Server Data Tools en Visual Studio.
2. Conectar la base de datos de tooElasticDBQuery y ejecute hello siga los comandos del código T-SQL:

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    "username" y "password" debe ser Hola igual como información de inicio de sesión utilizada en el paso 6 de [descargue y ejecute la aplicación de ejemplo de Hola](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) en [Introducción a las herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md).

### <a name="external-data-sources"></a>Orígenes de datos externos
toocreate un origen de datos externo, ejecute hello siguiente comando en la base de datos de Hola ElasticDBQuery:

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 "CustomerIDShardMap" es el nombre de hello del mapa de particiones de hello, si creó mapa de particiones de Hola y mapa de particiones con el ejemplo de herramientas de base de datos elástica Hola el administrador. Sin embargo, si utiliza la configuración personalizada de este ejemplo, a continuación, debe ser nombre de asignación de particiones de Hola que eligió en la aplicación.

### <a name="external-tables"></a>Tablas externas
Crear una tabla externa que coincide con la tabla de clientes de hello en particiones de hello ejecutando el siguiente comando en la base de datos de ElasticDBQuery de hello:

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>Ejecución de la consulta de T-SQL de la base de datos elástica de ejemplo
Una vez que haya definido el origen de datos externo y las tablas externas, puede usar el T-SQL completo en las tablas externas.

Ejecute esta consulta en la base de datos de Hola ElasticDBQuery:

    select count(CustomerId) from [dbo].[Customers]

Observará que consultan hello agrega los resultados de todas las particiones de Hola y proporciona Hola después de salida:

![Detalles de salida][4]

## <a name="import-elastic-database-query-results-tooexcel"></a>Importar tooExcel de resultados de consulta de base de datos elástica
 Puede importar los resultados de Hola desde un consulta tooan del archivo de Excel.

1. Inicie Excel 2013.
2. Navegue toohello **datos** la cinta de opciones.
3. Haga clic en **Desde otros orígenes** y luego en **Desde SQL Server**.

   ![Importación de Excel desde otros orígenes][5]
4. Hola **Asistente para la conexión de datos** escriba credenciales de inicio de sesión y nombre de servidor de Hola. A continuación, haga clic en **Siguiente**.
5. En el cuadro de diálogo de hello **base de datos de hello Select que contiene datos de Hola que desee**, seleccione hello **ElasticDBQuery** base de datos.
6. Seleccione hello **clientes** de tabla en la vista de lista de Hola y haga clic en **siguiente**. Haga clic en **Finalizar**.
7. Hola **importar datos** formulario, en **Seleccione cómo desea que tooview estos datos en el libro**, seleccione **tabla** y haga clic en **Aceptar**.

Todas las filas de Hola **clientes** tabla, almacenado en particiones diferentes rellenar la hoja de Excel de Hola.

Ahora puede usar las funciones de visualización de datos decisivas de Excel. Puede usar la cadena de conexión de hello con el nombre del servidor, nombre de base de datos y las credenciales tooconnect su BI y datos integración herramientas toohello elástico consultar base de datos. Asegúrese de que SQL Server se admite como origen de datos para la herramienta. Puede hacer referencia a base de datos de consulta flexible de toohello y tablas externas al igual que cualquier otra base de datos de SQL Server y las tablas de SQL Server que se conectará toowith la herramienta.

### <a name="cost"></a>Coste
No hay ningún cargo adicional para usar la característica de consulta de base de datos elástica Hola.

Para obtener información sobre los precios, consulte [Detalles de precios de Base de datos SQL](https://azure.microsoft.com/pricing/details/sql-database/).

## <a name="next-steps"></a>Pasos siguientes

* Para obtener información general sobre las consultas elásticas, consulte [Información general sobre las consultas elásticas](sql-database-elastic-query-overview.md).
* Para obtener un tutorial sobre la creación de particiones verticales, consulte [Introducción a las consultas entre bases de datos (particiones verticales)](sql-database-elastic-query-getting-started-vertical.md).
* Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento vertical, consulte [Consulta de datos particionados verticalmente](sql-database-elastic-query-vertical-partitioning.md)
* Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento horizontal, consulte [Consulta de datos particionados horizontalmente.](sql-database-elastic-query-horizontal-partitioning.md)
* Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para ver un procedimiento almacenado que ejecuta una instrucción de Transact-SQL en una sola instancia remota de Azure SQL Database o un conjunto de bases de datos que actúan como particiones en un esquema de particiones horizontales.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
