---
title: aaaWorking con cambio de hello fuente compatibilidad en base de datos de Azure Cosmos | Documentos de Microsoft
description: "Base de datos de uso Azure Cosmos cambiar compatibilidad con fuentes tootrack cambios en documentos y realizar el procesamiento basado en eventos como desencadenadores y mantener actualizadas las cachés y análisis de sistemas."
keywords: fuente de cambios
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a>Trabajar con compatibilidad de fuentes del cambio de hello en la base de datos de Azure Cosmos
[Azure Cosmos DB](../cosmos-db/introduction.md) es un servicio de base de datos rápido y flexible, replicado globalmente, que se usa para almacenar elevados volúmenes de datos de transacciones y operaciones con una latencia predecible inferior a 10 milisegundos en lecturas y escrituras. Esto hace que sea adecuado para IoT, juegos y aplicaciones de registro de operaciones. Un patrón de diseño habitual en estas aplicaciones es tootrack cambios realizan tooAzure Cosmos DB datos y actualización vistas materializadas, realizan análisis en tiempo real, almacenamiento de datos toocold y generar notificaciones sobre determinados eventos en función de estos cambios. Hola **Cambiar fuente compatibilidad** en base de datos de Azure Cosmos permite toobuild eficaces y escalables soluciones para cada uno de estos patrones.

A cambio de fuente de soporte técnico, base de datos de Azure Cosmos proporciona una lista ordenada de documentos dentro de una colección de base de datos de Azure Cosmos en orden de hello en el que se han modificado. Esta fuente puede ser toolisten usado para las modificaciones toodata dentro de la colección de Hola y realizar acciones tales como:

* Desencadenar una tooan llamada API cuando se inserta o modifica un documento
* Realizar el procesamiento en tiempo real (secuencia) sobre las actualizaciones
* Sincronizar datos con una caché, un motor de búsqueda o un almacén de datos

Los cambios en Azure Cosmos DB se conservan y se pueden procesar de manera asincrónica y distribuirse entre uno o varios clientes para un procesamiento en paralelo. Echemos un vistazo a hello las API para la alimentación de cambio y cómo se pueden utilizar aplicaciones escalables en tiempo real de toobuild. En este artículo se muestra cómo toowork con base de datos de Azure Cosmos cambiar hello API de documentos y fuente. 

