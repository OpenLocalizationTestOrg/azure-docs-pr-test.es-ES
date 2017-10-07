---
title: aaaHow toouse almacenamiento de cola de Azure con hello SDK de WebJobs
description: "Obtenga información acerca de cómo toouse Azure cola de almacenamiento con hello SDK de WebJobs. Cree y elimine colas; inserte, inspeccione, obtenga y elimine mensajes de la cola y mucho más."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: dbfac5d9-f4a0-4e3e-9ecc-af3d7bf80463
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 49f844436b0453489800b2762a5c7dc30b9db805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-queue-storage-with-hello-webjobs-sdk"></a>¿Cómo toouse Azure cola de almacenamiento con hello SDK de WebJobs
## <a name="overview"></a>Información general
Esta guía proporcionan ejemplos de código de C# que muestran cómo toouse Hola versión del SDK de WebJobs de Azure 1.x con hello servicio de almacenamiento de cola de Azure.

Guía de Hola se supone que sabe [cómo cadenas toocreate un proyecto WebJob en Visual Studio con una conexión de esa cuenta de almacenamiento de punto tooyour](websites-dotnet-webjobs-sdk-get-started.md) o demasiado[varias cuentas de almacenamiento](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

La mayoría de los fragmentos de código de hello mostrar sólo las funciones, no Hola código que crea hello `JobHost` objeto como en este ejemplo:

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

Guía de Hello incluye Hola temas siguientes:

* [¿Cómo tootrigger una función cuando se recibe un mensaje de la cola](#trigger)
  * Mensajes en cola de cadena
  * Mensaje en cola de POCO
  * Funciones asincrónicas
  * Atributo de tipos hello QueueTrigger funciona con
  * Algoritmo de sondeo
  * Varias instancias
  * Ejecución en paralelo
  * Obtener metadatos de cola o de mensaje en cola
  * Apagado correcto
* [¿Cómo toocreate una cola de mensajes al procesar un mensaje de cola](#createqueue)
  * Mensajes en cola de cadena
  * Mensaje en cola de POCO
  * Crear varios mensajes o en funciones asincrónicas
  * Atributo de cola de tipos Hola funciona con
  * Utilizar atributos de SDK de WebJobs en el cuerpo de Hola de una función
* [Cómo tooread y escritura de blobs al procesar un mensaje de cola](#blobs)
  * Mensajes en cola de cadena
  * Mensaje en cola de POCO
  * Atributo de Blob de tipos Hola funciona con
* [¿Cómo toohandle dudosos mensajes](#poison)
  * Control automático de mensajes dudosos
  * Control manual de mensajes dudosos
* [¿Cómo tooset las opciones de configuración](#config)
  * Establecer cadenas de conexión de SDK en el código
  * Configurar QueueTrigger
  * Establecer valores para los parámetros del constructor del SDK de WebJobs en el código
* [¿Cómo tootrigger una función manualmente](#manual)
* [Funcionamiento de los registros toowrite](#logs)
* [¿Cómo toohandle errores y configurar tiempos de espera](#errors)
* [Pasos siguientes](#nextsteps)

## <a id="trigger"></a>¿Cómo tootrigger una función cuando se recibe un mensaje de la cola
llama a una función que Hola SDK de WebJobs toowrite cuando se recibe un mensaje de la cola, utilice hello `QueueTrigger` atributo. constructor de atributo de Hello toma un parámetro de cadena que especifica el nombre hello de hello cola toopoll. También puede [establecer nombre de la cola de hello dinámicamente](#config).

### <a name="string-queue-messages"></a>Mensajes en cola de cadena
En el siguiente ejemplo de Hola, cola de hello contiene un mensaje de cadena, por lo que `QueueTrigger` es tooa aplicado parámetro de cadena denominado `logMessage` que incluye contenido de hello del mensaje de bienvenida de cola. Hola función [escribe un toohello de mensaje de registro panel](#logs).

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

Además `string`, parámetro hello puede ser una matriz de bytes, un `CloudQueueMessage` objeto o un POCO que defina.

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Mensajes en cola POCO [(objeto CRL estándar](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))
En el siguiente ejemplo de Hola, mensaje de bienvenida de cola contiene un valor JSON para un `BlobInformation` objeto que incluye un `BlobName` propiedad. Hola SDK automáticamente deserializa el objeto de Hola.

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Hola SDK utiliza hello [paquete NuGet de Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize y deserializar los mensajes. Si crea mensajes en cola en un programa que no utilice Hola SDK de WebJobs, puede escribir código como sigue toocreate un POCO de la cola de mensajes de ejemplo de Hola ese Hola que SDK puede analizar.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a>Funciones asincrónicas
Hola después de la función asincrónica [escribe un panel de registro toohello](#logs).

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

Funciones asincrónicas pueden tardar un [token de cancelación](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), tal y como se muestra en el siguiente ejemplo que copia un blob de Hola. (Para obtener una explicación de hello `queueTrigger` marcador de posición, vea hello [Blobs](#blobs) sección.)

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <a id="qtattributetypes"></a>Atributo de tipos hello QueueTrigger funciona con
Puede usar `QueueTrigger` con hello siguientes tipos:

* `string`
* Un tipo de POCO serializado como JSON
* `byte[]`
* `CloudQueueMessage`

### <a id="polling"></a> Algoritmo de sondeo
Hola SDK implementa un efecto de hello tooreduce aleatorio algoritmo de retroceso exponencial de sondeo en los costos de transacciones de almacenamiento de cola inactiva.  Cuando se encuentra un mensaje, Hola SDK espera dos segundos y, a continuación, comprueba si otro mensaje; Cuando se encuentra ningún mensaje espera unos cuatro segundos antes de volver a intentarlo. Después de los intentos subsiguientes tooget un mensaje de la cola, tiempo de espera de hello continúa tooincrease hasta que alcanza el tiempo de espera máximo de hello, qué minuto de tooone los valores predeterminados. [Hello tiempo de espera máximo es configurable](#config).

### <a id="instances"></a> Varias instancias
Si la aplicación web se ejecuta en varias instancias, se ejecuta un trabajo Web continuo en cada máquina e intentará toorun funciones y espere a que los desencadenadores cada máquina. Hola desencadenador de cola de SDK de WebJobs automáticamente impide que una función de procesamiento de un mensaje de cola varias veces; funciones no tienen toobe escrito toobe idempotente. Sin embargo, si desea que tooensure que solo una instancia de una función se ejecuta incluso si existen varias instancias de aplicación web de hello host, puede usar hello `Singleton` atributo.

### <a id="parallel"></a> Ejecución en paralelo
Si tiene varias funciones que escuchan en diferentes colas, Hola SDK llamará a ellos en paralelo cuando se reciben los mensajes al mismo tiempo.

Hello mismo puede decirse cuando se reciben varios mensajes de una sola cola. De forma predeterminada, Hola SDK Obtiene un lote de 16 mensajes en cola a la vez y ejecuta la función hello que los procesa en paralelo. [tamaño de lote de Hello es configurable](#config). Cuando se obtiene el número Hola procesando hacia abajo toohalf del tamaño de lote de hello, Hola SDK obtiene otro lote y empieza a procesar los mensajes. Por lo tanto, número máximo de Hola de mensajes simultáneos que se procesan por función es el tamaño del lote de una vez y Media Hola. Este límite aplica por separado tooeach función que tiene un `QueueTrigger` atributo.

Si no desea que la ejecución en paralelo para los mensajes recibidos en una cola, puede establecer too1 de tamaño de lote de Hola. Consulte también **más control sobre el procesamiento de colas** en [RTM de SDK de WebJobs de Azure 1.1.0](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).

### <a id="queuemetadata"></a>Obtener metadatos de cola o de mensaje en cola
Puede obtener Hola siguientes propiedades del mensaje mediante la adición de la firma del método toohello parámetros:

* `DateTimeOffset` expirationTime
* `DateTimeOffset` insertionTime
* `DateTimeOffset` nextVisibleTime
* `string` queueTrigger (contiene el texto del mensaje)
* `string` id
* `string` popReceipt
* `int` dequeueCount

Si desea que toowork directamente con hello API de almacenamiento de Azure, también puede agregar un `CloudStorageAccount` parámetro.

Hello en el ejemplo siguiente se escribe todos este metadatos tooan información registro de aplicación. En el ejemplo de Hola, logMessage y queueTrigger contengan Hola Hola del mensaje de cola.

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

Este es un registro de ejemplo escrito código de ejemplo de Hola:

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <a id="graceful"></a>Cierre estable
Una función que se ejecuta en un trabajo Web continuo puede aceptar un `CancellationToken` parámetro que permite Hola sistema operativo toonotify Hola función cuando hello trabajo Web es sobre toobe terminada. Puede usar este toomake notificación seguro función hello no finalizar inesperadamente de forma que deja los datos en un estado incoherente.

Hola siguiente ejemplo se muestra cómo toocheck de inminente finalización del trabajo Web en una función.

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

**Nota:** Hola panel no podría mostrar correctamente el estado de Hola y salida de funciones que se haya cerrado.

Para obtener más información, consulte [Cierre estable de WebJobs](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).   

## <a id="createqueue"></a>¿Cómo toocreate una cola de mensajes al procesar un mensaje de cola
una función que crea un nuevo mensaje de cola, use hello toowrite `Queue` atributo. Al igual que `QueueTrigger`, se pasa el nombre de la cola de hello como una cadena o bien puede [establecer nombre de la cola de hello dinámicamente](#config).

### <a name="string-queue-messages"></a>Mensajes en cola de cadena
Hola siguiendo el ejemplo de código asincrónico no crea un nuevo mensaje de cola en la cola de hello denominado "outputqueue" con hello igual contenido como mensaje de bienvenida de cola se recibió en cola Hola denominado "inputqueue". (En el caso de las funciones asincrónicas, use `IAsyncCollector<T>` como se muestra más adelante en esta sección).

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Mensajes en cola POCO [(objeto CRL estándar](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))
tipo de un mensaje de la cola que contiene un POCO en lugar de una cadena, pase Hola POCO toocreate como un toohello de parámetro de salida `Queue` constructor de atributos.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

Hola SDK serializa automáticamente Hola objeto tooJSON. Siempre se crea un mensaje de cola, incluso si el objeto de hello es null.

### <a name="create-multiple-messages-or-in-async-functions"></a>Crear varios mensajes o en funciones asincrónicas
toocreate varios mensajes, asegúrese de tipo de parámetro de hello para la cola de salida de hello `ICollector<T>` o `IAsyncCollector<T>`, tal y como se muestra en el siguiente ejemplo de Hola.

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Cada mensaje de la cola se crea inmediatamente cuando hello `Add` se llama al método.

### <a name="types-that-hello-queue-attribute-works-with"></a>Tipos de ese atributo de la cola de hello funciona con
Puede usar hello `Queue` atributo Hola siguientes tipos de parámetro:

* `out string`(se crea la cola de mensajes si el valor del parámetro es distinto de null cuando finaliza la función hello)
* `out byte[]` (funciona como `string`)
* `out CloudQueueMessage` (funciona como `string`)
* `out POCO`(un tipo serializable, crea un mensaje con un objeto null si el parámetro hello es nulo cuando finaliza la función hello)
* `ICollector`
* `IAsyncCollector`
* `CloudQueue`(para crear mensajes de forma manual mediante Hola API de almacenamiento de Azure directamente)

### <a id="ibinder"></a>Utilizar atributos de SDK de WebJobs en el cuerpo de Hola de una función
Si necesita toodo algunas funcionan en la función antes de usar como un atributo de SDK de WebJobs `Queue`, `Blob`, o `Table`, puede usar hello `IBinder` interfaz.

Hola siguiente ejemplo toma un mensaje de la cola de entrada y crea un nuevo mensaje con hello mismo contenido en una cola de salida. nombre de cola de salida de Hello se establece por código Hola cuerpo de función hello.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

Hola `IBinder` interfaz también se puede usar con hello `Table` y `Blob` atributos.

## <a id="blobs"></a>¿Cómo tooread y escritura de blobs y tablas al procesar un mensaje de cola
Hola `Blob` y `Table` atributos permiten tooread y escribir los blobs y tablas. ejemplos de Hello en esta sección aplican tooblobs. Para obtener ejemplos de código que muestran cómo tootrigger procesa cuando se crean o actualizan los blobs, vea [cómo toouse Azure blob storage con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)y para obtener ejemplos de código que leen y escriben las tablas, vea [cómo toouse tabla de Azure almacenamiento con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).

### <a name="string-queue-messages-triggering-blob-operations"></a>Mensajes en cola de cadena que desencadenan operaciones de blob
Para un mensaje de la cola que contiene una cadena, `queueTrigger` es un marcador de posición que se puede usar en hello `Blob` del atributo `blobPath` parámetro que contiene el contenido de Hola de mensaje de bienvenida.

Hello siguiente ejemplo se utiliza `Stream` objetos tooread y escritura de blobs. mensaje de bienvenida de cola es nombre Hola de un blob ubicado en hello textblobs contenedor. Una copia de blob de hello con "-nuevo" anexado toohello nombre se crea en Hola mismo contenedor.

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Hola `Blob` atributo constructor toma un `blobPath` parámetro que especifica el contenedor de Hola y el nombre de blob. Para obtener más información acerca de este marcador de posición, vea [cómo toouse Azure blob storage con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),

Cuando el atributo de hello decora un `Stream` objeto, otro parámetro de constructor especifica hello `FileAccess` modo como lectura, escritura o lectura/escritura.

Hello ejemplo siguiente se usa un `CloudBlockBlob` objeto toodelete un blob. mensaje de bienvenida de cola es nombre Hola de blob de Hola.

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a id="pocoblobs"></a> Mensajes en cola POCO [(objeto CRL estándar](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))
Para un POCO almacenado como JSON en el mensaje de bienvenida de cola, puede utilizar marcadores de posición que nombres de las propiedades del objeto de Hola Hola `Queue` del atributo `blobPath` parámetro. También puede utilizar [nombres de propiedad de metadatos de cola](#queuemetadata) como marcadores de posición.

Hello en el ejemplo siguiente se copia un blob nuevo de blob tooa con una extensión diferente. mensaje de bienvenida de cola es un `BlobInformation` objeto que incluya `BlobName` y `BlobNameWithoutExtension` propiedades. nombres de propiedad de Hola se utilizan como marcadores de posición en la ruta de acceso de blob de Hola para hello `Blob` atributos.

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Hola SDK utiliza hello [paquete NuGet de Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize y deserializar los mensajes. Si crea mensajes en cola en un programa que no utilice Hola SDK de WebJobs, puede escribir código como sigue toocreate un POCO de la cola de mensajes de ejemplo de Hola ese Hola que SDK puede analizar.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

Si necesita toodo algunas funcionan en la función antes de enlazar un objeto de tooan de blob, puede usar el atributo hello en el cuerpo de Hola de función de hello, [tal como se muestra anteriormente para el atributo de la cola de hello](#ibinder).

### <a id="blobattributetypes"></a>Tipos que puede usar Hola Blob de atributo con
Hola `Blob` atributo se puede usar con hello siguientes tipos:

* `Stream`(lectura o escritura, especificado mediante el parámetro de constructor de hello FileAccess)
* `TextReader`
* `TextWriter`
* `string` (lectura)
* `out string`(escribir; crea un blob solo si el parámetro de cadena de hello es distinto de null cuando la devolución de función hello)
* POCO (lectura)
* out POCO (escribir; siempre crea un blob, se crea como objeto null si POCO parámetro es null cuando la devolución de función hello)
* `CloudBlobStream` (escritura)
* `ICloudBlob` (lectura o escritura)
* `CloudBlockBlob` (lectura o escritura)
* `CloudPageBlob` (lectura o escritura)

## <a id="poison"></a>¿Cómo toohandle dudosos mensajes
Se denominan mensajes cuyo contenido hace que una función toofail *mensajes dudosos*. Cuando se produce un error en la función hello, mensaje de bienvenida de cola no se elimina y finalmente recoge nuevo, que producen Hola ciclo toobe repetido. Hola SDK automáticamente puede interrumpir el ciclo de hello después de un número limitado de iteraciones, o puede hacerlo manualmente.

### <a name="automatic-poison-message-handling"></a>Control automático de mensajes dudosos
Hola SDK llamará a una función de seguridad too5 veces tooprocess un mensaje de la cola. Si se produce un error en try quinto hello, mensaje de bienvenida es movida tooa cola de mensajes dudosos. [Hola número máximo de reintentos es configurable](#config).

cola de mensajes dudosos Hola se denomina *{originalqueuename}*-dudoso. Puede escribir una función tooprocess mensajes desde la cola de mensajes dudosos Hola registrarlos o enviar una notificación que se necesita atención manual.

Después de hello de ejemplo de Hola `CopyBlob` function no funcionará correctamente cuando un mensaje de la cola contiene el nombre de Hola de un blob que no existe. Cuando esto ocurre, mensaje de saludo se mueve desde hello copyblobqueue toohello copyblobqueue dudosos cola. Hola `ProcessPoisonMessage` , a continuación, registros de Hola de mensajes dudosos.

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

Hello en la ilustración siguiente se muestra la salida de consola de estas funciones cuando se procesa un mensaje dudoso.

![Salida de consola para el control de mensajes dudosos](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a>Control manual de mensajes dudosos
Puede obtener Hola número de veces que se ha detectado un mensaje para su procesamiento mediante la adición de un `int` parámetro denominado `dequeueCount` tooyour función. También puede, a continuación, Hola de comprobación de recuento en el código de la función de eliminación de cola y realizar su propio control de mensajes dudosos al número de hello supera un umbral, como se muestra en el siguiente ejemplo de Hola.

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a id="config"></a>¿Cómo tooset las opciones de configuración
Puede usar hello `JobHostConfiguration` Hola de tipo tooset opciones de configuración siguientes:

* Establecer las cadenas de conexión de SDK de hello en el código.
* Configurar `QueueTrigger` como el recuento de eliminación de cola máximo.
* Obtener nombres de cola a partir de la configuración.

### <a id="setconnstr"></a>Establecer cadenas de conexión de SDK en el código
Establecer las cadenas de conexión de SDK de hello en el código permite toouse sus propios nombres de cadena de conexión en archivos de configuración o las variables de entorno, como se muestra en el siguiente ejemplo de Hola.

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a id="configqueue"></a>Configurar QueueTrigger
Puede configurar Hola después de la configuración que se aplica el procesamiento de mensajes de cola de toohello:

* número máximo de mensajes en cola que se recogen simultáneamente toobe ejecutada en paralelo de Hola (el valor predeterminado es 16).
* Hola número máximo de reintentos antes de enviar un mensaje de cola de cola de mensajes dudosos tooa (el valor predeterminado es 5).
* tiempo de espera máximo de Hello antes de volver a sondear cuando una cola está vacía (el valor predeterminado es 1 minuto).

Hola siguiente ejemplo se muestra cómo tooconfigure esta configuración:

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a id="setnamesincode"></a>Establecer valores para los parámetros del constructor del SDK de WebJobs en el código
A veces desea toospecify un nombre de cola, un nombre de blob o contenedor o una tabla asígnele el nombre en código, en lugar de codificar de forma rígida. Por ejemplo, puede querer toospecify nombre de cola de Hola para `QueueTrigger` en una variable de entorno o de archivo de configuración.

Puede hacerlo pasando un `NameResolver` objeto toohello `JobHostConfiguration` tipo. Incluir marcadores de posición especial entre signos de porcentaje (%) en los parámetros del constructor de atributo de SDK de WebJobs y su `NameResolver` código especifica Hola valores reales toobe usar en lugar de los marcadores de posición.

Por ejemplo, suponga que desea toouse una cola denominada logqueuetest en entorno de prueba de hello y una logqueueprod con nombre en producción. En lugar de un nombre de cola codificado de forma rígida, desea que el nombre de Hola de toospecify de una entrada en hello `appSettings` colección que tendría el nombre de la cola real de Hola. Si hello `appSettings` clave es logqueue, la función podría tener el aspecto como el siguiente ejemplo de Hola.

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

Su `NameResolver` clase, a continuación, pudo obtener el nombre de la cola de Hola de `appSettings` tal y como se muestra en el siguiente ejemplo de Hola:

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

Pasar hello `NameResolver` clase toohello `JobHost` objeto tal y como se muestra en el siguiente ejemplo de Hola.

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

**Nota:** nombres de blob, cola y tabla son de resolver cada vez que se invoque una función, pero se resuelven los nombres de contenedor de blob solamente cuando se inicia la aplicación hello. No se puede cambiar el nombre del contenedor de blob mientras se ejecuta el trabajo de Hola.

## <a id="manual"></a>¿Cómo tootrigger una función manualmente
una función de tootrigger manualmente, use hello `Call` o `CallAsync` método en hello `JobHost` hello y objeto `NoAutomaticTrigger` del atributo en función de hello, como se muestra en el siguiente ejemplo de Hola.

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <a id="logs"></a>Funcionamiento de los registros toowrite
Hola panel muestra los registros en dos lugares: Hola para hello trabajo Web y Hola página para una invocación de trabajo Web determinada.

![Registros en la página del trabajo web](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Registros en la página de invocación de la función](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

Salida de métodos de consola que se llama en una función o en hello `Main()` método aparece en la página de panel de Hola de hello trabajo Web, no en la página de Hola para una invocación de método determinado. Resultado del objeto de TextWriter Hola que obtendrá de un parámetro en la firma del método aparece en la página de panel de Hola de una invocación de método.

Salida de la consola no puede ser la invocación del método determinado tooa vinculado porque Hola consola tiene un único subproceso, mientras que muchas de las funciones de trabajo pueden estar ejecutando en hello mismo tiempo. Por eso Hola SDK proporciona cada invocación de función con su propio objeto de escritor de inicio de sesión únicos.

toowrite [registros de seguimiento de la aplicación](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (crea registros marcados como información) y `Console.Error` (crea registros marcados como ERROR). Una alternativa es toouse [seguimiento o TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), que proporciona Verbose, advertencia, y niveles de crítico en tooInfo de adición y Error. Registros de seguimiento de la aplicación aparecen en archivos de registro en la aplicación web de hello, tablas de Azure, o blobs de Azure según cómo configure la aplicación web de Azure. Como ocurre con todos los resultados de la consola, registros de aplicación 100 más recientes de hello también aparecen en la página de panel de Hola de hello trabajo Web, no la página de Hola de una invocación de función.

Salida de la consola aparece en hello panel únicamente si se ejecuta el programa de hello en un trabajo Web de Azure, no si programa Hola se ejecuta localmente o en algún otro entorno.

Deshabilite el registro del panel para escenarios de alto rendimiento. De forma predeterminada, Hola SDK escribe registros toostorage y esta actividad puede reducir el rendimiento cuando se procesan muchos mensajes. toodisable registro, establezca toonull de cadena de conexión de hello panel tal y como se muestra en el siguiente ejemplo de Hola.

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

Hello en el ejemplo siguiente se muestra varias maneras de toowrite registros:

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

En el panel de SDK de WebJobs de hello, Hola salida de hello `TextWriter` objeto se muestra cuando se desplace página toohello para un determinado invocación de función y haga clic en **alternar salida**:

![Clic en el vínculo de invocación de la función](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Registros en la página de invocación de la función](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

En el panel de SDK de WebJobs de hello, líneas de hello 100 más reciente de la consola de salida mostrar una al ir a página toohello para hello trabajo Web (no de invocación de función hello) y haga clic en **alternar salida**.

![Clic en Alternar resultados](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

En un trabajo Web continuo, registros de aplicaciones se mostrarán en/datos/trabajos/continua/*{webjobname}*/job_log.txt en sistema de archivos de aplicación web de Hola.

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

En una aplicación Hola de blobs de Azure registros este aspecto: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write: Hola a todos!, 2014-09-26T21:01:13, Error, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.Error - Hola a todos!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out: Hola a todos!,

Y en un saludo de la tabla de Azure `Console.Out` y `Console.Error` registros tiene este aspecto:

![Registro de información en la tabla](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Registro de errores en la tabla](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

Si desea tooplug en su propio registrador, vea [en este ejemplo](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).

## <a id="errors"></a>¿Cómo toohandle errores y configurar tiempos de espera
Hello WebJobs SDK también incluye una [tiempo de espera](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) atributo que se puede utilizar toocause un toobe función cancela si no se completa dentro de un período de tiempo especificado. Y si desea tooraise una alerta cuando se producen demasiados errores dentro de un período de tiempo especificado, se puede usar hello `ErrorTrigger` atributo. Este es un [ejemplo de ErrorTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    too= "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors toohello Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

Puede deshabilitar y habilitar funciones toocontrol, si bien pueden ser desencadenados, mediante un modificador de configuración que podría ser un nombre de variable de entorno o una configuración de aplicación también dinámicamente. Ejemplo de código, vea hello `Disable` atributo [repositorio de ejemplos de SDK de WebJobs de hello](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).

## <a id="nextsteps"></a> Pasos siguientes
Esta guía proporciona código de ejemplos que muestran cómo toohandle escenarios comunes para trabajar con colas de Azure. Para obtener más información sobre cómo toouse WebJobs de Azure y Hola SDK de WebJobs, vea [Azure trabajos Web recomienda recursos](http://go.microsoft.com/fwlink/?linkid=390226).
