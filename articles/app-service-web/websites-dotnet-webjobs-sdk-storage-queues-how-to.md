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
# <a name="how-toouse-azure-queue-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="3b0b4-104">¿Cómo toouse Azure cola de almacenamiento con hello SDK de WebJobs</span><span class="sxs-lookup"><span data-stu-id="3b0b4-104">How toouse Azure queue storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="3b0b4-105">Información general</span><span class="sxs-lookup"><span data-stu-id="3b0b4-105">Overview</span></span>
<span data-ttu-id="3b0b4-106">Esta guía proporcionan ejemplos de código de C# que muestran cómo toouse Hola versión del SDK de WebJobs de Azure 1.x con hello servicio de almacenamiento de cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-106">This guide provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure queue storage service.</span></span>

<span data-ttu-id="3b0b4-107">Guía de Hola se supone que sabe [cómo cadenas toocreate un proyecto WebJob en Visual Studio con una conexión de esa cuenta de almacenamiento de punto tooyour](websites-dotnet-webjobs-sdk-get-started.md) o demasiado[varias cuentas de almacenamiento](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="3b0b4-108">La mayoría de los fragmentos de código de hello mostrar sólo las funciones, no Hola código que crea hello `JobHost` objeto como en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3b0b4-108">Most of hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

<span data-ttu-id="3b0b4-109">Guía de Hello incluye Hola temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="3b0b4-109">hello guide includes hello following topics:</span></span>

* [<span data-ttu-id="3b0b4-110">¿Cómo tootrigger una función cuando se recibe un mensaje de la cola</span><span class="sxs-lookup"><span data-stu-id="3b0b4-110">How tootrigger a function when a queue message is received</span></span>](#trigger)
  * <span data-ttu-id="3b0b4-111">Mensajes en cola de cadena</span><span class="sxs-lookup"><span data-stu-id="3b0b4-111">String queue messages</span></span>
  * <span data-ttu-id="3b0b4-112">Mensaje en cola de POCO</span><span class="sxs-lookup"><span data-stu-id="3b0b4-112">POCO queue messages</span></span>
  * <span data-ttu-id="3b0b4-113">Funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="3b0b4-113">Async functions</span></span>
  * <span data-ttu-id="3b0b4-114">Atributo de tipos hello QueueTrigger funciona con</span><span class="sxs-lookup"><span data-stu-id="3b0b4-114">Types hello QueueTrigger attribute works with</span></span>
  * <span data-ttu-id="3b0b4-115">Algoritmo de sondeo</span><span class="sxs-lookup"><span data-stu-id="3b0b4-115">Polling algorithm</span></span>
  * <span data-ttu-id="3b0b4-116">Varias instancias</span><span class="sxs-lookup"><span data-stu-id="3b0b4-116">Multiple instances</span></span>
  * <span data-ttu-id="3b0b4-117">Ejecución en paralelo</span><span class="sxs-lookup"><span data-stu-id="3b0b4-117">Parallel execution</span></span>
  * <span data-ttu-id="3b0b4-118">Obtener metadatos de cola o de mensaje en cola</span><span class="sxs-lookup"><span data-stu-id="3b0b4-118">Get queue or queue message metadata</span></span>
  * <span data-ttu-id="3b0b4-119">Apagado correcto</span><span class="sxs-lookup"><span data-stu-id="3b0b4-119">Graceful shutdown</span></span>
* [<span data-ttu-id="3b0b4-120">¿Cómo toocreate una cola de mensajes al procesar un mensaje de cola</span><span class="sxs-lookup"><span data-stu-id="3b0b4-120">How toocreate a queue message while processing a queue message</span></span>](#createqueue)
  * <span data-ttu-id="3b0b4-121">Mensajes en cola de cadena</span><span class="sxs-lookup"><span data-stu-id="3b0b4-121">String queue messages</span></span>
  * <span data-ttu-id="3b0b4-122">Mensaje en cola de POCO</span><span class="sxs-lookup"><span data-stu-id="3b0b4-122">POCO queue messages</span></span>
  * <span data-ttu-id="3b0b4-123">Crear varios mensajes o en funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="3b0b4-123">Create multiple messages or in async functions</span></span>
  * <span data-ttu-id="3b0b4-124">Atributo de cola de tipos Hola funciona con</span><span class="sxs-lookup"><span data-stu-id="3b0b4-124">Types hello Queue attribute works with</span></span>
  * <span data-ttu-id="3b0b4-125">Utilizar atributos de SDK de WebJobs en el cuerpo de Hola de una función</span><span class="sxs-lookup"><span data-stu-id="3b0b4-125">Use WebJobs SDK attributes in hello body of a function</span></span>
* [<span data-ttu-id="3b0b4-126">Cómo tooread y escritura de blobs al procesar un mensaje de cola</span><span class="sxs-lookup"><span data-stu-id="3b0b4-126">How tooread and write blobs while processing a queue message</span></span>](#blobs)
  * <span data-ttu-id="3b0b4-127">Mensajes en cola de cadena</span><span class="sxs-lookup"><span data-stu-id="3b0b4-127">String queue messages</span></span>
  * <span data-ttu-id="3b0b4-128">Mensaje en cola de POCO</span><span class="sxs-lookup"><span data-stu-id="3b0b4-128">POCO queue messages</span></span>
  * <span data-ttu-id="3b0b4-129">Atributo de Blob de tipos Hola funciona con</span><span class="sxs-lookup"><span data-stu-id="3b0b4-129">Types hello Blob attribute works with</span></span>
* [<span data-ttu-id="3b0b4-130">¿Cómo toohandle dudosos mensajes</span><span class="sxs-lookup"><span data-stu-id="3b0b4-130">How toohandle poison messages</span></span>](#poison)
  * <span data-ttu-id="3b0b4-131">Control automático de mensajes dudosos</span><span class="sxs-lookup"><span data-stu-id="3b0b4-131">Automatic poison message handling</span></span>
  * <span data-ttu-id="3b0b4-132">Control manual de mensajes dudosos</span><span class="sxs-lookup"><span data-stu-id="3b0b4-132">Manual poison message handling</span></span>
* [<span data-ttu-id="3b0b4-133">¿Cómo tooset las opciones de configuración</span><span class="sxs-lookup"><span data-stu-id="3b0b4-133">How tooset configuration options</span></span>](#config)
  * <span data-ttu-id="3b0b4-134">Establecer cadenas de conexión de SDK en el código</span><span class="sxs-lookup"><span data-stu-id="3b0b4-134">Set SDK connection strings in code</span></span>
  * <span data-ttu-id="3b0b4-135">Configurar QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="3b0b4-135">Configure QueueTrigger settings</span></span>
  * <span data-ttu-id="3b0b4-136">Establecer valores para los parámetros del constructor del SDK de WebJobs en el código</span><span class="sxs-lookup"><span data-stu-id="3b0b4-136">Set values for WebJobs SDK constructor parameters in code</span></span>
* [<span data-ttu-id="3b0b4-137">¿Cómo tootrigger una función manualmente</span><span class="sxs-lookup"><span data-stu-id="3b0b4-137">How tootrigger a function manually</span></span>](#manual)
* [<span data-ttu-id="3b0b4-138">Funcionamiento de los registros toowrite</span><span class="sxs-lookup"><span data-stu-id="3b0b4-138">How toowrite logs</span></span>](#logs)
* [<span data-ttu-id="3b0b4-139">¿Cómo toohandle errores y configurar tiempos de espera</span><span class="sxs-lookup"><span data-stu-id="3b0b4-139">How toohandle errors and configure timeouts</span></span>](#errors)
* [<span data-ttu-id="3b0b4-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3b0b4-140">Next steps</span></span>](#nextsteps)

## <span data-ttu-id="3b0b4-141"><a id="trigger"></a>¿Cómo tootrigger una función cuando se recibe un mensaje de la cola</span><span class="sxs-lookup"><span data-stu-id="3b0b4-141"><a id="trigger"></a> How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="3b0b4-142">llama a una función que Hola SDK de WebJobs toowrite cuando se recibe un mensaje de la cola, utilice hello `QueueTrigger` atributo.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-142">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `QueueTrigger` attribute.</span></span> <span data-ttu-id="3b0b4-143">constructor de atributo de Hello toma un parámetro de cadena que especifica el nombre hello de hello cola toopoll.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-143">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="3b0b4-144">También puede [establecer nombre de la cola de hello dinámicamente](#config).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-144">You can also [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="3b0b4-145">Mensajes en cola de cadena</span><span class="sxs-lookup"><span data-stu-id="3b0b4-145">String queue messages</span></span>
<span data-ttu-id="3b0b4-146">En el siguiente ejemplo de Hola, cola de hello contiene un mensaje de cadena, por lo que `QueueTrigger` es tooa aplicado parámetro de cadena denominado `logMessage` que incluye contenido de hello del mensaje de bienvenida de cola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-146">In hello following example, hello queue contains a string message, so `QueueTrigger` is applied tooa string parameter named `logMessage` which contains hello content of hello queue message.</span></span> <span data-ttu-id="3b0b4-147">Hola función [escribe un toohello de mensaje de registro panel](#logs).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-147">hello function [writes a log message toohello Dashboard](#logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="3b0b4-148">Además `string`, parámetro hello puede ser una matriz de bytes, un `CloudQueueMessage` objeto o un POCO que defina.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-148">Besides `string`, hello parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="3b0b4-149">Mensajes en cola POCO [(objeto CRL estándar](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="3b0b4-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="3b0b4-150">En el siguiente ejemplo de Hola, mensaje de bienvenida de cola contiene un valor JSON para un `BlobInformation` objeto que incluye un `BlobName` propiedad.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-150">In hello following example, hello queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span></span> <span data-ttu-id="3b0b4-151">Hola SDK automáticamente deserializa el objeto de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-151">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="3b0b4-152">Hola SDK utiliza hello [paquete NuGet de Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize y deserializar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-152">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="3b0b4-153">Si crea mensajes en cola en un programa que no utilice Hola SDK de WebJobs, puede escribir código como sigue toocreate un POCO de la cola de mensajes de ejemplo de Hola ese Hola que SDK puede analizar.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-153">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="3b0b4-154">Funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="3b0b4-154">Async functions</span></span>
<span data-ttu-id="3b0b4-155">Hola después de la función asincrónica [escribe un panel de registro toohello](#logs).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-155">hello following async function [writes a log toohello Dashboard](#logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="3b0b4-156">Funciones asincrónicas pueden tardar un [token de cancelación](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), tal y como se muestra en el siguiente ejemplo que copia un blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="3b0b4-157">(Para obtener una explicación de hello `queueTrigger` marcador de posición, vea hello [Blobs](#blobs) sección.)</span><span class="sxs-lookup"><span data-stu-id="3b0b4-157">(For an explanation of hello `queueTrigger` placeholder, see hello [Blobs](#blobs) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <span data-ttu-id="3b0b4-158"><a id="qtattributetypes"></a>Atributo de tipos hello QueueTrigger funciona con</span><span class="sxs-lookup"><span data-stu-id="3b0b4-158"><a id="qtattributetypes"></a> Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="3b0b4-159">Puede usar `QueueTrigger` con hello siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="3b0b4-159">You can use `QueueTrigger` with hello following types:</span></span>

* `string`
* <span data-ttu-id="3b0b4-160">Un tipo de POCO serializado como JSON</span><span class="sxs-lookup"><span data-stu-id="3b0b4-160">A POCO type serialized as JSON</span></span>
* `byte[]`
* `CloudQueueMessage`

### <span data-ttu-id="3b0b4-161"><a id="polling"></a> Algoritmo de sondeo</span><span class="sxs-lookup"><span data-stu-id="3b0b4-161"><a id="polling"></a> Polling algorithm</span></span>
<span data-ttu-id="3b0b4-162">Hola SDK implementa un efecto de hello tooreduce aleatorio algoritmo de retroceso exponencial de sondeo en los costos de transacciones de almacenamiento de cola inactiva.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-162">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="3b0b4-163">Cuando se encuentra un mensaje, Hola SDK espera dos segundos y, a continuación, comprueba si otro mensaje; Cuando se encuentra ningún mensaje espera unos cuatro segundos antes de volver a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-163">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="3b0b4-164">Después de los intentos subsiguientes tooget un mensaje de la cola, tiempo de espera de hello continúa tooincrease hasta que alcanza el tiempo de espera máximo de hello, qué minuto de tooone los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-164">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="3b0b4-165">[Hello tiempo de espera máximo es configurable](#config).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-165">[hello maximum wait time is configurable](#config).</span></span>

### <span data-ttu-id="3b0b4-166"><a id="instances"></a> Varias instancias</span><span class="sxs-lookup"><span data-stu-id="3b0b4-166"><a id="instances"></a> Multiple instances</span></span>
<span data-ttu-id="3b0b4-167">Si la aplicación web se ejecuta en varias instancias, se ejecuta un trabajo Web continuo en cada máquina e intentará toorun funciones y espere a que los desencadenadores cada máquina.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="3b0b4-168">Hola desencadenador de cola de SDK de WebJobs automáticamente impide que una función de procesamiento de un mensaje de cola varias veces; funciones no tienen toobe escrito toobe idempotente.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-168">hello WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have toobe written toobe idempotent.</span></span> <span data-ttu-id="3b0b4-169">Sin embargo, si desea que tooensure que solo una instancia de una función se ejecuta incluso si existen varias instancias de aplicación web de hello host, puede usar hello `Singleton` atributo.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-169">However, if you want tooensure that only one instance of a function runs even when there are multiple instances of hello host web app, you can use hello `Singleton` attribute.</span></span>

### <span data-ttu-id="3b0b4-170"><a id="parallel"></a> Ejecución en paralelo</span><span class="sxs-lookup"><span data-stu-id="3b0b4-170"><a id="parallel"></a> Parallel execution</span></span>
<span data-ttu-id="3b0b4-171">Si tiene varias funciones que escuchan en diferentes colas, Hola SDK llamará a ellos en paralelo cuando se reciben los mensajes al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-171">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="3b0b4-172">Hello mismo puede decirse cuando se reciben varios mensajes de una sola cola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-172">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="3b0b4-173">De forma predeterminada, Hola SDK Obtiene un lote de 16 mensajes en cola a la vez y ejecuta la función hello que los procesa en paralelo.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-173">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="3b0b4-174">[tamaño de lote de Hello es configurable](#config).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-174">[hello batch size is configurable](#config).</span></span> <span data-ttu-id="3b0b4-175">Cuando se obtiene el número Hola procesando hacia abajo toohalf del tamaño de lote de hello, Hola SDK obtiene otro lote y empieza a procesar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-175">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="3b0b4-176">Por lo tanto, número máximo de Hola de mensajes simultáneos que se procesan por función es el tamaño del lote de una vez y Media Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-176">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="3b0b4-177">Este límite aplica por separado tooeach función que tiene un `QueueTrigger` atributo.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-177">This limit applies separately tooeach function that has a `QueueTrigger` attribute.</span></span>

<span data-ttu-id="3b0b4-178">Si no desea que la ejecución en paralelo para los mensajes recibidos en una cola, puede establecer too1 de tamaño de lote de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-178">If you don't want parallel execution for messages received on one queue, you can set hello batch size too1.</span></span> <span data-ttu-id="3b0b4-179">Consulte también **más control sobre el procesamiento de colas** en [RTM de SDK de WebJobs de Azure 1.1.0](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span></span>

### <span data-ttu-id="3b0b4-180"><a id="queuemetadata"></a>Obtener metadatos de cola o de mensaje en cola</span><span class="sxs-lookup"><span data-stu-id="3b0b4-180"><a id="queuemetadata"></a>Get queue or queue message metadata</span></span>
<span data-ttu-id="3b0b4-181">Puede obtener Hola siguientes propiedades del mensaje mediante la adición de la firma del método toohello parámetros:</span><span class="sxs-lookup"><span data-stu-id="3b0b4-181">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="3b0b4-182">`DateTimeOffset` expirationTime</span><span class="sxs-lookup"><span data-stu-id="3b0b4-182">`DateTimeOffset` expirationTime</span></span>
* <span data-ttu-id="3b0b4-183">`DateTimeOffset` insertionTime</span><span class="sxs-lookup"><span data-stu-id="3b0b4-183">`DateTimeOffset` insertionTime</span></span>
* <span data-ttu-id="3b0b4-184">`DateTimeOffset` nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="3b0b4-184">`DateTimeOffset` nextVisibleTime</span></span>
* <span data-ttu-id="3b0b4-185">`string` queueTrigger (contiene el texto del mensaje)</span><span class="sxs-lookup"><span data-stu-id="3b0b4-185">`string` queueTrigger (contains message text)</span></span>
* <span data-ttu-id="3b0b4-186">`string` id</span><span class="sxs-lookup"><span data-stu-id="3b0b4-186">`string` id</span></span>
* <span data-ttu-id="3b0b4-187">`string` popReceipt</span><span class="sxs-lookup"><span data-stu-id="3b0b4-187">`string` popReceipt</span></span>
* <span data-ttu-id="3b0b4-188">`int` dequeueCount</span><span class="sxs-lookup"><span data-stu-id="3b0b4-188">`int` dequeueCount</span></span>

<span data-ttu-id="3b0b4-189">Si desea que toowork directamente con hello API de almacenamiento de Azure, también puede agregar un `CloudStorageAccount` parámetro.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-189">If you want toowork directly with hello Azure storage API, you can also add a `CloudStorageAccount` parameter.</span></span>

<span data-ttu-id="3b0b4-190">Hello en el ejemplo siguiente se escribe todos este metadatos tooan información registro de aplicación.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-190">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="3b0b4-191">En el ejemplo de Hola, logMessage y queueTrigger contengan Hola Hola del mensaje de cola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-191">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

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

<span data-ttu-id="3b0b4-192">Este es un registro de ejemplo escrito código de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="3b0b4-192">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <span data-ttu-id="3b0b4-193"><a id="graceful"></a>Cierre estable</span><span class="sxs-lookup"><span data-stu-id="3b0b4-193"><a id="graceful"></a>Graceful shutdown</span></span>
<span data-ttu-id="3b0b4-194">Una función que se ejecuta en un trabajo Web continuo puede aceptar un `CancellationToken` parámetro que permite Hola sistema operativo toonotify Hola función cuando hello trabajo Web es sobre toobe terminada.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="3b0b4-195">Puede usar este toomake notificación seguro función hello no finalizar inesperadamente de forma que deja los datos en un estado incoherente.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-195">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="3b0b4-196">Hola siguiente ejemplo se muestra cómo toocheck de inminente finalización del trabajo Web en una función.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-196">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="3b0b4-197">**Nota:** Hola panel no podría mostrar correctamente el estado de Hola y salida de funciones que se haya cerrado.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-197">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="3b0b4-198">Para obtener más información, consulte [Cierre estable de WebJobs](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <span data-ttu-id="3b0b4-199"><a id="createqueue"></a>¿Cómo toocreate una cola de mensajes al procesar un mensaje de cola</span><span class="sxs-lookup"><span data-stu-id="3b0b4-199"><a id="createqueue"></a> How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="3b0b4-200">una función que crea un nuevo mensaje de cola, use hello toowrite `Queue` atributo.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-200">toowrite a function that creates a new queue message, use hello `Queue` attribute.</span></span> <span data-ttu-id="3b0b4-201">Al igual que `QueueTrigger`, se pasa el nombre de la cola de hello como una cadena o bien puede [establecer nombre de la cola de hello dinámicamente](#config).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-201">Like `QueueTrigger`, you pass in hello queue name as a string or you can [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="3b0b4-202">Mensajes en cola de cadena</span><span class="sxs-lookup"><span data-stu-id="3b0b4-202">String queue messages</span></span>
<span data-ttu-id="3b0b4-203">Hola siguiendo el ejemplo de código asincrónico no crea un nuevo mensaje de cola en la cola de hello denominado "outputqueue" con hello igual contenido como mensaje de bienvenida de cola se recibió en cola Hola denominado "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="3b0b4-203">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="3b0b4-204">(En el caso de las funciones asincrónicas, use `IAsyncCollector<T>` como se muestra más adelante en esta sección).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="3b0b4-205">Mensajes en cola POCO [(objeto CRL estándar](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="3b0b4-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="3b0b4-206">tipo de un mensaje de la cola que contiene un POCO en lugar de una cadena, pase Hola POCO toocreate como un toohello de parámetro de salida `Queue` constructor de atributos.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-206">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello `Queue` attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="3b0b4-207">Hola SDK serializa automáticamente Hola objeto tooJSON.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-207">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="3b0b4-208">Siempre se crea un mensaje de cola, incluso si el objeto de hello es null.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-208">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="3b0b4-209">Crear varios mensajes o en funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="3b0b4-209">Create multiple messages or in async functions</span></span>
<span data-ttu-id="3b0b4-210">toocreate varios mensajes, asegúrese de tipo de parámetro de hello para la cola de salida de hello `ICollector<T>` o `IAsyncCollector<T>`, tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-210">toocreate multiple messages, make hello parameter type for hello output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="3b0b4-211">Cada mensaje de la cola se crea inmediatamente cuando hello `Add` se llama al método.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-211">Each queue message is created immediately when hello `Add` method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="3b0b4-212">Tipos de ese atributo de la cola de hello funciona con</span><span class="sxs-lookup"><span data-stu-id="3b0b4-212">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="3b0b4-213">Puede usar hello `Queue` atributo Hola siguientes tipos de parámetro:</span><span class="sxs-lookup"><span data-stu-id="3b0b4-213">You can use hello `Queue` attribute on hello following parameter types:</span></span>

* <span data-ttu-id="3b0b4-214">`out string`(se crea la cola de mensajes si el valor del parámetro es distinto de null cuando finaliza la función hello)</span><span class="sxs-lookup"><span data-stu-id="3b0b4-214">`out string` (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="3b0b4-215">`out byte[]` (funciona como `string`)</span><span class="sxs-lookup"><span data-stu-id="3b0b4-215">`out byte[]` (works like `string`)</span></span>
* <span data-ttu-id="3b0b4-216">`out CloudQueueMessage` (funciona como `string`)</span><span class="sxs-lookup"><span data-stu-id="3b0b4-216">`out CloudQueueMessage` (works like `string`)</span></span>
* <span data-ttu-id="3b0b4-217">`out POCO`(un tipo serializable, crea un mensaje con un objeto null si el parámetro hello es nulo cuando finaliza la función hello)</span><span class="sxs-lookup"><span data-stu-id="3b0b4-217">`out POCO` (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* `ICollector`
* `IAsyncCollector`
* <span data-ttu-id="3b0b4-218">`CloudQueue`(para crear mensajes de forma manual mediante Hola API de almacenamiento de Azure directamente)</span><span class="sxs-lookup"><span data-stu-id="3b0b4-218">`CloudQueue` (for creating messages manually using hello Azure Storage API directly)</span></span>

### <span data-ttu-id="3b0b4-219"><a id="ibinder"></a>Utilizar atributos de SDK de WebJobs en el cuerpo de Hola de una función</span><span class="sxs-lookup"><span data-stu-id="3b0b4-219"><a id="ibinder"></a>Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="3b0b4-220">Si necesita toodo algunas funcionan en la función antes de usar como un atributo de SDK de WebJobs `Queue`, `Blob`, o `Table`, puede usar hello `IBinder` interfaz.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-220">If you need toodo some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use hello `IBinder` interface.</span></span>

<span data-ttu-id="3b0b4-221">Hola siguiente ejemplo toma un mensaje de la cola de entrada y crea un nuevo mensaje con hello mismo contenido en una cola de salida.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-221">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="3b0b4-222">nombre de cola de salida de Hello se establece por código Hola cuerpo de función hello.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-222">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="3b0b4-223">Hola `IBinder` interfaz también se puede usar con hello `Table` y `Blob` atributos.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-223">hello `IBinder` interface can also be used with hello `Table` and `Blob` attributes.</span></span>

## <span data-ttu-id="3b0b4-224"><a id="blobs"></a>¿Cómo tooread y escritura de blobs y tablas al procesar un mensaje de cola</span><span class="sxs-lookup"><span data-stu-id="3b0b4-224"><a id="blobs"></a> How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="3b0b4-225">Hola `Blob` y `Table` atributos permiten tooread y escribir los blobs y tablas.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-225">hello `Blob` and `Table` attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="3b0b4-226">ejemplos de Hello en esta sección aplican tooblobs.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-226">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="3b0b4-227">Para obtener ejemplos de código que muestran cómo tootrigger procesa cuando se crean o actualizan los blobs, vea [cómo toouse Azure blob storage con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)y para obtener ejemplos de código que leen y escriben las tablas, vea [cómo toouse tabla de Azure almacenamiento con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-227">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="3b0b4-228">Mensajes en cola de cadena que desencadenan operaciones de blob</span><span class="sxs-lookup"><span data-stu-id="3b0b4-228">String queue messages triggering blob operations</span></span>
<span data-ttu-id="3b0b4-229">Para un mensaje de la cola que contiene una cadena, `queueTrigger` es un marcador de posición que se puede usar en hello `Blob` del atributo `blobPath` parámetro que contiene el contenido de Hola de mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in hello `Blob` attribute's `blobPath` parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="3b0b4-230">Hello siguiente ejemplo se utiliza `Stream` objetos tooread y escritura de blobs.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-230">hello following example uses `Stream` objects tooread and write blobs.</span></span> <span data-ttu-id="3b0b4-231">mensaje de bienvenida de cola es nombre Hola de un blob ubicado en hello textblobs contenedor.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-231">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="3b0b4-232">Una copia de blob de hello con "-nuevo" anexado toohello nombre se crea en Hola mismo contenedor.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-232">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="3b0b4-233">Hola `Blob` atributo constructor toma un `blobPath` parámetro que especifica el contenedor de Hola y el nombre de blob.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-233">hello `Blob` attribute constructor takes a `blobPath` parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="3b0b4-234">Para obtener más información acerca de este marcador de posición, vea [cómo toouse Azure blob storage con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span><span class="sxs-lookup"><span data-stu-id="3b0b4-234">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span></span>

<span data-ttu-id="3b0b4-235">Cuando el atributo de hello decora un `Stream` objeto, otro parámetro de constructor especifica hello `FileAccess` modo como lectura, escritura o lectura/escritura.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-235">When hello attribute decorates a `Stream` object, another constructor parameter specifies hello `FileAccess` mode as read, write, or read/write.</span></span>

<span data-ttu-id="3b0b4-236">Hello ejemplo siguiente se usa un `CloudBlockBlob` objeto toodelete un blob.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-236">hello following example uses a `CloudBlockBlob` object toodelete a blob.</span></span> <span data-ttu-id="3b0b4-237">mensaje de bienvenida de cola es nombre Hola de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-237">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <span data-ttu-id="3b0b4-238"><a id="pocoblobs"></a> Mensajes en cola POCO [(objeto CRL estándar](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="3b0b4-238"><a id="pocoblobs"></a> POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="3b0b4-239">Para un POCO almacenado como JSON en el mensaje de bienvenida de cola, puede utilizar marcadores de posición que nombres de las propiedades del objeto de Hola Hola `Queue` del atributo `blobPath` parámetro.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-239">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello `Queue` attribute's `blobPath` parameter.</span></span> <span data-ttu-id="3b0b4-240">También puede utilizar [nombres de propiedad de metadatos de cola](#queuemetadata) como marcadores de posición.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span></span>

<span data-ttu-id="3b0b4-241">Hello en el ejemplo siguiente se copia un blob nuevo de blob tooa con una extensión diferente.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-241">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="3b0b4-242">mensaje de bienvenida de cola es un `BlobInformation` objeto que incluya `BlobName` y `BlobNameWithoutExtension` propiedades.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-242">hello queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span></span> <span data-ttu-id="3b0b4-243">nombres de propiedad de Hola se utilizan como marcadores de posición en la ruta de acceso de blob de Hola para hello `Blob` atributos.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-243">hello property names are used as placeholders in hello blob path for hello `Blob` attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="3b0b4-244">Hola SDK utiliza hello [paquete NuGet de Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize y deserializar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-244">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="3b0b4-245">Si crea mensajes en cola en un programa que no utilice Hola SDK de WebJobs, puede escribir código como sigue toocreate un POCO de la cola de mensajes de ejemplo de Hola ese Hola que SDK puede analizar.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-245">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="3b0b4-246">Si necesita toodo algunas funcionan en la función antes de enlazar un objeto de tooan de blob, puede usar el atributo hello en el cuerpo de Hola de función de hello, [tal como se muestra anteriormente para el atributo de la cola de hello](#ibinder).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-246">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, [as shown earlier for hello Queue attribute](#ibinder).</span></span>

### <span data-ttu-id="3b0b4-247"><a id="blobattributetypes"></a>Tipos que puede usar Hola Blob de atributo con</span><span class="sxs-lookup"><span data-stu-id="3b0b4-247"><a id="blobattributetypes"></a> Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="3b0b4-248">Hola `Blob` atributo se puede usar con hello siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="3b0b4-248">hello `Blob` attribute can be used with hello following types:</span></span>

* <span data-ttu-id="3b0b4-249">`Stream`(lectura o escritura, especificado mediante el parámetro de constructor de hello FileAccess)</span><span class="sxs-lookup"><span data-stu-id="3b0b4-249">`Stream` (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* `TextReader`
* `TextWriter`
* <span data-ttu-id="3b0b4-250">`string` (lectura)</span><span class="sxs-lookup"><span data-stu-id="3b0b4-250">`string` (read)</span></span>
* <span data-ttu-id="3b0b4-251">`out string`(escribir; crea un blob solo si el parámetro de cadena de hello es distinto de null cuando la devolución de función hello)</span><span class="sxs-lookup"><span data-stu-id="3b0b4-251">`out string` (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="3b0b4-252">POCO (lectura)</span><span class="sxs-lookup"><span data-stu-id="3b0b4-252">POCO (read)</span></span>
* <span data-ttu-id="3b0b4-253">out POCO (escribir; siempre crea un blob, se crea como objeto null si POCO parámetro es null cuando la devolución de función hello)</span><span class="sxs-lookup"><span data-stu-id="3b0b4-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="3b0b4-254">`CloudBlobStream` (escritura)</span><span class="sxs-lookup"><span data-stu-id="3b0b4-254">`CloudBlobStream` (write)</span></span>
* <span data-ttu-id="3b0b4-255">`ICloudBlob` (lectura o escritura)</span><span class="sxs-lookup"><span data-stu-id="3b0b4-255">`ICloudBlob` (read or write)</span></span>
* <span data-ttu-id="3b0b4-256">`CloudBlockBlob` (lectura o escritura)</span><span class="sxs-lookup"><span data-stu-id="3b0b4-256">`CloudBlockBlob` (read or write)</span></span>
* <span data-ttu-id="3b0b4-257">`CloudPageBlob` (lectura o escritura)</span><span class="sxs-lookup"><span data-stu-id="3b0b4-257">`CloudPageBlob` (read or write)</span></span>

## <span data-ttu-id="3b0b4-258"><a id="poison"></a>¿Cómo toohandle dudosos mensajes</span><span class="sxs-lookup"><span data-stu-id="3b0b4-258"><a id="poison"></a> How toohandle poison messages</span></span>
<span data-ttu-id="3b0b4-259">Se denominan mensajes cuyo contenido hace que una función toofail *mensajes dudosos*.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-259">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="3b0b4-260">Cuando se produce un error en la función hello, mensaje de bienvenida de cola no se elimina y finalmente recoge nuevo, que producen Hola ciclo toobe repetido.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-260">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="3b0b4-261">Hola SDK automáticamente puede interrumpir el ciclo de hello después de un número limitado de iteraciones, o puede hacerlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-261">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="3b0b4-262">Control automático de mensajes dudosos</span><span class="sxs-lookup"><span data-stu-id="3b0b4-262">Automatic poison message handling</span></span>
<span data-ttu-id="3b0b4-263">Hola SDK llamará a una función de seguridad too5 veces tooprocess un mensaje de la cola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-263">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="3b0b4-264">Si se produce un error en try quinto hello, mensaje de bienvenida es movida tooa cola de mensajes dudosos.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-264">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="3b0b4-265">[Hola número máximo de reintentos es configurable](#config).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-265">[hello maximum number of retries is configurable](#config).</span></span>

<span data-ttu-id="3b0b4-266">cola de mensajes dudosos Hola se denomina *{originalqueuename}*-dudoso.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-266">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="3b0b4-267">Puede escribir una función tooprocess mensajes desde la cola de mensajes dudosos Hola registrarlos o enviar una notificación que se necesita atención manual.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-267">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="3b0b4-268">Después de hello de ejemplo de Hola `CopyBlob` function no funcionará correctamente cuando un mensaje de la cola contiene el nombre de Hola de un blob que no existe.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-268">In hello following example hello `CopyBlob` function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="3b0b4-269">Cuando esto ocurre, mensaje de saludo se mueve desde hello copyblobqueue toohello copyblobqueue dudosos cola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-269">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="3b0b4-270">Hola `ProcessPoisonMessage` , a continuación, registros de Hola de mensajes dudosos.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-270">hello `ProcessPoisonMessage` then logs hello poison message.</span></span>

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

<span data-ttu-id="3b0b4-271">Hello en la ilustración siguiente se muestra la salida de consola de estas funciones cuando se procesa un mensaje dudoso.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-271">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![Salida de consola para el control de mensajes dudosos](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="3b0b4-273">Control manual de mensajes dudosos</span><span class="sxs-lookup"><span data-stu-id="3b0b4-273">Manual poison message handling</span></span>
<span data-ttu-id="3b0b4-274">Puede obtener Hola número de veces que se ha detectado un mensaje para su procesamiento mediante la adición de un `int` parámetro denominado `dequeueCount` tooyour función.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-274">You can get hello number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` tooyour function.</span></span> <span data-ttu-id="3b0b4-275">También puede, a continuación, Hola de comprobación de recuento en el código de la función de eliminación de cola y realizar su propio control de mensajes dudosos al número de hello supera un umbral, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-275">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

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

## <span data-ttu-id="3b0b4-276"><a id="config"></a>¿Cómo tooset las opciones de configuración</span><span class="sxs-lookup"><span data-stu-id="3b0b4-276"><a id="config"></a> How tooset configuration options</span></span>
<span data-ttu-id="3b0b4-277">Puede usar hello `JobHostConfiguration` Hola de tipo tooset opciones de configuración siguientes:</span><span class="sxs-lookup"><span data-stu-id="3b0b4-277">You can use hello `JobHostConfiguration` type tooset hello following configuration options:</span></span>

* <span data-ttu-id="3b0b4-278">Establecer las cadenas de conexión de SDK de hello en el código.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-278">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="3b0b4-279">Configurar `QueueTrigger` como el recuento de eliminación de cola máximo.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="3b0b4-280">Obtener nombres de cola a partir de la configuración.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-280">Get queue names from configuration.</span></span>

### <span data-ttu-id="3b0b4-281"><a id="setconnstr"></a>Establecer cadenas de conexión de SDK en el código</span><span class="sxs-lookup"><span data-stu-id="3b0b4-281"><a id="setconnstr"></a>Set SDK connection strings in code</span></span>
<span data-ttu-id="3b0b4-282">Establecer las cadenas de conexión de SDK de hello en el código permite toouse sus propios nombres de cadena de conexión en archivos de configuración o las variables de entorno, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-282">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

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

### <span data-ttu-id="3b0b4-283"><a id="configqueue"></a>Configurar QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="3b0b4-283"><a id="configqueue"></a>Configure QueueTrigger  settings</span></span>
<span data-ttu-id="3b0b4-284">Puede configurar Hola después de la configuración que se aplica el procesamiento de mensajes de cola de toohello:</span><span class="sxs-lookup"><span data-stu-id="3b0b4-284">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="3b0b4-285">número máximo de mensajes en cola que se recogen simultáneamente toobe ejecutada en paralelo de Hola (el valor predeterminado es 16).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-285">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="3b0b4-286">Hola número máximo de reintentos antes de enviar un mensaje de cola de cola de mensajes dudosos tooa (el valor predeterminado es 5).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-286">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="3b0b4-287">tiempo de espera máximo de Hello antes de volver a sondear cuando una cola está vacía (el valor predeterminado es 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-287">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="3b0b4-288">Hola siguiente ejemplo se muestra cómo tooconfigure esta configuración:</span><span class="sxs-lookup"><span data-stu-id="3b0b4-288">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="3b0b4-289"><a id="setnamesincode"></a>Establecer valores para los parámetros del constructor del SDK de WebJobs en el código</span><span class="sxs-lookup"><span data-stu-id="3b0b4-289"><a id="setnamesincode"></a>Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="3b0b4-290">A veces desea toospecify un nombre de cola, un nombre de blob o contenedor o una tabla asígnele el nombre en código, en lugar de codificar de forma rígida.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-290">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="3b0b4-291">Por ejemplo, puede querer toospecify nombre de cola de Hola para `QueueTrigger` en una variable de entorno o de archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-291">For example, you might want toospecify hello queue name for `QueueTrigger` in a configuration file or environment variable.</span></span>

<span data-ttu-id="3b0b4-292">Puede hacerlo pasando un `NameResolver` objeto toohello `JobHostConfiguration` tipo.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-292">You can do that by passing in a `NameResolver` object toohello `JobHostConfiguration` type.</span></span> <span data-ttu-id="3b0b4-293">Incluir marcadores de posición especial entre signos de porcentaje (%) en los parámetros del constructor de atributo de SDK de WebJobs y su `NameResolver` código especifica Hola valores reales toobe usar en lugar de los marcadores de posición.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="3b0b4-294">Por ejemplo, suponga que desea toouse una cola denominada logqueuetest en entorno de prueba de hello y una logqueueprod con nombre en producción.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-294">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="3b0b4-295">En lugar de un nombre de cola codificado de forma rígida, desea que el nombre de Hola de toospecify de una entrada en hello `appSettings` colección que tendría el nombre de la cola real de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-295">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello `appSettings` collection that would have hello actual queue name.</span></span> <span data-ttu-id="3b0b4-296">Si hello `appSettings` clave es logqueue, la función podría tener el aspecto como el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-296">If hello `appSettings` key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="3b0b4-297">Su `NameResolver` clase, a continuación, pudo obtener el nombre de la cola de Hola de `appSettings` tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="3b0b4-297">Your `NameResolver` class could then get hello queue name from `appSettings` as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="3b0b4-298">Pasar hello `NameResolver` clase toohello `JobHost` objeto tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-298">You pass hello `NameResolver` class in toohello `JobHost` object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="3b0b4-299">**Nota:** nombres de blob, cola y tabla son de resolver cada vez que se invoque una función, pero se resuelven los nombres de contenedor de blob solamente cuando se inicia la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="3b0b4-300">No se puede cambiar el nombre del contenedor de blob mientras se ejecuta el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-300">You can't change blob container name while hello job is running.</span></span>

## <span data-ttu-id="3b0b4-301"><a id="manual"></a>¿Cómo tootrigger una función manualmente</span><span class="sxs-lookup"><span data-stu-id="3b0b4-301"><a id="manual"></a>How tootrigger a function manually</span></span>
<span data-ttu-id="3b0b4-302">una función de tootrigger manualmente, use hello `Call` o `CallAsync` método en hello `JobHost` hello y objeto `NoAutomaticTrigger` del atributo en función de hello, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-302">tootrigger a function manually, use hello `Call` or `CallAsync` method on hello `JobHost` object and hello `NoAutomaticTrigger` attribute on hello function, as shown in hello following example.</span></span>

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

## <span data-ttu-id="3b0b4-303"><a id="logs"></a>Funcionamiento de los registros toowrite</span><span class="sxs-lookup"><span data-stu-id="3b0b4-303"><a id="logs"></a>How toowrite logs</span></span>
<span data-ttu-id="3b0b4-304">Hola panel muestra los registros en dos lugares: Hola para hello trabajo Web y Hola página para una invocación de trabajo Web determinada.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-304">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![Registros en la página del trabajo web](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Registros en la página de invocación de la función](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="3b0b4-307">Salida de métodos de consola que se llama en una función o en hello `Main()` método aparece en la página de panel de Hola de hello trabajo Web, no en la página de Hola para una invocación de método determinado.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-307">Output from Console methods that you call in a function or in hello `Main()` method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="3b0b4-308">Resultado del objeto de TextWriter Hola que obtendrá de un parámetro en la firma del método aparece en la página de panel de Hola de una invocación de método.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-308">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="3b0b4-309">Salida de la consola no puede ser la invocación del método determinado tooa vinculado porque Hola consola tiene un único subproceso, mientras que muchas de las funciones de trabajo pueden estar ejecutando en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-309">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="3b0b4-310">Por eso Hola SDK proporciona cada invocación de función con su propio objeto de escritor de inicio de sesión únicos.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-310">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="3b0b4-311">toowrite [registros de seguimiento de la aplicación](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (crea registros marcados como información) y `Console.Error` (crea registros marcados como ERROR).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-311">toowrite [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span></span> <span data-ttu-id="3b0b4-312">Una alternativa es toouse [seguimiento o TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), que proporciona Verbose, advertencia, y niveles de crítico en tooInfo de adición y Error.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-312">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="3b0b4-313">Registros de seguimiento de la aplicación aparecen en archivos de registro en la aplicación web de hello, tablas de Azure, o blobs de Azure según cómo configure la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-313">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="3b0b4-314">Como ocurre con todos los resultados de la consola, registros de aplicación 100 más recientes de hello también aparecen en la página de panel de Hola de hello trabajo Web, no la página de Hola de una invocación de función.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-314">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="3b0b4-315">Salida de la consola aparece en hello panel únicamente si se ejecuta el programa de hello en un trabajo Web de Azure, no si programa Hola se ejecuta localmente o en algún otro entorno.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-315">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="3b0b4-316">Deshabilite el registro del panel para escenarios de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-316">Disable dashboard logging for high throughput scenarios.</span></span> <span data-ttu-id="3b0b4-317">De forma predeterminada, Hola SDK escribe registros toostorage y esta actividad puede reducir el rendimiento cuando se procesan muchos mensajes.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-317">By default, hello SDK writes logs toostorage, and this activity could degrade performance when you are processing many messages.</span></span> <span data-ttu-id="3b0b4-318">toodisable registro, establezca toonull de cadena de conexión de hello panel tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-318">toodisable logging, set hello dashboard connection string toonull as shown in hello following example.</span></span>

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

<span data-ttu-id="3b0b4-319">Hello en el ejemplo siguiente se muestra varias maneras de toowrite registros:</span><span class="sxs-lookup"><span data-stu-id="3b0b4-319">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="3b0b4-320">En el panel de SDK de WebJobs de hello, Hola salida de hello `TextWriter` objeto se muestra cuando se desplace página toohello para un determinado invocación de función y haga clic en **alternar salida**:</span><span class="sxs-lookup"><span data-stu-id="3b0b4-320">In hello WebJobs SDK Dashboard, hello output from hello `TextWriter` object shows up when you go toohello page for a particular function invocation and click **Toggle Output**:</span></span>

![Clic en el vínculo de invocación de la función](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Registros en la página de invocación de la función](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="3b0b4-323">En el panel de SDK de WebJobs de hello, líneas de hello 100 más reciente de la consola de salida mostrar una al ir a página toohello para hello trabajo Web (no de invocación de función hello) y haga clic en **alternar salida**.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-323">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and click **Toggle Output**.</span></span>

![Clic en Alternar resultados](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

<span data-ttu-id="3b0b4-325">En un trabajo Web continuo, registros de aplicaciones se mostrarán en/datos/trabajos/continua/*{webjobname}*/job_log.txt en sistema de archivos de aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="3b0b4-326">En una aplicación Hola de blobs de Azure registros este aspecto: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write: Hola a todos!, 2014-09-26T21:01:13, Error, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.Error - Hola a todos!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out: Hola a todos!,</span><span class="sxs-lookup"><span data-stu-id="3b0b4-326">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="3b0b4-327">Y en un saludo de la tabla de Azure `Console.Out` y `Console.Error` registros tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="3b0b4-327">And in an Azure table hello `Console.Out` and `Console.Error` logs look like this:</span></span>

![Registro de información en la tabla](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Registro de errores en la tabla](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

<span data-ttu-id="3b0b4-330">Si desea tooplug en su propio registrador, vea [en este ejemplo](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-330">If you want tooplug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span></span>

## <span data-ttu-id="3b0b4-331"><a id="errors"></a>¿Cómo toohandle errores y configurar tiempos de espera</span><span class="sxs-lookup"><span data-stu-id="3b0b4-331"><a id="errors"></a>How toohandle errors and configure timeouts</span></span>
<span data-ttu-id="3b0b4-332">Hello WebJobs SDK también incluye una [tiempo de espera](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) atributo que se puede utilizar toocause un toobe función cancela si no se completa dentro de un período de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-332">hello WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use toocause a function toobe canceled if doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="3b0b4-333">Y si desea tooraise una alerta cuando se producen demasiados errores dentro de un período de tiempo especificado, se puede usar hello `ErrorTrigger` atributo.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-333">And if you want tooraise an alert when too many errors happen within a specified period of time, you can use hello `ErrorTrigger` attribute.</span></span> <span data-ttu-id="3b0b4-334">Este es un [ejemplo de ErrorTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span></span>

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

<span data-ttu-id="3b0b4-335">Puede deshabilitar y habilitar funciones toocontrol, si bien pueden ser desencadenados, mediante un modificador de configuración que podría ser un nombre de variable de entorno o una configuración de aplicación también dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-335">You can also dynamically disable and enable functions toocontrol whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span></span> <span data-ttu-id="3b0b4-336">Ejemplo de código, vea hello `Disable` atributo [repositorio de ejemplos de SDK de WebJobs de hello](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-336">For sample code, see hello `Disable` attribute in [hello WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span></span>

## <span data-ttu-id="3b0b4-337"><a id="nextsteps"></a> Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3b0b4-337"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="3b0b4-338">Esta guía proporciona código de ejemplos que muestran cómo toohandle escenarios comunes para trabajar con colas de Azure.</span><span class="sxs-lookup"><span data-stu-id="3b0b4-338">This guide has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="3b0b4-339">Para obtener más información sobre cómo toouse WebJobs de Azure y Hola SDK de WebJobs, vea [Azure trabajos Web recomienda recursos](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="3b0b4-339">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>