![Usar cambio de base de datos de Azure Cosmos el salto de análisis en tiempo real de toopower y escenarios informáticos orientada a eventos](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> Cambiar fuente compatibilidad solo se proporciona para hello API de documentos en este momento; Hola API Graph y la API de tabla no se admiten actualmente.

## <a name="use-cases-and-scenarios"></a>Casos de uso y escenarios
Cambiar fuente permite un procesamiento eficiente de grandes conjuntos de datos con un gran volumen de escrituras y ofrece un tooidentify de conjuntos de datos completo alternativo tooquerying qué ha cambiado. Por ejemplo, puede realizar Hola siguiente de forma eficaz las tareas:

* Actualizar una caché, un índice de búsqueda o un almacenamiento de datos con los datos almacenados en Azure Cosmos DB.
* Implementar niveles y el archivado de datos de nivel de aplicación, es decir, almacenar "datos activos" en la base de datos de Azure Cosmos y se reemplazan "datos inactivos" demasiado[almacenamiento de blobs de Azure](../storage/common/storage-introduction.md) o [almacén de Azure Data Lake](../data-lake-store/data-lake-store-overview.md).
* Implementar análisis por lotes sobre los datos mediante [Apache Hadoop](run-hadoop-with-hdinsight.md).
* Implementar [canalizaciones Lambda en Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) con Azure Cosmos DB. Azure Cosmos DB proporciona una solución de base de datos escalable que puede hacer frente tanto a la ingesta como a la consulta, e implementar arquitecturas Lambda con un bajo TCO. 
* Realizar cero tooanother migraciones de tiempo de inactividad de cuenta de base de datos de Azure Cosmos con un esquema de partición diferente.

**Canalizaciones Lambda con Azure Cosmos DB para ingesta y consulta:**

![Canalización Lambda basada en Azure Cosmos DB para ingesta y consulta](./media/change-feed/lambda.png)

Puede usar la base de datos de Azure Cosmos tooreceive y almacenar los datos de evento de dispositivos, sensores, infraestructura y las aplicaciones y procesar estos eventos en tiempo real con [análisis de transmisiones de Azure](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), o [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md). 

Dentro de su [sin servidor](http://azure.com/serverless) web y aplicaciones móviles, puede seguimiento de eventos como tootrigger de perfil, preferencias o la ubicación del cliente de cambios tooyour determinadas acciones como enviar inserción dispositivos de tootheir de notificaciones mediante [Las funciones de azure](../azure-functions/functions-bindings-documentdb.md) o [servicios de aplicaciones](https://azure.microsoft.com/services/app-service/). Si usa la base de datos de Azure Cosmos toobuild un juego, por ejemplo, puede utilizar tablas de líderes de cambio de fuente tooimplement en tiempo real en función de las puntuaciones de juegos completadas.

## <a name="how-change-feed-works-in-azure-cosmos-db"></a>Funcionamiento de la fuente de cambios en Azure Cosmos DB
Base de datos de Azure Cosmos proporciona Hola capacidad tooincrementally lee las actualizaciones realizadas tooan colección de base de datos de Azure Cosmos. Esta fuente de cambio tiene Hola propiedades siguientes:

* Los cambios son persistentes en Azure Cosmos DB y pueden procesarse de forma asincrónica.
* Toodocuments de cambios dentro de una colección están disponibles inmediatamente en fuente de cambio de Hola.
* Cada documento tooa de cambio aparece exactamente una vez en fuente de cambio de Hola y clientes administren la lógica de puntos de comprobación. biblioteca de fuentes del procesador de cambios de Hello proporciona semántica de puntos de comprobación automáticos y "al menos una vez".
* Único cambio más reciente de Hola para un documento determinado se incluye en el registro de cambios de Hola. Puede que los cambios intermedios no estén disponibles.
* Hola Cambiar fuente está ordenada por orden de modificación dentro de cada valor de clave de partición. No hay ningún orden garantizado entre valores de clave de partición.
* Los cambios se pueden sincronizar desde cualquier punto en el tiempo, es decir, no hay ningún período fijo de retención de datos en el que los cambios estén disponibles.
* Los cambios están disponibles en fragmentos de intervalos de claves de partición. Esta capacidad permite que los cambios de toobe de las colecciones grandes que se procesan en paralelo mediante varios consumidores/servidores.
* Las aplicaciones pueden solicitar para cambiar varias fuentes de distribución simultáneamente en hello misma colección.

La fuente de cambios de Azure DB Cosmos está habilitada de forma predeterminada para todas las cuentas. Puede usar el [rendimiento aprovisionado](request-units.md) en su región de escritura o cualquier [leer región](distribute-data-globally.md) tooread de hello Cambiar fuente, al igual que cualquier otra operación de base de datos de Azure Cosmos. Hola Cambiar fuente incluye inserciones y las operaciones de actualización realizadas toodocuments dentro de la colección de Hola. Puede capturar eliminaciones estableciendo un indicador "eliminación temporal" dentro de los documentos en lugar de eliminaciones. Como alternativa, puede establecer un período de caducidad finita para los documentos a través de hello [capacidad TTL](time-to-live.md), por ejemplo, 24 horas y use Hola valor de esa propiedad elimina toocapture. Con esta solución, ha cambiado de tooprocess dentro de un intervalo de tiempo más corto que el período de expiración del período de vida de Hola. Hola Cambiar fuente está disponible para cada intervalo de claves de partición dentro de la colección de documentos de hello y, por tanto, se puede distribuir en uno o varios consumidores para el procesamiento paralelo. 

![Procesamiento distribuido de la fuente de cambios de Azure Cosmos DB](./media/change-feed/changefeedvisual.png)

Tiene algunas opciones para implementar una fuente de cambios en el código de cliente. Hola secciones inmediatamente seguimiento describen cómo tooimplement Hola fuente de cambio mediante API de REST de base de datos de Azure Cosmos Hola y Hola SDK de DocumentDB. Sin embargo, para aplicaciones. NET, recomendamos usar Hola nueva [biblioteca de procesador de fuentes de cambio](#change-feed-processor) para procesar eventos de hello cambian fuente ya que simplifica los cambios de lectura en particiones y permite que varios subprocesos que se trabaja en paralelo. 

## <a id="rest-apis"></a>Trabajar con hello REST API y SDK de DocumentDB
Azure Cosmos DB proporciona contenedores elásticos de almacenamiento y rendimiento denominados **colecciones**. Los datos dentro de las colecciones están agrupados de manera lógica mediante [claves de partición](partition-data.md) para mejorar la escalabilidad y el rendimiento. Azure Cosmos DB proporciona varias API para acceder a estos datos, entre las que se incluyen búsqueda por identificador (leer/obtener), consulta y fuentes de lectura (exámenes). Hello Cambiar fuente puede obtenerse rellenando dos toohello de encabezados de solicitud nuevos documentos `ReadDocumentFeed` API y se pueden procesar en paralelo en intervalos de claves de partición.

### <a name="readdocumentfeed-api"></a>ReadDocumentFeed API
Examinemos brevemente cómo funciona ReadDocumentFeed. Base de datos de Azure Cosmos admite la lectura de una fuente de documentos dentro de una colección a través de hello `ReadDocumentFeed` API. Por ejemplo, hello solicitud siguiente devuelve una página de documentos dentro de hello `serverlogs` colección. 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Pueden estar limitados resultados mediante el uso de hello `x-ms-max-item-count` encabezado y las lecturas se pueden reanudar para volver a enviar la solicitud de hello con un `x-ms-continuation` encabezado se devuelve en la respuesta anterior Hola. Cuando se realiza desde un único cliente, `ReadDocumentFeed` realiza la iteración de los resultados entre particiones en serie. 

**Fuente de documento de lectura en serie**

También puede recuperar fuente hello de documentos mediante uno de hello admitida [SDK de base de datos de Azure Cosmos](documentdb-sdk-dotnet.md). Por ejemplo, hello fragmento siguiente muestra cómo hello toouse [ReadDocumentFeedAsync método](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) en. NET.

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a>Ejecución distribuida del ReadDocumentFeed
En el caso de colecciones que contienen terabytes de datos o mayores, o que realizan la ingesta de grandes volúmenes de actualizaciones, la ejecución en serie de la fuente de lectura desde una única máquina cliente puede que no sea una solución práctica. En orden toosupport estos escenarios de grandes cantidades de datos, base de datos de Azure Cosmos proporciona las API toodistribute `ReadDocumentFeed` llamadas de forma transparente a través de varios lectores/consumidores de cliente. 

**Fuente de documentos de lectura distribuida**

tooprovide escalables de procesamiento de cambios incrementales, Azure Cosmos DB admite un modelo de escalabilidad horizontal de cambio de hello fuente API basada en rangos de las claves de partición.

* Puede obtener una lista de intervalos de claves de partición para una colección mediante la ejecución de una llamada a `ReadPartitionKeyRanges`. 
* Para cada intervalo de claves de partición, puede realizar un `ReadDocumentFeed` tooread documentos con las claves de partición dentro de ese intervalo.

### <a name="retrieving-partition-key-ranges-for-a-collection"></a>Recuperación de los intervalos de claves de partición para una colección
Puede recuperar los intervalos de clave de partición de Hola Hola solicitante `pkranges` recursos dentro de una colección. Por ejemplo hello siguiente solicitud recupera Hola lista de intervalos de clave de partición para hello `serverlogs` colección:

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

Esta solicitud devuelve Hola después de respuesta que contiene metadatos sobre los intervalos de clave de partición de hello:

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


**Propiedades de intervalo de claves de partición**: cada intervalo de claves de partición incluye propiedades de metadatos de hello en hello en la tabla siguiente:

<table>
    <tr>
        <th>Nombre de encabezado</th>
        <th>Descripción</th>
    </tr>
    <tr>
        <td>id</td>
        <td>
            <p>Id. de Hello para el intervalo de claves de partición de Hola. Se trata de un identificador estable y único dentro de cada colección.</p>
            <p>Debe utilizarse en hello después llamada tooread cambios por intervalo de claves de partición.</p>
        </td>
    </tr>
    <tr>
        <td>maxExclusive</td>
        <td>valor de hash de clave de Hello máximo de las particiones de intervalo de claves de partición de Hola. Solo para uso interno.</td>
    </tr>
    <tr>
        <td>minInclusive</td>
        <td>valor de hash de clave de Hello mínimo de la partición de intervalo de claves de partición de Hola. Solo para uso interno.</td>
    </tr>       
</table>

Puede hacerlo mediante uno de hello admitida [SDK de base de datos de Azure Cosmos](documentdb-sdk-dotnet.md). Por ejemplo, hello fragmento de código siguiente muestra cómo intervalos de clave de partición tooretrieve en .NET mediante hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) método.

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

Base de datos de Azure Cosmos admite la recuperación de documentos por intervalo de claves de partición por hello configuración opcional `x-ms-documentdb-partitionkeyrangeid` encabezado. 

### <a name="performing-an-incremental-readdocumentfeed"></a>Realización de una operación ReadDocumentFeed incremental
ReadDocumentFeed admite Hola siguiente escenarios y las tareas para el procesamiento incremental de cambios en las colecciones de base de datos de Azure Cosmos:

* Lectura de todos los cambios toodocuments desde el principio de hello, es decir, de creación de la colección.
* Lectura de todos los cambios toofuture actualizaciones toodocuments de hora actual, o bien los cambios desde un tiempo especificado por el usuario.
* Leer toodocuments de todos los cambios de una versión lógica de colección de hello (ETag). Puede que los consumidores según Hola procedente de las solicitudes de lectura fuente incrementales la ETag de punto de comprobación.

los cambios de Hello incluyen toodocuments inserciones y actualizaciones. elimina toocapture, debe usar una propiedad de "eliminación temporal" dentro de los documentos o usar hello [propiedad TTL integrada](time-to-live.md) toosignal una eliminación pendiente en hello Cambiar fuente.

Hola siguientes Hola de listas de tabla [solicitud](/rest/api/documentdb/common-documentdb-rest-request-headers.md) y [encabezados de respuesta](/rest/api/documentdb/common-documentdb-rest-response-headers.md) para las operaciones de ReadDocumentFeed.

**Encabezados de solicitud para ReadDocumentFeed incremental**:

<table>
    <tr>
        <th>Nombre de encabezado</th>
        <th>Descripción</th>
    </tr>
    <tr>
        <td>A-IM</td>
        <td>Debe establecerse demasiado "Incremental fuente de distribución", o se omite en caso contrario</td>
    </tr>
    <tr>
        <td>If-None-Match</td>
        <td>
            <p>Ningún encabezado: devuelve todos los cambios de hello partir (creación de la colección)</p>
            <p>"*": devuelve todos los nuevos toodata cambios dentro de la colección de Hola</p>         
            <p>&lt;ETag&gt;: si establece tooa colección ETag, devuelve todos los cambios realizados desde esa marca de tiempo lógico</p>
        </td>
    </tr>
    <tr>    
        <td>If-Modified-Since</td> 
        <td>Formato de hora RFC 1123; se omite si se especifica If-None-Match</td> 
    </tr> 
    <tr>
        <td>x-ms-documentdb-partitionkeyrangeid</td>
        <td>Hola el identificador del intervalo de claves de partición para leer los datos.</td>
    </tr>
</table>

**Encabezados de respuesta para ReadDocumentFeed incremental**:

<table> <tr>
        <th>Nombre de encabezado</th>
        <th>Descripción</th>
    </tr>
    <tr>
        <td>ETag</td>
        <td>
            <p>número de secuencia lógica de Hello (LSN) del último documento devuelto en respuesta de Hola.</p>
            <p>La operación ReadDocumentFeed incremental se puede reanudar reenviando este valor en If-None-Match.</p>
        </td>
    </tr>
</table>

Este es un tooreturn de solicitud de ejemplo todos los cambios incrementales en la colección de versión/ETag lógico hello `28535` y rangos con clave de partición = `16`:

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Cambios se ordenan por tiempo dentro de cada valor de clave de partición dentro de intervalo de claves de partición de Hola. No hay ningún orden garantizado entre valores de clave de partición. Si no hay más resultados que pueden caber en una sola página, puede leer la siguiente página de resultados de Hola para volver a enviar la solicitud de hello con hello `If-None-Match` encabezado con valor igual toohello `etag` de respuesta de hello anterior. Si varios documentos fueron insertadas o actualizadas transaccionalmente dentro de un procedimiento almacenado o desencadenador, todos se devolverá en hello mismo página de respuesta.

> [!NOTE]
> A cambio de fuente, podría obtener más elementos devueltos en una página que los especificados en `x-ms-max-item-count` en caso de hello de varios documentos insertados o actualizados en los procedimientos almacenados o desencadenadores. 

Al utilizar Hola .NET SDK (1.17.0), establezca el campo de hello `StartTime` en `ChangeFeedOptions` toodirectly devuelto cambiado documentos desde `StartTime` al llamar a `CreateDocumentChangeFeedQuery`. Mediante la especificación de `If-Modified-Since` con hello API de REST, la solicitud devolverá no Hola documentos por sí mismos, pero en su lugar el token de continuación Hola o `etag` en el encabezado de respuesta de Hola. documentos de hello tooreturn Hola modificado especificado tiempo, token de continuación hello `etag` , a continuación, debe usarse en la siguiente solicitud de hello con `If-None-Match` tooreturn Hola documentos en cuestión. 

Hola .NET SDK proporciona hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) y [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) tooaccess realizados tooa colección de las clases auxiliares. Hello fragmento de código siguiente muestra cómo tooretrieve todos los cambios desde principio hello mediante Hola .NET SDK desde un solo cliente.

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
Y hello fragmento de código siguiente muestra cómo tooprocess cambia en tiempo real con la base de datos de Azure Cosmos mediante cambios de hello fuente soporte técnico y Hola delante de la función. Hola primera llamada devuelve todos los documentos de hello en la colección de Hola y Hola en segundo lugar solo devuelve Hola dos documentos creados que se crearon desde el último punto de comprobación Hola.

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

También puede filtrar la fuente de cambio de hello mediante lógica tooselectively proceso eventos de cliente. Por ejemplo, este es un fragmento de código que usa tooprocess LINQ de lado de cliente solo los eventos de cambio de temperatura de sensores de dispositivo.

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <a id="change-feed-processor"></a>Biblioteca de procesadores de fuente de cambios
Otra opción es hello toouse [biblioteca DB Cosmos Azure Cambiar fuente procesador](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), que puede ayudar a distribuir fácilmente el procesamiento de un cambio de fuente de distribución a través de varios consumidores de eventos. biblioteca de Hello es excelente para la creación de cambio de los lectores de fuentes de distribución en la plataforma .NET de Hola. Algunos flujos de trabajo que se simplifica mediante el uso de biblioteca de fuente de distribución de procesador de cambios de Hola a través de métodos de hello incluidos en hello otros SDK de base de datos de Cosmos incluyen: 

* Extracción de actualizaciones de fuente de cambios cuando los datos se almacenan en varias particiones
* Mover o replicar datos de una colección tooanother
* Ejecución en paralelo de las acciones desencadenadas por toodata de actualizaciones y cambio de fuente 

Aunque utilizando Hola API Hola Cosmos SDK proporciona acceso preciso toochange fuente de distribución de actualizaciones en cada partición, el uso de biblioteca de fuente de distribución de procesador de cambios de hello simplifica cambios de lectura a través de las particiones y varios subprocesos funcionan en paralelo. En lugar de leer manualmente los cambios de cada contenedor y guardar un token de continuación para cada partición, Hola Cambiar fuente procesador administra automáticamente los cambios de lectura a través de las particiones que usan un mecanismo de concesión.

biblioteca de Hello está disponible como un paquete de NuGet: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) y desde el código de origen como un Github [ejemplo](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor). 

