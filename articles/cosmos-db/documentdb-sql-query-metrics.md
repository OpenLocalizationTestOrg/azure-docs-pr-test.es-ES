---
title: "aaaSQL las métricas de consulta para la API de documentos de base de datos de Azure Cosmos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooinstrument y depuración Hola rendimiento de las consultas SQL de las solicitudes de base de datos de Azure Cosmos."
keywords: consulta sql, consultas sql, sintaxis sql, lenguaje de consulta json, conceptos de base de datos y consultas sql, funciones de agregado
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: b2fa8e8f-7291-45a3-9bd1-7284ed9077f8
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 2fee3786b7d48d254162699471943e316764b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-query-performance-with-azure-cosmos-db"></a>Optimización del rendimiento de consultas con Azure Cosmos DB
Azure Cosmos DB proporciona una [API de SQL para consultar datos](documentdb-sql-query.md), sin necesidad de índices de esquema o secundarios. Este artículo ofrece Hola siguiente información para desarrolladores:

* Detalles de alto nivel sobre cómo funciona la ejecución de consultas SQL de Azure Cosmos DB
* Detalles sobre cómo consultar encabezados de solicitud y respuesta y opciones del SDK de cliente
* Sugerencias y procedimientos recomendados para el rendimiento de consultas
* Ejemplos de cómo toodebug de estadísticas de ejecución de SQL tooutilize rendimiento de las consultas

## <a name="about-sql-query-execution"></a>Acerca de la ejecución de consultas SQL

En la base de datos de Azure Cosmos, almacenar datos en contenedores, lo que pueden crecer tooany [rendimiento de tamaño o la solicitud de almacenamiento](partition-data.md). Base de datos de Azure Cosmos escala perfectamente datos a través de particiones físicas en crecimiento de los datos toohandle Hola portadas o aumentar el rendimiento aprovisionado de. Puede emitir contenedor de tooany de consultas SQL mediante API de REST de Hola o uno de hello admitida [SDK de DocumentDB](documentdb-sdk-dotnet.md).

Una breve introducción a la creación de particiones: se define una clave de partición como "ciudad", que determina la forma en que los datos se dividen entre particiones físicas. Clave de una sola partición de datos que pertenecen tooa (por ejemplo, "ciudad" == "Seattle") se almacena en una partición física, pero normalmente una sola partición física tiene varias claves de partición. Cuando una partición alcanza el tamaño de almacenamiento, servicio de hello perfectamente partición Hola divide en dos nuevas particiones y divide la clave de partición de hello uniformemente a través de estas particiones. Puesto que las particiones son transitorias, hello API usar una abstracción de una "clave intervalo de partición", que denota intervalos Hola de hash de clave de partición. 

Cuando se emite un tooAzure consulta Cosmos DB, Hola SDK realiza estos pasos lógicos:

* Analizar el plan de ejecución de consulta de hello SQL consulta toodetermine Hola. 
* Si consulta Hola incluye un filtro con la clave de partición de hello, como `SELECT * FROM c WHERE c.city = "Seattle"`, resulta tooa enrutado sola partición. Si consulta hello no tiene un filtro en la clave de partición, a continuación, se ejecuta en todas las particiones y se combinan los resultados del cliente.
* consulta de Hola se ejecuta dentro de cada partición en serie o paralelo, en función de la configuración del cliente. En cada partición, consulta Hola podría provocar que uno o más ciclos de ida y vuelta según la complejidad de la consulta de hello, configura el tamaño de página y aprovisionar el rendimiento de la colección de Hola. Cada ejecución devuelve el número de Hola de [unidades de solicitud](request-units.md) consumido por la ejecución de la consulta y, opcionalmente, las estadísticas de ejecución de consulta. 
* Hola SDK realiza un resumen de los resultados de la consulta de hello en particiones. Por ejemplo, si consulta Hola implica una cláusula ORDER BY en particiones, los resultados de las particiones individuales son tooreturn ordenada de mezcla resultados ordenados globalmente. Si consulta hello es una agregación como `COUNT`, recuentos de Hola de particiones individuales están tooproduce sumado Hola el número total.

SDK de Hello proporcionan distintas opciones para la ejecución de la consulta. Por ejemplo, en .NET estas opciones están disponibles en hello `FeedOptions` clase. Hello tabla siguiente describen estas opciones y qué manera pueden afectar el tiempo de ejecución de consulta. 

