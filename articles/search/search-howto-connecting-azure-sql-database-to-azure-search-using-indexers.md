---
title: "tooAzure de base de datos de SQL Azure aaaConnecting búsqueda usando indizadores | Documentos de Microsoft"
description: "Obtenga información acerca de cómo utilizar indizadores de índice de toopull datos de base de datos de SQL Azure tooan búsqueda de Azure."
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: e9bbf352-dfff-4872-9b17-b1351aae519f
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/13/2017
ms.author: eugenesh
ms.openlocfilehash: b28a11cf18ef994de99e09af90bbfeb171ef3cde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-sql-database-tooazure-search-using-indexers"></a>Conectar tooAzure de base de datos de SQL Azure Buscar utilizar indizadores

Antes de poder consultar un [índice de Azure Search](search-what-is-an-index.md) debe rellenarlo con datos. Si los datos de hello vive en una base de datos de SQL Azure, un **indizador de búsqueda de Azure para la base de datos de SQL Azure** (o **indizador de SQL Azure** abreviado) puede automatizar el proceso de indización de hello, lo que significa menos código toowrite y menos infraestructura toocare sobre.

Este artículo tratan mecánica de hello del uso de [indizadores](search-indexer-overview.md), pero también se describen características solo está disponibles con bases de datos de SQL Azure (por ejemplo, seguimiento de cambios integrado). 

