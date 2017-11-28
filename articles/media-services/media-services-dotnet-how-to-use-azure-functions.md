---
title: aaaDevelop funciones de Azure con servicios multimedia
description: "Este tema muestra cómo desarrollar las funciones de Azure con el uso de servicios multimedia de toostart Hola portal de Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 51bdcb01-1846-4e1f-bd90-70020ab471b0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/21/2017
ms.author: juliako
ms.openlocfilehash: 3b2c2fb498fea399c862dfbdb63033d06cabf6d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="29987-103">Desarrollo de Azure Functions con Media Services</span><span class="sxs-lookup"><span data-stu-id="29987-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="29987-104">Este tema muestra cómo tooget se inicia con la creación de funciones de Azure que usan los servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="29987-104">This topic shows you how tooget started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="29987-105">Hola definido en este tema de función de Azure supervisa un contenedor de la cuenta de almacenamiento denominado **entrada** para los nuevos archivos MP4.</span><span class="sxs-lookup"><span data-stu-id="29987-105">hello Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="29987-106">Una vez que un archivo se coloca en el contenedor de almacenamiento de hello, desencadenador de blob de Hola ejecutará la función hello.</span><span class="sxs-lookup"><span data-stu-id="29987-106">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>

<span data-ttu-id="29987-107">Si desea tooexplore e implementa las funciones de Azure existentes que usan los servicios multimedia de Azure, visite [funciones de Azure Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="29987-107">If you want tooexplore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="29987-108">Este repositorio incluye ejemplos que utilizan los servicios multimedia tooshow flujos de trabajo relacionado tooingesting contenido directamente desde el almacenamiento de blobs, codificación y escribir el contenido nuevo tooblob almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="29987-108">This repository contains examples that use Media Services tooshow workflows related tooingesting content directly from blob storage, encoding, and writing content back tooblob storage.</span></span> <span data-ttu-id="29987-109">También incluye ejemplos de cómo toomonitor trabajo notificaciones a través de las colas de Azure y Webhook.</span><span class="sxs-lookup"><span data-stu-id="29987-109">It also includes examples of how toomonitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="29987-110">También puede desarrollar sus funciones basadas en los ejemplos de hello en hello [funciones de Azure Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repositorio.</span><span class="sxs-lookup"><span data-stu-id="29987-110">You can also develop your Functions based on hello examples in hello [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="29987-111">funciones de hello toodeploy, presione hello **implementar tooAzure** botón.</span><span class="sxs-lookup"><span data-stu-id="29987-111">toodeploy hello functions, press hello **Deploy tooAzure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29987-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="29987-112">Prerequisites</span></span>

- <span data-ttu-id="29987-113">Antes de crear la primera función, deberá toohave una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="29987-113">Before you can create your first function, you need toohave an active Azure account.</span></span> <span data-ttu-id="29987-114">Si aún no tiene una cuenta de Azure, [tiene a su disposición la creación de una cuenta gratis](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="29987-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="29987-115">Si va toocreate Azure funciones que realizan acciones en su cuenta de servicios de multimedia de Azure (AMS) o escuchar tooevents enviados por los servicios multimedia, debe crear una cuenta de AMS, tal como se describe [aquí](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="29987-115">If you are going toocreate Azure Functions that perform actions on your Azure Media Services (AMS) account or listen tooevents sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="29987-116">Descripción de [cómo toouse Azure funciones](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="29987-116">Understanding of [how toouse Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="29987-117">Además, revise lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="29987-117">Also, review:</span></span>
    - [<span data-ttu-id="29987-118">Enlaces HTTP y webhook en Azure Functions</span><span class="sxs-lookup"><span data-stu-id="29987-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="29987-119">¿Cómo tooconfigure configuración de la aplicación de Azure (función)</span><span class="sxs-lookup"><span data-stu-id="29987-119">How tooconfigure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="29987-120">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="29987-120">Considerations</span></span>

-  <span data-ttu-id="29987-121">Las funciones de Azure ejecutando bajo el plan de consumo de hello tengan tiempo de espera de 5 minutos limitar.</span><span class="sxs-lookup"><span data-stu-id="29987-121">Azure Functions running under hello Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="29987-122">Creación de una aplicación de función</span><span class="sxs-lookup"><span data-stu-id="29987-122">Create a function app</span></span>

1. <span data-ttu-id="29987-123">Vaya toohello [portal de Azure](http://portal.azure.com) e inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="29987-123">Go toohello [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="29987-124">Cree una aplicación de función como se describe [aquí](../azure-functions/functions-create-function-app-portal.md).</span><span class="sxs-lookup"><span data-stu-id="29987-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="29987-125">Una cuenta de almacenamiento que especifique en hello **StorageConnection** (vea el paso siguiente de hello) debe ser la variable de entorno en hello misma región que la aplicación.</span><span class="sxs-lookup"><span data-stu-id="29987-125">A storage account that you specify in hello **StorageConnection** environment variable (see hello next step) should be in hello same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="29987-126">Configuración de la aplicación de función</span><span class="sxs-lookup"><span data-stu-id="29987-126">Configure function app settings</span></span>

<span data-ttu-id="29987-127">Cuando desarrolle las funciones de servicios multimedia, resulta práctica tooadd variables de entorno que se utilizará a lo largo de las funciones.</span><span class="sxs-lookup"><span data-stu-id="29987-127">When developing Media Services functions, it is handy tooadd environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="29987-128">tooconfigure configuración de la aplicación, haga clic en el vínculo de configuración de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="29987-128">tooconfigure app settings, click hello Configure App Settings link.</span></span> <span data-ttu-id="29987-129">Para obtener más información, consulte [la configuración de la aplicación Azure función tooconfigure](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="29987-129">For more information, see  [How tooconfigure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="29987-130">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="29987-130">For example:</span></span>

![Settings](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="29987-132">función Hello, definida en este artículo, se supone que tiene Hola después de las variables de entorno en la configuración de aplicación:</span><span class="sxs-lookup"><span data-stu-id="29987-132">hello function, defined in this article, assumes you have hello following environment variables in your app settings:</span></span>

<span data-ttu-id="29987-133">**AMSAccount**: *nombre de la cuenta de AMS* (p. ej., testams)</span><span class="sxs-lookup"><span data-stu-id="29987-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="29987-134">**AMSKey**: *clave de la cuenta de AMS* (p. ej., IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span><span class="sxs-lookup"><span data-stu-id="29987-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="29987-135">**MediaServicesStorageAccountName**: *nombre de la cuenta de almacenamiento* (p. ej., testamsstorage)</span><span class="sxs-lookup"><span data-stu-id="29987-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="29987-136">**MediaServicesStorageAccountKey**: *clave de cuenta de almacenamiento* (p. ej., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span><span class="sxs-lookup"><span data-stu-id="29987-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="29987-137">**StorageConnection**: *conexión de almacenamiento* (p. ej., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span><span class="sxs-lookup"><span data-stu-id="29987-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="29987-138">Creación de una función</span><span class="sxs-lookup"><span data-stu-id="29987-138">Create a function</span></span>

<span data-ttu-id="29987-139">Una vez implementada su instancia de Function App, puede encontrarla entre Azure Functions de **App Services**.</span><span class="sxs-lookup"><span data-stu-id="29987-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="29987-140">Seleccione la aplicación de función y haga clic en **Nueva función**.</span><span class="sxs-lookup"><span data-stu-id="29987-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="29987-141">Elija hello **C#** lenguaje y **procesamiento de datos** escenario.</span><span class="sxs-lookup"><span data-stu-id="29987-141">Choose hello **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="29987-142">Elija la plantilla **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="29987-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="29987-143">Esta función se desencadenará cada vez que se carga un blob en hello **entrada** contenedor.</span><span class="sxs-lookup"><span data-stu-id="29987-143">This function will be triggered whenever a blob is uploaded into hello **input** container.</span></span> <span data-ttu-id="29987-144">Hola **entrada** nombre se especifica en hello **ruta de acceso**, en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="29987-144">hello **input** name is specified in hello **Path**, in hello next step.</span></span>

    ![files](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="29987-146">Una vez que seleccione **BlobTrigger**, algunos controles más aparecerá en la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="29987-146">Once you select **BlobTrigger**, some more controls will appear on hello page.</span></span>

    ![files](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="29987-148">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="29987-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="29987-149">Archivos</span><span class="sxs-lookup"><span data-stu-id="29987-149">Files</span></span>

<span data-ttu-id="29987-150">La función de Azure está asociada a archivos de código y otros archivos que se describen en esta sección.</span><span class="sxs-lookup"><span data-stu-id="29987-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="29987-151">De forma predeterminada, una función está asociada con los archivos **function.json** y **run.csx** (C#).</span><span class="sxs-lookup"><span data-stu-id="29987-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="29987-152">Deberá tooadd un **project.json** archivo.</span><span class="sxs-lookup"><span data-stu-id="29987-152">You will need tooadd a **project.json** file.</span></span> <span data-ttu-id="29987-153">resto de Hola de esta sección muestra las definiciones de Hola para estos archivos.</span><span class="sxs-lookup"><span data-stu-id="29987-153">hello rest of this section shows hello definitions for these files.</span></span>

![files](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="29987-155">function.json</span><span class="sxs-lookup"><span data-stu-id="29987-155">function.json</span></span>

<span data-ttu-id="29987-156">archivo de Hello function.json define los enlaces de función hello y otras opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="29987-156">hello function.json file defines hello function bindings and other configuration settings.</span></span> <span data-ttu-id="29987-157">Hola en tiempo de ejecución utiliza este toomonitor de eventos de archivo toodetermine hello y toopass y devolución de datos de funcionamiento de ejecución.</span><span class="sxs-lookup"><span data-stu-id="29987-157">hello runtime uses this file toodetermine hello events toomonitor and how toopass data into and return data from function execution.</span></span> <span data-ttu-id="29987-158">Para obtener más información, consulte [Enlaces HTTP y webhook en Azure Functions](../azure-functions/functions-reference.md#function-code).</span><span class="sxs-lookup"><span data-stu-id="29987-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="29987-159">Conjunto hello **deshabilitado** propiedad demasiado**true** función de hello tooprevent desde que se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="29987-159">Set hello **disabled** property too**true** tooprevent hello function from being executed.</span></span> 


<span data-ttu-id="29987-160">Este es un ejemplo de archivo **function.json**.</span><span class="sxs-lookup"><span data-stu-id="29987-160">Here is an example of **function.json** file.</span></span>

    {
    "bindings": [
      {
        "name": "myBlob",
        "type": "blobTrigger",
        "direction": "in",
        "path": "input/{fileName}.mp4",
        "connection": "StorageConnection"
      }
    ],
    "disabled": false
    }

### <a name="projectjson"></a><span data-ttu-id="29987-161">project.json</span><span class="sxs-lookup"><span data-stu-id="29987-161">project.json</span></span>

<span data-ttu-id="29987-162">archivo project.json de Hello contiene dependencias.</span><span class="sxs-lookup"><span data-stu-id="29987-162">hello project.json file contains dependencies.</span></span> <span data-ttu-id="29987-163">Este es un ejemplo de **project.json** archivo que incluye servicios de multimedia de Azure de hello requerido .NET paquetes de Nuget.</span><span class="sxs-lookup"><span data-stu-id="29987-163">Here is an example of **project.json** file that includes hello required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="29987-164">Tenga en cuenta que los números de versión de Hola cambiará con las últimas actualizaciones toohello paquetes, por lo que debe confirmar versiones más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="29987-164">Note that hello version numbers will change with latest updates toohello packages, so you should confirm hello most recent versions.</span></span> 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a><span data-ttu-id="29987-165">run.csx</span><span class="sxs-lookup"><span data-stu-id="29987-165">run.csx</span></span>

<span data-ttu-id="29987-166">Se trata de código C# hello para la función.</span><span class="sxs-lookup"><span data-stu-id="29987-166">This is hello C# code for your function.</span></span>  <span data-ttu-id="29987-167">función Hello define a continuación de monitores de un contenedor de la cuenta de almacenamiento denominado **entrada** (que es lo que se especificó en la ruta de acceso de hello) para los nuevos archivos MP4.</span><span class="sxs-lookup"><span data-stu-id="29987-167">hello function defined below monitors a storage account container named **input** (that is what was specified in hello path) for new MP4 files.</span></span> <span data-ttu-id="29987-168">Una vez que un archivo se coloca en el contenedor de almacenamiento de hello, desencadenador de blob de Hola ejecutará la función hello.</span><span class="sxs-lookup"><span data-stu-id="29987-168">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>
    
<span data-ttu-id="29987-169">ejemplo de Hola definido en esta sección se muestra</span><span class="sxs-lookup"><span data-stu-id="29987-169">hello example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="29987-170">la cuenta de tooingest un activo en los servicios multimedia (a copiar un blob en un recurso de AMS) y</span><span class="sxs-lookup"><span data-stu-id="29987-170">how tooingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="29987-171">¿Cómo toosubmit un trabajo de codificación que usa "Transmisión por secuencias adaptativa" Media Encoder estándar preestablecido.</span><span class="sxs-lookup"><span data-stu-id="29987-171">how toosubmit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="29987-172">En el escenario de uso real de hello, lo más probable es que desee tootrack progreso del trabajo y, a continuación, publica el activo codificado.</span><span class="sxs-lookup"><span data-stu-id="29987-172">In hello real life scenario, you most likely want tootrack job progress and then publish your encoded asset.</span></span> <span data-ttu-id="29987-173">Para obtener más información, consulte [notificaciones de trabajo de servicios multimedia de uso Azure WebHooks toomonitor](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="29987-173">For more information, see [Use Azure WebHooks toomonitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="29987-174">Para obtener más ejemplos, consulte [Azure Functions de Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="29987-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="29987-175">Una vez que haya terminado de definir la función, haga clic en **Guardar y ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="29987-175">Once you are done defining your function click **Save and Run**.</span></span>

    #r "Microsoft.WindowsAzure.Storage"
    #r "Newtonsoft.Json"
    #r "System.Web"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Net;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Auth;

    private static readonly string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    private static readonly string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static string _storageAccountName = Environment.GetEnvironmentVariable("MediaServicesStorageAccountName");
    static string _storageAccountKey = Environment.GetEnvironmentVariable("MediaServicesStorageAccountKey");

    private static CloudStorageAccount _destinationStorageAccount = null;

    // Field for service context.
    private static CloudMediaContext _context = null;
    private static MediaServicesCredentials _cachedCredentials = null;

    public static void Run(CloudBlockBlob myBlob, string fileName, TraceWriter log)
    {
        // NOTE that hello variables {fileName} here come from hello path setting in function.json
        // and are passed into hello  Run method signature above. We can use this toomake decisions on what type of file
        // was dropped into hello input container for hello function. 

        // No need toodo any Retry strategy in this function, By default, hello SDK calls a function up too5 times for a 
        // given blob. If hello fifth try fails, hello SDK adds a message tooa queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used hello chached credentials toocreate CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy hello Blob into a new Input Asset for hello Job
        // ***NOTE: Ideally we would have a method tooingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with hello Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with hello encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify hello input asset toobe encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset toocontain hello results of hello job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means hello output asset is not encrypted. 
        task.OutputAssets.AddNew(fileName, AssetCreationOptions.None);

        job.Submit();
        log.Info("Job Submitted");

        }
        catch (Exception ex)
        {
        log.Error("ERROR: failed.");
        log.Info($"StackTrace : {ex.StackTrace}");
        throw ex;
        }
    }

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


    public static async Task<IAsset> CreateAssetFromBlob(CloudBlockBlob blob, string assetName, TraceWriter log){
        IAsset newAsset = null;

        try{
            Task<IAsset> copyAssetTask = CreateAssetFromBlobAsync(blob, assetName, log);
            newAsset = await copyAssetTask;
            log.Info($"Asset Copied : {newAsset.Id}");
        }
        catch(Exception ex){
            log.Info("Copy Failed");
            log.Info($"ERROR : {ex.Message}");
            throw ex;
        }

        return newAsset;
    }

    /// <summary>
    /// Creates a new asset and copies blobs from hello specifed storage account.
    /// </summary>
    /// <param name="blob">hello specified blob.</param>
    /// <returns>hello new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference toohello storage account that is associated with hello Media Services account. 
        StorageCredentials mediaServicesStorageCredentials =
        new StorageCredentials(_storageAccountName, _storageAccountKey);
        _destinationStorageAccount = new CloudStorageAccount(mediaServicesStorageCredentials, false);

        // Create a new asset. 
        var asset = _context.Assets.Create(blob.Name, AssetCreationOptions.None);
        log.Info($"Created new asset {asset.Name}");

        IAccessPolicy writePolicy = _context.AccessPolicies.Create("writePolicy",
        TimeSpan.FromHours(4), AccessPermissions.Write);
        ILocator destinationLocator = _context.Locators.CreateLocator(LocatorType.Sas, asset, writePolicy);
        CloudBlobClient destBlobStorage = _destinationStorageAccount.CreateCloudBlobClient();

        // Get hello destination asset container reference
        string destinationContainerName = (new Uri(destinationLocator.Path)).Segments[1];
        CloudBlobContainer assetContainer = destBlobStorage.GetContainerReference(destinationContainerName);

        try{
        assetContainer.CreateIfNotExists();
        }
        catch (Exception ex)
        {
        log.Error ("ERROR:" + ex.Message);
        }

        log.Info("Created asset.");

        // Get hold of hello destination blob
        CloudBlockBlob destinationBlob = assetContainer.GetBlockBlobReference(blob.Name);

        // Copy Blob
        try
        {
        using (var stream = await blob.OpenReadAsync()) 
        {            
            await destinationBlob.UploadFromStreamAsync(stream);          
        }

        log.Info("Copy Complete.");

        var assetFile = asset.AssetFiles.Create(blob.Name);
        assetFile.ContentFileSize = blob.Properties.Length;
        assetFile.IsPrimary = true;
        assetFile.Update();
        asset.Update();
        }
        catch (Exception ex)
        {
        log.Error(ex.Message);
        log.Info (ex.StackTrace);
        log.Info ("Copy Failed.");
        throw;
        }

        destinationLocator.Delete();
        writePolicy.Delete();

        return asset;
    }
##<a name="test-your-function"></a><span data-ttu-id="29987-176">Probar la función</span><span class="sxs-lookup"><span data-stu-id="29987-176">Test your function</span></span>

<span data-ttu-id="29987-177">tootest la función, deberá tooupload un archivo MP4 en hello **entrada** contenedor de cuenta de almacenamiento de Hola que especificó en la cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="29987-177">tootest your function, you need tooupload an MP4 file into hello **input** container of hello storage account that you specified in hello connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="29987-178">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="29987-178">Next step</span></span>

<span data-ttu-id="29987-179">En este punto, está listo toostart desarrollar una aplicación de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="29987-179">At this point, you are ready toostart developing a Media Services application.</span></span> 
 
<span data-ttu-id="29987-180">Para obtener más detalles y ejemplos/soluciones completas del uso de funciones de Azure y las aplicaciones lógicas con flujos de trabajo de creación de contenido personalizado de toocreate de servicios multimedia de Azure, vea hello [ejemplo de integración de Media Services .NET funciones en GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span><span class="sxs-lookup"><span data-stu-id="29987-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services toocreate custom content creation workflows, see hello [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="29987-181">Consulte también [notificaciones con .NET de trabajo de servicios multimedia de uso Azure WebHooks toomonitor](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="29987-181">Also, see [Use Azure WebHooks toomonitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="29987-182">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="29987-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="29987-183">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="29987-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