### <a name="understanding-change-feed-processor-library"></a>Descripción de la biblioteca de procesadores de fuente de cambios 

Hay cuatro componentes principales de la implementación de hello Cambiar fuente procesador: Hola supervisa la colección, la recopilación de concesión de hello, host de procesador de Hola y los consumidores de Hola. 

**Recopilación supervisada:** colección Hola supervisado es datos de Hola desde qué Hola se genera el cambio de fuente. Cualquier recopilación de toohello supervisando las inserciones y cambios se reflejan en la fuente de cambio de Hola de colección de Hola. 

**Colección de concesión:** Hola coordenadas de la colección de concesión procesar cambio Hola fuente entre varios trabajadores. Una colección independiente es toostore usado Hola concesiones con una concesión por partición. Resulta ventajoso toostore esta colección de concesión en otra cuenta con hello escribir Hola región de toowhere cuanto más se acerque el procesador de fuente de cambio está ejecutando. Un objeto de concesión contiene Hola siguientes atributos: 
* Propietario: Especifica el host de Hola que posee la concesión de Hola
* Continuación: Especifica la posición de hello (token de continuación) en fuentes de distribución para una partición determinada, cambie Hola
* Marca de tiempo: Última vez que se actualizó la concesión; marca de tiempo de Hello puede ser toocheck usado si concesión Hola se considera caducado 