| Opción | Descripción |
| ------ | ----------- |
| `EnableCrossPartitionQuery` | Se debe establecer tootrue para cualquier consulta que requiere toobe ejecutado a través de más de una partición. Se trata de un tooenable de marca explícita que compensaciones de rendimiento consciente de toomake durante el tiempo de desarrollo. |
| `EnableScanInQuery` | Se debe establecer tootrue si ha decidido no indizar, pero desea consulta de hello toorun a través de un recorrido de todos modos. Solo es aplicable si la indización para hello solicitada está deshabilitada la ruta de acceso de filtro. | 
| `MaxItemCount` | número máximo de Hola de tooreturn elementos por servidor toohello de ida y vuelta. Al establecer demasiado-1, puede permitir que servidor hello administrar Hola número de elementos. O bien, puede reducir este tooretrieve valor solo un pequeño número de elementos por de ida y vuelta. 
| `MaxBufferedItemCount` | Esto es una opción de cliente y el consumo de memoria de hello toolimit a utilizar al realizar entre particiones ORDER BY. Un valor más alto le ayuda a reducir la latencia de Hola de ordenación, entre particiones. |
| `MaxDegreeOfParallelism` | Obtiene o establece el número de Hola de operaciones simultáneas que se ejecuten en paralelo de cliente durante la ejecución de consultas en paralelo en hello servicio de base de datos de documentos de Azure. Un valor de propiedad positivo limita Hola valor del número de operaciones simultáneas toohello conjunto. Si se establece a que no requiere herramientas que 0, el sistema de hello decide automáticamente número Hola de toorun de operaciones simultáneas. |
| `PopulateQueryMetrics` | Permite el registro detallado de estadísticas del tiempo empleado en diversas fases de la ejecución de consultas, como tiempo de compilación, hora de ciclo del índice y tiempo de carga de documentos. Salida de las estadísticas de consulta se puede compartir con problemas de rendimiento de consultas de toodiagnose de soporte técnico de Azure. |
| `RequestContinuation` | Para reanudar la ejecución de consulta pasando token de continuación opaco de hello devuelto por una consulta. token de continuación Hola encapsula todo el estado necesario para la ejecución de la consulta. |
| `ResponseContinuationTokenLimitInKb` | Puede limitar el tamaño máximo de Hola Hola de token de continuación devuelto por el servidor de Hola. Tendrá que tooset esto si el host de la aplicación tiene límites de tamaño de encabezado de respuesta. Establecer este valor puede aumentar Hola general duración y RUs utilizados para consultas de Hola.  |

Por ejemplo, consideremos una consulta de ejemplo en la clave de partición solicitado en una colección con `/city` como partición de hello clave y aprovisionada con 100 000 RU/s de rendimiento. Solicitar esta consulta con `CreateDocumentQuery<T>` en .NET como Hola siguiente:

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
        MaxItemCount = -1, 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();
```

Hello mostrado anteriormente, el fragmento de SDK corresponde toohello después de la solicitud de API de REST:

```
POST https://arramacquerymetrics-westus.documents.azure.com/dbs/db/colls/sample/docs HTTP/1.1
x-ms-continuation: 
x-ms-documentdb-isquery: True
x-ms-max-item-count: -1
x-ms-documentdb-query-enablecrosspartition: True
x-ms-documentdb-query-parallelizecrosspartitionquery: True
x-ms-documentdb-query-iscontinuationexpected: True
x-ms-documentdb-populatequerymetrics: True
x-ms-date: Tue, 27 Jun 2017 21:52:18 GMT
authorization: type%3dmaster%26ver%3d1.0%26sig%3drp1Hi83Y8aVV5V6LzZ6xhtQVXRAMz0WNMnUuvriUv%2b4%3d
x-ms-session-token: 7:8,6:2008,5:8,4:2008,3:8,2:2008,1:8,0:8,9:8,8:4008
Cache-Control: no-cache
x-ms-consistency-level: Session
User-Agent: documentdb-dotnet-sdk/1.14.1 Host/32-bit MicrosoftWindowsNT/6.2.9200.0
x-ms-version: 2017-02-22
Accept: application/json
Content-Type: application/query+json
Host: arramacquerymetrics-westus.documents.azure.com
Content-Length: 52
Expect: 100-continue

