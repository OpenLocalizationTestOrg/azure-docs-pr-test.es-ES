---
title: aaaHow toouse Service Bus de Azure con hello SDK de WebJobs
description: "Obtenga información acerca de cómo toouse colas de Service Bus de Azure y temas con Hola SDK de WebJobs."
services: app-service\web, service-bus
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 2114a934-135b-42b8-871c-6cc040214e76
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: cb801a9320a20c276da4f48c8941c09d3f09bb1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a><span data-ttu-id="96090-103">Cómo toouse de Bus de servicio de Azure con Hola SDK de WebJobs</span><span class="sxs-lookup"><span data-stu-id="96090-103">How toouse Azure Service Bus with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="96090-104">Información general</span><span class="sxs-lookup"><span data-stu-id="96090-104">Overview</span></span>
<span data-ttu-id="96090-105">Esta guía proporciona C# de ejemplos de código que muestran cómo tootrigger un proceso cuando se recibe un mensaje de Service Bus de Azure.</span><span class="sxs-lookup"><span data-stu-id="96090-105">This guide provides C# code samples that show how tootrigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="96090-106">uso de ejemplos de código de Hello [SDK de WebJobs](websites-dotnet-webjobs-sdk.md) versión 1.x.</span><span class="sxs-lookup"><span data-stu-id="96090-106">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="96090-107">Guía de Hola se supone que sabe [cómo cadenas toocreate un proyecto WebJob en Visual Studio con una conexión de esa cuenta de almacenamiento de punto tooyour](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="96090-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="96090-108">fragmentos de código de Hello solo muestran las funciones, no Hola código que crea hello `JobHost` objeto como en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="96090-108">hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

```
public class Program
{
   public static void Main()
   {
      JobHostConfiguration config = new JobHostConfiguration();
      config.UseServiceBus();
      JobHost host = new JobHost(config);
      host.RunAndBlock();
   }
}
```

