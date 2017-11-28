---
title: "Administración de recursos de Media Services entre varias cuentas de almacenamiento | Microsoft Docs"
description: "En este artículo se dan instrucciones sobre cómo administrar recursos de servicios de multimedia en varias cuentas de almacenamiento."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4e4a9ec3-8ddb-4938-aec1-d7172d3db858
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 0b407c3b092fd2c706775154cee3164a9869315a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="managing-media-services-assets-across-multiple-storage-accounts"></a><span data-ttu-id="8a922-103">Administración de recursos de Servicios multimedia entre varias cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8a922-103">Managing Media Services Assets across Multiple Storage Accounts</span></span>
<span data-ttu-id="8a922-104">A partir de Servicios multimedia de Microsoft Azure  2.2, puede asociar varias cuentas de almacenamiento a una sola cuenta de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="8a922-104">Starting with Microsoft Azure Media Services 2.2, you can attach multiple storage accounts to a single Media Services account.</span></span> <span data-ttu-id="8a922-105">La capacidad de asociar varias cuentas de almacenamiento a una cuenta de Servicios multimedia ofrece las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8a922-105">Ability to attach multiple storage accounts to a Media Services account provides the following benefits:</span></span>

* <span data-ttu-id="8a922-106">Equilibrio de carga de sus activos entre varias cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8a922-106">Load balancing your assets across multiple storage accounts.</span></span>
* <span data-ttu-id="8a922-107">Escalado de Servicios multimedia para grandes cantidades de procesamiento de contenido (ya que actualmente una única cuenta de almacenamiento tiene un límite máximo de 500 TB).</span><span class="sxs-lookup"><span data-stu-id="8a922-107">Scaling Media Services for large amounts of content processing (as currently a single storage account has a max limit of 500 TB).</span></span> 