{"query":"SELECT * FROM c WHERE c.city = 'Seattle'"}
```

Cada página de la ejecución de consulta corresponde tooa API de REST `POST` con hello `Accept: application/query+json` encabezado y consulta SQL de hello en el cuerpo de Hola. Cada consulta convierte a uno o más redondean server toohello de viajes con hello `x-ms-continuation` muestra el símbolo (token) entre la ejecución de tooresume de cliente y servidor hello. Opciones de configuración de Hello en FeedOptions se pasan toohello servidor en forma de Hola de encabezados de solicitud. Por ejemplo, `MaxItemCount` corresponde demasiado`x-ms-max-item-count`. 

solicitud Hello devuelve siguiente hello (truncado para mejorar la legibilidad) respuesta:

```
HTTP/1.1 200 Ok
Cache-Control: no-store, no-cache
Pragma: no-cache
Transfer-Encoding: chunked
Content-Type: application/json
Server: Microsoft-HTTPAPI/2.0
Strict-Transport-Security: max-age=31536000
x-ms-last-state-change-utc: Tue, 27 Jun 2017 21:01:57.561 GMT
x-ms-resource-quota: documentSize=10240;documentsSize=10485760;documentsCount=-1;collectionSize=10485760;
x-ms-resource-usage: documentSize=1;documentsSize=884;documentsCount=2000;collectionSize=1408;
x-ms-item-count: 2000
x-ms-schemaversion: 1.3
x-ms-alt-content-path: dbs/db/colls/sample
x-ms-content-path: +9kEANVq0wA=
x-ms-xp-role: 1
x-ms-documentdb-query-metrics: totalExecutionTimeInMs=33.67;queryCompileTimeInMs=0.06;queryLogicalPlanBuildTimeInMs=0.02;queryPhysicalPlanBuildTimeInMs=0.10;queryOptimizationTimeInMs=0.00;VMExecutionTimeInMs=32.56;indexLookupTimeInMs=0.36;documentLoadTimeInMs=9.58;systemFunctionExecuteTimeInMs=0.00;userFunctionExecuteTimeInMs=0.00;retrievedDocumentCount=2000;retrievedDocumentSize=1125600;outputDocumentCount=2000;writeOutputTimeInMs=18.10;indexUtilizationRatio=1.00
x-ms-request-charge: 604.42
x-ms-serviceversion: version=1.14.34.4
x-ms-activity-id: 0df8b5f6-83b9-4493-abda-cce6d0f91486
x-ms-session-token: 2:2008
x-ms-gatewayversion: version=1.14.33.2
Date: Tue, 27 Jun 2017 21:59:49 GMT
```

encabezados de respuesta de la tecla de Hello procedentes de la consulta de Hola Hola siguientes:

| Opción | Descripción |
| ------ | ----------- |
| `x-ms-item-count` | número de Hola de elementos devueltos en la respuesta de Hola. Esto depende en hello proporcionado `x-ms-max-item-count`, Hola número de elementos que puede ajustarse de tamaño de carga máximo de respuesta de Hola y rendimiento aprovisionado hello, tiempo de ejecución de consulta. |  
| `x-ms-continuation:` | Hola continuación token tooresume la ejecución de consulta de hello, si hay resultados adicionales disponibles. | 
| `x-ms-documentdb-query-metrics` | estadísticas de consulta de Hello para la ejecución de Hola. Se trata de una cadena delimitada que contiene las estadísticas de tiempo empleado en hello distintas fases de ejecución de la consulta. Se devuelve si `x-ms-documentdb-populatequerymetrics` se establece demasiado`True`. | 
| `x-ms-request-charge` | Hola número de [unidades de solicitud](request-units.md) utilizados por consulta Hola. | 

Para obtener más información sobre encabezados de solicitud de API de REST de Hola y opciones, consulte [consultar recursos usando la API de REST de documentos de hello](https://docs.microsoft.com/rest/api/documentdb/querying-documentdb-resources-using-the-rest-api).

## <a name="best-practices-for-query-performance"></a>Procedimientos recomendados para el rendimiento de consultas
siguiente Hola es factores más comunes de Hola que afectan al rendimiento de la consulta de base de datos de Azure Cosmos. Cada uno de estos temas se tratará con mayor detalle en este artículo.

| Factor | Sugerencia | 
| ------ | -----| 
| Rendimiento aprovisionado | Medir RU por cada consulta y asegúrese de que tiene rendimiento aprovisionado de hello necesarios para las consultas. | 
| Creación de particiones y claves de partición | Dé prioridad a las consultas con el valor de clave de partición de Hola de cláusula de filtro de Hola de baja latencia. |
| SDK y opciones de consulta | Siga los procedimientos recomendados del SDK, como las opciones de conectividad directa y optimización de la ejecución de consultas de cliente. |
| Latencia de red | Cuenta de red sobrecarga en la medida y usar tooread hospedaje múltiple de las API de hello más cercano de la región. |
| Directiva de indexación | Asegúrese de que tiene Hola requiere rutas de acceso/directiva de indexación de consulta de Hola. |
| Métricas de ejecución de consultas | Analizar Hola consulta ejecución métricas tooidentify posibles de escribir de nuevo las formas de consulta y los datos.  |

### <a name="provisioned-throughput"></a>Rendimiento aprovisionado
En Cosmos DB, se crean contenedores de datos, cada uno con un rendimiento reservado expresado en unidades de solicitud (RU) por segundo. Una lectura de un documento de 1 KB es 1 RU y cada operación (incluidas las consultas) está normalizado tooa número fijo de RUs basándose en su complejidad. Por ejemplo, si tiene 1000 RU/s aprovisionadas en su contenedor y tiene una consulta como `SELECT * FROM c WHERE c.city = 'Seattle'` que consume 5 RU, puede realizar entonces (1000 RU/s)/(5 RU/consulta) = 200 consultas/s de estas por segundo. 

Si envía más de 200 consultas/s, servicio de hello inicia solicitudes entrantes de limitación de velocidad por encima de 200/s. Hola SDK automáticamente controlar este caso mediante la realización de un reintento de retroceso, por lo tanto, podría observar una latencia mayor para estas consultas. Aumentar Hola aprovisionado rendimiento toohello requiere valor mejora la latencia de las consultas y el rendimiento. 

toolearn más acerca de las unidades de solicitud, vea [unidades de solicitud](request-units.md).

### <a name="partitioning-and-partition-keys"></a>Creación de particiones y claves de partición
Con la base de datos de Azure Cosmos, por lo general las consultas realizan en hello siguiendo el orden de más rápido y más eficiente tooslower/menos eficaz. 

* GET en una única clave de partición y una clave de elemento
* Consulta con una cláusula de filtro en una única clave de partición
* Consulta sin una cláusula de filtro de igualdad o intervalo en cualquier propiedad
* Sin filtros de consulta

Las consultas que tooconsult necesidad de todas las particiones necesidad de una latencia mayor y puede consumir RUs superior. Puesto que cada partición tiene la indexación automática en todas las propiedades, consultas de hello pueden proporcionarse eficazmente desde el índice de hello en este caso. Puede hacer que las consultas que abarcan las particiones más rápidas con las opciones de paralelismo de Hola.

toolearn más información sobre la creación de particiones y las claves de partición, vea [particiones en la base de datos de Azure Cosmos](partition-data.md).

### <a name="sdk-and-query-options"></a>SDK y opciones de consulta
Vea [sugerencias de rendimiento](performance-tips.md) y [las pruebas de rendimiento](performance-testing.md) para cómo tooget Hola mejor rendimiento de cliente de base de datos de Azure Cosmos. Esto incluye el uso de Hola SDK más reciente, configurar las configuraciones específicas de la plataforma como número predeterminado de conexiones, frecuencia de recolección de elementos y con opciones de conectividad ligera como Direct/TCP. 


#### <a name="max-item-count"></a>Recuento máximo de elementos
Para las consultas, Hola valo `MaxItemCount` puede tener un impacto significativo en el momento de la consulta to-end. Cada acción de ida y devolverá no más de número de Hola de elementos de servidor toohello `MaxItemCount` (valor predeterminado de 100 elementos). Al establecer este valor más alto de tooa (-1 es máximos y recomendados) mejorará la duración de consulta general limitando el número de Hola de ida y vuelta entre el servidor y cliente, especialmente para las consultas con grandes conjuntos de resultados.

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxItemCount = -1, 
    }).AsDocumentQuery();
```

#### <a name="max-degree-of-parallelism"></a>Grado máximo de paralelismo
Para las consultas, optimizar hello `MaxDegreeOfParallelism` tooidentify configuraciones de mejores hello para la aplicación, especialmente si lleva a cabo las consultas entre particiones (sin un filtro en el valor de clave de partición de hello). `MaxDegreeOfParallelism`controla Hola número máximo de tareas en paralelo, es decir, máximo hello toobe particiones visitado en paralelo. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();
```

Supongamos que
* D. = número máximo predeterminado de tareas en paralelo (= número total de procesador en el equipo de cliente hello)
* P = número máximo especificado por el usuario de tareas en paralelo
* N = número de particiones que necesita toobe visitado para responder a una consulta

Son las siguientes implicaciones de cómo las consultas en paralelo Hola comportaría para los distintos valores de P.
* (P == 0) => modo serie
* (P == 1) => un máximo de una tarea
* (P > 1) => mínimo de tareas en paralelo (P, N) 
* (P < 1) => mínimo de tareas en paralelo (N, D)

Para acceder a notas de versión de SDK y conocer detalles sobre las clases y los métodos implementados, consulte [SDK de DocumentDB](documentdb-sdk-dotnet.md)

### <a name="network-latency"></a>Latencia de red
Vea [distribución global de base de datos de Azure Cosmos](tutorial-global-distribution-documentdb.md) acerca de cómo tooset una copia de seguridad distribución global y conectar la región más cercana de toohello. Latencia de red tiene un impacto significativo en el rendimiento de las consultas cuando necesite toomake varios ida y vuelta o recuperar un gran conjunto de resultados de consulta de Hola. 

Hello sección en métricas de ejecución de consulta explica cómo tooretrieve Hola servidor tiempo de ejecución de consultas ( `totalExecutionTimeInMs`), de modo que puede diferenciar entre el tiempo invertido en la ejecución de la consulta y el tiempo empleado en tránsito de la red.

### <a name="indexing-policy"></a>Directiva de indexación
Para información sobre las rutas de indexación, las clases y los modos y cómo afectan a la ejecución de consultas, consulte [Configuración de la directiva de indexación](indexing-policies.md). De forma predeterminada, directiva de indexación de hello utiliza indización de Hash para las cadenas, que es efectivo para las consultas de igualdad, pero no para las consultas de intervalo/order por las consultas. Si tiene consultas por rango para las cadenas, se recomienda especificar tipo de índice de intervalo para todas las cadenas de Hola. 

## <a name="query-execution-metrics"></a>Métricas de ejecución de consultas
Puede obtener métricas detalladas en ejecución de la consulta pasando Hola opcional `x-ms-documentdb-populatequerymetrics` encabezado (`FeedOptions.PopulateQueryMetrics` Hola .NET SDK). Hola de valor devuelto en `x-ms-documentdb-query-metrics` tiene Hola siguientes pares de clave-valor dirigidas a los de solución de problemas de ejecución de consulta avanzada. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();

// Returns metrics by partition key range Id
IReadOnlyDictionary<string, QueryMetrics> metrics = result.QueryMetrics;

```