<span data-ttu-id="96090-109">A [ejemplo de código completo de Bus de servicio](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) está en el repositorio de azure-webjobs-sdk-samples de hello en GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="96090-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in hello azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="96090-110"><a id="prerequisites"></a> Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="96090-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="96090-111">toowork con Bus de servicio tiene hello tooinstall [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet paquete además toohello otros paquetes de SDK de WebJobs.</span><span class="sxs-lookup"><span data-stu-id="96090-111">toowork with Service Bus you have tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition toohello other WebJobs SDK packages.</span></span> 

<span data-ttu-id="96090-112">Tiene también la cadena de conexión de tooset hello AzureWebJobsServiceBus en cadenas de conexión de almacenamiento de toohello de adición.</span><span class="sxs-lookup"><span data-stu-id="96090-112">You also have tooset hello AzureWebJobsServiceBus connection string in addition toohello storage connection strings.</span></span>  <span data-ttu-id="96090-113">Para hacer esto en hello `connectionStrings` sección del archivo App.config de hello, como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="96090-113">You can do this in hello `connectionStrings` section of hello App.config file, as shown in hello following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="96090-114">Para un proyecto de ejemplo que incluye la configuración de la cadena de conexión de hello Bus de servicio en el archivo App.config de hello, consulte [ejemplo de Bus de servicio](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="96090-114">For a sample project that includes hello Service Bus connection string setting in hello App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="96090-115">las cadenas de conexión de Hello también pueden establecerse en entorno de Azure en tiempo de ejecución de hello, que invalida a continuación, configuración del archivo App.config hello cuando Hola trabajo Web se ejecuta en Azure; Para obtener más información, consulte [empezar a trabajar con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span><span class="sxs-lookup"><span data-stu-id="96090-115">hello connection strings can also be set in hello Azure runtime environment, which then overrides hello App.config settings when hello WebJob runs in Azure; for more information, see [Get Started with hello WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="96090-116"><a id="trigger"></a>¿Cómo se recibe tootrigger una función cuando un Bus de servicio cola de mensajes</span><span class="sxs-lookup"><span data-stu-id="96090-116"><a id="trigger"></a> How tootrigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="96090-117">llama a una función que Hola SDK de WebJobs toowrite cuando se recibe un mensaje de la cola, utilice hello `ServiceBusTrigger` atributo.</span><span class="sxs-lookup"><span data-stu-id="96090-117">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="96090-118">constructor de atributos de Hello toma un parámetro que especifica el nombre de Hola de hello cola toopoll.</span><span class="sxs-lookup"><span data-stu-id="96090-118">hello attribute constructor takes a parameter that specifies hello name of hello queue toopoll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="96090-119">Cómo funciona ServiceBusTrigger</span><span class="sxs-lookup"><span data-stu-id="96090-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="96090-120">Hello SDK recibe un mensaje en `PeekLock` modo y llamadas `Complete` en el mensaje de bienvenida de si la función hello finaliza correctamente, o llamadas a `Abandon` si se produce un error en la función hello.</span><span class="sxs-lookup"><span data-stu-id="96090-120">hello SDK receives a message in `PeekLock` mode and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> <span data-ttu-id="96090-121">Si se ejecuta más de hello función hello `PeekLock` tiempo de espera de bloqueo de Hola se renovará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="96090-121">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<span data-ttu-id="96090-122">Bus de servicio hace su propio control de la cola de mensajes dudosos que no puede ser controlado o configurado por hello SDK de WebJobs.</span><span class="sxs-lookup"><span data-stu-id="96090-122">Service Bus does its own poison queue handling which cannot be controlled or configured by hello WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="96090-123">Mensajes en cola de cadena</span><span class="sxs-lookup"><span data-stu-id="96090-123">String queue message</span></span>
<span data-ttu-id="96090-124">Hello ejemplo de código siguiente lee un mensaje de la cola que contiene una cadena y escribe la cadena de hello toohello panel de SDK de WebJobs.</span><span class="sxs-lookup"><span data-stu-id="96090-124">hello following code sample reads a queue message that contains a string and writes hello string toohello WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="96090-125">**Nota:** si está creando Hola mensajes en cola en una aplicación que no utilice Hola SDK de WebJobs, asegúrese de tooset seguro [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) demasiado "text/plain".</span><span class="sxs-lookup"><span data-stu-id="96090-125">**Note:** If you are creating hello queue messages in an application that doesn't use hello WebJobs SDK, make sure tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) too"text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="96090-126">Mensaje en cola de POCO</span><span class="sxs-lookup"><span data-stu-id="96090-126">POCO queue message</span></span>
<span data-ttu-id="96090-127">Hola SDK deserializará automáticamente un mensaje de la cola que contiene un valor JSON para un POCO [(objeto de CLR Plain Old](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) tipo.</span><span class="sxs-lookup"><span data-stu-id="96090-127">hello SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="96090-128">ejemplo de código siguiente Hello lee un mensaje de la cola que contiene un `BlobInformation` objeto que tiene un `BlobName` propiedad:</span><span class="sxs-lookup"><span data-stu-id="96090-128">hello following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="96090-129">Para obtener ejemplos de código que muestra cómo las propiedades de toouse de hello POCO toowork con blobs y tablas de Hola igual, función, vea hello [versión de las colas de almacenamiento de información de este artículo](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span><span class="sxs-lookup"><span data-stu-id="96090-129">For code samples showing how toouse properties of hello POCO toowork with blobs and tables in hello same function, see hello [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="96090-130">Si el código que crea el mensaje de bienvenida de cola no utiliza Hola SDK de WebJobs, utilice código toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="96090-130">If your code that creates hello queue message doesn't use hello WebJobs SDK, use code similar toohello following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="96090-131">Los tipos ServiceBusTrigger funcionan con</span><span class="sxs-lookup"><span data-stu-id="96090-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="96090-132">Además `string` y tipos POCO, puede usar hello `ServiceBusTrigger` atributo con una matriz de bytes o una `BrokeredMessage` objeto.</span><span class="sxs-lookup"><span data-stu-id="96090-132">Besides `string` and POCO  types, you can use hello `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="96090-133"><a id="create"></a>¿Cómo toocreate Bus de servicio cola de mensajes</span><span class="sxs-lookup"><span data-stu-id="96090-133"><a id="create"></a> How toocreate Service Bus queue messages</span></span>
<span data-ttu-id="96090-134">una función que crea un nuevo mensaje de cola de toowrite usar hello `ServiceBus` atributo y pase un constructor de atributos de toohello de nombre de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="96090-134">toowrite a function that creates a new queue message use hello `ServiceBus` attribute and pass in hello queue name toohello attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="96090-135">Crear un mensaje en cola único en una función no asincrónica</span><span class="sxs-lookup"><span data-stu-id="96090-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="96090-136">Hola siguiendo el ejemplo de código utiliza un toocreate de parámetro de salida un nuevo mensaje en cola Hola denominado "outputqueue" con el mismo contenido como Hola en cola Hola denominado "inputqueue" se recibió un mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="96090-136">hello following code sample uses an output parameter toocreate a new message in hello queue named "outputqueue" with hello same content as hello message received in hello queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="96090-137">parámetro de salida de Hello para la creación de un mensaje de la cola solo puede ser cualquiera de los siguientes tipos de hello:</span><span class="sxs-lookup"><span data-stu-id="96090-137">hello output parameter for creating a single queue message can be any of hello following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="96090-138">Un tipo POCO serializable que define</span><span class="sxs-lookup"><span data-stu-id="96090-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="96090-139">Seriado automáticamente como JSON.</span><span class="sxs-lookup"><span data-stu-id="96090-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="96090-140">Para los parámetros de tipo POCO, siempre se crea un mensaje de la cola cuando finaliza la función hello; Si el parámetro hello es null, Hola SDK crea un mensaje de cola que devolverá null cuando se recibe y deserializar los mensajes de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="96090-140">For POCO type parameters, a queue message is always created when hello function ends; if hello parameter is null, hello SDK creates a queue message that will return null when hello message is received and deserialized.</span></span> <span data-ttu-id="96090-141">Para Hola otros tipos, si el parámetro hello es null no se crea ningún mensaje de la cola.</span><span class="sxs-lookup"><span data-stu-id="96090-141">For hello other types, if hello parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="96090-142">Crear varios mensajes en cola o en funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="96090-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="96090-143">toocreate varios mensajes, usar hello `ServiceBus` atribuir a `ICollector<T>` o `IAsyncCollector<T>`, tal y como se muestra en el siguiente ejemplo de código de hello:</span><span class="sxs-lookup"><span data-stu-id="96090-143">toocreate multiple messages, use  hello `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="96090-144">Cada mensaje de la cola se crea inmediatamente cuando hello `Add` se llama al método.</span><span class="sxs-lookup"><span data-stu-id="96090-144">Each queue message is created immediately when hello `Add` method is called.</span></span>

## <span data-ttu-id="96090-145"><a id="topics"></a>¿Cómo toowork con temas de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="96090-145"><a id="topics"></a>How toowork with Service Bus topics</span></span>
<span data-ttu-id="96090-146">llama a una función que Hola SDK toowrite cuando se recibe un mensaje en un tema de Bus de servicio, use hello `ServiceBusTrigger` atributo con el constructor de Hola que toma el nombre del tema y nombre de la suscripción, como se muestra en el siguiente ejemplo de código de hello:</span><span class="sxs-lookup"><span data-stu-id="96090-146">toowrite a function that hello SDK calls when a message is received on a Service Bus topic, use hello `ServiceBusTrigger` attribute with hello constructor that takes topic name and subscription name, as shown in hello following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="96090-147">toocreate un mensaje en un tema, use hello `ServiceBus` atributo con un hello de nombre de tema igual forma que se utiliza con un nombre de la cola.</span><span class="sxs-lookup"><span data-stu-id="96090-147">toocreate a message on a topic, use hello `ServiceBus` attribute with a topic name hello same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="96090-148">Características agregadas en la versión 1.1</span><span class="sxs-lookup"><span data-stu-id="96090-148">Features added in release 1.1</span></span>
<span data-ttu-id="96090-149">Hola siguientes características se agregaron en la versión 1.1:</span><span class="sxs-lookup"><span data-stu-id="96090-149">hello following features were added in release 1.1:</span></span>

* <span data-ttu-id="96090-150">Se permite la personalización profunda del procesamiento de mensajes a través de `ServiceBusConfiguration.MessagingProvider`.</span><span class="sxs-lookup"><span data-stu-id="96090-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="96090-151">`MessagingProvider`admite la personalización de hello Service Bus `MessagingFactory` y `NamespaceManager`.</span><span class="sxs-lookup"><span data-stu-id="96090-151">`MessagingProvider` supports customization of hello Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="96090-152">Un `MessageProcessor` patrón de estrategia le permite toospecify un procesador por cola/tema.</span><span class="sxs-lookup"><span data-stu-id="96090-152">A `MessageProcessor` strategy pattern allows you toospecify a processor per queue/topic.</span></span>
* <span data-ttu-id="96090-153">La simultaneidad del procesamiento de mensajes se admite de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="96090-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="96090-154">La personalización sencilla de `OnMessageOptions` a través de `ServiceBusConfiguration.MessageOptions`.</span><span class="sxs-lookup"><span data-stu-id="96090-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="96090-155">Permitir [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe especificado en `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (para escenarios donde puede que no tenga derechos de administración).</span><span class="sxs-lookup"><span data-stu-id="96090-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="96090-156">Tenga en cuenta que WebJobs de Azure es temas sin administrar AccessRights y colas de tooautomatically no se puede aprovisionar inexistente.</span><span class="sxs-lookup"><span data-stu-id="96090-156">Note that Azure WebJobs is unable tooautomatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="96090-157"><a id="queues"></a>Temas relacionados cubiertos por las colas de almacenamiento de hello cómo-tooarticle</span><span class="sxs-lookup"><span data-stu-id="96090-157"><a id="queues"></a>Related topics covered by hello storage queues how-tooarticle</span></span>
<span data-ttu-id="96090-158">Para obtener información acerca de los escenarios de SDK de WebJobs tooService no específico del Bus, vea [cómo toouse Azure cola de almacenamiento con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="96090-158">For information about WebJobs SDK scenarios not specific tooService Bus, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="96090-159">Los temas tratados en dicho artículo Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="96090-159">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="96090-160">Funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="96090-160">Async functions</span></span>
* <span data-ttu-id="96090-161">Varias instancias</span><span class="sxs-lookup"><span data-stu-id="96090-161">Multiple instances</span></span>
* <span data-ttu-id="96090-162">Apagado correcto</span><span class="sxs-lookup"><span data-stu-id="96090-162">Graceful shutdown</span></span>
* <span data-ttu-id="96090-163">Utilizar atributos de SDK de WebJobs en el cuerpo de Hola de una función</span><span class="sxs-lookup"><span data-stu-id="96090-163">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="96090-164">Establecer las cadenas de conexión de SDK de hello en el código</span><span class="sxs-lookup"><span data-stu-id="96090-164">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="96090-165">Establecer valores para los parámetros del constructor del SDK de WebJobs en el código</span><span class="sxs-lookup"><span data-stu-id="96090-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="96090-166">Desencadenar una función manualmente</span><span class="sxs-lookup"><span data-stu-id="96090-166">Trigger a function manually</span></span>
* <span data-ttu-id="96090-167">Escribir registros</span><span class="sxs-lookup"><span data-stu-id="96090-167">Write logs</span></span>

## <span data-ttu-id="96090-168"><a id="nextsteps"></a> Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="96090-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="96090-169">Esta guía proporciona código de ejemplos que muestran cómo toohandle escenarios comunes para trabajar con el Bus de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="96090-169">This guide has provided code samples that show how toohandle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="96090-170">Para obtener más información sobre cómo toouse WebJobs de Azure y Hola SDK de WebJobs, vea [Azure trabajos Web recomienda recursos](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="96090-170">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

