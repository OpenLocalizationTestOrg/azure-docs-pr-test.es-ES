---
title: "aaaEncode un activo con Media Encoder estándar Hola portal de Azure | Documentos de Microsoft"
description: "Este tutorial le guiará por los pasos de Hola de codificación de un activo con Media Encoder estándar Hola portal de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a><span data-ttu-id="644aa-103">Codificar un activo con Media Encoder estándar con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="644aa-103">Encode an asset using Media Encoder Standard with hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="644aa-104">toocomplete este tutorial, necesita una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="644aa-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="644aa-105">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="644aa-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="644aa-106">Cuando se trabaja con servicios de multimedia de Azure, uno de los escenarios más comunes de hello entrega a clientes tooyour streaming de velocidad de bits adaptativa.</span><span class="sxs-lookup"><span data-stu-id="644aa-106">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="644aa-107">Servicios multimedia admite Hola siguiendo las tecnologías de streaming de velocidad de bits adaptativa: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="644aa-107">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="644aa-108">tooprepare los vídeos de streaming de velocidad de bits adaptativa, necesita tooencode el origen de vídeo en archivos de varias velocidades de bits.</span><span class="sxs-lookup"><span data-stu-id="644aa-108">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="644aa-109">Debe usar hello **Media Encoder estándar** codificador tooencode sus vídeos.</span><span class="sxs-lookup"><span data-stu-id="644aa-109">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="644aa-110">Servicios multimedia también proporciona el empaquetado dinámico que permite toodeliver su MP4s velocidades de bits en los siguientes formatos de streaming de Hola: MPEG DASH, HLS, Smooth Streaming, sin necesidad de toore-package en estos formatos de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="644aa-110">Media Services also provides dynamic packaging which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toore-package into these streaming formats.</span></span> <span data-ttu-id="644aa-111">Con el empaquetado dinámico solo tendrá toostore y pago para archivos de hello en formato de almacenamiento único y servicios multimedia creará y proporcionará Hola respuesta adecuada según las solicitudes de un cliente.</span><span class="sxs-lookup"><span data-stu-id="644aa-111">With dynamic packaging you only need toostore and pay for hello files in single storage format and Media Services will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="644aa-112">tootake ventaja del empaquetado dinámico, debe tooencode el archivo de origen en un conjunto de archivos MP4 de velocidad de bits múltiple (pasos de codificación de Hola se muestran más adelante en esta sección).</span><span class="sxs-lookup"><span data-stu-id="644aa-112">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="644aa-113">media de tooscale de procesamiento, consulte [esto](media-services-portal-scale-media-processing.md) tema.</span><span class="sxs-lookup"><span data-stu-id="644aa-113">tooscale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-hello-azure-portal"></a><span data-ttu-id="644aa-114">Codificar con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="644aa-114">Encode with hello Azure portal</span></span>
<span data-ttu-id="644aa-115">Esta sección describen los pasos de Hola que puede seguir tooencode el contenido con Media Encoder estándar.</span><span class="sxs-lookup"><span data-stu-id="644aa-115">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="644aa-116">Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="644aa-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="644aa-117">Hola **configuración** ventana, seleccione **activos**.</span><span class="sxs-lookup"><span data-stu-id="644aa-117">In hello **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="644aa-118">Hola **activos** (ventana), activo Hola select que desearía tooencode.</span><span class="sxs-lookup"><span data-stu-id="644aa-118">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
4. <span data-ttu-id="644aa-119">Hola presione **Encode** botón.</span><span class="sxs-lookup"><span data-stu-id="644aa-119">Press hello **Encode** button.</span></span>
5. <span data-ttu-id="644aa-120">Hola **codificar un activo** ventana, procesador "Media Encoder" estándar"hello select y un valor preestablecido.</span><span class="sxs-lookup"><span data-stu-id="644aa-120">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="644aa-121">Para más información acerca de los valores preestablecidos, consulte [Generación automática de una escalera de velocidad de bits](media-services-autogen-bitrate-ladder-with-mes.md) y [Valores preestablecidos de tarea para MES](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="644aa-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="644aa-122">Si tiene previsto toocontrol se utiliza el valor predeterminado de codificación, Téngalo en cuenta: es importante tooselect Hola preestablecido que sea más adecuado para el vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="644aa-122">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="644aa-123">Por ejemplo, si sabe que el vídeo de entrada tiene una resolución de 1920 x 1080 píxeles, a continuación, podría utilizar Hola "H264 1080p de velocidad de bits múltiple" preestablecido.</span><span class="sxs-lookup"><span data-stu-id="644aa-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="644aa-124">Si tiene un vídeo de baja resolución (640 x 360), no debería utilizar el valor preestablecido "H264 Multiple Bitrate 1080p".</span><span class="sxs-lookup"><span data-stu-id="644aa-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="644aa-125">Para facilitar la administración, tendrá una opción de edición nombre Hola de recurso de salida de hello y nombre de Hola de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="644aa-125">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![Codificación de recursos](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="644aa-127">Pulse **Crear**.</span><span class="sxs-lookup"><span data-stu-id="644aa-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="644aa-128">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="644aa-128">Next step</span></span>
<span data-ttu-id="644aa-129">Puede supervisar el progreso de trabajo de codificación con hello portal de Azure, como se describe en [esto](media-services-portal-check-job-progress.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="644aa-129">You can monitor encoding job progress with hello Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="644aa-130">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="644aa-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="644aa-131">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="644aa-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

