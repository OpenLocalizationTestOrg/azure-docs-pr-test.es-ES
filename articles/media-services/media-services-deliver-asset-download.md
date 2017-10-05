---
title: Descarga de recursos de Media Services en el equipo - Azure | Microsoft Docs
description: "Aprenda a descargar recursos en el equipo. Los ejemplos de código están escritos en C# y utilizan el SDK de Servicios multimedia para .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 8908a1dd-3ffb-4f18-955d-4c8e2d82fc5d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: d8e740e969f68c85842f42c109328423da1b4414
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-deliver-an-asset-by-download"></a><span data-ttu-id="d558a-104">Entrega de un recurso mediante descarga</span><span class="sxs-lookup"><span data-stu-id="d558a-104">How to: Deliver an Asset by Download</span></span>
<span data-ttu-id="d558a-105">En este tema se analizan las opciones para entregar recursos multimedia cargados en Media Services.</span><span class="sxs-lookup"><span data-stu-id="d558a-105">This topic discusses options for delivering media assets uploaded to Media Services.</span></span> <span data-ttu-id="d558a-106">Puede entregar contenido de los Servicios multimedia en diversos escenarios de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d558a-106">You can deliver Media Services content in numerous application scenarios.</span></span> <span data-ttu-id="d558a-107">Puede descargar recursos multimedia o tener acceso a ellos mediante un localizador.</span><span class="sxs-lookup"><span data-stu-id="d558a-107">You can download media assets, or access them by using a locator.</span></span> <span data-ttu-id="d558a-108">Puede enviar contenido multimedia a otra aplicación o a otro proveedor de contenido.</span><span class="sxs-lookup"><span data-stu-id="d558a-108">You can send media content to another application or to another content provider.</span></span> <span data-ttu-id="d558a-109">Para mejorar el rendimiento y la escalabilidad, también puede entregar contenido si utiliza una Red de entrega de contenido (CDN).</span><span class="sxs-lookup"><span data-stu-id="d558a-109">For improved performance and scalability, you can also deliver content by using a Content Delivery Network (CDN).</span></span>

<span data-ttu-id="d558a-110">En este ejemplo se muestra cómo descargar recursos multimedia desde los Servicios multimedia en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="d558a-110">This example shows how to download media assets from Media Services to your local computer.</span></span> <span data-ttu-id="d558a-111">El código consulta los trabajos asociados con la cuenta de Servicios multimedia por identificador de trabajo y tiene acceso a su colección **OutputMediaAssets** (que es el conjunto de uno o más recursos multimedia de salida que resultan de la ejecución de un trabajo).</span><span class="sxs-lookup"><span data-stu-id="d558a-111">The code queries the jobs associated with the Media Services account by job ID and accesses its **OutputMediaAssets** collection (which is the set of one or more output media assets that results from running a job).</span></span> <span data-ttu-id="d558a-112">Este ejemplo muestra cómo descargar recursos multimedia de salida desde un trabajo, pero puede aplicar el mismo enfoque para descargar otros recursos.</span><span class="sxs-lookup"><span data-stu-id="d558a-112">This  example shows how to download output media assets from a job, but you can apply the same approach to download other assets.</span></span>

>[!NOTE]
><span data-ttu-id="d558a-113">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="d558a-113">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="d558a-114">Debe usar el mismo identificador de directiva si siempre usa los mismos permisos de acceso y días, por ejemplo, directivas para localizadores que vayan a aplicarse durante mucho tiempo (directivas distintas a carga).</span><span class="sxs-lookup"><span data-stu-id="d558a-114">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="d558a-115">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="d558a-115">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    // Download the output asset of the specified job to a local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how to download a single asset. 
        // However, you can iterate through the OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference to the job. 
        IJob job = GetJob(jobId);

        // Get a reference to the first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator to download the asset
        IAccessPolicy accessPolicy = _context.AccessPolicies.Create("File Download Policy", TimeSpan.FromDays(30), AccessPermissions.Read);
        ILocator locator = _context.Locators.CreateLocator(LocatorType.Sas, outputAsset, accessPolicy);

        BlobTransferClient blobTransfer = new BlobTransferClient
        {
            NumberOfConcurrentTransfers = 20,
            ParallelTransferThreadCount = 20
        };

        var downloadTasks = new List<Task>();
        foreach (IAssetFile outputFile in outputAsset.AssetFiles)
        {
            // Use the following event handler to check download progress.
            outputFile.DownloadProgressChanged += DownloadProgress;

            string localDownloadPath = Path.Combine(outputFolder, outputFile.Name);

            Console.WriteLine("File download path:  " + localDownloadPath);

            downloadTasks.Add(outputFile.DownloadAsync(Path.GetFullPath(localDownloadPath), blobTransfer, locator, CancellationToken.None));

            outputFile.DownloadProgressChanged -= DownloadProgress;
        }

        Task.WaitAll(downloadTasks.ToArray());

        return outputAsset;
    }

    static void DownloadProgress(object sender, DownloadProgressChangedEventArgs e)
    {
        Console.WriteLine(string.Format("{0} % download progress. ", e.Progress));
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="d558a-116">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="d558a-116">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d558a-117">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="d558a-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="d558a-118">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="d558a-118">See Also</span></span>
[<span data-ttu-id="d558a-119">contenido por secuencias</span><span class="sxs-lookup"><span data-stu-id="d558a-119">Deliver streaming content</span></span>](media-services-deliver-streaming-content.md)