| Métrica | Unidad | Descripción | 
| ------ | -----| ----------- |
| `totalExecutionTimeInMs` | milisegundos | Tiempo de ejecución de consulta | 
| `queryCompileTimeInMs` | milisegundos | Tiempo de compilación de consulta  | 
| `queryLogicalPlanBuildTimeInMs` | milisegundos | Plan de consulta lógica toobuild de tiempo | 
| `queryPhysicalPlanBuildTimeInMs` | milisegundos | Plan de consulta físico de toobuild de tiempo | 
| `queryOptimizationTimeInMs` | milisegundos | Tiempo invertido en optimizar la consulta | 
| `VMExecutionTimeInMs` | milisegundos | Tiempo invertido en el tiempo de ejecución de consulta | 
| `indexLookupTimeInMs` | milisegundos | Tiempo invertido en la capa física de índice | 
| `documentLoadTimeInMs` | milisegundos | Tiempo invertido en la carga de documentos  | 
| `systemFunctionExecuteTimeInMs` | milisegundos | Tiempo total invertido en ejecutar funciones del sistema (integradas), en milisegundos  | 
| `userFunctionExecuteTimeInMs` | milisegundos | Tiempo total invertido en ejecutar funciones definidas por el usuario, en milisegundos | 
| `retrievedDocumentCount` | milisegundos | Número total de documentos recuperados  | 
| `retrievedDocumentSize` | bytes | Tamaño total de los documentos recuperados, en bytes  | 
| `outputDocumentCount` | count | Número de documentos de salida | 
| `writeOutputTimeInMs` | milisegundos | Tiempo de ejecución de consultas, en milisegundos | 
| `indexUtilizationRatio` | relación (<= 1) | Proporción del número de documentos que coincide con el número de toohello de filtro de Hola de documentos cargados  | 