**Host de procesador:** cada host determina cuántos tooprocess particiones según el número de instancias de hosts tengan concesiones activas. 
1.  Cuando se inicia un host, adquiere la carga de trabajo de concesiones toobalance hello en todos los hosts. Un host renueva periódicamente concesiones, por lo que las concesiones permanecen activas. 
2.  Una host puntos de control hello última continuación tooits token concesión para cada lectura. comprobaciones de un host de seguridad de simultaneidad tooensure, hello ETag para cada actualización de la concesión. También se admiten otras estrategias de puntos de control.  
3.  Tras el cierre, un host libera todas las concesiones pero mantiene Hola información de continuación, por lo que puede reanudar la lectura desde el punto de comprobación almacenado Hola más adelante. 

En este momento el número de Hola de hosts no puede ser mayor que el número de Hola de particiones (concesiones).

**Los consumidores:** consumidores o los trabajadores, son los subprocesos que realizan cambios Hola fuente procesamiento iniciado por cada host. Cada host de procesador puede tener varios consumidores. Cada consumidor lee Hola Cambiar fuente de hello partición se asigna tooand notifica a su host de cambios y expirado concesiones.

toofurther comprender cómo funcionan conjuntamente estos cuatro elementos de procesador de fuente de cambios, echemos un vistazo a un ejemplo de Hola siguiente diagrama. Hola supervisa colección almacena los documentos y utiliza Hola "city" como clave de partición de Hola. Vemos que partición Hola azul contiene documentos con el campo "city" hello "A-e" y así sucesivamente. Hay dos hosts, cada uno con dos consumidores leyendo de particiones de hello cuatro en paralelo. las flechas de Hello muestran los consumidores de hello leer desde un punto específico en hello Cambiar fuente. En la primera partición hello, azul de hello borde más oscuro representa los cambios no leídos mientras azul claro Hola representa Hola ya leer los cambios en la fuente de cambio de Hola. los hosts de Hello usan Hola concesión colección toostore una pista de tookeep del valor de "continuación" de hello actual de lectura de posición para cada consumidor. 