En bases de datos SQL de tooAzure adición, búsqueda de Azure proporciona los indizadores para [base de datos de Azure Cosmos](search-howto-index-documentdb.md), [almacenamiento de blobs de Azure](search-howto-indexing-azure-blob-storage.md), y [almacenamiento de tabla de Azure](search-howto-indexing-azure-tables.md). compatibilidad con toorequest para otros orígenes de datos, proporcione sus comentarios en hello [foro de comentarios de búsqueda de Azure](https://feedback.azure.com/forums/263029-azure-search/).

## <a name="indexers-and-data-sources"></a>Indexadores y orígenes de datos

A **origen de datos** especifica qué tooindex de datos, las credenciales de acceso a datos y las directivas que identifican eficazmente los cambios en los datos de hello (filas nuevas, modificadas o eliminadas). Se define como un recurso independiente para que puedan usarlo múltiples indizadores.

Un **indexador**  es un recurso que conecta un origen de datos con un índice de búsqueda de destino. Un indizador que se usa en hello siguientes maneras:

* Realizar una copia única de hello datos toopopulate un índice.
* Actualizar un índice con los cambios en el origen de datos de hello según una programación.
* Ejecutar a petición tooupdate un índice según sea necesario.

Un indizador único solo puede utilizar una tabla o vista, pero puede crear varios indizadores si desea toopopulate varios índices de búsqueda. Para más información sobre los conceptos, vea [Indexer Operations: Typical workflow](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations#typical-workflow) (Operaciones de indexador: flujo de trabajo típico).

Puede instalar y configurar un indexador de SQL de Azure mediante:

* Asistente para importar datos en hello [portal de Azure](https://portal.azure.com)
* [SDK de .NET de Azure Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.indexer?view=azure-dotnet)
* [API de REST](https://docs.microsoft.com/en-us/rest/api/searchservice/indexer-operations) de Azure Search

En este artículo, vamos a usar Hola API de REST toocreate **indizadores** y **orígenes de datos**.

## <a name="when-toouse-azure-sql-indexer"></a>Cuando toouse indizador de SQL Azure
Dependiendo de varios factores relacionados con datos tooyour, uso de Hola de indizador de SQL Azure puede o puede no ser adecuado. Si los datos se ajusta a Hola según los requisitos, puede utilizar el indizador de SQL Azure.

| Criterios | Detalles |
|----------|---------|
| Los datos proceden de una sola tabla o vista. | Si los datos de hello están distribuidos en varias tablas, puede crear una única vista de datos de Hola. Sin embargo, si usa una vista, no será capaz de toouse integrada de SQL Server cambio detección toorefresh un índice con los cambios incrementales. Para más información, vea [Capturar filas cambiadas y eliminadas](#CaptureChangedRows) a continuación. |
| Los tipos de datos son compatibles | Se admiten la mayoría, pero no todos los tipos SQL de hello en un índice de búsqueda de Azure. Para obtener una lista, vea [Asignación de tipos de datos](#TypeMapping). |
| No se requiere la sincronización de datos en tiempo real | Un indexador puede volver a indexar la tabla cada cinco minutos como máximo. Si los cambios de datos y con frecuencia, hello cambia toobe de necesidad de que se reflejan en el índice de hello en segundos o minutos únicos, se recomienda usar hello [API de REST](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) o [.NET SDK](search-import-data-dotnet.md) toopush actualizar filas directamente. |
| Se permite la indexación incremental | Si tiene un gran conjunto de datos y debe ser capaz de indizador de plan toorun Hola según una programación, búsqueda de Azure tooefficiently identificar filas nuevas, modificadas o eliminadas. Solo se permite la indexación no incremental si se indexa a petición (no en una programación), o se indexan menos de 100 000 filas. Para más información, vea [Capturar filas cambiadas y eliminadas](#CaptureChangedRows) a continuación. |

## <a name="create-an-azure-sql-indexer"></a>Crear un indexador de Azure SQL

1. Crear origen de datos de hello:

   ```
    POST https://myservice.search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:<your server>.database.windows.net,1433;Database=<your database>;User ID=<your user name>;Password=<your password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "name of hello table or view that you want tooindex" }
    }
   ```

   Puede obtener la cadena de conexión de Hola de hello [portal de Azure](https://portal.azure.com); usar hello `ADO.NET connection string` opción.

2. Crear el índice de búsqueda de Azure de destino de hello si aún no tiene uno. Puede crear un índice mediante hello [portal](https://portal.azure.com) o hello [crear índice API](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Asegúrese de que Hola esquema de su índice de destino es compatible con el esquema de Hola de tabla de origen de Hola: vea [asignación de tipos de datos entre SQL y búsqueda de Azure](#TypeMapping).

3. Creación de indizador de hello darle un nombre y haciendo referencia al índice de origen y de destino de datos de hello:

    ```
    POST https://myservice.search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myindexer",
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name"
    }
    ```

Un indizador creado de esta forma no tiene una programación. Se ejecuta automáticamente una vez en cuanto se crea. Puede volver a ejecutarlo en cualquier momento mediante una solicitud **ejecutar indizador** :

    POST https://myservice.search.windows.net/indexers/myindexer/run?api-version=2016-09-01
    api-key: admin-key

Puede personalizar varios aspectos del comportamiento del indexador, como el tamaño de lote y el número de documentos que se puede omitir antes de que la ejecución de un indexador produzca un error. Para más información, consulte [Create Indexer API](https://docs.microsoft.com/rest/api/searchservice/Create-Indexer)(API para crear índices).

Puede que tenga la base de datos de tooallow servicios de Azure tooconnect tooyour. Vea [conectarse desde Azure](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) para obtener instrucciones sobre cómo toodo que.

toomonitor Hola estado del indizador y el historial de ejecución (número de elementos indizados, errores, etc.), utilice un **estado del indizador** solicitud:

    GET https://myservice.search.windows.net/indexers/myindexer/status?api-version=2016-09-01
    api-key: admin-key

respuesta de Hello debe tener un aspecto similar siguiente toohello:

    {
        "@odata.context":"https://myservice.search.windows.net/$metadata#Microsoft.Azure.Search.V2015_02_28.IndexerExecutionInfo",
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2015-02-21T00:23:24.957Z",
            "endTime":"2015-02-21T00:36:47.752Z",
            "errors":[],
            "itemsProcessed":1599501,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        },
        "executionHistory":
        [
            {
                "status":"success",
                "errorMessage":null,
                "startTime":"2015-02-21T00:23:24.957Z",
                "endTime":"2015-02-21T00:36:47.752Z",
                "errors":[],
                "itemsProcessed":1599501,
                "itemsFailed":0,
                "initialTrackingState":null,
                "finalTrackingState":null
            },
            ... earlier history items
        ]
    }

Historial de ejecución contiene la too50 de ejecuciones de hello completado más recientemente, que se ordenan en orden cronológico inverso de hello (de modo que ocurra ejecución más reciente de Hola en respuesta de hello).
Encontrará información adicional acerca de la respuesta de hello en [obtener estado del indizador](http://go.microsoft.com/fwlink/p/?LinkId=528198)

## <a name="run-indexers-on-a-schedule"></a>Ejecutar indexadores según una programación
También puede organizar Hola indizador toorun periódicamente según una programación. toodo, agregar hello **programación** propiedad al crear o actualizar el indizador de Hola. ejemplo de Hola siguiente muestra un indizador de hello PUT tooupdate de solicitud:

    PUT https://myservice.search.windows.net/indexers/myindexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name",
        "schedule" : { "interval" : "PT10M", "startTime" : "2015-01-01T00:00:00Z" }
    }

Hola **intervalo** parámetro es obligatorio. intervalo de saludo refiere toohello tiempo entre el inicio de Hola de dos ejecuciones de indizador consecutivos. Hola más pequeño permitido intervalo es 5 minutos. Hola más larga es un día. Debe tener el formato de un valor "dayTimeDuration" XSD (subconjunto restringido de un valor de [duración ISO 8601](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) ). patrón de Hola para esto es: `P(nD)(T(nH)(nM))`. Ejemplos: `PT15M` para cada 15 minutos, `PT2H` para cada 2 horas.

Hola opcional **startTime** indica cuándo hello ejecuciones programadas deben comenzar. Si se omite, se usa la hora UTC actual de Hola. Este tiempo puede estar en hello más allá, en cuyo caso se programa la primera ejecución de hello como si se ha ejecutado el indizador de hello continuamente desde Hola startTime.  

Solo se puede ejecutar a la vez una ejecución de un indexador. Si un indizador que se está ejecutando cuando esté programada su ejecución, ejecución de Hola se pospone hasta Hola siguiente hora programada.

Veamos un ejemplo toomake esto más concreto. Suponga que se Hola después de cada hora programación configurada:

    "schedule" : { "interval" : "PT1H", "startTime" : "2015-03-01T00:00:00Z" }

Esto es lo que sucede:

1. la primera ejecución del indizador Hola inicia en o alrededor de 1 de marzo de 2015 12:00 a.m. hora UTC.
2. Suponga que esta ejecución tarda 20 minutos (o un período inferior a 1 hora).
3. inicia la ejecución del segundo de Hello en o alrededor de 1 de marzo de 2015, 1:00 a.m.
4. Ahora suponga que esta ejecución tarda más de una hora (por ejemplo, 70 minutos), de forma que finalice aproximadamente 2:10 a.m.
5. Es ahora 2:00 a.m., hora de hello tercera ejecución toostart. Sin embargo, dado que Hola segunda ejecución desde la 1 a.m. sigue ejecutándose, se omite la tercera ejecución de Hola. inicia la ejecución terceros de Hola a las 3 a.m.

Puede agregar, cambiar o eliminar la programación de un indizador existente mediante una solicitud **PUT de indizador** .

<a name="CaptureChangedRows"></a>

## <a name="capture-new-changed-and-deleted-rows"></a>Capturar filas nuevas, cambiadas y eliminadas

Búsqueda de Azure usa **indización incremental** tooavoid cuyo índice de toore Hola toda la tabla o vista cada vez que se ejecuta un indizador. Búsqueda de Azure proporciona que dos cambiar detección directivas toosupport incremental indización. 

### <a name="sql-integrated-change-tracking-policy"></a>Directiva de seguimiento de cambios integrada de SQL
Si la base de datos SQL admite el [seguimiento de cambios](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-tracking-sql-server), se recomienda usar la **directiva de seguimiento de cambios integrada de SQL**. Se trata de una directiva más eficaz de Hola. Además, permite búsqueda de Azure tooidentify elimina filas sin necesidad de tooadd una tabla de tooyour de columna de "eliminación temporal" explícita.

#### <a name="requirements"></a>Requisitos 

+ Requisitos de versión de la base de datos:
  * SQL Server 2012 SP3 y versiones posteriores, si usa SQL Server en máquinas virtuales de Azure.
  * Base de datos SQL de Azure V12, si está usando la Base de datos SQL de Azure.
+ Solo tablas (vistas no). 
+ En la base de datos de hello, [habilitar el seguimiento de cambios](https://docs.microsoft.com/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server) para la tabla de Hola. 
+ Ninguna clave principal compuesta (una clave principal que contiene más de una columna) en la tabla de Hola.  

#### <a name="usage"></a>Uso

toouse esta directiva, crear o actualizar el origen de datos similar al siguiente:

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy"
      }
    }

Al usar la directiva de seguimiento de cambios integrada de SQL, no especifique una directiva de detección de eliminación de datos independiente, ya que esta directiva tiene compatibilidad integrada para identificar las filas eliminadas. Sin embargo, para hello eliminaciones toobe detectado "modo automático", clave de documento de hello en el índice de búsqueda debe ser Hola igual a la clave principal de Hola Hola table de SQL. 

<a name="HighWaterMarkPolicy"></a>

### <a name="high-water-mark-change-detection-policy"></a>Directiva de detección de cambios de límite superior

Esta directiva de detección de cambios se basa en una columna de "marca de agua" capturar la versión de Hola o tiempo se actualizó por última vez una fila. Si usa una vista, debe usar una directiva de marca de límite superior. columna de marca de agua de Hello debe cumplir Hola según los requisitos.

#### <a name="requirements"></a>Requisitos 

* Todas las inserciones especifican un valor para la columna de Hola.
* Elemento de tooan de todas las actualizaciones también cambie el valor de Hola de columna Hola.
* valor de Hola de esta columna aumenta con cada inserción o actualización.
* Consultas con Hola después de WHERE y cláusulas ORDER BY se pueden ejecutar eficientemente:`WHERE [High Water Mark Column] > [Current High Water Mark Value] ORDER BY [High Water Mark Column]`

> [!IMPORTANT] 
> Se recomienda encarecidamente usar hello [rowversion](https://docs.microsoft.com/sql/t-sql/data-types/rowversion-transact-sql) tipo de datos para la columna de marca de agua de Hola. Si se utiliza cualquier otro tipo de datos, seguimiento de cambios no se garantiza toocapture todos los cambios realizados en presencia de Hola de transacciones que se ejecutan simultáneamente con una consulta de indizador. Cuando se usa **rowversion** en una configuración con réplicas de solo lectura, debe señalar el indizador de hello en la réplica principal de Hola. Solo se puede usar una réplica principal para escenarios de sincronización de datos.

#### <a name="usage"></a>Uso

toouse una directiva de marca de agua, crear o actualizar el origen de datos similar al siguiente:

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
           "highWaterMarkColumnName" : "[a rowversion or last_updated column name]"
      }
    }

> [!WARNING]
> Si la tabla de origen de hello no tiene un índice en la columna de marca de agua de hello, consultas utilizadas por el indizador de hello SQL pueden agotar el tiempo. En concreto, Hola `ORDER BY [High Water Mark Column]` cláusula requiere un índice toorun eficazmente cuando Hola tabla contiene muchas filas.
>
>

Si se producen errores de tiempo de espera, puede usar hello `queryTimeout` indizador tooset Hola consulta tiempo de espera tooa valor de configuración de mayor que el tiempo de espera de hello predeterminado 5 minutos. Por ejemplo, minutos de too10 de tiempo de espera de hello tooset, crear o actualizar indizador Hola con hello siguiente configuración:

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

También puede deshabilitar hello `ORDER BY [High Water Mark Column]` cláusula. Sin embargo, esto no se recomienda porque si se interrumpe la ejecución de indizador de hello debido a un error, Hola indizador tiene toore proceso todas las filas si se ejecuta más tarde - incluso si el indizador de hello ya procesado casi todas las filas de Hola por tiempo de presentación que se interrumpió. Hola toodisable `ORDER BY` cláusula, use hello `disableOrderByHighWaterMarkColumn` establecer en la definición de indizador de hello:  

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "disableOrderByHighWaterMarkColumn" : true } }
    }

### <a name="soft-delete-column-deletion-detection-policy"></a>Directiva de detección de eliminación de columna de eliminación temporal
Cuando se eliminan filas de tabla de origen de hello, probablemente le convenga toodelete las filas del índice de búsqueda de hello así. Si usa Hola SQL había integrado en directiva de seguimiento de cambios, se prepara para usted. Sin embargo, directiva de seguimiento de cambios de marca de agua de hello no ayudarán con las filas eliminadas. ¿Qué toodo?

Si las filas de Hola se quitan físicamente de tabla de hello, búsqueda de Azure no tiene ninguna presencia de manera tooinfer Hola de registros que ya no existen.  Sin embargo, puede usar toologically eliminar filas de Hola "soft-delete" técnica sin quitarlos de la tabla de Hola. Agregar una columna tooyour tabla o vista y marcar filas como eliminados con esa columna.

Cuando se utiliza la técnica de eliminación de software de hello, puede especificar la directiva de eliminación temporal de hello como se indica a continuación al crear o actualizar el origen de datos de hello:

    {
        …,
        "dataDeletionDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
           "softDeleteColumnName" : "[a column name]",
           "softDeleteMarkerValue" : "[hello value that indicates that a row is deleted]"
        }
    }

Hola **softDeleteMarkerValue** debe ser una cadena: usar la representación de cadena de Hola de su valor real. Por ejemplo, si tiene una columna de enteros donde las filas eliminadas se marcan con el valor 1 de hello, use `"1"`. Si tiene una columna de tipo BIT donde las filas eliminadas se marcan con hello valor booleano true, use `"True"`.

<a name="TypeMapping"></a>

## <a name="mapping-between-sql-and-azure-search-data-types"></a>Asignación entre tipos de datos de SQL y de Azure Search
| Tipo de datos de SQL | Tipos de campos de índice de destino permitidos | Notas |
| --- | --- | --- |
| bit |Edm.Boolean, Edm.String | |
| int, smallint, tinyint |Edm.Int32, Edm.Int64, Edm.String | |
| bigint |Edm.Int64, Edm.String | |
| real, float |Edm.Double, Edm.String | |
| smallmoney, numérico decimal de dinero |Edm.String |Búsqueda de Azure no admite la conversión de tipos decimales en Edm.Double porque esto podría provocar la pérdida de precisión |
| char, nchar, varchar, nvarchar |Edm.String<br/>Collection(Edm.String) |Una cadena SQL puede ser toopopulate usa un campo Collection (EDM.String) si la cadena de hello representa una matriz JSON de cadenas:`["red", "white", "blue"]` |
| smalldatetime, datetime, datetime2, date, datetimeoffset |Edm.DateTimeOffset, Edm.String | |
| uniqueidentifer |Edm.String | |
| geography |Edm.GeographyPoint |Se admiten solo las instancias de geography de tipo POINT con SRID 4326 (que es el valor predeterminado de hello) |
| rowversion |N/D |Columnas de versión de fila no se puede almacenar en el índice de búsqueda de hello, pero pueden usarse para el seguimiento de cambios |
| time, timespan, binary, varbinary, image, xml, geometry, tipos CLR |N/D |No compatible |

## <a name="configuration-settings"></a>Valores de configuración
El indexador de SQL expone varios valores de configuración:

| Configuración | Tipo de datos | Propósito | Valor predeterminado |
| --- | --- | --- | --- |
| queryTimeout |cadena |Conjuntos de Hola tiempo de espera de ejecución de consultas SQL |5 minutos ("00:05:00") |
| disableOrderByHighWaterMarkColumn |booleano |Hace que consulta SQL Hola usada por hello marca de agua directiva tooomit Hola cláusula ORDER BY. Consulte [Directiva de detección de cambios de límite superior](#HighWaterMarkPolicy). |false |

Esta configuración se usa en hello `parameters.configuration` objeto de definición de indizador de Hola. Por ejemplo, tooset minutos de too10 de tiempo de espera de consulta de hello, crear o actualizar indizador Hola con hello siguiente configuración:

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

## <a name="faq"></a>P+F

**P: ¿Puedo usar un indexador de Azure SQL con bases de datos SQL que se ejecutan en máquinas virtuales de IaaS en Azure?**

Sí. Sin embargo, deberá tooallow la base de datos de búsqueda servicio tooconnect tooyour. Para obtener más información, consulte [configurar una conexión desde un tooSQL de indizador de búsqueda de Azure Server en una máquina virtual de Azure](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md).

**P: ¿Puedo usar un indexador de Azure SQL con bases de datos SQL que se ejecutan localmente?**

No directamente. No se recomienda o admitir una conexión directa, como hacerlo le exigiría tooopen el tráfico de tooInternet de las bases de datos. Los clientes han realizado correctamente este escenario mediante tecnologías de puente como Azure Data Factory. Para obtener más información, consulte [índice de búsqueda de Azure tooan inserción de datos mediante Data Factory de Azure](https://docs.microsoft.com/azure/data-factory/data-factory-azure-search-connector).

**P: ¿Puedo usar un indexador de Azure SQL con bases de datos que no son de SQL Server que se ejecutan en IaaS en Azure?**

No. No se admite este escenario, porque ya no hemos comprobado indizador Hola con las bases de datos que no sea de SQL Server.  

**P: ¿Puedo crear varios indexadores que se ejecuten según una programación?**

Sí. Sin embargo, solo puede ejecutarse un indizador en un nodo de cada vez. Si tiene varios indizadores ejecución simultánea, considere la posibilidad de escalar verticalmente el toomore de servicio de búsqueda de una unidad de búsqueda.

**P: ¿Afecta la ejecución de un indexador a la carga de trabajo de la consulta?**

Sí. Indizador se ejecuta en uno de los nodos de hello en el servicio de búsqueda y los recursos de ese nodo se comparten entre la indización y que sirve al tráfico de consultas y otras solicitudes de API. Si al ejecutar cargas de trabajo intensivas de indexación y consulta detecta una frecuencia alta de errores 503 o el aumento de los tiempos de respuesta, considere la posibilidad de [escalar verticalmente el servicio de búsqueda](search-capacity-planning.md).

**P: ¿Puedo usar una réplica secundaria en un [clúster de conmutación por error](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview) como un origen de datos?**

Depende. Para la indexación completa de una tabla o vista, puede usar una réplica secundaria. 

Para la indexación incremental, Azure Search admite dos directivas de detección de cambios: seguimiento de cambios integrado de SQL y Marca de límite superior.

En las réplicas de solo lectura, la base de datos SQL no admite el seguimiento de cambios integrado. Por tanto, debe usar la directiva Marca de límite superior. 

Nuestra recomendación estándar es toouse Hola el tipo de datos de rowversion para la columna de marca de agua de Hola. Pero el uso de rowversion se basa en la función `MIN_ACTIVE_ROWVERSION` de SQL Database, que no se admite en las réplicas de solo lectura. Por lo tanto, debe señalar la réplica principal de hello indizador tooa si usas rowversion.

Si intentas toouse rowversion en una réplica de solo lectura, verá Hola siguiente error: 

    "Using a rowversion column for change tracking is not supported on secondary (read-only) availability replicas. Please update hello datasource and specify a connection toohello primary availability replica.Current database 'Updateability' property is 'READ_ONLY'".

**P: ¿Puedo usar una columna alternativa, que no sea rowversion, para el seguimiento de los cambios de marca de límite superior?**

No se recomienda. Solo **rowversion** permite la sincronización de datos confiable. Pero según la lógica de aplicación, puede ser seguro si:

+ Puede asegurarse de que cuando se ejecute el indexador de hello, no hay ninguna transacción pendiente en la tabla de Hola que se indiza (por ejemplo, todas las actualizaciones de tabla se realizan como un lote según una programación y programación de indizador de búsqueda de Azure Hola se establece tooavoid solaparse con tabla de Hola programación de actualización).  

+ Periódicamente, lo hace un toopick reindización completa de las filas que faltan. 
