---
title: Uso del Bus de servicio de Azure con el SDK de WebJobs
description: Aprenda a usar los temas y las colas del Bus de servicio de Azure con el SDK de WebJobs.
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
ms.openlocfilehash: 7cec03cae5d20d1ead9eb24e99415c33d8b76f05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-service-bus-with-the-webjobs-sdk"></a><span data-ttu-id="21aac-103">Uso del Bus de servicio de Azure con el SDK de WebJobs</span><span class="sxs-lookup"><span data-stu-id="21aac-103">How to use Azure Service Bus with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="21aac-104">Información general</span><span class="sxs-lookup"><span data-stu-id="21aac-104">Overview</span></span>
<span data-ttu-id="21aac-105">Esta guía proporciona muestras de código de C# que muestran la manera de desencadenar un proceso cuando se recibe un mensaje de Bus de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="21aac-105">This guide provides C# code samples that show how to trigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="21aac-106">Las muestras de código usan el [SDK de WebJobs](websites-dotnet-webjobs-sdk.md) versión 1.x.</span><span class="sxs-lookup"><span data-stu-id="21aac-106">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="21aac-107">En la guía se supone que sabe [cómo crear un proyecto de trabajos web en Visual Studio con cadenas de conexión que señalan a su cuenta de almacenamiento](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="21aac-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="21aac-108">Los fragmentos de código solo muestran funciones, no el código que crea el objeto `JobHost` como en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="21aac-108">The code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

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

