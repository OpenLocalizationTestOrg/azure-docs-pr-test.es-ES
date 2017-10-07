---
title: aaa"cargar archivos en una cuenta de servicios multimedia con hello portal de Azure | Documentos de Microsoft"
description: "Este tutorial le guiará por los pasos de Hola de carga de archivos en una cuenta de servicios multimedia con hello portal de Azure"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a><span data-ttu-id="1fdce-103">Cargar archivos en una cuenta de servicios multimedia mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1fdce-103">Upload files into a Media Services account using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1fdce-104">Portal</span><span class="sxs-lookup"><span data-stu-id="1fdce-104">Portal</span></span>](media-services-portal-upload-files.md)
> * [<span data-ttu-id="1fdce-105">.NET</span><span class="sxs-lookup"><span data-stu-id="1fdce-105">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="1fdce-106">REST</span><span class="sxs-lookup"><span data-stu-id="1fdce-106">REST</span></span>](media-services-rest-upload-files.md)
> 
> [!NOTE]
> <span data-ttu-id="1fdce-107">toocomplete este tutorial, necesita una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="1fdce-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="1fdce-108">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1fdce-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 


<span data-ttu-id="1fdce-109">En Servicios multimedia, cargue los archivos digitales en un recurso.</span><span class="sxs-lookup"><span data-stu-id="1fdce-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="1fdce-110">Hola activo puede contener vídeo, audio, imágenes, colecciones de miniaturas, texto realiza un seguimiento y subtítulos archivos (y Hola metadatos acerca de estos archivos.) Una vez que se cargan archivos de hello, el contenido está almacenado en forma segura en nube de Hola para su posterior procesamiento y transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="1fdce-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>


## <a name="upload-files"></a><span data-ttu-id="1fdce-111">Carga de archivos</span><span class="sxs-lookup"><span data-stu-id="1fdce-111">Upload files</span></span>

>[!NOTE]
><span data-ttu-id="1fdce-112">Hay un tamaño de archivo máximo de toohello límite admitido para el procesamiento de los servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="1fdce-112">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="1fdce-113">Vea [esto](media-services-quotas-and-limitations.md) tema para obtener más información acerca de la limitación de tamaño de archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1fdce-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

1. <span data-ttu-id="1fdce-114">Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="1fdce-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="1fdce-115">En hello **configuración** hoja, haga clic en **activos**.</span><span class="sxs-lookup"><span data-stu-id="1fdce-115">On hello **Settings** blade, click **Assets**.</span></span>
   
    ![Carga de archivos](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. <span data-ttu-id="1fdce-117">Haga clic en hello **cargar** botón.</span><span class="sxs-lookup"><span data-stu-id="1fdce-117">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="1fdce-118">Hola **cargar un recurso de vídeo** aparecerá la ventana.</span><span class="sxs-lookup"><span data-stu-id="1fdce-118">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1fdce-119">No hay ninguna limitación de tamaño de archivo.</span><span class="sxs-lookup"><span data-stu-id="1fdce-119">There is no file size limitation.</span></span>
   > 
   > 
4. <span data-ttu-id="1fdce-120">Examinar vídeo toohello deseado en el equipo, selecciónelo y haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="1fdce-120">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="1fdce-121">inicia la carga de Hola y puede ver progreso de hello en nombre de archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1fdce-121">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="1fdce-122">Una vez completada la carga de hello, verá activo nuevo Hola enumerado en hello **activos** ventana.</span><span class="sxs-lookup"><span data-stu-id="1fdce-122">Once hello upload completes, you will see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1fdce-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1fdce-123">Next steps</span></span>
<span data-ttu-id="1fdce-124">Ahora puede codificar los recursos cargados.</span><span class="sxs-lookup"><span data-stu-id="1fdce-124">You can now encode your uploaded assets.</span></span> <span data-ttu-id="1fdce-125">Para más información, consulte [Encode an asset using Media Encoder Standard with the Azure portal](media-services-portal-encode.md)(Codificación de recursos mediante el estándar de codificador multimedia con Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="1fdce-125">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="1fdce-126">También puede utilizar las funciones de Azure tootrigger un trabajo de codificación basado en un archivo que llegan en el contenedor de hello configurado.</span><span class="sxs-lookup"><span data-stu-id="1fdce-126">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="1fdce-127">Para más información, consulte [este ejemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="1fdce-127">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="1fdce-128">Rutas de aprendizaje de Media Services</span><span class="sxs-lookup"><span data-stu-id="1fdce-128">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1fdce-129">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="1fdce-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

