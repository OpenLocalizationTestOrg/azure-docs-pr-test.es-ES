---
title: "Codificación de un recurso mediante Media Encoder Standard con Azure Portal | Microsoft Docs"
description: "Este tutorial lo guiará a través de los pasos de codificación de un recurso mediante Media Encoder Standard con Azure Portal."
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
ms.openlocfilehash: a299245e285c4caa68988b184799cd6f4d13e080
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-the-azure-portal"></a><span data-ttu-id="fbb91-103">Codificación de un recurso mediante Media Encoder Standard con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fbb91-103">Encode an asset using Media Encoder Standard with the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="fbb91-104">Para completar este tutorial, deberá tener una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbb91-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="fbb91-105">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbb91-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="fbb91-106">Cuando se trabaja con Azure Media Services, uno de los escenarios más comunes es entregar streaming de velocidad de bits adaptable a los clientes.</span><span class="sxs-lookup"><span data-stu-id="fbb91-106">When working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="fbb91-107">Media Services admite las siguientes tecnologías de streaming con velocidad de bits adaptable: HTTP Live Streaming (HLS), Smooth Streaming y MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="fbb91-107">Media Services supports the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="fbb91-108">Para preparar vídeos para streaming con velocidad de bits adaptable, debe codificar el vídeo de origen en archivos de varias velocidades de bits.</span><span class="sxs-lookup"><span data-stu-id="fbb91-108">To prepare your videos for adaptive bitrate streaming, you need to encode your source video into multi-bitrate files.</span></span> <span data-ttu-id="fbb91-109">Debe utilizar el **Codificador multimedia estándar** para codificar sus vídeos.</span><span class="sxs-lookup"><span data-stu-id="fbb91-109">You should use the **Media Encoder Standard** encoder to encode your videos.</span></span>  

<span data-ttu-id="fbb91-110">Media Services también proporciona empaquetado dinámico, que permite entregar archivos MP4 de velocidad de bits múltiple en los siguientes formatos de streaming: MPEG DASH, HLS o Smooth Streaming sin tener que volver a empaquetar en dichos formatos.</span><span class="sxs-lookup"><span data-stu-id="fbb91-110">Media Services also provides dynamic packaging which allows you to deliver your multi-bitrate MP4s in the following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having to re-package into these streaming formats.</span></span> <span data-ttu-id="fbb91-111">Con el empaquetado dinámico solo necesita almacenar y pagar por los archivos en formato de almacenamiento sencillo y Media Services creará y servirá la respuesta adecuada en función de las solicitudes del cliente.</span><span class="sxs-lookup"><span data-stu-id="fbb91-111">With dynamic packaging you only need to store and pay for the files in single storage format and Media Services will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="fbb91-112">Para sacar partido del empaquetado dinámico, tiene que codificar su archivo de origen en un conjunto de archivos MP4 de velocidad de bits múltiple (los pasos de codificación se muestran más adelante en esta sección).</span><span class="sxs-lookup"><span data-stu-id="fbb91-112">To take advantage of dynamic packaging, you need to encode your source file into a set of multi-bitrate MP4 files (the encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="fbb91-113">Para escalar el procesamiento de medios, consulte [este](media-services-portal-scale-media-processing.md) tema.</span><span class="sxs-lookup"><span data-stu-id="fbb91-113">To scale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-the-azure-portal"></a><span data-ttu-id="fbb91-114">Codificación con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fbb91-114">Encode with the Azure portal</span></span>
<span data-ttu-id="fbb91-115">En esta sección se describen los pasos que puede seguir para codificar el contenido con Estándar de codificador multimedia.</span><span class="sxs-lookup"><span data-stu-id="fbb91-115">This section describes the steps you can take to encode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="fbb91-116">En [Azure Portal](https://portal.azure.com/), seleccione la cuenta de Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="fbb91-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="fbb91-117">En la ventana **Configuración**, seleccione **Activos**.</span><span class="sxs-lookup"><span data-stu-id="fbb91-117">In the **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="fbb91-118">En la ventana **Activos** , seleccione el recurso que desea codificar.</span><span class="sxs-lookup"><span data-stu-id="fbb91-118">In the **Assets** window, select the asset that you would like to encode.</span></span>
4. <span data-ttu-id="fbb91-119">Presione el botón **Codificar** .</span><span class="sxs-lookup"><span data-stu-id="fbb91-119">Press the **Encode** button.</span></span>
5. <span data-ttu-id="fbb91-120">En la ventana **Encode an asset** (Codificar un recurso), seleccione el procesador "Codificador multimedia estándar" y un valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="fbb91-120">In the **Encode an asset** window, select the "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="fbb91-121">Para más información acerca de los valores preestablecidos, consulte [Generación automática de una escalera de velocidad de bits](media-services-autogen-bitrate-ladder-with-mes.md) y [Valores preestablecidos de tarea para MES](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fbb91-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="fbb91-122">Si tiene previsto controlar qué valor preestablecido de codificación se usa, tenga en cuenta: es importante seleccionar el valor preestablecido más adecuado para la entrada de vídeo.</span><span class="sxs-lookup"><span data-stu-id="fbb91-122">If you plan to control which encoding preset is used, keep this in mind: it is important to select the preset that is most appropriate for your input video.</span></span> <span data-ttu-id="fbb91-123">Por ejemplo, si sabe que el vídeo de entrada tiene una resolución de 1920 x 1080 píxeles, se podría utilizar el valor predeterminado "H264 Multiple Bitrate 1080p".</span><span class="sxs-lookup"><span data-stu-id="fbb91-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use the "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="fbb91-124">Si tiene un vídeo de baja resolución (640 x 360), no debería utilizar el valor preestablecido "H264 Multiple Bitrate 1080p".</span><span class="sxs-lookup"><span data-stu-id="fbb91-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="fbb91-125">Para facilitar la administración, se puede editar el nombre del recurso de salida y el nombre del trabajo.</span><span class="sxs-lookup"><span data-stu-id="fbb91-125">For easier management, you have an option of editing the name of the output asset, and the name of the job.</span></span>
   
   ![Codificación de recursos](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="fbb91-127">Pulse **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fbb91-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="fbb91-128">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="fbb91-128">Next step</span></span>
<span data-ttu-id="fbb91-129">Puede supervisar el progreso del trabajo de codificación con Azure Portal, tal y como se describe en [este](media-services-portal-check-job-progress.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="fbb91-129">You can monitor encoding job progress with the Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="fbb91-130">Rutas de aprendizaje de Media Services</span><span class="sxs-lookup"><span data-stu-id="fbb91-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fbb91-131">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="fbb91-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

