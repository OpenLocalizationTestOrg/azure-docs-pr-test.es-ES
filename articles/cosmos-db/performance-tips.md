---
title: sugerencias de aaaPerformance - Azure Cosmos DB NoSQL | Documentos de Microsoft
description: "Obtenga información acerca de rendimiento de base de datos de base de datos de Azure Cosmos de cliente configuración opciones tooimprove"
keywords: "¿Cómo tooimprove base de datos de rendimiento"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 94ff155e-f9bc-488f-8c7a-5e7037091bb9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: mimig
ms.openlocfilehash: 4f3e82ae5048e3dbc20b0fd891a2d3aa22adf3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tips-for-azure-cosmos-db"></a>Sugerencias de rendimiento para Azure Cosmos DB
Azure Cosmos DB es una base de datos distribuida rápida y flexible que se escala sin problemas con una latencia y un rendimiento garantizados. No tiene cambios de la arquitectura principal de toomake o escribir código complejo tooscale la base de datos con la base de datos de Cosmos. Escalar o reducir verticalmente es tan sencillo como realizar una única llamada de API o con el [método SDK](set-throughput.md#set-throughput-sdk). Sin embargo, dado que Cosmos DB se tiene acceso a través de llamadas de red no existe son las optimizaciones de lado cliente puede realizar tooachieve obtener un buen rendimiento.

Así que si se está preguntando "¿Cómo puedo mejorar el rendimiento de la base de datos?", Considere la posibilidad de hello siguientes opciones:

## <a name="networking"></a>Redes
<a id="direct-connection"></a>

1. **Directiva de conexión: uso del modo de conexión directa**

    Cómo un cliente conecta tooCosmos DB tiene importantes implicaciones en el rendimiento, especialmente en cuanto a la latencia de cliente observado. Hay dos opciones de configuración clave para la configuración de cliente de directiva de conexión: conexión de hello *modo* hello y [conexión *protocolo*](#connection-protocol).  Hola dos modos disponibles son:

   1. Modo de puerta de enlace (predeterminado)
   2. Modo directo

      Modo de puerta de enlace se admite en todas las plataformas SDK y es el predeterminado de hello configurado.  Si la aplicación se ejecuta dentro de una red corporativa con las restricciones del firewall estricta, modo de puerta de enlace es Hola mejor opción ya que utiliza el puerto HTTPS estándar hello y un extremo único. Hola contrapartida del rendimiento, sin embargo, es que el modo de puerta de enlace implica un salto de red adicional cada vez que se lee o escritos tooCosmos DB datos. Por este motivo, el modo Direct ofrece mejor rendimiento debido toofewer saltos de red.
<a id="use-tcp"></a>
2. **Directiva de conexión: usar el protocolo TCP de Hola**

    Al usar el modo directo, hay dos opciones de protocolo disponibles:

   * TCP
   * HTTPS

     Cosmos DB ofrece un modelo de programación RESTful sencillo y abierto sobre HTTPS. Además, ofrece un eficaz protocolo TCP, que también es RESTful en su modelo de comunicación y está disponible a través del SDK de cliente de .NET de Hola. Tanto HTTPS como TCP directo usan SSL para la autenticación inicial y cifrar el tráfico. Para obtener el mejor rendimiento, usar el protocolo TCP de hello cuando sea posible.

     Al usar TCP en modo de puerta de enlace, puerto TCP 443 es hello puerto DB Cosmos y 10255 es el puerto de la API de MongoDB de Hola. Cuando se utiliza TCP en modo directo, en puertos de puerta de enlace de suma toohello, necesita tooensure Hola puerto está abierto entre 10000 y 20000 porque Cosmos DB usa puertos TCP dinámicos. Si estos puertos no están abiertos e intentas toouse TCP, recibirá un error 503 Servicio no disponible.

     Hola modo de conectividad se configura durante la construcción de Hola de instancia de hello DocumentClient con el parámetro ConnectionPolicy Hola. Si se utiliza el modo directo, Hola protocolo también puede establecerse en el parámetro de ConnectionPolicy Hola.

    ```C#
    var serviceEndpoint = new Uri("https://contoso.documents.net");
    var authKey = new "your authKey from hello Azure portal";
    DocumentClient client = new DocumentClient(serviceEndpoint, authKey,
    new ConnectionPolicy
    {
        ConnectionMode = ConnectionMode.Direct,
        ConnectionProtocol = Protocol.Tcp
    });
    ```

    Dado que TCP solo se admite en modo directo, si se utiliza el modo de puerta de enlace, a continuación, Hola protocolo HTTPS siempre es usa toocommunicate con puerta de enlace de Hola y Hola valor para el protocolo en hello que connectionpolicy se omite.

    ![Ilustración de hello directiva de conexión de base de datos de Azure Cosmos](./media/performance-tips/connection-policy.png)

3. **Llame a la latencia de inicio de OpenAsync tooavoid en la primera solicitud**

    De forma predeterminada, primera solicitud de hello tiene una latencia mayor porque tiene la tabla de enrutamiento de direcciones de hello toofetch. tooavoid esta latencia de inicio en hello solicitar en primer lugar, debe llamar a OpenAsync() una vez durante la inicialización como se indica a continuación.

        await client.OpenAsync();
   <a id="same-region"></a>
4. **Colocación de los clientes en la misma región de Azure para aumentar el rendimiento**

    Cuando sea posible, las aplicaciones que llaman a base de datos de Cosmos Hola misma región que el contexto Hola base de datos de base de datos de Cosmos. Para ver una comparación aproximada, llama a tooCosmos DB dentro de hello misma región se completa en 1 o 2 ms, pero latencia Hola entre Hola oeste y este costa de hello US es > 50 ms. Esta latencia probablemente puede variar de solicitud toorequest según la ruta de hello realizada por solicitud de hello cuando pasan del límite de hello cliente toohello centro de datos de Azure. Hola menor latencia posible se consigue asegurándose de que realiza la llamada Hola aplicación se encuentra dentro de hello misma región de Azure como Hola aprovisionado el punto de conexión de base de datos de Cosmos. Para obtener una lista de regiones disponibles, consulte [Regiones de Azure](https://azure.microsoft.com/regions/#services).

    ![Ilustración de hello directiva de conexión de base de datos de Azure Cosmos](./media/performance-tips/same-region.png)
   <a id="increase-threads"></a>
5. **Aumento del número de subprocesos y tareas**

    Puesto que se realizan llamadas tooAzure Cosmos DB a través de red de hello, deberá grado de hello toovary de paralelismo de las solicitudes para que pase de aplicación de cliente de hello muy poco tiempo de espera entre solicitudes. Por ejemplo, si está usando. De NET [Task Parallel Library](https://msdn.microsoft.com//library/dd460717.aspx), cree en orden de Hola de 100s de tareas de lectura o escritura tooCosmos base de datos.

## <a name="sdk-usage"></a>Uso del SDK
1. **Instalar Hola SDK más reciente**

    Hola Cosmos DB SDK constantemente se están tooprovide mejorada Hola obtener el mejor rendimiento. Vea hello [Cosmos DB SDK](documentdb-sdk-dotnet.md) páginas toodetermine Hola SDK más reciente y revise mejoras.
2. **Usar a un cliente de base de datos de Cosmos de singleton para duración de saludo de la aplicación**

    Tenga en cuenta que cada instancia de DocumentClient está protegida frente amenazas y realiza una administración de conexiones y un almacenamiento en caché de las direcciones de manera eficiente cuando funciona en modo directo. administración de conexiones eficaz de tooallow y un mejor rendimiento si DocumentClient, resulta recomendable toouse una única instancia de DocumentClient por AppDomain dure Hola de aplicación hello.

   <a id="max-connection"></a>
3. **Aumento de System.Net MaxConnections por host al usar el modo de puerta de enlace**

    Las solicitudes de COSMOS DB se realizan a través de HTTPS/REST al utilizar el modo de puerta de enlace y son el límite de conexiones predeterminado toohello sometidos por nombre de host o dirección IP. Puede que tenga tooset Hola MaxConnections tooa alto (100-1000) para que hello biblioteca de cliente puede utilizar varias conexiones simultáneas tooCosmos base de datos. Hola .NET SDK 1.8.0 y anteriormente, Hola el valor predeterminado de [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx) es 50 y toochange Hola valor, puede establecer hello [Documents.Client.ConnectionPolicy.MaxConnectionLimit ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.connectionpolicy.maxconnectionlimit.aspx) tooa mayor valor.   
4. **Ajuste de consultas paralelas en colecciones particionadas**

     Versión 1.9.0 del SDK de .NET de DocumentDB y versiones posteriores de compatibilidad con las consultas en paralelo, lo que permitirá tooquery una colección con particiones en paralelo (vea [trabajar con hello SDK](documentdb-partition-data.md#working-with-the-azure-cosmos-db-sdks) hello relacionados y [ejemplos de código](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Queries/Program.cs) para obtener más información.) Las consultas en paralelo son tooimprove diseñada la latencia de consulta y el rendimiento a través de su serie correspondiente. Las consultas en paralelo proporcionan dos parámetros que los usuarios pueden ajustar toocustom ajustar sus requisitos, MaxDegreeOfParallelism (a): número máximo de hello toocontrol de particiones, a continuación, se puede consultar en paralelo y (b) MaxBufferedItemCount: número de hello toocontrol de resultados capturados previamente.

    (a) La consulta paralela ***Tuning MaxDegreeOfParallelism\:*** realiza consultas en varias particiones en paralelo. Sin embargo, los datos de una recopilación con particiones individual se capturan en serie con sentido toohello consulta. Por lo tanto, al establecer Hola MaxDegreeOfParallelism toohello número de particiones tiene la oportunidad máximo de Hola de lograr Hola mayoría de rendimiento de consulta, siempre que todas las demás condiciones de sistema permanecen igual Hola. Si no conoce el número de Hola de particiones, puede establecer número elevado de hello MaxDegreeOfParallelism tooa y sistema de hello elige mínimo hello (número de particiones, proporcionados por el usuario proporcionado) como Hola MaxDegreeOfParallelism.

    Es importante toonote que mejor ventajas de las consultas producen hello en paralelo si los datos de Hola se distribuyen uniformemente en todas las particiones con sentido toohello consulta. Si Hola particiones colección se crean particiones de tal forma que todos o a la mayoría de los datos de hello devueltos por una consulta se concentra en algunas particiones (una partición en el peor de los casos), a continuación, rendimiento Hola de consulta de Hola podría ser restringido por esas particiones.

    (b) ***para la optimización MaxBufferedItemCount\: *** consultas en paralelo es resultados de búsqueda toopre diseñada mientras se está procesando el lote actual de Hola de resultados por cliente hello. Hola ayuda general mejora la latencia de una consulta en la captura previa. MaxBufferedItemCount es número de hello parámetro toolimit Hola de resultados previamente capturados. Establecer MaxBufferedItemCount toohello espera el número de resultados devueltos (o un número mayor) permite Hola consulta tooreceive máximo aprovechan la captura previa.

    Tenga en cuenta que funciona la búsqueda anticipada Hola misma forma independientemente de hello MaxDegreeOfParallelism, y no hay un único búfer para los datos de Hola de todas las particiones.  
5. **Activación de GC del lado servidor**

    Puede ayudar a reducir la frecuencia de Hola de recolección de elementos en algunos casos. En. NET, establezca [gcServer](https://msdn.microsoft.com/library/ms229357.aspx) tootrue.
6. **Implementación del retroceso según intervalos RetryAfter**

    Durante las pruebas de rendimiento, debe aumentar la carga hasta que se limite una tasa de solicitudes pequeña. Si limita, Hola aplicación cliente debe intervalo de reintento de interrupción en la limitación de hello especificado por el servidor. Respeta Hola retroceso garantiza que dedicar una cantidad mínima de espera de tiempo entre reintentos. Compatibilidad con la directiva de reintento se incluye en la versión 1.8.0 y versiones posteriores de hello DocumentDB [.NET](documentdb-sdk-dotnet.md) y [Java](documentdb-sdk-java.md), versión 1.9.0 y versiones posteriores de hello [Node.js](documentdb-sdk-node.md) y [ Python](documentdb-sdk-python.md), y todas las versiones compatibles de hello [.NET Core](documentdb-sdk-dotnet-core.md) SDK. Para más información, consulte [Superación de los límites de rendimiento reservados](request-units.md#RequestRateTooLarge) y [RetryAfter](https://msdn.microsoft.com/library/microsoft.azure.documents.documentclientexception.retryafter.aspx).
7. **Escalado horizontal de la carga de trabajo de cliente**

    Si va a probar en los niveles de rendimiento alto (> 50.000 RU/s), aplicación de cliente de Hola quede cuello de botella de hello debido toohello máquina límite de uso de CPU o la red. Si alcanza este punto, puede continuar cuenta de base de datos de Cosmos de Hola de toopush aún más mediante el escalado horizontal de las aplicaciones cliente en varios servidores.
8. **Almacenamiento en caché de los identificadores URI de documentos para una latencia menor en las operaciones de lectura**

    Documento de la memoria caché URI siempre que sea posible para obtener el mejor rendimiento de lectura Hola.
   <a id="tune-page-size"></a>
9. **Ajustar el tamaño de página de Hola para consultas o leer fuentes para mejorar el rendimiento**

    Cuando realiza una masiva lee de documentos mediante la lectura fuente funcionalidad (por ejemplo, ReadDocumentFeedAsync) o al emitir una consulta SQL de DocumentDB, se devuelven resultados de hello en un modo segmentado si el conjunto de resultados de hello es demasiado grande. De forma predeterminada, se devuelven resultados en fragmentos de 1 MB o de 100 artículos, el límite que se alcance primero.

    número de hello tooreduce de red tooretrieve de viajes de ida y requiere todos los resultados aplicables, puede aumentar el tamaño de página de hello mediante too1000 de tooup de encabezado de solicitud de x-ms-max-item-count. En casos donde es necesario toodisplay solo unos pocos resultados, por ejemplo, si la API de interfaz o aplicación de usuario se devuelve solo 10 da como resultado un tiempo, también puede reducir Hola tamaño too10 tooreduce Hola rendimiento de páginas utilizado para las lecturas y las consultas.

    También es posible establecer el tamaño de página de hello utilizando Hola disponible Cosmos DB SDK.  Por ejemplo:

        IQueryable<dynamic> authorResults = client.CreateDocumentQuery(documentCollection.SelfLink, "SELECT p.Author FROM Pages p WHERE p.Title = 'About Seattle'", new FeedOptions { MaxItemCount = 1000 });
10. **Aumento del número de subprocesos y tareas**

    Vea [aumentar el número de subprocesos/tareas](#increase-threads) Hola sección de redes.

11. **Uso del proceso de host de 64 bits**

    Hola DocumentDB SDK funciona en un proceso de host de 32 bits cuando se utiliza la versión 1.11.4 del SDK de .NET de DocumentDB y versiones posteriores. Sin embargo, si utiliza consultas entre particiones, se recomienda el proceso de host de 64 bits para obtener un mejor rendimiento. Hola siguientes tipos de aplicaciones tiene el host de 32 bits procesa como valor predeterminado de hello, en orden toochange es too64 bits, siga estos pasos en función de tipo de saludo de la aplicación:

    - Para las aplicaciones ejecutables, esto puede hacerse por hello desactivando **preferencia de 32 bits** opción Hola **propiedades del proyecto** ventana hello **compilar** ficha.

    - Para VSTest basados en proyectos de prueba, puede hacerlo seleccionando **probar**->**una configuración de pruebas**->**predeterminado de arquitectura de procesador como X64**, de hello **Visual Studio Test** opción de menú.

    - Para aplicaciones Web ASP.NET implementadas localmente, esto puede hacerse mediante la comprobación de hello **versión de 64 bits del Hola uso de IIS Express para proyectos y sitios web**, en **herramientas** ->  **Opciones de**->**proyectos y soluciones**->**proyectos Web**.

    - Para aplicaciones Web ASP.NET implementadas en Azure, puede hacerlo eligiendo hello **plataforma de 64 bits** en hello **configuración de la aplicación** en hello portal de Azure.

## <a name="indexing-policy"></a>Directiva de indexación
1. **Uso de la indexación diferida para lograr tasas de ingesta más rápidas a horas punta**

    Base de datos de COSMOS permite toospecify – en nivel de colección de hello: una directiva de indexación, lo que le permite toochoose si desea que los documentos de hello en un toobe de colección que se indizan automáticamente o no.  Además, puede elegir entre actualizaciones de índices sincrónicas (coherentes) y asincrónicas (diferidas). De forma predeterminada, el índice de Hola se actualiza sincrónicamente en cada insert, replace o delete de una colección de toohello de documento. Sincrónicamente toohonor de las consultas de modo permite Hola Hola mismo [nivel de coherencia](consistency-levels.md) que Hola documento lee sin ningún retraso índice Hola demasiado "ponerse al día".

    Puede considerar la indexación diferida para escenarios en los que los datos se escriben en ráfagas y desea tooamortize Hola trabajo necesario tooindex contenido durante un período más largo de tiempo. La indexación diferida también le permite toouse su aprovisionado el rendimiento de forma eficaz y servir las solicitudes de escritura en momentos de máxima con una latencia mínima. Es importante toonote, sin embargo, que, cuando está habilitada la indexación diferida, resultados de la consulta son coherentes independientemente del nivel de coherencia de hello configurada para la cuenta de base de datos de Cosmos Hola.

    Por lo tanto, modo de indexación coherente (IndexingPolicy.IndexingMode se establece tooConsistent) incurre Hola mayor solicitud cargo por unidad por escritura mientras Lazy indización modo (IndexingPolicy.IndexingMode tooLazy) y no la indización (IndexingPolicy.Automatic está establecido tooFalse) tienen un coste cero indización en tiempo de Hola de escritura.
2. **Exclusión de rutas de acceso sin utilizar de la indexación para acelerar las escrituras**

    Directiva de indexación de COSMOS de base de datos también le permite toospecify que tooinclude de rutas de acceso de documento o excluir de la indización mediante el aprovechamiento de las rutas de indización (IndexingPolicy.IncludedPaths y IndexingPolicy.ExcludedPaths). uso de Hola de rutas de acceso de la indización puede ofrecer un rendimiento de escritura mejorado y almacenamiento de índice inferior en escenarios en qué Hola patrones de consulta se conocen de antemano, ya que los costos de indización directamente correlacionados toohello número de rutas de acceso únicas indizadas.  Por ejemplo, hello siguiente código muestra cómo tooexclude toda una sección de hello documenta (conocido como) un subárbol) de la indización utilizando Hola "*" comodín.

    ```C#
    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*");
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);
    ```

    Para más información, consulte [Directivas de indexación de Azure Cosmos DB](indexing-policies.md).

## <a name="throughput"></a>Rendimiento
<a id="measure-rus"></a>

1. **Medición y optimización del uso menor de unidades de solicitud por segundo**

    COSMOS DB ofrece un amplio conjunto de operaciones de base de datos incluidas relacionales y jerárquicas de las consultas con UDF, procedimientos almacenados y desencadenadores: todos los controles en documentos de hello dentro de una colección de base de datos. costo de Hello asociada a cada una de estas operaciones varía en función de hello CPU, E/S y memoria necesaria toocomplete Hola operación. En lugar de pensar y administrar los recursos de hardware, se pueden considerar una unidad de solicitud (RU) como una única medida de hello recursos necesarios tooperform varias operaciones de base de datos y el servicio una solicitud de aplicación.

    [Unidades de solicitud](request-units.md) aprovisionados para cada cuenta de base de datos según el número de Hola de unidades de capacidad que adquiera. El consumo de la unidad de solicitud se evalúa como frecuencia por segundo. Las aplicaciones que superan la unidad de solicitud de aprovisionamiento de hello velocidad se limita su cuenta hasta que la velocidad de hello cae por debajo de hello nivel reservado para la cuenta de hello. Si su aplicación necesita un nivel mayor de capacidad de proceso, puede adquirir unidades de capacidad adicionales.

    complejidad de Hola de una consulta afecta a cuántas unidades de solicitud se usan para una operación. número de Hola de predicados, naturaleza de los predicados de hello, el número de UDF y tamaño de hello del conjunto de datos de origen de hello todos influyen en el costo de Hola de operaciones de consulta.

    sobrecarga de hello toomeasure de cualquier operación (crear, actualizar o eliminar), inspeccionar el encabezado x-ms-solicitud-cargo de hello (u Hola propiedad RequestCharge equivalente en ResourceResponse<T> o FeedResponse<T> Hola .NET SDK) toomeasure número de Hola de unidades de solicitud utilizado por estas operaciones.

    ```C#
    // Measure hello performance (request units) of writes
    ResourceResponse<Document> response = await client.CreateDocumentAsync(collectionSelfLink, myDocument);
    Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);
    // Measure hello performance (request units) of queries
    IDocumentQuery<dynamic> queryable = client.CreateDocumentQuery(collectionSelfLink, queryString).AsDocumentQuery();
    while (queryable.HasMoreResults)
         {
              FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>();
              Console.WriteLine("Query batch consumed {0} request units", queryResponse.RequestCharge);
         }
    ```             

    Hello devuelve en el encabezado de carga de solicitud es una fracción de su rendimiento aprovisionado (es decir, 2000 RUs / segundo). Por ejemplo, si hello consulta anterior devuelve documentos de 1KB de 1000, costo de Hola de operación de hello es 1000. Por lo tanto, dentro de un segundo servidor hello respeta sólo dos de estas solicitudes antes de la limitación de las solicitudes posteriores. Para obtener más información, consulte [unidades de solicitud](request-units.md) hello y [Calculadora de unidades de solicitud](https://www.documentdb.com/capacityplanner).
<a id="429"></a>
2. **Administración de la limitación de velocidad y la tasa de solicitudes demasiado grande**

    Cuando un cliente intenta tooexceed Hola reservado el rendimiento de una cuenta, no hay ninguna degradación del rendimiento en el servidor de Hola y ningún uso de la capacidad de rendimiento supera el nivel de hello reservado. servidor de Hola forma preferente finalizará solicitud Hola con RequestRateTooLarge (código de estado HTTP 429) y Hola devuelto x reintento ms después de ms de encabezado, indicando Hola período de tiempo, en milisegundos, que Hola usuario debe esperar antes de volver a intentar realizar la solicitud de Hola.

        HTTP Status 429,
        Status Line: RequestRateTooLarge
        x-ms-retry-after-ms :100

    implícitamente todos los SDK de Hello detecta esta respuesta, respeta encabezado Hola especificado por el servidor retry-after y vuelva a intentar la solicitud de saludo. A menos que su cuenta está obteniendo acceso al mismo tiempo varios clientes, el siguiente reintento de Hola se realizará correctamente.

    Si tiene más de un cliente de manera acumulativa operativo constantemente por encima de la tasa de solicitud de hello, Hola número de reintentos predeterminado actualmente conjunto too9 internamente por el cliente de hello puede no ser suficiente; en este caso, el cliente de hello produce un DocumentClientException con 429 toohello aplicación de código de estado. número de reintentos de Hello predeterminado puede cambiarse mediante hello RetryOptions de configuración en la instancia de ConnectionPolicy Hola. De forma predeterminada, se devuelve hello DocumentClientException con código de estado 429 después de un tiempo de espera acumulado de 30 segundos si solicitud Hola continúa toooperate por encima de la tasa de solicitud de Hola. Esto ocurre incluso si el número de reintentos actual de hello es inferior Hola máximo de reintentos, ya sea el valor predeterminado es Hola 9 o un valor definido por el usuario.

    Mientras Hola automatizada comportamiento para reintentar la ayuda a tooimprove resistencia y facilidad de uso para hello mayoría de las aplicaciones, podría realizar enfrentado al realizar pruebas comparativas de rendimiento, especialmente al medir la latencia.  latencia de Hello observados por el cliente tendrá un pico si experimento Hola aciertos Acelerador de servidor hello y hace que el cliente de hello reintento toosilently SDK. latencia de tooavoid tiene un pico en los experimentos de rendimiento, medida Hola cargo devueltos por cada operación y asegurarse de que las solicitudes están funcionando por debajo de la tasa de solicitud reservada de Hola. Para más información, consulte [Unidades de solicitud](request-units.md).
3. **Diseño de documentos más pequeños para un mayor rendimiento**

    Hola cargo de solicitud (es decir, el costo de procesamiento de la solicitud) de una operación determinada es directamente correlacionados toohello tamaño de documento de Hola. Las operaciones con documentos grandes cuestan más que las operaciones con documentos pequeños.

## <a name="next-steps"></a>Pasos siguientes
Para una tooevaluate de aplicación que se usa de ejemplo DB Cosmos para escenarios de alto rendimiento en algunos equipos cliente, consulte [pruebas con la base de datos de Cosmos de escala y rendimiento](performance-testing.md).

Además, toolearn más acerca de cómo diseñar la aplicación para la escala y alto rendimiento, consulte [particiones y ajuste de escala en la base de datos de Azure Cosmos](partition-data.md).
