---
title: aaaGetting a trabajar con Visual Studio y el almacenamiento de cola servicios conectados (proyectos de trabajo Web) | Documentos de Microsoft
description: "Cómo tooget iniciado mediante el almacenamiento de cola de Azure en un proyecto WebJob después de conectar la cuenta de almacenamiento de tooa con Visual Studio servicios conectados."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 720e96fda734c31e1b1d68d4f95aa9531a20a3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a>Introducción al Almacenamiento de colas de Azure y servicios conectados de Visual Studio (proyectos de WebJobs)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Información general
Este artículo se describe cómo obtener iniciado mediante la cola de Azure Hola de almacenamiento en un proyecto WebJob de Azure de Visual Studio después de haber creado o hace referencia a una cuenta de almacenamiento de Azure mediante Visual Studio **agregar servicios conectados** cuadro de diálogo. Cuando agrega un proyecto de WebJob de tooa de cuenta de almacenamiento mediante el uso de Visual Studio hello **agregar servicios conectados** cuadro de diálogo, se han instalado paquetes de NuGet de almacenamiento de Azure adecuados de hello, referencias de hello adecuadas .NET son toohello agregado proyecto y cadenas de conexión para la cuenta de almacenamiento de Hola se actualizan en el archivo App.config de hello.  

Este artículo proporciona ejemplos de código de C# que muestran cómo toouse Hola versión del SDK de WebJobs de Azure 1.x con hello servicio de almacenamiento de cola de Azure.

