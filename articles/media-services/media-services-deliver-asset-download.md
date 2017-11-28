---
title: equipo de tooyour de activos de servicios multimedia aaaDownload - Azure | Documentos de Microsoft
description: "Obtenga información sobre el equipo de tooyour de toodownload activos. Ejemplos de código están escritos en C# y usar hello SDK de servicios multimedia para. NET."
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
ms.openlocfilehash: 6c6e764720caa59d8371178a2682700345f7bc57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-deliver-an-asset-by-download"></a><span data-ttu-id="44648-104">Entrega de un recurso mediante descarga</span><span class="sxs-lookup"><span data-stu-id="44648-104">How to: Deliver an Asset by Download</span></span>
<span data-ttu-id="44648-105">Este tema describe las opciones de entrega de activos multimedia había cargado tooMedia servicios.</span><span class="sxs-lookup"><span data-stu-id="44648-105">This topic discusses options for delivering media assets uploaded tooMedia Services.</span></span> <span data-ttu-id="44648-106">Puede entregar contenido de los Servicios multimedia en diversos escenarios de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="44648-106">You can deliver Media Services content in numerous application scenarios.</span></span> <span data-ttu-id="44648-107">Puede descargar recursos multimedia o tener acceso a ellos mediante un localizador.</span><span class="sxs-lookup"><span data-stu-id="44648-107">You can download media assets, or access them by using a locator.</span></span> <span data-ttu-id="44648-108">Puede enviar la aplicación de tooanother contenido multimedia o el proveedor de contenido de tooanother.</span><span class="sxs-lookup"><span data-stu-id="44648-108">You can send media content tooanother application or tooanother content provider.</span></span> <span data-ttu-id="44648-109">Para mejorar el rendimiento y la escalabilidad, también puede entregar contenido si utiliza una Red de entrega de contenido (CDN).</span><span class="sxs-lookup"><span data-stu-id="44648-109">For improved performance and scalability, you can also deliver content by using a Content Delivery Network (CDN).</span></span>

<span data-ttu-id="44648-110">Este ejemplo se muestra cómo los activos de medios de toodownload desde el equipo local de servicios multimedia tooyour.</span><span class="sxs-lookup"><span data-stu-id="44648-110">This example shows how toodownload media assets from Media Services tooyour local computer.</span></span> <span data-ttu-id="44648-111">las consultas de código Hola Hola trabajos asociados con la cuenta de servicios multimedia de Hola por Id. de trabajo y tiene acceso a su **OutputMediaAssets** colección (que es el conjunto de Hola de uno o varios recursos de medios de salida que se obtiene al ejecutar un trabajo).</span><span class="sxs-lookup"><span data-stu-id="44648-111">hello code queries hello jobs associated with hello Media Services account by job ID and accesses its **OutputMediaAssets** collection (which is hello set of one or more output media assets that results from running a job).</span></span> <span data-ttu-id="44648-112">Este ejemplo muestra cómo multimedia de salida toodownload activos desde un trabajo, pero pueden aplicar Hola mismo toodownload enfoque otros activos.</span><span class="sxs-lookup"><span data-stu-id="44648-112">This  example shows how toodownload output media assets from a job, but you can apply hello same approach toodownload other assets.</span></span>

>[!NOTE]
><span data-ttu-id="44648-113">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="44648-113">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="44648-114">Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / acceso permisos, por ejemplo, las directivas para localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga).</span><span class="sxs-lookup"><span data-stu-id="44648-114">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="44648-115">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="44648-115">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    // Download hello output asset of hello specified job tooa local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how toodownload a single asset. 
        // However, you can iterate through hello OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference toohello job. 
        IJob job = GetJob(jobId);

        // Get a reference toohello first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator toodownload hello asset
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
            // Use hello following event handler toocheck download progress.
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



## <a name="media-services-learning-paths"></a><span data-ttu-id="44648-116">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="44648-116">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="44648-117">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="44648-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="44648-118">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="44648-118">See Also</span></span>
[<span data-ttu-id="44648-119">contenido por secuencias</span><span class="sxs-lookup"><span data-stu-id="44648-119">Deliver streaming content</span></span>](media-services-deliver-streaming-content.md)