![Cambio de la base de datos de Azure Cosmos de Hola de usar el salto de host de procesador](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a>Uso de la biblioteca de procesadores de fuente de cambios 
Hola siguiente sección explica cómo toouse Hola biblioteca de procesador de fuente de cambios en el contexto de Hola de replicación de cambios de una colección de destino de tooa de colección de origen. En este caso, Hola origen colección está Hola supervisado en el procesador de fuente de cambios. 

**Instalar e incluyen el paquete de NuGet del procesador de fuente de cambio de Hola** 

Antes de instalar el paquete NuGet del procesador de fuente de cambios, instale primero: 
* Microsoft.Azure.DocumentDB, versión 1.13.1 o posterior 
* Newtonsoft.Json, versión 9.0.1 o una versión posterior. Instale `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` e inclúyalo como una referencia.

**Creación una colección supervisada, de concesión y de destino**  

Hola de orden toouse biblioteca de procesador de cambios de fuente, colección de concesión de hello debe toobe creado antes de ejecutar hosts de procesador de Hola. Una vez más, es recomendable que almacene una colección de concesión en otra cuenta con un hello más cerca de toowhere de escritura región que está ejecutando el procesador de fuente de cambios. En este ejemplo de movimiento de datos, necesitamos recopilación de destino de hello toocreate antes de ejecutar el host de procesador de fuente de cambio de Hola. En el código de ejemplo de Hola llamamos un Hola de toocreate del método auxiliar supervisado, concedidas por y las colecciones de destino si aún no existen. 

> [!WARNING]
> Crear una colección tiene precios implicaciones, tal y como está reservando para hello toocommunicate de aplicación con la base de datos de Azure Cosmos rendimiento. Para obtener más detalles, visite hello [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

*Creación de un host de procesador*

Hola `ChangeFeedProcessorHost` clase proporciona un entorno en tiempo de ejecución de subprocesos, varios procesos y segura para las implementaciones de procesador de eventos que también proporciona administración de concesión de puntos de comprobación y la partición. Hola toouse `ChangeFeedProcessorHost` (clase), puede implementar `IChangeFeedObserver`. Esta interfaz contiene tres métodos:

* `OpenAsync`: Esta función se llama cuando se abre el observador de la fuente de cambios. Puede ser modificado tooperform una acción específica cuando se abre el consumidor/observador.  
* `CloseAsync`: Esta función se llama cuando se termina el observador de la fuente de cambios. Puede ser modificado tooperform una acción específica cuando se cierra el consumidor/observador.  
* `ProcessChangesAsync`: Esta función se llama cuando hay disponibles nuevos cambios de documento en la fuente de cambios. Puede ser modificado tooperform una acción específica en todas las actualizaciones de cambio de fuente.  

En nuestro ejemplo, implementamos interfaz hello `IChangeFeedObserver` a través de hello `DocumentFeedObserver` clase. En este caso, Hola `ProcessChangesAsync` función upserts (actualizaciones de) un documento de cambio de fuente en la colección de destino Hola. En este ejemplo es útil para mover datos de una colección tooanother en clave de partición de orden toochange Hola de un conjunto de datos. 

*Hola ejecución procesador de Host*

Antes de iniciar el procesamiento de eventos, se pueden personalizar tanto las opciones de fuente de cambios como las opciones de host de fuente de cambios. 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
en hello las tablas siguientes se resumen los campos específicos de Hola que se pueden personalizar. 

**Opciones de fuente de cambio**:
<table>
    <tr>
        <th>Nombre de propiedad</th>
        <th>Descripción</th>
    </tr>
    <tr>
        <td>MaxItemCount</td>
        <td>Obtiene o establece el número máximo de Hola de toobe de elementos devuelto en la operación de enumeración de hello en el servicio de base de datos de la base de datos de Azure Cosmos Hola.</td>
    </tr>
    <tr>
        <td>PartitionKeyRangeId</td>
        <td>Obtiene o establece el Id. del intervalo de claves de partición de hello para la solicitud actual de hello en el servicio de base de datos de base de datos de Azure Cosmos Hola.</td>
    </tr>
    <tr>
        <td>RequestContinuation</td>
        <td>Obtiene o establece el token de continuación de solicitud de hello en el servicio de base de datos de base de datos de Azure Cosmos Hola.</td>
    </tr>
        <tr>
        <td>SessionToken</td>
        <td>Obtiene o establece el token de sesión de Hola para su uso con coherencia de la sesión en el servicio de base de datos de la base de datos de Azure Cosmos Hola.</td>
    </tr>
        <tr>
        <td>StartFromBeginning</td>
        <td>Obtiene o establece si el cambio de la fuente en el servicio de base de datos de base de datos de Azure Cosmos Hola debe iniciar desde Hola partir (true) o actual (false). De forma predeterminada, se inicia desde la posición actual (false).</td>
    </tr>
</table>

**Opciones de host de fuente de cambios**:
<table>
    <tr>
        <th>Nombre de propiedad</th>
        <th>Tipo</th>
        <th>Descripción</th>
    </tr>
    <tr>
        <td>LeaseRenewInterval</td>
        <td>TimeSpan</td>
        <td>intervalo de saludo para todas las concesiones para las particiones que actualmente mantenidos por la instancia de ChangeFeedEventHost Hola.</td>
    </tr>
    <tr>
        <td>LeaseAcquireInterval</td>
        <td>TimeSpan</td>
        <td>Hola tookick intervalo desactivar un toocompute tarea si las particiones se distribuyen uniformemente entre las instancias de host conocidos.</td>
    </tr>
    <tr>
        <td>LeaseExpirationInterval</td>
        <td>TimeSpan</td>
        <td>intervalo de saludo para qué Hola concesión se usa en una concesión que representa una partición. Si no se renueva la concesión de hello dentro de este intervalo, ha expirado y propiedad de partición de hello pasa tooanother ChangeFeedEventHost instancia.</td>
    </tr>
    <tr>
        <td>FeedPollDelay</td>
        <td>TimeSpan</td>
        <td>fuente de retraso de Hello entre el sondeo de una partición para los nuevos cambios en hello, después de que se agotan todos los cambios actuales.</td>
    </tr>
    <tr>
        <td>CheckpointFrequency</td>
        <td>CheckpointFrequency</td>
        <td>Hola concesiones de toocheckpoint de frecuencia.</td>
    </tr>
    <tr>
        <td>MinPartitionCount</td>
        <td>int</td>
        <td>Recuento mínimo de la partición de Hello para el host de Hola.</td>
    </tr>
    <tr>
        <td>MaxPartitionCount</td>
        <td>int</td>
        <td>número máximo de Hola de host de Hola de particiones puede servir.</td>
    </tr>
    <tr>
        <td>DiscardExistingLeases</td>
        <td>Booleano</td>
        <td>Si en hello inicio del host de hello todas las concesiones existentes debe eliminarse y host de hello debe empezar desde cero.</td>
    </tr>
</table>


crear una instancia de toostart procesamiento de eventos, `ChangeFeedProcessorHost`, proporcionando los parámetros apropiados de hello para la colección de la base de datos de Azure Cosmos. A continuación, llame a `RegisterObserverAsync` tooregister su `IChangeFeedObserver` implementación (DocumentFeedObserver en este ejemplo) con hello en tiempo de ejecución. En este momento, el host de hello intente tooacquire una concesión en cada intervalo de claves de partición en la colección de base de datos de Azure Cosmos Hola usando un algoritmo "expansivo". Estas concesiones duran un período de tiempo determinado y después deben renovarse. Como nuevos nodos, instancias de trabajo, en este caso, se ponen en línea, colocan reservas de concesiones y con el tiempo carga Hola se desplaza entre los nodos como los intentos de cada host tooacquire más concesiones. 

En el código de ejemplo de Hola, usamos un toocreate (DocumentFeedObserverFactory.cs) de la clase de generador un observador y hello `RegistObserverFactoryAsync` observador de hello tooregister. 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
Con el tiempo, se establece un equilibrio. Esta capacidad dinámica permite basada en CPU tooconsumers toobe aplica la escala automática de ampliación y reducción. Si los cambios están disponibles en la base de datos de Azure Cosmos en mayor velocidad que los consumidores pueden procesar, aumento de la CPU de hello en los consumidores puede ser usado toocause una escala automática en el recuento de instancias de trabajo.

## <a name="next-steps"></a>Pasos siguientes
* Intente hello [cambio de base de datos de Azure Cosmos fuente ejemplos de código en GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)
* Comenzar a codificar con hello [SDK de base de datos de Azure Cosmos](documentdb-sdk-dotnet.md) o hello [API de REST](/rest/api/documentdb/).