Hello cliente SDK puede internamente realizar varias operaciones tooserve Hola consulta dentro de cada partición. cliente de Hello realiza más de una llamada por partición si superan los resultados totales de hello `x-ms-max-item-count`si consulta Hola supera el rendimiento aprovisionado de hello para la partición de hello, o si hello carga de consulta alcanza el tamaño máximo de Hola por página, o si hello consulta alcanza Hola sistema asignado el límite de tiempo de espera. Cada ejecución de consultas parcial devuelve un valor `x-ms-documentdb-query-metrics` para esa página. 

Estas son algunas consultas de ejemplo y cómo toointerpret algunas de las métricas de hello proceden de la ejecución de la consulta: 

| Consultar | Métrica de ejemplo | Descripción | 
| ------ | -----| ----------- |
| `SELECT TOP 100 * FROM c` | `"RetrievedDocumentCount": 101` | Hola número de documentos directamente recuperados es 100 + 1 cláusula TOP de toomatch Hola. El tiempo de la consulta se invierte mayormente en `WriteOutputTime` y `DocumentLoadTime` dado que es un examen. | 
| `SELECT TOP 500 * FROM c` | `"RetrievedDocumentCount": 501` | RetrievedDocumentCount es ahora mayor (500 + 1 toomatch Hola cláusula TOP). | 
| `SELECT * FROM c WHERE c.N = 55` | `"IndexLookupTime": "00:00:00.0009500"` | 0,9 ms se invierten en IndexLookupTime en una búsqueda de claves, porque es una búsqueda de índice en `/N/?`. | 
| `SELECT * FROM c WHERE c.N > 55` | `"IndexLookupTime": "00:00:00.0017700"` | Un poco más de tiempo (1,7 ms) se invierte en IndexLookupTime durante un examen de intervalo, porque es una búsqueda de índice en `/N/?`. | 
| `SELECT TOP 500 c.N FROM c` | `"IndexLookupTime": "00:00:00.0017700"` | El mismo tiempo se invierte en `DocumentLoadTime` que en las consultas anteriores, pero menos `WriteOutputTime` porque solo se proyecta una propiedad. | 
| `SELECT TOP 500 udf.toPercent(c.N) FROM c` | `"UserDefinedFunctionExecutionTime": "00:00:00.2136500"` | Se dedica unos 213 ms `UserDefinedFunctionExecutionTime` ejecutar Hola UDF en cada valor de `c.N`. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(c.Name, 'Den')` | `"IndexLookupTime": "00:00:00.0006400", "SystemFunctionExecutionTime": "00:00:00.0074100"` | Aproximadamente 0,6 ms se invierten en `IndexLookupTime` en `/Name/?`. La mayoría de hello consulta el tiempo de ejecución (ms ~ 7) en `SystemFunctionExecutionTime`. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(LOWER(c.Name), 'den')` | `"IndexLookupTime": "00:00:00", "RetrievedDocumentCount": 2491,  "OutputDocumentCount": 500` | La consulta se realiza como un examen porque se emplea `LOWER`, y se devuelven 500 de los 2491 documentos recuperados. |


## <a name="next-steps"></a>Pasos siguientes
* toolearn sobre Hola admite operadores de consulta SQL y las palabras clave, consulte [consulta SQL](documentdb-sql-query.md). 
* toolearn acerca de las unidades de solicitud, vea [unidades de solicitud](request-units.md).
* toolearn sobre la directiva de indización, consulte [directiva de indexación](indexing-policies.md) 