Almacenamiento de la cola de Azure es un servicio para almacenar grandes cantidades de mensajes que pueden tener acceso desde cualquier lugar Hola mundo a través de llamadas autenticadas mediante HTTP o HTTPS. Un mensaje de la cola solo puede estar too64 KB de tamaño y una cola puede contener millones de mensajes, seguridad toohello límite de capacidad total de una cuenta de almacenamiento. Consulte [Introducción al Almacenamiento en cola de Azure mediante .NET](storage-dotnet-how-to-use-queues.md) para más información. Para obtener más información acerca de ASP.NET, consulte [ASP.NET](http://www.asp.net).

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a>¿Cómo tootrigger una función cuando se recibe un mensaje de la cola
llama a una función que Hola SDK de WebJobs toowrite cuando se recibe un mensaje de la cola, utilice hello **QueueTrigger** atributo. constructor de atributo de Hello toma un parámetro de cadena que especifica el nombre hello de hello cola toopoll. toosee cómo tooset Hola nombre de la cola de forma dinámica, consulte [cómo tooset opciones de configuración](#how-to-set-configuration-options).

### <a name="string-queue-messages"></a>Mensajes en cola de cadena
En el siguiente ejemplo de Hola, cola de hello contiene un mensaje de cadena, por lo que **QueueTrigger** es tooa aplicado parámetro de cadena denominado **logMessage** que incluye contenido de hello del mensaje de bienvenida de cola. Hola función [escribe un toohello de mensaje de registro panel](#how-to-write-logs).

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

Además **cadena**, parámetro hello puede ser una matriz de bytes, un **CloudQueueMessage** objeto o un POCO que defina.

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Mensajes en cola POCO [(objeto CRL estándar](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))
En el siguiente ejemplo de Hola, mensaje de bienvenida de cola contiene un valor JSON para un **BlobInformation** objeto que incluye un **BlobName** propiedad. Hola SDK automáticamente deserializa el objeto de Hola.

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Hola SDK utiliza hello [paquete NuGet de Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize y deserializar los mensajes. Si crea mensajes en cola en un programa que no utilice Hola SDK de WebJobs, puede escribir código como sigue toocreate un POCO de la cola de mensajes de ejemplo de Hola ese Hola que SDK puede analizar.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a>Funciones asincrónicas
Hola después de la función asincrónica [escribe un panel de registro toohello](#how-to-write-logs).

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

Funciones asincrónicas pueden tardar un [token de cancelación](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), tal y como se muestra en el siguiente ejemplo que copia un blob de Hola. (Para obtener una explicación de hello **queueTrigger** marcador de posición, vea hello [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) sección.)

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a>Atributo de tipos hello QueueTrigger funciona con
Puede usar **QueueTrigger** con hello siguientes tipos:

* **cadena**
* Un tipo de POCO serializado como JSON
* **byte[]**
* **CloudQueueMessage**

## <a name="polling-algorithm"></a>Algoritmo de sondeo
Hola SDK implementa un efecto de hello tooreduce aleatorio algoritmo de retroceso exponencial de sondeo en los costos de transacciones de almacenamiento de cola inactiva.  Cuando se encuentra un mensaje, Hola SDK espera dos segundos y, a continuación, comprueba si otro mensaje; Cuando se encuentra ningún mensaje espera unos cuatro segundos antes de volver a intentarlo. Después de los intentos subsiguientes tooget un mensaje de la cola, tiempo de espera de hello continúa tooincrease hasta que alcanza el tiempo de espera máximo de hello, qué minuto de tooone los valores predeterminados. [Hello tiempo de espera máximo es configurable](#how-to-set-configuration-options).

## <a name="multiple-instances"></a>Varias instancias
Si la aplicación web se ejecuta en varias instancias, una trabajos Web continuos se ejecuta en cada equipo e intentará toorun funciones y espere a que los desencadenadores cada máquina. En algunos casos que esto puede provocar funciones toosome procesamiento Hola mismos datos dos veces, por lo que funciones deben ser idempotentes (escrito por lo llamar varias veces con hello no generan los mismos datos de entrada Duplicar resultados).  

## <a name="parallel-execution"></a>Ejecución en paralelo
Si tiene varias funciones que escuchan en diferentes colas, Hola SDK llamará a ellos en paralelo cuando se reciben los mensajes al mismo tiempo.

Hello mismo puede decirse cuando se reciben varios mensajes de una sola cola. De forma predeterminada, Hola SDK Obtiene un lote de 16 mensajes en cola a la vez y ejecuta la función hello que los procesa en paralelo. [tamaño de lote de Hello es configurable](#how-to-set-configuration-options). Cuando se obtiene el número Hola procesando hacia abajo toohalf del tamaño de lote de hello, Hola SDK obtiene otro lote y empieza a procesar los mensajes. Por lo tanto, número máximo de Hola de mensajes simultáneos que se procesan por función es el tamaño del lote de una vez y Media Hola. Este límite aplica por separado tooeach función que tiene un **QueueTrigger** atributo. Si no desea que la ejecución en paralelo para los mensajes recibidos en una cola, Establece too1 de tamaño de lote de Hola.

## <a name="get-queue-or-queue-message-metadata"></a>Obtener metadatos de cola o de mensaje en cola
Puede obtener Hola siguientes propiedades del mensaje mediante la adición de la firma del método toohello parámetros:

* **DateTimeOffset** expirationTime
* **DateTimeOffset** insertionTime
* **DateTimeOffset** nextVisibleTime
* **string** queueTrigger (contiene texto de mensaje)
* **string** id
* **string** popReceipt
* **int** dequeueCount

Si desea que toowork directamente con hello API de almacenamiento de Azure, también puede agregar un **CloudStorageAccount** parámetro.

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

## <a name="graceful-shutdown"></a>Apagado correcto
Una función que se ejecuta en un trabajo Web continuo puede aceptar un **CancellationToken** parámetro que permite Hola sistema operativo toonotify Hola función cuando hello trabajo Web es sobre toobe terminada. Puede usar este toomake notificación seguro función hello no finalizar inesperadamente de forma que deja los datos en un estado incoherente.

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

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a>¿Cómo toocreate una cola de mensajes al procesar un mensaje de cola
una función que crea un nuevo mensaje de cola, use hello toowrite **cola** atributo. Al igual que **QueueTrigger**, se pasa el nombre de la cola de hello como una cadena o bien puede [establecer nombre de la cola de hello dinámicamente](#how-to-set-configuration-options).

### <a name="string-queue-messages"></a>Mensajes en cola de cadena
Hola siguiendo el ejemplo de código asincrónico no crea un nuevo mensaje de cola en la cola de hello denominado "outputqueue" con hello igual contenido como mensaje de bienvenida de cola se recibió en cola Hola denominado "inputqueue". (En el caso de las funciones asincrónicas, use **IAsyncCollector<T>** como se muestra más adelante en esta sección).

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Mensajes en cola POCO [(objeto CRL estándar](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))
tipo de un mensaje de la cola que contiene un POCO en lugar de una cadena, pase Hola POCO toocreate como un toohello de parámetro de salida **cola** constructor de atributos.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

Hola SDK serializa automáticamente Hola objeto tooJSON. Siempre se crea un mensaje de cola, incluso si el objeto de hello es null.

### <a name="create-multiple-messages-or-in-async-functions"></a>Crear varios mensajes o en funciones asincrónicas
toocreate varios mensajes, asegúrese de tipo de parámetro de hello para la cola de salida de hello **ICollector<T>**  o **IAsyncCollector<T>**, tal y como se muestra en el siguiente ejemplo de Hola.

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Cada mensaje de la cola se crea inmediatamente cuando hello **agregar** se llama al método.

### <a name="types-that-hello-queue-attribute-works-with"></a>Tipos de ese atributo de la cola de hello funciona con
Puede usar hello **cola** atributo Hola siguientes tipos de parámetro:

* **cadena** (crea la cola de mensajes si el valor del parámetro es distinto de null cuando finaliza la función hello)
* **out byte** (funciona como **cadena**)
* **out CloudQueueMessage** (funciona como **cadena**)
* **out POCO** (un tipo serializable, crea un mensaje con un objeto null si el parámetro hello es nulo cuando finaliza la función hello)
* **ICollector**
* **IAsyncCollector**
* **CloudQueue** (para crear mensajes manualmente utilizando Hola API de almacenamiento de Azure directamente)

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a>Utilizar atributos de SDK de WebJobs en el cuerpo de Hola de una función
Si necesita toodo algunas funcionan en la función antes de usar como un atributo de SDK de WebJobs **cola**, **Blob**, o **tabla**, puede usar hello **IBinder** interfaz.

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

Hola **IBinder** interfaz también se puede usar con hello **tabla** y **Blob** atributos.

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a>¿Cómo tooread y escritura de blobs y tablas al procesar un mensaje de cola
Hola **Blob** y **tabla** atributos permiten tooread y escribir los blobs y tablas. ejemplos de Hello en esta sección aplican tooblobs. Para obtener ejemplos de código que muestran cómo tootrigger procesa cuando se crean o actualizan los blobs, vea [cómo toouse Azure blob storage con hello SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)y para obtener ejemplos de código que leen y escriben las tablas, vea [cómo toouse tabla de Azure almacenamiento con hello SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).

### <a name="string-queue-messages-triggering-blob-operations"></a>Mensajes en cola de cadena que desencadenan operaciones de blob
Para un mensaje de la cola que contiene una cadena, **queueTrigger** es un marcador de posición que se puede usar en hello **Blob** del atributo **blobPath** parámetro que contiene el contenido de Hola de mensaje de saludo.

Hello siguiente ejemplo se utiliza **flujo** objetos tooread y escritura de blobs. mensaje de bienvenida de cola es nombre Hola de un blob ubicado en hello textblobs contenedor. Una copia de blob de hello con "-nuevo" anexado toohello nombre se crea en Hola mismo contenedor.

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Hola **Blob** atributo constructor toma un **blobPath** parámetro que especifica el contenedor de Hola y el nombre de blob. Para obtener más información acerca de este marcador de posición, vea [cómo toouse Azure blob storage con hello SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).

Cuando el atributo de hello decora un **flujo** objeto, otro parámetro de constructor especifica hello **FileAccess** modo como lectura, escritura o lectura/escritura.

Hello ejemplo siguiente se usa un **CloudBlockBlob** toodelete un blob del objeto. mensaje de bienvenida de cola es nombre Hola de blob de Hola.

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Mensajes en cola POCO [(objeto CRL estándar](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))
Para un POCO almacenado como JSON en el mensaje de bienvenida de cola, puede utilizar marcadores de posición que nombres de las propiedades del objeto de Hola Hola **cola** del atributo **blobPath** parámetro. También puede utilizar nombres de propiedad de metadatos de cola como marcadores de posición. Consulte [Obtener metadatos de cola o de mensaje en cola](#get-queue-or-queue-message-metadata).

Hello en el ejemplo siguiente se copia un blob nuevo de blob tooa con una extensión diferente. mensaje de bienvenida de cola es un **BlobInformation** objeto que incluya **BlobName** y **BlobNameWithoutExtension** propiedades. nombres de propiedad de Hola se utilizan como marcadores de posición en la ruta de acceso de blob de Hola para hello **Blob** atributos.

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

Si necesita toodo algunas funcionan en la función antes de enlazar un objeto de tooan de blob, puede utilizar atributos de hello en el cuerpo de Hola de función de hello, tal y como se muestra en [atributos de usar el SDK de WebJobs en el cuerpo de Hola de una función](#use-webjobs-sdk-attributes-in-the-body-of-a-function).

### <a name="types-you-can-use-hello-blob-attribute-with"></a>Tipos que puede usar Hola Blob de atributo con
Hola **Blob** atributo se puede usar con hello siguientes tipos:

* **Secuencia** (lectura o escritura, especificado mediante el parámetro de constructor de hello FileAccess)
* **TextReader**
* **TextWriter**
* **string** (lectura)
* **cadena** (escribir; crea un blob solo si el parámetro de cadena de hello es distinto de null cuando la devolución de función hello)
* POCO (lectura)
* out POCO (escribir; siempre crea un blob, se crea como objeto null si POCO parámetro es null cuando la devolución de función hello)
* **CloudBlobStream** (escritura)
* **ICloudBlob** (lectura o escritura)
* **CloudBlockBlob** (lectura o escritura)
* **CloudPageBlob** (lectura o escritura)

## <a name="how-toohandle-poison-messages"></a>¿Cómo toohandle dudosos mensajes
Se denominan mensajes cuyo contenido hace que una función toofail *mensajes dudosos*. Cuando se produce un error en la función hello, mensaje de bienvenida de cola no se elimina y finalmente recoge nuevo, que producen Hola ciclo toobe repetido. Hola SDK automáticamente puede interrumpir el ciclo de hello después de un número limitado de iteraciones, o puede hacerlo manualmente.

### <a name="automatic-poison-message-handling"></a>Control automático de mensajes dudosos
Hola SDK llamará a una función de seguridad too5 veces tooprocess un mensaje de la cola. Si se produce un error en try quinto hello, mensaje de bienvenida es movida tooa cola de mensajes dudosos. Puede ver cómo tooconfigure Hola número máximo de reintentos en [cómo opciones de configuración de tooset](#how-to-set-configuration-options).

cola de mensajes dudosos Hola se denomina *{originalqueuename}*-dudoso. Puede escribir una función tooprocess mensajes desde la cola de mensajes dudosos Hola registrarlos o enviar una notificación que se necesita atención manual.

Después de hello de ejemplo de Hola **CopyBlob** function no funcionará correctamente cuando un mensaje de la cola contiene el nombre de Hola de un blob que no existe. Cuando esto ocurre, mensaje de saludo se mueve desde hello copyblobqueue toohello copyblobqueue dudosos cola. Hola **ProcessPoisonMessage** , a continuación, registros de Hola de mensajes dudosos.

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

![Salida de consola para el control de mensajes dudosos](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a>Control manual de mensajes dudosos
Puede obtener Hola número de veces que se ha detectado un mensaje para su procesamiento mediante la adición de un **int** parámetro denominado **dequeueCount** tooyour (función). También puede, a continuación, Hola de comprobación de recuento en el código de la función de eliminación de cola y realizar su propio control de mensajes dudosos al número de hello supera un umbral, como se muestra en el siguiente ejemplo de Hola.

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

## <a name="how-tooset-configuration-options"></a>¿Cómo tooset las opciones de configuración
Puede usar hello **JobHostConfiguration** Hola de tipo tooset opciones de configuración siguientes:

* Establecer las cadenas de conexión de SDK de hello en el código.
* Definir la configuración **QueueTrigger** como el número máximo de eliminaciones de la cola.
* Obtener nombres de cola a partir de la configuración.

### <a name="set-sdk-connection-strings-in-code"></a>Establecer cadenas de conexión de SDK en el código
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

### <a name="configure-queuetrigger--settings"></a>Configurar QueueTrigger
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

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a>Establecer valores para los parámetros del constructor del SDK de WebJobs en el código
A veces desea toospecify un nombre de cola, un nombre de blob o contenedor o una tabla asígnele el nombre en código, en lugar de codificar de forma rígida. Por ejemplo, puede querer toospecify nombre de cola de Hola para **QueueTrigger** en una variable de entorno o de archivo de configuración.

Puede hacerlo pasando un **NameResolver** objeto toohello **JobHostConfiguration** tipo. Incluir marcadores de posición especial entre signos de porcentaje (%) en los parámetros del constructor de atributo de SDK de WebJobs y su **NameResolver** código especifica Hola valores reales toobe usar en lugar de los marcadores de posición.

Por ejemplo, suponga que desea toouse una cola denominada logqueuetest en entorno de prueba de hello y una logqueueprod con nombre en producción. En lugar de un nombre de cola codificado de forma rígida, desea que el nombre de Hola de toospecify de una entrada en hello **appSettings** colección que tendría el nombre de la cola real de Hola. Si hello **appSettings** clave es logqueue, la función podría tener el aspecto como el siguiente ejemplo de Hola.

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

Su **NameResolver** clase, a continuación, pudo obtener el nombre de la cola de Hola de **appSettings** tal y como se muestra en el siguiente ejemplo de Hola:

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

Pasar hello **NameResolver** clase toohello **JobHost** objeto tal y como se muestra en el siguiente ejemplo de Hola.

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

**Nota:** nombres de blob, cola y tabla son de resolver cada vez que se invoque una función, pero se resuelven los nombres de contenedor de blob solamente cuando se inicia la aplicación hello. No se puede cambiar el nombre del contenedor de blob mientras se ejecuta el trabajo de Hola.

## <a name="how-tootrigger-a-function-manually"></a>¿Cómo tootrigger una función manualmente
una función de tootrigger manualmente, use hello **llamar a** o **CallAsync** método en hello **JobHost** hello y objeto **NoAutomaticTrigger** atributo en función de hello, como se muestra en el siguiente ejemplo de Hola.

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

## <a name="how-toowrite-logs"></a>Funcionamiento de los registros toowrite
Hola panel muestra los registros en dos lugares: Hola para hello trabajo Web y Hola página para una invocación de trabajo Web determinada.

![Registros en la página del trabajo web](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Registros en la página de invocación de la función](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

Salida de métodos de consola que se llama en una función o en hello **Main()** método aparece en la página de panel de Hola de hello trabajo Web, no en la página de Hola para una invocación de método determinado. Resultado del objeto de TextWriter Hola que obtendrá de un parámetro en la firma del método aparece en la página de panel de Hola de una invocación de método.

Salida de la consola no puede ser la invocación del método determinado tooa vinculado porque Hola consola tiene un único subproceso, mientras que muchas de las funciones de trabajo pueden estar ejecutando en hello mismo tiempo. Por eso Hola SDK proporciona cada invocación de función con su propio objeto de escritor de inicio de sesión únicos.

toowrite [registros de seguimiento de la aplicación](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (crea registros marcados como información) y **Console.Error** (crea registros marcados como ERROR). Una alternativa es toouse [seguimiento o TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), que proporciona Verbose, advertencia, y niveles de crítico en tooInfo de adición y Error. Registros de seguimiento de la aplicación aparecen en archivos de registro en la aplicación web de hello, tablas de Azure, o blobs de Azure según cómo configure la aplicación web de Azure. Como ocurre con todos los resultados de la consola, registros de aplicación 100 más recientes de hello también aparecen en la página de panel de Hola de hello trabajo Web, no la página de Hola de una invocación de función.

Salida de la consola aparece en hello panel únicamente si se ejecuta el programa de hello en un trabajo Web de Azure, no si programa Hola se ejecuta localmente o en algún otro entorno.

Puede deshabilitar el registro estableciendo toonull de cadena de conexión de hello panel. Para obtener más información, consulte [cómo tooset opciones de configuración](#how-to-set-configuration-options).

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

En el panel de SDK de WebJobs de hello, Hola salida de hello **TextWriter** se muestra cuando se desplace página toohello para un determinado invocación de función y seleccione objetos **alternar salida**:

![Vínculo de invocación](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Registros en la página de invocación de la función](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

En el panel de SDK de WebJobs de hello, líneas de hello 100 más reciente de la consola de salida mostrar una al ir a página toohello para hello trabajo Web (no de invocación de función hello) y seleccione **alternar salida**.

![Toggle Output](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

En un trabajo Web continuo, registros de aplicaciones se mostrarán en/datos/trabajos/continua/*{webjobname}*/job_log.txt en sistema de archivos de aplicación web de Hola.

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

En una aplicación Hola de blobs de Azure registros este aspecto: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write: Hola a todos!, 2014-09-26T21:01:13, Error, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.Error - Hola a todos!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out: Hola a todos!,

Y en un saludo de la tabla de Azure **Console.Out** y **Console.Error** registros tiene este aspecto:

![Registro de información en la tabla](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Registro de errores en la tabla](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a>Pasos siguientes
En este artículo ha proporcionado el código de ejemplos que muestran cómo toohandle escenarios comunes para trabajar con colas de Azure. Para obtener más información sobre cómo toouse WebJobs de Azure y Hola SDK de WebJobs, vea [recursos de documentación de WebJobs de Azure](http://go.microsoft.com/fwlink/?linkid=390226).