<span data-ttu-id="21aac-109">Puede encontrar un [ejemplo de código de Bus de servicio completo](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) en el repositorio azure-webjobs-sdk-samples en GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="21aac-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in the azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="21aac-110"><a id="prerequisites"></a> Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="21aac-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="21aac-111">Para trabajar con el Bus de servicio debe instalar el paquete NuGet [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) además de los otros paquetes del SDK de trabajos web.</span><span class="sxs-lookup"><span data-stu-id="21aac-111">To work with Service Bus you have to install the [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition to the other WebJobs SDK packages.</span></span> 

<span data-ttu-id="21aac-112">También debe establecer la cadena de conexión AzureWebJobsServiceBus además de las cadenas de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="21aac-112">You also have to set the AzureWebJobsServiceBus connection string in addition to the storage connection strings.</span></span>  <span data-ttu-id="21aac-113">Esto puede hacerlo en la sección `connectionStrings` del archivo App.config, como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="21aac-113">You can do this in the `connectionStrings` section of the App.config file, as shown in the following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="21aac-114">Para ver un proyecto de muestra que incluye la configuración de la cadena de conexión del Bus de servicio App.config, consulte [Ejemplo de Bus de servicio](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="21aac-114">For a sample project that includes the Service Bus connection string setting in the App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="21aac-115">Las cadenas de conexión también se puede definir en el entorno de tiempo de ejecución de Azure, con lo que se reemplaza la configuración de App.config cuando WebJob se ejecuta en Azure. Si desea más información, consulte [Introducción al SDK de WebJobs](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span><span class="sxs-lookup"><span data-stu-id="21aac-115">The connection strings can also be set in the Azure runtime environment, which then overrides the App.config settings when the WebJob runs in Azure; for more information, see [Get Started with the WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="21aac-116"><a id="trigger"></a> Cómo desencadenar una función cuando se recibe un mensaje de la cola de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="21aac-116"><a id="trigger"></a> How to trigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="21aac-117">Para escribir una función que el SDK de WebJobs llama cuando se recibe un mensaje en cola, use el atributo `ServiceBusTrigger` .</span><span class="sxs-lookup"><span data-stu-id="21aac-117">To write a function that the WebJobs SDK calls when a queue message is received, use the `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="21aac-118">El constructor de atributo toma un parámetro de cadena que especifica el nombre de la cola que se va a sondear.</span><span class="sxs-lookup"><span data-stu-id="21aac-118">The attribute constructor takes a parameter that specifies the name of the queue to poll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="21aac-119">Cómo funciona ServiceBusTrigger</span><span class="sxs-lookup"><span data-stu-id="21aac-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="21aac-120">El SDK de recibe un mensaje en el modo `PeekLock` y llama a `Complete` en el mensaje si la función finaliza correctamente, o llama a `Abandon` si se produce un error en la función.</span><span class="sxs-lookup"><span data-stu-id="21aac-120">The SDK receives a message in `PeekLock` mode and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> <span data-ttu-id="21aac-121">Si la ejecución de la función dura más que el tiempo de espera de `PeekLock` , el bloqueo se renovará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="21aac-121">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<span data-ttu-id="21aac-122">El Bus de servicio realiza su propia administración de la cola de daños que el SDK de WebJobs no puede controlar ni configurar.</span><span class="sxs-lookup"><span data-stu-id="21aac-122">Service Bus does its own poison queue handling which cannot be controlled or configured by the WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="21aac-123">Mensajes en cola de cadena</span><span class="sxs-lookup"><span data-stu-id="21aac-123">String queue message</span></span>
<span data-ttu-id="21aac-124">La siguiente muestra de código lee un mensaje en cola que contiene una cadena y escribe la cadena en el panel del SDK de WebJobs.</span><span class="sxs-lookup"><span data-stu-id="21aac-124">The following code sample reads a queue message that contains a string and writes the string to the WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="21aac-125">**Nota:** si va a crear los mensajes en cola en una aplicación que no usa el SDK de WebJobs, asegúrese de establecer [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) en "text/plain".</span><span class="sxs-lookup"><span data-stu-id="21aac-125">**Note:** If you are creating the queue messages in an application that doesn't use the WebJobs SDK, make sure to set [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) to "text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="21aac-126">Mensaje en cola de POCO</span><span class="sxs-lookup"><span data-stu-id="21aac-126">POCO queue message</span></span>
<span data-ttu-id="21aac-127">El SDK deserializará automáticamente un mensaje en cola que contenga JSON para un tipo POCO [(objeto CLR antiguo sin formato)](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object).</span><span class="sxs-lookup"><span data-stu-id="21aac-127">The SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="21aac-128">El siguiente ejemplo de código lee un mensaje en cola que contiene un objeto `BlobInformation` que tiene una propiedad `BlobName`:</span><span class="sxs-lookup"><span data-stu-id="21aac-128">The following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="21aac-129">Para los ejemplos de código que muestran cómo utilizar las propiedades de POCO para que funcionen con blobs y tablas en la misma función, vea la [versión para colas de almacenamiento de este artículo](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span><span class="sxs-lookup"><span data-stu-id="21aac-129">For code samples showing how to use properties of the POCO to work with blobs and tables in the same function, see the [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="21aac-130">Si el código que crea el mensaje en cola no usa el SDK de WebJobs, use código similar al del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="21aac-130">If your code that creates the queue message doesn't use the WebJobs SDK, use code similar to the following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="21aac-131">Los tipos ServiceBusTrigger funcionan con</span><span class="sxs-lookup"><span data-stu-id="21aac-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="21aac-132">Además de los tipos `string` y POCO, puede usar el atributo `ServiceBusTrigger` con una matriz de bytes o un objeto `BrokeredMessage`.</span><span class="sxs-lookup"><span data-stu-id="21aac-132">Besides `string` and POCO  types, you can use the `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="21aac-133"><a id="create"></a> Creación de mensajes en cola del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="21aac-133"><a id="create"></a> How to create Service Bus queue messages</span></span>
<span data-ttu-id="21aac-134">Para escribir una función que cree un nuevo mensaje en cola, use el atributo `ServiceBus` y pase el nombre de la cola al constructor de atributos.</span><span class="sxs-lookup"><span data-stu-id="21aac-134">To write a function that creates a new queue message use the `ServiceBus` attribute and pass in the queue name to the attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="21aac-135">Crear un mensaje en cola único en una función no asincrónica</span><span class="sxs-lookup"><span data-stu-id="21aac-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="21aac-136">La siguiente muestra de código utiliza un parámetro de salida para crear un nuevo mensaje en la cola llamado "outputqueue" con el mismo contenido que el mensaje recibido en la cola llamada "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="21aac-136">The following code sample uses an output parameter to create a new message in the queue named "outputqueue" with the same content as the message received in the queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="21aac-137">El parámetro de salida para crear un mensaje en cola único puede ser cualquiera de los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="21aac-137">The output parameter for creating a single queue message can be any of the following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="21aac-138">Un tipo POCO serializable que define</span><span class="sxs-lookup"><span data-stu-id="21aac-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="21aac-139">Seriado automáticamente como JSON.</span><span class="sxs-lookup"><span data-stu-id="21aac-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="21aac-140">Para los parámetros de tipo POCO, siempre se crea un mensaje en cola cuando finaliza la función; si el parámetro es null, el SDK crea un mensaje en cola que devolverá null cuando se reciba y se deserialice el mensaje.</span><span class="sxs-lookup"><span data-stu-id="21aac-140">For POCO type parameters, a queue message is always created when the function ends; if the parameter is null, the SDK creates a queue message that will return null when the message is received and deserialized.</span></span> <span data-ttu-id="21aac-141">Para los demás tipos, si el parámetro es null, no se creará ningún mensaje en cola.</span><span class="sxs-lookup"><span data-stu-id="21aac-141">For the other types, if the parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="21aac-142">Crear varios mensajes en cola o en funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="21aac-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="21aac-143">Para crear varios mensajes, utilice el atributo `ServiceBus` con `ICollector<T>` o `IAsyncCollector<T>`, como se muestra en el ejemplo de código siguiente:</span><span class="sxs-lookup"><span data-stu-id="21aac-143">To create multiple messages, use  the `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="21aac-144">Cada mensaje en cola se crea inmediatamente cuando se llama al método `Add` .</span><span class="sxs-lookup"><span data-stu-id="21aac-144">Each queue message is created immediately when the `Add` method is called.</span></span>

## <span data-ttu-id="21aac-145"><a id="topics"></a>Trabajo con temas del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="21aac-145"><a id="topics"></a>How to work with Service Bus topics</span></span>
<span data-ttu-id="21aac-146">Para escribir una función a la que llama el SDK cuando se recibe un mensaje en un tema del Bus de servicio, use el atributo `ServiceBusTrigger` con el constructor que toma el nombre del tema y el nombre de la suscripción, como se muestra en el siguiente código de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="21aac-146">To write a function that the SDK calls when a message is received on a Service Bus topic, use the `ServiceBusTrigger` attribute with the constructor that takes topic name and subscription name, as shown in the following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="21aac-147">Para crear un mensaje sobre un tema, use el atributo `ServiceBus` con un nombre de un tema de la misma manera que lo usa con un nombre de cola.</span><span class="sxs-lookup"><span data-stu-id="21aac-147">To create a message on a topic, use the `ServiceBus` attribute with a topic name the same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="21aac-148">Características agregadas en la versión 1.1</span><span class="sxs-lookup"><span data-stu-id="21aac-148">Features added in release 1.1</span></span>
<span data-ttu-id="21aac-149">Las siguientes características se agregaron en la versión 1.1:</span><span class="sxs-lookup"><span data-stu-id="21aac-149">The following features were added in release 1.1:</span></span>

* <span data-ttu-id="21aac-150">Se permite la personalización profunda del procesamiento de mensajes a través de `ServiceBusConfiguration.MessagingProvider`.</span><span class="sxs-lookup"><span data-stu-id="21aac-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="21aac-151">`MessagingProvider` admite la personalización de `MessagingFactory` y `NamespaceManager` de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="21aac-151">`MessagingProvider` supports customization of the Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="21aac-152">Un patrón de estrategia `MessageProcessor` le permite especificar un procesador por cola/tema.</span><span class="sxs-lookup"><span data-stu-id="21aac-152">A `MessageProcessor` strategy pattern allows you to specify a processor per queue/topic.</span></span>
* <span data-ttu-id="21aac-153">La simultaneidad del procesamiento de mensajes se admite de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="21aac-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="21aac-154">La personalización sencilla de `OnMessageOptions` a través de `ServiceBusConfiguration.MessageOptions`.</span><span class="sxs-lookup"><span data-stu-id="21aac-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="21aac-155">Se permite especificar [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) en `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (en los escenarios donde es probable que no tenga derechos de administración).</span><span class="sxs-lookup"><span data-stu-id="21aac-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) to be specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="21aac-156">Tenga en cuenta que WebJobs de Azure no puede aprovisionar automáticamente temas y colas inexistente sin Manage AccessRights.</span><span class="sxs-lookup"><span data-stu-id="21aac-156">Note that Azure WebJobs is unable to automatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="21aac-157"><a id="queues"></a>Temas relacionados tratados en el artículo de procedimientos de las colas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="21aac-157"><a id="queues"></a>Related topics covered by the storage queues how-to article</span></span>
<span data-ttu-id="21aac-158">Para obtener información acerca de los escenarios del SDK de trabajos web no específicos del Bus de servicio, vea [Uso del almacenamiento de colas de Azure con el SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="21aac-158">For information about WebJobs SDK scenarios not specific to Service Bus, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="21aac-159">Entre los temas tratados en este artículo se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="21aac-159">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="21aac-160">Funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="21aac-160">Async functions</span></span>
* <span data-ttu-id="21aac-161">Varias instancias</span><span class="sxs-lookup"><span data-stu-id="21aac-161">Multiple instances</span></span>
* <span data-ttu-id="21aac-162">Apagado correcto</span><span class="sxs-lookup"><span data-stu-id="21aac-162">Graceful shutdown</span></span>
* <span data-ttu-id="21aac-163">Utilizar atributos del SDK de WebJobs en el cuerpo de una función</span><span class="sxs-lookup"><span data-stu-id="21aac-163">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="21aac-164">Establecer las cadenas de conexión del SDK en el código.</span><span class="sxs-lookup"><span data-stu-id="21aac-164">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="21aac-165">Establecer valores para los parámetros del constructor del SDK de WebJobs en el código</span><span class="sxs-lookup"><span data-stu-id="21aac-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="21aac-166">Desencadenar una función manualmente</span><span class="sxs-lookup"><span data-stu-id="21aac-166">Trigger a function manually</span></span>
* <span data-ttu-id="21aac-167">Escribir registros</span><span class="sxs-lookup"><span data-stu-id="21aac-167">Write logs</span></span>

## <span data-ttu-id="21aac-168"><a id="nextsteps"></a> Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="21aac-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="21aac-169">En esta guía se han proporcionado ejemplos de código que muestran cómo controlar los escenarios comunes para trabajar con el Bus de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="21aac-169">This guide has provided code samples that show how to handle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="21aac-170">Para obtener más información acerca de cómo usar el SDK de WebJobs y WebJobs de Azure, consulte [Recursos de WebJobs de Azure recomendados](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="21aac-170">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