<span data-ttu-id="8a922-108">En este tema se muestra cómo asociar varias cuentas de almacenamiento a una cuenta de Media Services mediante [API de Azure Resource Manager](https://docs.microsoft.com/rest/api/media/mediaservice) y [PowerShell](/powershell/module/azurerm.media).</span><span class="sxs-lookup"><span data-stu-id="8a922-108">This topic demonstrates how to attach multiple storage accounts to a Media Services account using [Azure Resource Manager APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](/powershell/module/azurerm.media).</span></span> <span data-ttu-id="8a922-109">También muestra cómo especificar diferentes cuentas de almacenamiento al crear activos mediante el SDK de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="8a922-109">It also shows how to specify different storage accounts when creating assets using the Media Services SDK.</span></span> 

## <a name="considerations"></a><span data-ttu-id="8a922-110">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="8a922-110">Considerations</span></span>
<span data-ttu-id="8a922-111">Al asociar varias cuentas de almacenamiento a su cuenta de Servicios multimedia, se aplican las siguientes consideraciones:</span><span class="sxs-lookup"><span data-stu-id="8a922-111">When attaching multiple storage accounts to your Media Services account, the following considerations apply:</span></span>

* <span data-ttu-id="8a922-112">Todas las cuentas de almacenamiento asociadas a una cuenta de Servicios multimedia deben estar en el mismo centro de datos que la cuenta de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="8a922-112">All storage accounts attached to a Media Services account must be in the same data center as the Media Services account.</span></span>
* <span data-ttu-id="8a922-113">Actualmente, cuando se asocia una cuenta de almacenamiento a la cuenta especificada de Servicios multimedia, no se puede desasociar.</span><span class="sxs-lookup"><span data-stu-id="8a922-113">Currently, once a storage account is attached to the specified Media Services account, it cannot be detached.</span></span>
* <span data-ttu-id="8a922-114">La cuenta de almacenamiento principal es la indicada durante el tiempo de creación de cuenta de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="8a922-114">Primary storage account is the one indicated during Media Services account creation time.</span></span> <span data-ttu-id="8a922-115">Actualmente, no puede cambiar la cuenta de almacenamiento predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8a922-115">Currently, you cannot change the default storage account.</span></span> 
* <span data-ttu-id="8a922-116">Actualmente, si desea agregar una cuenta de almacenamiento de acceso esporádico a la cuenta de AMS, la cuenta de almacenamiento debe ser de tipo Blob y no estar establecida como principal.</span><span class="sxs-lookup"><span data-stu-id="8a922-116">Currently, if you want to add a Cool Storage account to the AMS account, the storage account must be a Blob type and set to non-primary.</span></span>

<span data-ttu-id="8a922-117">Otras consideraciones:</span><span class="sxs-lookup"><span data-stu-id="8a922-117">Other considerations:</span></span>

<span data-ttu-id="8a922-118">Los Media Services usan el valor de la propiedad **IAssetFile.Name** al generar direcciones URL para el contenido de streaming (por ejemplo, http://{WAMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esta razón, no se permite la codificación porcentual.</span><span class="sxs-lookup"><span data-stu-id="8a922-118">Media Services uses the value of the **IAssetFile.Name** property when building URLs for the streaming content (for example, http://{WAMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="8a922-119">El valor de la propiedad Name no puede tener ninguno de los siguientes [caracteres reservados para la codificación porcentual](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span><span class="sxs-lookup"><span data-stu-id="8a922-119">The value of the Name property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="8a922-120">Además, solo puede haber un "."</span><span class="sxs-lookup"><span data-stu-id="8a922-120">Also, there can only be one ‘.’</span></span> <span data-ttu-id="8a922-121">Además, solo puede haber un '.' para la extensión del nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="8a922-121">for the file name extension.</span></span>

## <a name="to-attach-storage-accounts"></a><span data-ttu-id="8a922-122">Para asociar cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8a922-122">To attach storage accounts</span></span>  

<span data-ttu-id="8a922-123">Para asociar cuentas de almacenamiento a su cuenta de AMS, use [API de Azure Resource Manager](https://docs.microsoft.com/rest/api/media/mediaservice) y [PowerShell](/powershell/module/azurerm.media), como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="8a922-123">To attach storage accounts to your AMS account, use [Azure Resource Manager APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](/powershell/module/azurerm.media), as shown in the following example.</span></span>

    $regionName = "West US"
    $subscriptionId = " xxxxxxxx-xxxx-xxxx-xxxx- xxxxxxxxxxxx "
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccount1Name = "skystorage1"
    $storageAccount2Name = "skystorage2"
    $storageAccount1Id = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccount1Name"
    $storageAccount2Id = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccount2Name"
    $storageAccount1 = New-AzureRmMediaServiceStorageConfig -StorageAccountId $storageAccount1Id -IsPrimary
    $storageAccount2 = New-AzureRmMediaServiceStorageConfig -StorageAccountId $storageAccount2Id
    $storageAccounts = @($storageAccount1, $storageAccount2)
    
    Set-AzureRmMediaService -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccounts $storageAccounts

### <a name="support-for-cool-storage"></a><span data-ttu-id="8a922-124">Compatibilidad con el almacenamiento de acceso esporádico</span><span class="sxs-lookup"><span data-stu-id="8a922-124">Support for Cool Storage</span></span>

<span data-ttu-id="8a922-125">Actualmente, si desea agregar una cuenta de almacenamiento de acceso esporádico a la cuenta de AMS, la cuenta de almacenamiento debe ser de tipo Blob y no estar establecida como principal.</span><span class="sxs-lookup"><span data-stu-id="8a922-125">Currently, if you want to add a Cool Storage account to the AMS account, the storage account must be a Blob type and set to non-primary.</span></span>

## <a name="to-manage-media-services-assets-across-multiple-storage-accounts"></a><span data-ttu-id="8a922-126">Para administrar los recursos de Servicios multimedia entre varias cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8a922-126">To manage Media Services assets across multiple Storage Accounts</span></span>
<span data-ttu-id="8a922-127">El código siguiente usa el último SDK de Servicios multimedia para realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="8a922-127">The following code uses the latest Media Services SDK to perform the following tasks:</span></span>

1. <span data-ttu-id="8a922-128">Muestre todas las cuentas de almacenamiento asociadas a la cuenta de Servicios multimedia especificada.</span><span class="sxs-lookup"><span data-stu-id="8a922-128">Display all the storage accounts associated with the specified Media Services account.</span></span>
2. <span data-ttu-id="8a922-129">Recupere el nombre de la cuenta de almacenamiento predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8a922-129">Retrieve the name of the default storage account.</span></span>
3. <span data-ttu-id="8a922-130">Cree un nuevo recurso en la cuenta de almacenamiento predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8a922-130">Create a new asset in the default storage account.</span></span>
4. <span data-ttu-id="8a922-131">Cree un recurso de salida del trabajo de codificación en la cuenta de almacenamiento especificada.</span><span class="sxs-lookup"><span data-stu-id="8a922-131">Create an output asset of the encoding job in the specified storage account.</span></span>
   
```
using Microsoft.WindowsAzure.MediaServices.Client;
using System;
using System.Collections.Generic;
using System.Configuration;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;

namespace MultipleStorageAccounts
{
    class Program
    {
        // Location of the media file that you want to encode. 
        private static readonly string _singleInputFilePath =
            Path.GetFullPath(@"../..\supportFiles\multifile\interview2.wmv");

        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Display the storage accounts associated with 
            // the specified Media Services account:
            foreach (var sa in _context.StorageAccounts)
                Console.WriteLine(sa.Name);

            // Retrieve the name of the default storage account.
            var defaultStorageName = _context.StorageAccounts.Where(s => s.IsDefault == true).FirstOrDefault();
            Console.WriteLine("Name: {0}", defaultStorageName.Name);
            Console.WriteLine("IsDefault: {0}", defaultStorageName.IsDefault);

            // Retrieve the name of a storage account that is not the default one.
            var notDefaultStroageName = _context.StorageAccounts.Where(s => s.IsDefault == false).FirstOrDefault();
            Console.WriteLine("Name: {0}", notDefaultStroageName.Name);
            Console.WriteLine("IsDefault: {0}", notDefaultStroageName.IsDefault);

            // Create the original asset in the default storage account.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.None,
                defaultStorageName.Name, _singleInputFilePath);
            Console.WriteLine("Created the asset in the {0} storage account", asset.StorageAccountName);

            // Create an output asset of the encoding job in the other storage account.
            IAsset outputAsset = CreateEncodingJob(asset, notDefaultStroageName.Name, _singleInputFilePath);
            if (outputAsset != null)
                Console.WriteLine("Created the output asset in the {0} storage account", outputAsset.StorageAccountName);

        }

        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string storageName, string singleFilePath)
        {
            var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();

            // If you are creating an asset in the default storage account, you can omit the StorageName parameter.
            var asset = _context.Assets.Create(assetName, storageName, assetCreationOptions);

            var fileName = Path.GetFileName(singleFilePath);

            var assetFile = asset.AssetFiles.Create(fileName);

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);

            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return asset;
        }

        static IAsset CreateEncodingJob(IAsset asset, string storageName, string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My encoding job");
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.ProtectedConfiguration);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset", storageName,
                AssetCreationOptions.None);

            // Use the following event handler to check job progress.  
            job.StateChanged += new
                    EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch the job.
            job.Submit();

            // Check job execution and wait for job to finish. 
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
            progressJobTask.Wait();

            // Get an updated job reference.
            job = GetJob(job.Id);

            // If job state is Error the event handling 
            // method for job progress should log errors.  Here we check 
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
                Console.WriteLine("\nExiting method due to job error.");
                return null;
            }

            // Get a reference to the output asset from the job.
            IAsset outputAsset = job.OutputMediaAssets[0];

            return outputAsset;
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        private static void StateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);

            switch (e.CurrentState)
            {
                case JobState.Finished:
                    Console.WriteLine();
                    Console.WriteLine("********************");
                    Console.WriteLine("Job is finished.");
                    Console.WriteLine("Please wait while local tasks or downloads complete...");
                    Console.WriteLine("********************");
                    Console.WriteLine();
                    Console.WriteLine();
                    break;
                case JobState.Canceling:
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    Console.WriteLine("Please wait...\n");
                    break;
                case JobState.Canceled:
                case JobState.Error:
                    // Cast sender as a job.
                    IJob job = (IJob)sender;
                    // Display or log error details as needed.
                    Console.WriteLine("An error occurred in {0}", job.Id);
                    break;
                default:
                    break;
            }
        }

        static IJob GetJob(string jobId)
        {
            // Use a Linq select query to get an updated 
            // reference by Id. 
            var jobInstance =
                from j in _context.Jobs
                where j.Id == jobId
                select j;
            // Return the job reference as an Ijob. 
            IJob job = jobInstance.FirstOrDefault();

            return job;
        }
    }
}
```

## <a name="media-services-learning-paths"></a><span data-ttu-id="8a922-132">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="8a922-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8a922-133">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="8a922-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

