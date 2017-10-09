---
title: aaaUsing .NET clase bibliotecas con funciones de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooauthor bibliotecas de clases de .NET para usar con funciones de Azure"
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
ms.openlocfilehash: 4e0fd954b554006ba1d8ecc47403a9fb1c67c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a><span data-ttu-id="79ed8-104">Utilizar bibliotecas de clases de .NET con Azure Functions</span><span class="sxs-lookup"><span data-stu-id="79ed8-104">Using .NET class libraries with Azure Functions</span></span>

<span data-ttu-id="79ed8-105">Además tooscript archivos, las funciones de Azure es compatible con la publicación de una biblioteca de clases como implementación de Hola para una o más funciones.</span><span class="sxs-lookup"><span data-stu-id="79ed8-105">In addition tooscript files, Azure Functions supports publishing a class library as hello implementation for one or more functions.</span></span> <span data-ttu-id="79ed8-106">Le recomendamos que use hello [Azure funciones de Visual Studio de 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="79ed8-106">We recommend that you use hello [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79ed8-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="79ed8-107">Prerequisites</span></span> 

<span data-ttu-id="79ed8-108">Este artículo tiene Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="79ed8-108">This article has hello following prerequisites:</span></span>

- <span data-ttu-id="79ed8-109">[Versión preliminar de Visual Studio 2017 15.3](https://www.visualstudio.com/vs/preview/).</span><span class="sxs-lookup"><span data-stu-id="79ed8-109">[Visual Studio 2017 15.3 Preview](https://www.visualstudio.com/vs/preview/).</span></span> <span data-ttu-id="79ed8-110">Instalar las cargas de trabajo de hello **ASP.NET y desarrollo web** y **desarrollo Azure**.</span><span class="sxs-lookup"><span data-stu-id="79ed8-110">Install hello workloads **ASP.NET and web development** and **Azure development**.</span></span>
- [<span data-ttu-id="79ed8-111">Herramientas de Azure Functions para Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="79ed8-111">Azure Function Tools for Visual Studio 2017</span></span>](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a><span data-ttu-id="79ed8-112">Proyecto de biblioteca de clases de Functions</span><span class="sxs-lookup"><span data-stu-id="79ed8-112">Functions class library project</span></span>

<span data-ttu-id="79ed8-113">En Visual Studio, cree un nuevo proyecto de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="79ed8-113">From Visual Studio, create a new Azure Functions project.</span></span> <span data-ttu-id="79ed8-114">nueva plantilla de proyecto Hola crea archivos de hello *host.json* y *local.settings.json*.</span><span class="sxs-lookup"><span data-stu-id="79ed8-114">hello new project template creates hello files *host.json* and *local.settings.json*.</span></span> <span data-ttu-id="79ed8-115">Puede [personalizar la configuración en tiempo de ejecución de Azure Functions en host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="79ed8-115">You can [customize Azure Functions runtime settings in host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span> 

<span data-ttu-id="79ed8-116">archivo hello *local.settings.json* almacena la configuración de aplicación, las cadenas de conexión y configuración de herramientas básicas de las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="79ed8-116">hello file *local.settings.json* stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="79ed8-117">toolearn más información acerca de su estructura, vea [código y probar las funciones de Azure localmente](functions-run-local.md#local-settings).</span><span class="sxs-lookup"><span data-stu-id="79ed8-117">toolearn more about its structure, see [Code and test Azure functions locally](functions-run-local.md#local-settings).</span></span>

### <a name="functionname-attribute"></a><span data-ttu-id="79ed8-118">Atributo FunctionName</span><span class="sxs-lookup"><span data-stu-id="79ed8-118">FunctionName attribute</span></span>

<span data-ttu-id="79ed8-119">atributo de Hello [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marca un método como un punto de entrada de función.</span><span class="sxs-lookup"><span data-stu-id="79ed8-119">hello attribute [`FunctionNameAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marks a method as a function entry point.</span></span> <span data-ttu-id="79ed8-120">Se debe utilizar exactamente con un desencadenador y 0 o más enlaces de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="79ed8-120">It must be used with exactly one trigger and 0 or more input and output bindings.</span></span>

### <a name="conversion-toofunctionjson"></a><span data-ttu-id="79ed8-121">Conversión toofunction.json</span><span class="sxs-lookup"><span data-stu-id="79ed8-121">Conversion toofunction.json</span></span>

<span data-ttu-id="79ed8-122">Cuando se compila un proyecto de las funciones de Azure, genera un archivo `function.json` en el directorio de hello con el mismo nombre de función hello definido por `[FunctionName]`.</span><span class="sxs-lookup"><span data-stu-id="79ed8-122">When an Azure Functions project is built, it produces a file `function.json` in hello directory matching hello function name defined by `[FunctionName]`.</span></span> <span data-ttu-id="79ed8-123">Especifica los desencadenadores y los enlaces y puntos toohello el archivo de ensamblado de proyecto.</span><span class="sxs-lookup"><span data-stu-id="79ed8-123">It specifies triggers and bindings and points toohello project assembly file.</span></span>

<span data-ttu-id="79ed8-124">Esta conversión se realiza por paquete de NuGet hello [Microsoft\.NET\.Sdk\.funciones](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span><span class="sxs-lookup"><span data-stu-id="79ed8-124">This conversion is performed by hello NuGet package [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span></span> <span data-ttu-id="79ed8-125">Hola origen está disponible en el repositorio de GitHub de hello [azure\-funciones\-frente a\-generar\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span><span class="sxs-lookup"><span data-stu-id="79ed8-125">hello source is available in hello GitHub repo [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span></span>

## <a name="triggers-and-bindings"></a><span data-ttu-id="79ed8-126">Desencadenadores y enlaces</span><span class="sxs-lookup"><span data-stu-id="79ed8-126">Triggers and bindings</span></span>

<span data-ttu-id="79ed8-127">Hello tabla siguiente enumeran los desencadenadores de Hola y enlaces que están disponibles en un proyecto de biblioteca de clases de las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="79ed8-127">hello following table lists hello triggers and bindings that are available in an Azure Functions class library project.</span></span> <span data-ttu-id="79ed8-128">Todos los atributos no están en el espacio de nombres de hello `Microsoft.Azure.WebJobs`.</span><span class="sxs-lookup"><span data-stu-id="79ed8-128">All attributes are in hello namespace `Microsoft.Azure.WebJobs`.</span></span>

| <span data-ttu-id="79ed8-129">Enlace</span><span class="sxs-lookup"><span data-stu-id="79ed8-129">Binding</span></span> | <span data-ttu-id="79ed8-130">Atributo</span><span class="sxs-lookup"><span data-stu-id="79ed8-130">Attribute</span></span> | <span data-ttu-id="79ed8-131">Paquete de NuGet</span><span class="sxs-lookup"><span data-stu-id="79ed8-131">NuGet package</span></span> |
|------   | ------    | ------        |
| [<span data-ttu-id="79ed8-132">Desencadenador de almacenamiento de blobs, entrada, salida</span><span class="sxs-lookup"><span data-stu-id="79ed8-132">Blob storage trigger, input, output</span></span>](#blob-storage) | <span data-ttu-id="79ed8-133">[BlobAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="79ed8-133">[BlobAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="79ed8-134">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="79ed8-134">[Microsoft.Azure.WebJobs]</span></span> | <span data-ttu-id="79ed8-135">[Almacenamiento de blobs]</span><span class="sxs-lookup"><span data-stu-id="79ed8-135">[Blob storage]</span></span> |
| [<span data-ttu-id="79ed8-136">Enlaces de entrada y salida de Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="79ed8-136">Cosmos DB input and output binding</span></span>](#cosmos-db) | <span data-ttu-id="79ed8-137">[DocumentDBAttribute]</span><span class="sxs-lookup"><span data-stu-id="79ed8-137">[DocumentDBAttribute]</span></span> | <span data-ttu-id="79ed8-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span><span class="sxs-lookup"><span data-stu-id="79ed8-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span></span> | 
| [<span data-ttu-id="79ed8-139">Desencadenador y salida de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="79ed8-139">Event Hubs trigger and output</span></span>](#event-hub) | <span data-ttu-id="79ed8-140">[EventHubTriggerAttribute], [EventHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="79ed8-140">[EventHubTriggerAttribute], [EventHubAttribute]</span></span> | <span data-ttu-id="79ed8-141">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="79ed8-141">[Microsoft.Azure.WebJobs.ServiceBus]</span></span> |
| [<span data-ttu-id="79ed8-142">Entrada y salida de archivos externos</span><span class="sxs-lookup"><span data-stu-id="79ed8-142">External file input and output</span></span>](#api-hub) | <span data-ttu-id="79ed8-143">[ApiHubFileAttribute]</span><span class="sxs-lookup"><span data-stu-id="79ed8-143">[ApiHubFileAttribute]</span></span> | <span data-ttu-id="79ed8-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span><span class="sxs-lookup"><span data-stu-id="79ed8-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span></span> |
| [<span data-ttu-id="79ed8-145">Desencadenador HTTP y webhook</span><span class="sxs-lookup"><span data-stu-id="79ed8-145">HTTP and webhook trigger</span></span>](#http) | <span data-ttu-id="79ed8-146">[HttpTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="79ed8-146">[HttpTriggerAttribute]</span></span> | <span data-ttu-id="79ed8-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span><span class="sxs-lookup"><span data-stu-id="79ed8-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span></span> |
| [<span data-ttu-id="79ed8-148">Entrada y salida de Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="79ed8-148">Mobile Apps input and output</span></span>](#mobile-apps) | <span data-ttu-id="79ed8-149">[MobileTableAttribute]</span><span class="sxs-lookup"><span data-stu-id="79ed8-149">[MobileTableAttribute]</span></span> | <span data-ttu-id="79ed8-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span><span class="sxs-lookup"><span data-stu-id="79ed8-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span></span> | 
| [<span data-ttu-id="79ed8-151">Salida de Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="79ed8-151">Notification Hubs output</span></span>](#nh) | <span data-ttu-id="79ed8-152">[NotificationHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="79ed8-152">[NotificationHubAttribute]</span></span> | <span data-ttu-id="79ed8-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span><span class="sxs-lookup"><span data-stu-id="79ed8-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span></span> | 
| [<span data-ttu-id="79ed8-154">Desencadenador y salida de Queue Storage</span><span class="sxs-lookup"><span data-stu-id="79ed8-154">Queue storage trigger and output</span></span>](#queue) | <span data-ttu-id="79ed8-155">[QueueAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="79ed8-155">[QueueAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="79ed8-156">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="79ed8-156">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="79ed8-157">Salida de SendGrid</span><span class="sxs-lookup"><span data-stu-id="79ed8-157">SendGrid output</span></span>](#sendgrid) | <span data-ttu-id="79ed8-158">[SendGridAttribute]</span><span class="sxs-lookup"><span data-stu-id="79ed8-158">[SendGridAttribute]</span></span> | <span data-ttu-id="79ed8-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span><span class="sxs-lookup"><span data-stu-id="79ed8-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span></span> | 
| [<span data-ttu-id="79ed8-160">Desencadenador y salida de Service Bus</span><span class="sxs-lookup"><span data-stu-id="79ed8-160">Service Bus trigger and output</span></span>](#service-bus) | <span data-ttu-id="79ed8-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="79ed8-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span></span> | <span data-ttu-id="79ed8-162">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="79ed8-162">[Microsoft.Azure.WebJobs.ServiceBus]</span></span>
| [<span data-ttu-id="79ed8-163">Entrada y salida de Table Storage</span><span class="sxs-lookup"><span data-stu-id="79ed8-163">Table storage input and output</span></span>](#table) | <span data-ttu-id="79ed8-164">[TableAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="79ed8-164">[TableAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="79ed8-165">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="79ed8-165">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="79ed8-166">Desencadenador de temporizador</span><span class="sxs-lookup"><span data-stu-id="79ed8-166">Timer trigger</span></span>](#timer) | <span data-ttu-id="79ed8-167">[TimerTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="79ed8-167">[TimerTriggerAttribute]</span></span> | <span data-ttu-id="79ed8-168">[Microsoft.Azure.WebJobs.Extensions]</span><span class="sxs-lookup"><span data-stu-id="79ed8-168">[Microsoft.Azure.WebJobs.Extensions]</span></span> | 
| [<span data-ttu-id="79ed8-169">Salida de Twilio</span><span class="sxs-lookup"><span data-stu-id="79ed8-169">Twilio output</span></span>](#twilio) | <span data-ttu-id="79ed8-170">[TwilioSmsAttribute]</span><span class="sxs-lookup"><span data-stu-id="79ed8-170">[TwilioSmsAttribute]</span></span> | <span data-ttu-id="79ed8-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span><span class="sxs-lookup"><span data-stu-id="79ed8-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span></span> | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a><span data-ttu-id="79ed8-172">Desencadenador y enlaces de entrada y salida de Blob Storage</span><span class="sxs-lookup"><span data-stu-id="79ed8-172">Blob storage trigger, input, and output bindings</span></span>

<span data-ttu-id="79ed8-173">Azure Functions admite desencadenador y enlaces de entrada y salida para Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="79ed8-173">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="79ed8-174">Para más información sobre las expresiones de enlace y los metadatos, consulte [Enlaces de Blob Storage de Azure Functions](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="79ed8-174">For more information on binding expressions and metadata, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>

<span data-ttu-id="79ed8-175">Se define un desencadenador de blob con hello `[BlobTrigger]` atributo.</span><span class="sxs-lookup"><span data-stu-id="79ed8-175">A blob trigger is defined with hello `[BlobTrigger]` attribute.</span></span> <span data-ttu-id="79ed8-176">Puede usar el atributo de hello `[StorageAccount]` cuenta de almacenamiento de hello toodefine utilizado por una función completa o clase.</span><span class="sxs-lookup"><span data-stu-id="79ed8-176">You can use hello attribute `[StorageAccount]` toodefine hello storage account that is used by an entire function or class.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

<span data-ttu-id="79ed8-177">BLOB de entrada y salida se definen mediante hello `[Blob]` atributo, junto con un `FileAccess` que indica el parámetro de lectura o escritura.</span><span class="sxs-lookup"><span data-stu-id="79ed8-177">Blob input and output are defined using hello `[Blob]` attribute, along with a `FileAccess` parameter indicating read or write.</span></span> <span data-ttu-id="79ed8-178">Hola siguiente ejemplo se usa un desencadenador de blob y enlace de salida de blobs.</span><span class="sxs-lookup"><span data-stu-id="79ed8-178">hello following example uses a blob trigger and blob output binding.</span></span>

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

### <a name="cosmos-db-input-and-output-bindings"></a><span data-ttu-id="79ed8-179">Enlaces de entrada y salida de Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="79ed8-179">Cosmos DB input and output bindings</span></span>

<span data-ttu-id="79ed8-180">Azure Functions admite enlaces de entrada y salida para Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79ed8-180">Azure Functions supports input and output bindings for Cosmos DB.</span></span> <span data-ttu-id="79ed8-181">vea toolearn más información acerca de características de Hola de enlace, la base de datos de Cosmos hello [enlaces de base de datos de Azure funciones Cosmos](functions-bindings-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="79ed8-181">toolearn more about hello features of hello Cosmos DB binding, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>

<span data-ttu-id="79ed8-182">toobind tooa documento de Cosmos DB, utilice el atributo de hello `[DocumentDB]` en paquete de NuGet hello [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span><span class="sxs-lookup"><span data-stu-id="79ed8-182">toobind tooa Cosmos DB document, use hello attribute `[DocumentDB]` in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span></span> <span data-ttu-id="79ed8-183">Hola siguiente ejemplo tiene un desencadenador de cola y una API de documentos que el enlace de salida:</span><span class="sxs-lookup"><span data-stu-id="79ed8-183">hello following example has a queue trigger and a DocumentDB API output binding:</span></span>

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

### <a name="event-hubs-trigger-and-output"></a><span data-ttu-id="79ed8-184">Desencadenador y salida de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="79ed8-184">Event Hubs trigger and output</span></span>

<span data-ttu-id="79ed8-185">Azure Functions admite enlaces de desencadenador y salida para Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="79ed8-185">Azure Functions supports trigger and output bindings for Event Hubs.</span></span> <span data-ttu-id="79ed8-186">Para más información, consulte [Enlaces de Event Hub de Azure Functions](functions-bindings-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="79ed8-186">For more information, see  [Azure Functions Event Hub bindings](functions-bindings-event-hubs.md).</span></span>

<span data-ttu-id="79ed8-187">Hola tipos `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` y `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` se definen en el paquete de NuGet hello [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="79ed8-187">hello types `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` and `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="79ed8-188">Hello en el ejemplo siguiente se usa un desencadenador de concentrador de eventos:</span><span class="sxs-lookup"><span data-stu-id="79ed8-188">hello following example uses an Event Hub trigger:</span></span>

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="79ed8-189">Hello en el ejemplo siguiente se tiene un concentrador de eventos de salida, utilizando el valor devuelto del método hello como salida de hello:</span><span class="sxs-lookup"><span data-stu-id="79ed8-189">hello following example has an Event Hub output, using hello method return value as hello output:</span></span>

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

### <a name="external-file-input-and-output"></a><span data-ttu-id="79ed8-190">Entrada y salida de archivo externo</span><span class="sxs-lookup"><span data-stu-id="79ed8-190">External file input and output</span></span>

<span data-ttu-id="79ed8-191">Azure Functions admite enlaces de desencadenador, entrada y salida para archivos externos, como Google Drive, Dropbox y OneDrive.</span><span class="sxs-lookup"><span data-stu-id="79ed8-191">Azure Functions supports trigger, input, and output bindings for external files, such as Google Drive, Dropbox, and OneDrive.</span></span> <span data-ttu-id="79ed8-192">más información, consulte toolearn [enlaces del archivo externo de las funciones de Azure](functions-bindings-external-file.md).</span><span class="sxs-lookup"><span data-stu-id="79ed8-192">toolearn more, see [Azure Functions External File bindings](functions-bindings-external-file.md).</span></span> <span data-ttu-id="79ed8-193">Hola atributos `[ExternalFileTrigger]` y `[ExternalFile]` se definen en el paquete de NuGet hello [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span><span class="sxs-lookup"><span data-stu-id="79ed8-193">hello attributes `[ExternalFileTrigger]` and `[ExternalFile]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span></span>

<span data-ttu-id="79ed8-194">Hola el ejemplo de C# siguiente se muestra un archivo externo de entrada y salida de enlace.</span><span class="sxs-lookup"><span data-stu-id="79ed8-194">hello following C# example demonstrates an external file input and output binding.</span></span> <span data-ttu-id="79ed8-195">copias de código de Hello Hola archivo de salida de toohello de archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="79ed8-195">hello code copies hello input file toohello output file.</span></span>

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

### <a name="http-and-webhooks"></a><span data-ttu-id="79ed8-196">HTTP y webhooks</span><span class="sxs-lookup"><span data-stu-id="79ed8-196">HTTP and webhooks</span></span>

<span data-ttu-id="79ed8-197">Hola de uso `HttpTrigger` webhook o el desencadenador de toodefine HTTP de atributo.</span><span class="sxs-lookup"><span data-stu-id="79ed8-197">Use hello `HttpTrigger` attribute toodefine an HTTP trigger or webhook.</span></span> <span data-ttu-id="79ed8-198">Este atributo se define en el paquete de NuGet hello [Microsoft.Azure.WebJobs.Extensions.Http].</span><span class="sxs-lookup"><span data-stu-id="79ed8-198">This attribute is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.Http].</span></span> <span data-ttu-id="79ed8-199">Puede personalizar el nivel de autorización de hello, tipo de webhook, ruta y métodos.</span><span class="sxs-lookup"><span data-stu-id="79ed8-199">You can customize hello authorization level, webhook type, route, and methods.</span></span> <span data-ttu-id="79ed8-200">Hello en el ejemplo siguiente se define un desencadenador HTTP con la autenticación anónima y _genericJson_ webhook tipo.</span><span class="sxs-lookup"><span data-stu-id="79ed8-200">hello following example defines an HTTP trigger with anonymous authentication and _genericJson_ webhook type.</span></span>

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a><span data-ttu-id="79ed8-201">Entrada y salida de Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="79ed8-201">Mobile Apps input and output</span></span>

<span data-ttu-id="79ed8-202">Azure Functions admite enlaces de entrada y salida para Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="79ed8-202">Azure Functions supports input and output bindings for Mobile Apps.</span></span> <span data-ttu-id="79ed8-203">más información, consulte toolearn [enlaces de aplicaciones móviles de Azure funciones](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="79ed8-203">toolearn more, see [Azure Functions Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span> <span data-ttu-id="79ed8-204">atributo de Hello `[MobileTable]` se define en el paquete de NuGet hello [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span><span class="sxs-lookup"><span data-stu-id="79ed8-204">hello attribute `[MobileTable]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span></span>

<span data-ttu-id="79ed8-205">Hello en el ejemplo siguiente se muestra un aplicaciones móviles de enlace de salida:</span><span class="sxs-lookup"><span data-stu-id="79ed8-205">hello following example demonstrates a Mobile Apps output binding:</span></span>

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a><span data-ttu-id="79ed8-206">Salida de Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="79ed8-206">Notification Hubs output</span></span>

<span data-ttu-id="79ed8-207">Azure Functions admite un enlace de salida para Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="79ed8-207">Azure Functions supports an output binding for Notification Hubs.</span></span> <span data-ttu-id="79ed8-208">más información, consulte toolearn [enlace de salida del centro de notificaciones de las funciones de Azure](functions-bindings-notification-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="79ed8-208">toolearn more, see [Azure Functions Notification Hub output binding](functions-bindings-notification-hubs.md).</span></span> <span data-ttu-id="79ed8-209">atributo de Hello `[NotificationHub]` se define en el paquete de NuGet hello [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span><span class="sxs-lookup"><span data-stu-id="79ed8-209">hello attribute `[NotificationHub]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span></span>

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a><span data-ttu-id="79ed8-210">Desencadenador y salida de Queue Storage</span><span class="sxs-lookup"><span data-stu-id="79ed8-210">Queue storage trigger and output</span></span>

<span data-ttu-id="79ed8-211">Azure Functions admite desencadenador y enlaces de salida para Azure Queues.</span><span class="sxs-lookup"><span data-stu-id="79ed8-211">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="79ed8-212">Para más información, consulte [Enlaces de Queue Storage de Azure Functions](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="79ed8-212">For more information, see [Azure Functions Queue Storage bindings](functions-bindings-storage-queue.md).</span></span>

<span data-ttu-id="79ed8-213">Hello en el ejemplo siguiente se muestra la función de hello toouse tipo de valor devuelto con una salida de cola de enlace, el uso de hello `[Queue]` atributo.</span><span class="sxs-lookup"><span data-stu-id="79ed8-213">hello following example shows how toouse hello function return type with a queue output binding, using hello `[Queue]` attribute.</span></span> <span data-ttu-id="79ed8-214">toodefine un desencadenador de cola, usar hello `[QueueTrigger]` atributo.</span><span class="sxs-lookup"><span data-stu-id="79ed8-214">toodefine a queue trigger, use hello `[QueueTrigger]` attribute.</span></span>

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

### <a name="sendgrid-output"></a><span data-ttu-id="79ed8-215">Salida de SendGrid</span><span class="sxs-lookup"><span data-stu-id="79ed8-215">SendGrid output</span></span>

<span data-ttu-id="79ed8-216">Azure Functions admite un enlace de salida de SendGrid para el envío de correo electrónico mediante programación.</span><span class="sxs-lookup"><span data-stu-id="79ed8-216">Azure Functions supports a SendGrid output binding for sending email programmatically.</span></span> <span data-ttu-id="79ed8-217">más información, consulte toolearn [SendGrid de funciones de Azure enlaces](functions-bindings-sendgrid.md).</span><span class="sxs-lookup"><span data-stu-id="79ed8-217">toolearn more, see [Azure Functions SendGrid bindings](functions-bindings-sendgrid.md).</span></span>

<span data-ttu-id="79ed8-218">atributo de Hello `[SendGrid]` se define en el paquete de NuGet hello [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span><span class="sxs-lookup"><span data-stu-id="79ed8-218">hello attribute `[SendGrid]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span></span>

<span data-ttu-id="79ed8-219">Hello siguiente es un ejemplo del uso de un desencadenador de cola de Bus de servicio y un enlace de salida de SendGrid mediante `SendGridMessage`:</span><span class="sxs-lookup"><span data-stu-id="79ed8-219">hello following is an example of using a Service Bus queue trigger and a SendGrid output binding using `SendGridMessage`:</span></span>

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
    public string too{ get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a><span data-ttu-id="79ed8-220">Desencadenador y salida de Service Bus</span><span class="sxs-lookup"><span data-stu-id="79ed8-220">Service Bus trigger and output</span></span>

<span data-ttu-id="79ed8-221">Azure Functions admite enlaces de desencadenador y salida para colas y temas de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="79ed8-221">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span> <span data-ttu-id="79ed8-222">Para más información sobre la configuración de enlaces, consulte [Enlaces de Service Bus de Azure Functions](functions-bindings-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="79ed8-222">For more information on configuring bindings, see [Azure Functions Service Bus bindings](functions-bindings-service-bus.md).</span></span>

<span data-ttu-id="79ed8-223">Hola atributos `[ServiceBusTrigger]` y `[ServiceBus]` se definen en el paquete de NuGet hello [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="79ed8-223">hello attributes `[ServiceBusTrigger]` and `[ServiceBus]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="79ed8-224">Hola te mostramos un ejemplo de un desencadenador de cola de Bus de servicio:</span><span class="sxs-lookup"><span data-stu-id="79ed8-224">hello following is an example of a Service Bus queue trigger:</span></span>

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<span data-ttu-id="79ed8-225">Hola te mostramos un ejemplo de una salida de Bus de servicio de enlace, utilizando el tipo de valor devuelto de método hello como salida de hello:</span><span class="sxs-lookup"><span data-stu-id="79ed8-225">hello following is an example of a Service Bus output binding, using hello method return type as hello output:</span></span>

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

### <a name="table-storage-input-and-output"></a><span data-ttu-id="79ed8-226">Entrada y salida de Table Storage</span><span class="sxs-lookup"><span data-stu-id="79ed8-226">Table storage input and output</span></span>

<span data-ttu-id="79ed8-227">Azure Functions admite enlaces de entrada y salida para Table Storage de Azure.</span><span class="sxs-lookup"><span data-stu-id="79ed8-227">Azure Functions supports input and output bindings for Azure Table storage.</span></span> <span data-ttu-id="79ed8-228">más información, consulte toolearn [enlaces de almacenamiento de tabla de funciones de Azure](functions-bindings-storage-table.md).</span><span class="sxs-lookup"><span data-stu-id="79ed8-228">toolearn more, see [Azure Functions Table storage bindings](functions-bindings-storage-table.md).</span></span>

<span data-ttu-id="79ed8-229">Hello siguiente ejemplo es una clase con dos funciones, que muestra la salida de almacenamiento de tabla y los enlaces de entrada.</span><span class="sxs-lookup"><span data-stu-id="79ed8-229">hello following example is a class with two functions, demonstrating table storage output and input bindings.</span></span> 

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

    // use hello metadata parameter "queueTrigger" toobind hello queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a><span data-ttu-id="79ed8-230">Desencadenador de temporizador</span><span class="sxs-lookup"><span data-stu-id="79ed8-230">Timer trigger</span></span>

<span data-ttu-id="79ed8-231">Azure Functions incluye un enlace a un desencadenador de temporizador que le permite ejecutar su código de función según una programación definida.</span><span class="sxs-lookup"><span data-stu-id="79ed8-231">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> <span data-ttu-id="79ed8-232">toolearn más información acerca de características de hello del enlace de hello, consulte [programar la ejecución del código con las funciones de Azure](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="79ed8-232">toolearn more about hello features of hello binding, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>

<span data-ttu-id="79ed8-233">Plan de consumo de hello, puede definir programaciones con un [expresión CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span><span class="sxs-lookup"><span data-stu-id="79ed8-233">On hello Consumption plan, you can define schedules with a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span></span> <span data-ttu-id="79ed8-234">Si utiliza un plan de App Service, también puede usar una cadena TimeSpan.</span><span class="sxs-lookup"><span data-stu-id="79ed8-234">If you're using an App Service Plan, you can also use a TimeSpan string.</span></span> 

<span data-ttu-id="79ed8-235">Hola de ejemplo siguiente define un desencadenador de temporizador que se ejecuta cada 5 minutos:</span><span class="sxs-lookup"><span data-stu-id="79ed8-235">hello following example defines a timer trigger that runs every 5 minutes:</span></span>

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a><span data-ttu-id="79ed8-236">Salida de Twilio</span><span class="sxs-lookup"><span data-stu-id="79ed8-236">Twilio output</span></span>

<span data-ttu-id="79ed8-237">Azure funciones es compatible con Twilio habían salida enlaces tooenable los mensajes de texto SMS de toosend de funciones.</span><span class="sxs-lookup"><span data-stu-id="79ed8-237">Azure Functions supports Twilio output bindings tooenable your functions toosend SMS text messages.</span></span> <span data-ttu-id="79ed8-238">más información, consulte toolearn [enlace de salida de SMS enviar mensajes desde las funciones de Azure mediante Twilio hello](functions-bindings-twilio.md).</span><span class="sxs-lookup"><span data-stu-id="79ed8-238">toolearn more, see [Send SMS messages from Azure Functions using hello Twilio output binding](functions-bindings-twilio.md).</span></span> 

<span data-ttu-id="79ed8-239">atributo de Hello `[TwilioSms]` se define en el paquete de hello [Microsoft.Azure.WebJobs.Extensions.Twilio].</span><span class="sxs-lookup"><span data-stu-id="79ed8-239">hello attribute `[TwilioSms]` is defined in hello package [Microsoft.Azure.WebJobs.Extensions.Twilio].</span></span>

<span data-ttu-id="79ed8-240">Hello ejemplo C# siguiente utiliza una cola de desencadenador y un Twilio el enlace de salida:</span><span class="sxs-lookup"><span data-stu-id="79ed8-240">hello following C# example uses a queue trigger and a Twilio output binding:</span></span>

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        too= order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a><span data-ttu-id="79ed8-241">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="79ed8-241">Next steps</span></span>

<span data-ttu-id="79ed8-242">Para más información sobre el uso de Azure Functions en C# de scripting, consulte [Referencia para desarrolladores de C\# de script de Azure Functions](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="79ed8-242">For more information on using Azure Functions in C# scripting, see [Azure Functions C\# script developer reference](functions-reference-csharp.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4
[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1


<!-- Links toosource --> 
[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs
[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs
[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs
[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs
[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs 
[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs
[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs
[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs
[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs
[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs
[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs
[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs
[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs
[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs
[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs
[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs
