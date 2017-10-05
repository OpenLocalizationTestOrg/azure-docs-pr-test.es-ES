---
title: Utilizar bibliotecas de clases de .NET con Azure Functions | Microsoft Docs
description: "Obtenga información acerca de cómo crear bibliotecas de clases de .NET para su uso con Azure Functions"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: 9f5db0c2-a88e-4fa8-9b59-37a7096fc828
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/09/2017
ms.author: donnam
ms.openlocfilehash: 0613bb96d3afb85ff7e684246b128e4eef518d23
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a><span data-ttu-id="72087-104">Utilizar bibliotecas de clases de .NET con Azure Functions</span><span class="sxs-lookup"><span data-stu-id="72087-104">Using .NET class libraries with Azure Functions</span></span>

<span data-ttu-id="72087-105">Además de los archivos de script, Azure Functions admite la publicación de una biblioteca de clases como la implementación para una o más funciones.</span><span class="sxs-lookup"><span data-stu-id="72087-105">In addition to script files, Azure Functions supports publishing a class library as the implementation for one or more functions.</span></span> <span data-ttu-id="72087-106">Se recomienda utilizar [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="72087-106">We recommend that you use the [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72087-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="72087-107">Prerequisites</span></span> 

<span data-ttu-id="72087-108">Este artículo tiene los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="72087-108">This article has the following prerequisites:</span></span>

- <span data-ttu-id="72087-109">[Versión preliminar de Visual Studio 2017 15.3](https://www.visualstudio.com/vs/preview/).</span><span class="sxs-lookup"><span data-stu-id="72087-109">[Visual Studio 2017 15.3 Preview](https://www.visualstudio.com/vs/preview/).</span></span> <span data-ttu-id="72087-110">Instalación de las cargas de trabajo **ASP.NET y desarrollo web** y **Desarrollo de Azure**.</span><span class="sxs-lookup"><span data-stu-id="72087-110">Install the workloads **ASP.NET and web development** and **Azure development**.</span></span>
- [<span data-ttu-id="72087-111">Herramientas de Azure Functions para Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="72087-111">Azure Function Tools for Visual Studio 2017</span></span>](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a><span data-ttu-id="72087-112">Proyecto de biblioteca de clases de Functions</span><span class="sxs-lookup"><span data-stu-id="72087-112">Functions class library project</span></span>

<span data-ttu-id="72087-113">En Visual Studio, cree un nuevo proyecto de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="72087-113">From Visual Studio, create a new Azure Functions project.</span></span> <span data-ttu-id="72087-114">La nueva plantilla de proyecto crea los archivos *host.json* y *local.settings.json*.</span><span class="sxs-lookup"><span data-stu-id="72087-114">The new project template creates the files *host.json* and *local.settings.json*.</span></span> <span data-ttu-id="72087-115">Puede [personalizar la configuración en tiempo de ejecución de Azure Functions en host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="72087-115">You can [customize Azure Functions runtime settings in host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span> 

<span data-ttu-id="72087-116">El archivo *local.settings.json* almacena la configuración de la aplicación, las cadenas de conexión y la configuración de Azure Functions Core Tools.</span><span class="sxs-lookup"><span data-stu-id="72087-116">The file *local.settings.json* stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="72087-117">Para más información acerca de su estructura, consulte [Codificar y probar Azure Functions localmente](functions-run-local.md#local-settings).</span><span class="sxs-lookup"><span data-stu-id="72087-117">To learn more about its structure, see [Code and test Azure functions locally](functions-run-local.md#local-settings).</span></span>

### <a name="functionname-attribute"></a><span data-ttu-id="72087-118">Atributo FunctionName</span><span class="sxs-lookup"><span data-stu-id="72087-118">FunctionName attribute</span></span>

<span data-ttu-id="72087-119">El atributo [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marca un método como punto de entrada de una función.</span><span class="sxs-lookup"><span data-stu-id="72087-119">The attribute [`FunctionNameAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marks a method as a function entry point.</span></span> <span data-ttu-id="72087-120">Se debe utilizar exactamente con un desencadenador y 0 o más enlaces de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="72087-120">It must be used with exactly one trigger and 0 or more input and output bindings.</span></span>

### <a name="conversion-to-functionjson"></a><span data-ttu-id="72087-121">Conversión a function.json</span><span class="sxs-lookup"><span data-stu-id="72087-121">Conversion to function.json</span></span>

<span data-ttu-id="72087-122">Cuando se compila un proyecto de Azure Functions, se genera un archivo `function.json` en el directorio, que coincide con el nombre de función definido por `[FunctionName]`.</span><span class="sxs-lookup"><span data-stu-id="72087-122">When an Azure Functions project is built, it produces a file `function.json` in the directory matching the function name defined by `[FunctionName]`.</span></span> <span data-ttu-id="72087-123">Especifica los desencadenadores y los enlaces y puntos en el archivo de ensamblado del proyecto.</span><span class="sxs-lookup"><span data-stu-id="72087-123">It specifies triggers and bindings and points to the project assembly file.</span></span>

<span data-ttu-id="72087-124">Esta conversión la realiza el paquete de NuGet [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span><span class="sxs-lookup"><span data-stu-id="72087-124">This conversion is performed by the NuGet package [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span></span> <span data-ttu-id="72087-125">El código fuente está disponible en el repositorio de GitHub [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span><span class="sxs-lookup"><span data-stu-id="72087-125">The source is available in the GitHub repo [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span></span>

## <a name="triggers-and-bindings"></a><span data-ttu-id="72087-126">Desencadenadores y enlaces</span><span class="sxs-lookup"><span data-stu-id="72087-126">Triggers and bindings</span></span>

<span data-ttu-id="72087-127">En la tabla siguiente se enumeran los desencadenadores y los enlaces que están disponibles en un proyecto de biblioteca de clases de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="72087-127">The following table lists the triggers and bindings that are available in an Azure Functions class library project.</span></span> <span data-ttu-id="72087-128">Todos los atributos están en el espacio de nombres `Microsoft.Azure.WebJobs`.</span><span class="sxs-lookup"><span data-stu-id="72087-128">All attributes are in the namespace `Microsoft.Azure.WebJobs`.</span></span>

| <span data-ttu-id="72087-129">Enlace</span><span class="sxs-lookup"><span data-stu-id="72087-129">Binding</span></span> | <span data-ttu-id="72087-130">Atributo</span><span class="sxs-lookup"><span data-stu-id="72087-130">Attribute</span></span> | <span data-ttu-id="72087-131">Paquete de NuGet</span><span class="sxs-lookup"><span data-stu-id="72087-131">NuGet package</span></span> |
|------   | ------    | ------        |
| [<span data-ttu-id="72087-132">Desencadenador de almacenamiento de blobs, entrada, salida</span><span class="sxs-lookup"><span data-stu-id="72087-132">Blob storage trigger, input, output</span></span>](#blob-storage) | <span data-ttu-id="72087-133">[BlobAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="72087-133">[BlobAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="72087-134">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="72087-134">[Microsoft.Azure.WebJobs]</span></span> | <span data-ttu-id="72087-135">[Almacenamiento de blobs]</span><span class="sxs-lookup"><span data-stu-id="72087-135">[Blob storage]</span></span> |
| [<span data-ttu-id="72087-136">Enlaces de entrada y salida de Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="72087-136">Cosmos DB input and output binding</span></span>](#cosmos-db) | <span data-ttu-id="72087-137">[DocumentDBAttribute]</span><span class="sxs-lookup"><span data-stu-id="72087-137">[DocumentDBAttribute]</span></span> | <span data-ttu-id="72087-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span><span class="sxs-lookup"><span data-stu-id="72087-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span></span> | 
| [<span data-ttu-id="72087-139">Desencadenador y salida de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="72087-139">Event Hubs trigger and output</span></span>](#event-hub) | <span data-ttu-id="72087-140">[EventHubTriggerAttribute], [EventHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="72087-140">[EventHubTriggerAttribute], [EventHubAttribute]</span></span> | <span data-ttu-id="72087-141">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="72087-141">[Microsoft.Azure.WebJobs.ServiceBus]</span></span> |
| [<span data-ttu-id="72087-142">Entrada y salida de archivos externos</span><span class="sxs-lookup"><span data-stu-id="72087-142">External file input and output</span></span>](#api-hub) | <span data-ttu-id="72087-143">[ApiHubFileAttribute]</span><span class="sxs-lookup"><span data-stu-id="72087-143">[ApiHubFileAttribute]</span></span> | <span data-ttu-id="72087-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span><span class="sxs-lookup"><span data-stu-id="72087-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span></span> |
| [<span data-ttu-id="72087-145">Desencadenador HTTP y webhook</span><span class="sxs-lookup"><span data-stu-id="72087-145">HTTP and webhook trigger</span></span>](#http) | <span data-ttu-id="72087-146">[HttpTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="72087-146">[HttpTriggerAttribute]</span></span> | <span data-ttu-id="72087-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span><span class="sxs-lookup"><span data-stu-id="72087-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span></span> |
| [<span data-ttu-id="72087-148">Entrada y salida de Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="72087-148">Mobile Apps input and output</span></span>](#mobile-apps) | <span data-ttu-id="72087-149">[MobileTableAttribute]</span><span class="sxs-lookup"><span data-stu-id="72087-149">[MobileTableAttribute]</span></span> | <span data-ttu-id="72087-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span><span class="sxs-lookup"><span data-stu-id="72087-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span></span> | 
| [<span data-ttu-id="72087-151">Salida de Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="72087-151">Notification Hubs output</span></span>](#nh) | <span data-ttu-id="72087-152">[NotificationHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="72087-152">[NotificationHubAttribute]</span></span> | <span data-ttu-id="72087-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span><span class="sxs-lookup"><span data-stu-id="72087-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span></span> | 
| [<span data-ttu-id="72087-154">Desencadenador y salida de Queue Storage</span><span class="sxs-lookup"><span data-stu-id="72087-154">Queue storage trigger and output</span></span>](#queue) | <span data-ttu-id="72087-155">[QueueAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="72087-155">[QueueAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="72087-156">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="72087-156">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="72087-157">Salida de SendGrid</span><span class="sxs-lookup"><span data-stu-id="72087-157">SendGrid output</span></span>](#sendgrid) | <span data-ttu-id="72087-158">[SendGridAttribute]</span><span class="sxs-lookup"><span data-stu-id="72087-158">[SendGridAttribute]</span></span> | <span data-ttu-id="72087-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span><span class="sxs-lookup"><span data-stu-id="72087-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span></span> | 
| [<span data-ttu-id="72087-160">Desencadenador y salida de Service Bus</span><span class="sxs-lookup"><span data-stu-id="72087-160">Service Bus trigger and output</span></span>](#service-bus) | <span data-ttu-id="72087-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="72087-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span></span> | <span data-ttu-id="72087-162">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="72087-162">[Microsoft.Azure.WebJobs.ServiceBus]</span></span>
| [<span data-ttu-id="72087-163">Entrada y salida de Table Storage</span><span class="sxs-lookup"><span data-stu-id="72087-163">Table storage input and output</span></span>](#table) | <span data-ttu-id="72087-164">[TableAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="72087-164">[TableAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="72087-165">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="72087-165">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="72087-166">Desencadenador de temporizador</span><span class="sxs-lookup"><span data-stu-id="72087-166">Timer trigger</span></span>](#timer) | <span data-ttu-id="72087-167">[TimerTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="72087-167">[TimerTriggerAttribute]</span></span> | <span data-ttu-id="72087-168">[Microsoft.Azure.WebJobs.Extensions]</span><span class="sxs-lookup"><span data-stu-id="72087-168">[Microsoft.Azure.WebJobs.Extensions]</span></span> | 
| [<span data-ttu-id="72087-169">Salida de Twilio</span><span class="sxs-lookup"><span data-stu-id="72087-169">Twilio output</span></span>](#twilio) | <span data-ttu-id="72087-170">[TwilioSmsAttribute]</span><span class="sxs-lookup"><span data-stu-id="72087-170">[TwilioSmsAttribute]</span></span> | <span data-ttu-id="72087-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span><span class="sxs-lookup"><span data-stu-id="72087-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span></span> | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a><span data-ttu-id="72087-172">Desencadenador y enlaces de entrada y salida de Blob Storage</span><span class="sxs-lookup"><span data-stu-id="72087-172">Blob storage trigger, input, and output bindings</span></span>

<span data-ttu-id="72087-173">Azure Functions admite desencadenador y enlaces de entrada y salida para Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="72087-173">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="72087-174">Para más información sobre las expresiones de enlace y los metadatos, consulte [Enlaces de Blob Storage de Azure Functions](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="72087-174">For more information on binding expressions and metadata, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>

<span data-ttu-id="72087-175">Un desencadenador de blob se define con el atributo `[BlobTrigger]`.</span><span class="sxs-lookup"><span data-stu-id="72087-175">A blob trigger is defined with the `[BlobTrigger]` attribute.</span></span> <span data-ttu-id="72087-176">Puede utilizar el atributo `[StorageAccount]` para definir la cuenta de almacenamiento que se usa en una función completa o clase.</span><span class="sxs-lookup"><span data-stu-id="72087-176">You can use the attribute `[StorageAccount]` to define the storage account that is used by an entire function or class.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

<span data-ttu-id="72087-177">La entrada y salida de blob se definen utilizando el atributo `[Blob]` junto con un parámetro `FileAccess` que indica lectura o escritura.</span><span class="sxs-lookup"><span data-stu-id="72087-177">Blob input and output are defined using the `[Blob]` attribute, along with a `FileAccess` parameter indicating read or write.</span></span> <span data-ttu-id="72087-178">En el ejemplo siguiente se usa un desencadenador de blob y un enlace de salida.</span><span class="sxs-lookup"><span data-stu-id="72087-178">The following example uses a blob trigger and blob output binding.</span></span>

```csharp
[FunctionName("ResizeImage")]
[StorageAccount("AzureWebJobsStorage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-sm/{name}", FileAccess.Write)] Stream imageSmall, 
    [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageMedium)
{
    var imageBuilder = ImageResizer.ImageBuilder.Current;
    var size = imageDimensionsTable[ImageSize.Small];

    imageBuilder.Build(image, imageSmall,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);

    image.Position = 0;
    size = imageDimensionsTable[ImageSize.Medium];

    imageBuilder.Build(image, imageMedium,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);
}

public enum ImageSize { ExtraSmall, Small, Medium }

private static Dictionary<ImageSize, (int, int)> imageDimensionsTable = new Dictionary<ImageSize, (int, int)>() {
    { ImageSize.ExtraSmall, (320, 200) },
    { ImageSize.Small,      (640, 400) },
    { ImageSize.Medium,     (800, 600) }
};
```        

<a name="cosmos-db"></a>

### <a name="cosmos-db-input-and-output-bindings"></a><span data-ttu-id="72087-179">Enlaces de entrada y salida de Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="72087-179">Cosmos DB input and output bindings</span></span>

<span data-ttu-id="72087-180">Azure Functions admite enlaces de entrada y salida para Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="72087-180">Azure Functions supports input and output bindings for Cosmos DB.</span></span> <span data-ttu-id="72087-181">Para más información sobre las características del enlace de Cosmos DB, consulte [Enlaces de Cosmos DB de Azure Functions](functions-bindings-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="72087-181">To learn more about the features of the Cosmos DB binding, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>

<span data-ttu-id="72087-182">Para enlazar a un documento de Cosmos DB, use el atributo `[DocumentDB]` en el paquete de NuGet [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span><span class="sxs-lookup"><span data-stu-id="72087-182">To bind to a Cosmos DB document, use the attribute `[DocumentDB]` in the NuGet package [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span></span> <span data-ttu-id="72087-183">El siguiente ejemplo tiene un desencadenador de cola y un enlace de salida de la API de DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="72087-183">The following example has a queue trigger and a DocumentDB API output binding:</span></span>

```csharp
[FunctionName("QueueToDocDB")]        
public static void Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, 
    [DocumentDB("ToDoList", "Items", ConnectionStringSetting = "DocDBConnection")] out dynamic document)
{
    document = new { Text = myQueueItem, id = Guid.NewGuid() };
}

```

<a name="event-hub"></a>

### <a name="event-hubs-trigger-and-output"></a><span data-ttu-id="72087-184">Desencadenador y salida de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="72087-184">Event Hubs trigger and output</span></span>

<span data-ttu-id="72087-185">Azure Functions admite enlaces de desencadenador y salida para Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="72087-185">Azure Functions supports trigger and output bindings for Event Hubs.</span></span> <span data-ttu-id="72087-186">Para más información, consulte [Enlaces de Event Hub de Azure Functions](functions-bindings-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="72087-186">For more information, see  [Azure Functions Event Hub bindings](functions-bindings-event-hubs.md).</span></span>

<span data-ttu-id="72087-187">Los tipos `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` y `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` se definen en el paquete de NuGet [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="72087-187">The types `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` and `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` are defined in the NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="72087-188">En el ejemplo siguiente se usa un desencadenador de Event Hub:</span><span class="sxs-lookup"><span data-stu-id="72087-188">The following example uses an Event Hub trigger:</span></span>

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="72087-189">El siguiente ejemplo tiene una salida de Event Hub, utilizando el valor devuelto por el método como salida:</span><span class="sxs-lookup"><span data-stu-id="72087-189">The following example has an Event Hub output, using the method return value as the output:</span></span>

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    return $"{DateTime.Now}";
}
```

<a name="api-hub"></a>

### <a name="external-file-input-and-output"></a><span data-ttu-id="72087-190">Entrada y salida de archivo externo</span><span class="sxs-lookup"><span data-stu-id="72087-190">External file input and output</span></span>

<span data-ttu-id="72087-191">Azure Functions admite enlaces de desencadenador, entrada y salida para archivos externos, como Google Drive, Dropbox y OneDrive.</span><span class="sxs-lookup"><span data-stu-id="72087-191">Azure Functions supports trigger, input, and output bindings for external files, such as Google Drive, Dropbox, and OneDrive.</span></span> <span data-ttu-id="72087-192">Para más información, consulte [Enlaces de archivos externos de Azure Functions](functions-bindings-external-file.md).</span><span class="sxs-lookup"><span data-stu-id="72087-192">To learn more, see [Azure Functions External File bindings](functions-bindings-external-file.md).</span></span> <span data-ttu-id="72087-193">Los atributos `[ExternalFileTrigger]` y `[ExternalFile]` se definen en el paquete de NuGet [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span><span class="sxs-lookup"><span data-stu-id="72087-193">The attributes `[ExternalFileTrigger]` and `[ExternalFile]` are defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span></span>

<span data-ttu-id="72087-194">En el ejemplo de C# siguiente se muestran enlaces de archivo externo de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="72087-194">The following C# example demonstrates an external file input and output binding.</span></span> <span data-ttu-id="72087-195">El código copia el archivo de entrada en el archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="72087-195">The code copies the input file to the output file.</span></span>

```csharp
[StorageAccount("MyStorageConnection")]
[FunctionName("ExternalFile")]
[return: ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}-Copy", FileAccess.Write)]
public static string Run([QueueTrigger("myqueue-items")] string myQueueItem, 
    [ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}", FileAccess.Read)] string myInputFile, 
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    return myInputFile;
}
```

<a name="http"></a>

### <a name="http-and-webhooks"></a><span data-ttu-id="72087-196">HTTP y webhooks</span><span class="sxs-lookup"><span data-stu-id="72087-196">HTTP and webhooks</span></span>

<span data-ttu-id="72087-197">Use el atributo `HttpTrigger` para definir un desencadenador HTTP o un webhook.</span><span class="sxs-lookup"><span data-stu-id="72087-197">Use the `HttpTrigger` attribute to define an HTTP trigger or webhook.</span></span> <span data-ttu-id="72087-198">Este atributo se define en el paquete de NuGet [Microsoft.Azure.WebJobs.Extensions.Http].</span><span class="sxs-lookup"><span data-stu-id="72087-198">This attribute is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.Http].</span></span> <span data-ttu-id="72087-199">Puede personalizar el nivel de autorización, el tipo de webhook, la ruta y los métodos.</span><span class="sxs-lookup"><span data-stu-id="72087-199">You can customize the authorization level, webhook type, route, and methods.</span></span> <span data-ttu-id="72087-200">En el ejemplo siguiente se define un desencadenador HTTP con autenticación anónima y tipo de webhook _genericJson_.</span><span class="sxs-lookup"><span data-stu-id="72087-200">The following example defines an HTTP trigger with anonymous authentication and _genericJson_ webhook type.</span></span>

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a><span data-ttu-id="72087-201">Entrada y salida de Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="72087-201">Mobile Apps input and output</span></span>

<span data-ttu-id="72087-202">Azure Functions admite enlaces de entrada y salida para Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="72087-202">Azure Functions supports input and output bindings for Mobile Apps.</span></span> <span data-ttu-id="72087-203">Para más información, consulte [Enlaces de Mobile Apps de Azure Functions](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="72087-203">To learn more, see [Azure Functions Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span> <span data-ttu-id="72087-204">El atributo `[MobileTable]` se define en el paquete de NuGet [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span><span class="sxs-lookup"><span data-stu-id="72087-204">The attribute `[MobileTable]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span></span>

<span data-ttu-id="72087-205">En el siguiente ejemplo se muestra un enlace de salida de Mobile Apps:</span><span class="sxs-lookup"><span data-stu-id="72087-205">The following example demonstrates a Mobile Apps output binding:</span></span>

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a><span data-ttu-id="72087-206">Salida de Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="72087-206">Notification Hubs output</span></span>

<span data-ttu-id="72087-207">Azure Functions admite un enlace de salida para Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="72087-207">Azure Functions supports an output binding for Notification Hubs.</span></span> <span data-ttu-id="72087-208">Para más información, consulte [Enlace de salida de Notification Hub de Azure Functions](functions-bindings-notification-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="72087-208">To learn more, see [Azure Functions Notification Hub output binding](functions-bindings-notification-hubs.md).</span></span> <span data-ttu-id="72087-209">El atributo `[NotificationHub]` se define en el paquete de NuGet [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span><span class="sxs-lookup"><span data-stu-id="72087-209">The attribute `[NotificationHub]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span></span>

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a><span data-ttu-id="72087-210">Desencadenador y salida de Queue Storage</span><span class="sxs-lookup"><span data-stu-id="72087-210">Queue storage trigger and output</span></span>

<span data-ttu-id="72087-211">Azure Functions admite desencadenador y enlaces de salida para Azure Queues.</span><span class="sxs-lookup"><span data-stu-id="72087-211">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="72087-212">Para más información, consulte [Enlaces de Queue Storage de Azure Functions](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="72087-212">For more information, see [Azure Functions Queue Storage bindings](functions-bindings-storage-queue.md).</span></span>

<span data-ttu-id="72087-213">En el ejemplo siguiente se muestra cómo usar el tipo de valor devuelto por la función con un enlace de salida de cola, usando el atributo `[Queue]`.</span><span class="sxs-lookup"><span data-stu-id="72087-213">The following example shows how to use the function return type with a queue output binding, using the `[Queue]` attribute.</span></span> <span data-ttu-id="72087-214">Para definir un desencadenador de cola, utilice el atributo `[QueueTrigger]`.</span><span class="sxs-lookup"><span data-stu-id="72087-214">To define a queue trigger, use the `[QueueTrigger]` attribute.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
public static class QueueFunctions
{
    // HTTP trigger with queue output binding
    [FunctionName("QueueOutput")]
    [return: Queue("myqueue-items")]
    public static string QueueOutput([HttpTrigger] dynamic input,  TraceWriter log)
    {
        log.Info($"C# function processed: {input.Text}");
        return input.Text;
    }

    // Queue trigger
    [FunctionName("QueueTrigger")]
    [StorageAccount("AzureWebJobsStorage")]
    public static void QueueTrigger([QueueTrigger("myqueue-items")] string myQueueItem, TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
}

```

<a name="sendgrid"></a>

### <a name="sendgrid-output"></a><span data-ttu-id="72087-215">Salida de SendGrid</span><span class="sxs-lookup"><span data-stu-id="72087-215">SendGrid output</span></span>

<span data-ttu-id="72087-216">Azure Functions admite un enlace de salida de SendGrid para el envío de correo electrónico mediante programación.</span><span class="sxs-lookup"><span data-stu-id="72087-216">Azure Functions supports a SendGrid output binding for sending email programmatically.</span></span> <span data-ttu-id="72087-217">Para más información, consulte [Enlaces de SendGrid de Azure Functions](functions-bindings-sendgrid.md).</span><span class="sxs-lookup"><span data-stu-id="72087-217">To learn more, see [Azure Functions SendGrid bindings](functions-bindings-sendgrid.md).</span></span>

<span data-ttu-id="72087-218">El atributo `[SendGrid]` se define en el paquete de NuGet [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span><span class="sxs-lookup"><span data-stu-id="72087-218">The attribute `[SendGrid]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span></span>

<span data-ttu-id="72087-219">El siguiente es un ejemplo del uso de un desencadenador de cola de Service Bus y un enlace de salida de SendGrid mediante `SendGridMessage`:</span><span class="sxs-lookup"><span data-stu-id="72087-219">The following is an example of using a Service Bus queue trigger and a SendGrid output binding using `SendGridMessage`:</span></span>

```csharp
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid] out SendGridMessage message)
{
    message = new SendGridMessage();
    message.AddTo(email.To);
    message.AddContent("text/html", email.Body);
    message.SetFrom(new EmailAddress(email.From));
    message.SetSubject(email.Subject);
}

public class OutgoingEmail
{
    public string To { get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a><span data-ttu-id="72087-220">Desencadenador y salida de Service Bus</span><span class="sxs-lookup"><span data-stu-id="72087-220">Service Bus trigger and output</span></span>

<span data-ttu-id="72087-221">Azure Functions admite enlaces de desencadenador y salida para colas y temas de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="72087-221">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span> <span data-ttu-id="72087-222">Para más información sobre la configuración de enlaces, consulte [Enlaces de Service Bus de Azure Functions](functions-bindings-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="72087-222">For more information on configuring bindings, see [Azure Functions Service Bus bindings](functions-bindings-service-bus.md).</span></span>

<span data-ttu-id="72087-223">Los atributos `[ServiceBusTrigger]` y `[ServiceBus]` se definen en el paquete de NuGet [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="72087-223">The attributes `[ServiceBusTrigger]` and `[ServiceBus]` are defined in the NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="72087-224">A continuación se muestra un ejemplo de un desencadenador de cola de Service Bus:</span><span class="sxs-lookup"><span data-stu-id="72087-224">The following is an example of a Service Bus queue trigger:</span></span>

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<span data-ttu-id="72087-225">El siguiente es un ejemplo de un enlace de salida de Service Bus, utilizando el tipo de valor devuelto por el método como salida:</span><span class="sxs-lookup"><span data-stu-id="72087-225">The following is an example of a Service Bus output binding, using the method return type as the output:</span></span>

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string ServiceBusOutput([HttpTrigger] dynamic input, TraceWriter log)
{
    log.Info($"C# function processed: {input.Text}");
    return input.Text;
}
```        

<a name="table"></a>

### <a name="table-storage-input-and-output"></a><span data-ttu-id="72087-226">Entrada y salida de Table Storage</span><span class="sxs-lookup"><span data-stu-id="72087-226">Table storage input and output</span></span>

<span data-ttu-id="72087-227">Azure Functions admite enlaces de entrada y salida para Table Storage de Azure.</span><span class="sxs-lookup"><span data-stu-id="72087-227">Azure Functions supports input and output bindings for Azure Table storage.</span></span> <span data-ttu-id="72087-228">Para más información, consulte [Enlaces de Table Storage de Azure Functions](functions-bindings-storage-table.md).</span><span class="sxs-lookup"><span data-stu-id="72087-228">To learn more, see [Azure Functions Table storage bindings](functions-bindings-storage-table.md).</span></span>

<span data-ttu-id="72087-229">El siguiente ejemplo es una clase con dos funciones, mostrando los enlaces de entrada y salida de Table Storage.</span><span class="sxs-lookup"><span data-stu-id="72087-229">The following example is a class with two functions, demonstrating table storage output and input bindings.</span></span> 

```csharp
[StorageAccount("AzureWebJobsStorage")]
public class TableStorage
{
    public class MyPoco
    {
        public string PartitionKey { get; set; }
        public string RowKey { get; set; }
        public string Text { get; set; }
    }

    [FunctionName("TableOutput")]
    [return: Table("MyTable")]
    public static MyPoco TableOutput([HttpTrigger] dynamic input, TraceWriter log)
    {
        log.Info($"C# http trigger function processed: {input.Text}");
        return new MyPoco { PartitionKey = "Http", RowKey = Guid.NewGuid().ToString(), Text = input.Text };
    }

    // use the metadata parameter "queueTrigger" to bind the queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a><span data-ttu-id="72087-230">Desencadenador de temporizador</span><span class="sxs-lookup"><span data-stu-id="72087-230">Timer trigger</span></span>

<span data-ttu-id="72087-231">Azure Functions incluye un enlace a un desencadenador de temporizador que le permite ejecutar su código de función según una programación definida.</span><span class="sxs-lookup"><span data-stu-id="72087-231">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> <span data-ttu-id="72087-232">Para más información sobre las características del enlace, consulte [Programar la ejecución de código con Azure Functions](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="72087-232">To learn more about the features of the binding, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>

<span data-ttu-id="72087-233">En el plan de Consumo, puede definir programaciones con una [expresión CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span><span class="sxs-lookup"><span data-stu-id="72087-233">On the Consumption plan, you can define schedules with a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span></span> <span data-ttu-id="72087-234">Si utiliza un plan de App Service, también puede usar una cadena TimeSpan.</span><span class="sxs-lookup"><span data-stu-id="72087-234">If you're using an App Service Plan, you can also use a TimeSpan string.</span></span> 

<span data-ttu-id="72087-235">En el ejemplo siguiente se define un desencadenador de temporizador que se ejecuta cada 5 minutos:</span><span class="sxs-lookup"><span data-stu-id="72087-235">The following example defines a timer trigger that runs every 5 minutes:</span></span>

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a><span data-ttu-id="72087-236">Salida de Twilio</span><span class="sxs-lookup"><span data-stu-id="72087-236">Twilio output</span></span>

<span data-ttu-id="72087-237">Azure Functions admite enlaces de salida de Twilio para permitir a sus funciones enviar mensajes de texto SMS.</span><span class="sxs-lookup"><span data-stu-id="72087-237">Azure Functions supports Twilio output bindings to enable your functions to send SMS text messages.</span></span> <span data-ttu-id="72087-238">Para más información, consulte [Envío de mensajes SMS desde Azure Functions mediante el enlace de salida de Twilio](functions-bindings-twilio.md).</span><span class="sxs-lookup"><span data-stu-id="72087-238">To learn more, see [Send SMS messages from Azure Functions using the Twilio output binding](functions-bindings-twilio.md).</span></span> 

<span data-ttu-id="72087-239">El atributo `[TwilioSms]` se define en el paquete [Microsoft.Azure.WebJobs.Extensions.Twilio].</span><span class="sxs-lookup"><span data-stu-id="72087-239">The attribute `[TwilioSms]` is defined in the package [Microsoft.Azure.WebJobs.Extensions.Twilio].</span></span>

<span data-ttu-id="72087-240">En el ejemplo de C# siguiente se utiliza un desencadenador de cola y un enlace de salida de Twilio:</span><span class="sxs-lookup"><span data-stu-id="72087-240">The following C# example uses a queue trigger and a Twilio output binding:</span></span>

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        To = order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a><span data-ttu-id="72087-241">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="72087-241">Next steps</span></span>

<span data-ttu-id="72087-242">Para más información sobre el uso de Azure Functions en C# de scripting, consulte [Referencia para desarrolladores de C\# de script de Azure Functions](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="72087-242">For more information on using Azure Functions in C# scripting, see [Azure Functions C\# script developer reference](functions-reference-csharp.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
<span data-ttu-id="72087-243">[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="72087-243">[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1</span></span>
<span data-ttu-id="72087-244">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="72087-244">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1</span></span>
<span data-ttu-id="72087-245">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="72087-245">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span></span>
<span data-ttu-id="72087-246">[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="72087-246">[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1</span></span>
<span data-ttu-id="72087-247">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="72087-247">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1</span></span>
<span data-ttu-id="72087-248">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="72087-248">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span></span>
<span data-ttu-id="72087-249">[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="72087-249">[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1</span></span>
<span data-ttu-id="72087-250">[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1</span><span class="sxs-lookup"><span data-stu-id="72087-250">[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1</span></span>
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
<span data-ttu-id="72087-251">[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4</span><span class="sxs-lookup"><span data-stu-id="72087-251">[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4</span></span>
<span data-ttu-id="72087-252">[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="72087-252">[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1</span></span>
<span data-ttu-id="72087-253">[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="72087-253">[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1</span></span>


<!-- Links to source --> 
<span data-ttu-id="72087-254">[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="72087-254">[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs</span></span>
<span data-ttu-id="72087-255">[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="72087-255">[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs</span></span>
<span data-ttu-id="72087-256">[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="72087-256">[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs</span></span>
<span data-ttu-id="72087-257">[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="72087-257">[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs</span></span>
<span data-ttu-id="72087-258">[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs </span><span class="sxs-lookup"><span data-stu-id="72087-258">[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs </span></span>
<span data-ttu-id="72087-259">[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="72087-259">[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs</span></span>
<span data-ttu-id="72087-260">[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="72087-260">[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs</span></span>
<span data-ttu-id="72087-261">[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="72087-261">[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs</span></span>
<span data-ttu-id="72087-262">[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="72087-262">[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs</span></span>
<span data-ttu-id="72087-263">[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="72087-263">[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs</span></span>
<span data-ttu-id="72087-264">[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="72087-264">[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs</span></span>
<span data-ttu-id="72087-265">[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="72087-265">[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs</span></span>
<span data-ttu-id="72087-266">[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="72087-266">[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs</span></span>
<span data-ttu-id="72087-267">[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="72087-267">[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs</span></span>
<span data-ttu-id="72087-268">[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="72087-268">[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs</span></span>
<span data-ttu-id="72087-269">[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="72087-269">[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs</span></span>
