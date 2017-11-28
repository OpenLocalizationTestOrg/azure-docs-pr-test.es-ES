---
title: archivos de aaaUpload en una cuenta de servicios multimedia de Azure de StorSimple de Azure | Documentos de Microsoft
description: "Este artículo ofrece una breve introducción a Azure StorSimple Data Manager. artículo de Hello también incluye vínculos tootutorials que le muestran cómo tooextract datos de StorSimple y cargarlo como activos tooan cuenta de servicios multimedia de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a><span data-ttu-id="aca33-104">Carga de archivos en una cuenta de Azure Media Services mediante Azure StorSimple</span><span class="sxs-lookup"><span data-stu-id="aca33-104">Upload files into an Azure Media Services account from Azure StorSimple</span></span>

<span data-ttu-id="aca33-105">Este artículo ofrece una breve introducción a Azure StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="aca33-105">This article gives a brief overview of Azure StorSimple Data Manager.</span></span> <span data-ttu-id="aca33-106">artículo de Hello también incluye vínculos tootutorials que le muestran cómo tooextract datos de StorSimple y cargar estos datos como activos tooan cuenta de servicios de multimedia de Azure (AMS).</span><span class="sxs-lookup"><span data-stu-id="aca33-106">hello article also links tootutorials that show you how tooextract data from StorSimple and upload this data as assets tooan Azure Media Services (AMS) account.</span></span>

> 
> [!NOTE]
> <span data-ttu-id="aca33-107">Azure StorSimple Data Manager actualmente está en versión preliminar privada.</span><span class="sxs-lookup"><span data-stu-id="aca33-107">Azure StorSimple Data Manager is currently in private preview.</span></span> 
> 

## <a name="overview"></a><span data-ttu-id="aca33-108">Información general</span><span class="sxs-lookup"><span data-stu-id="aca33-108">Overview</span></span>

<span data-ttu-id="aca33-109">En Servicios multimedia, cargue los archivos digitales en un recurso.</span><span class="sxs-lookup"><span data-stu-id="aca33-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="aca33-110">Hola activo puede contener vídeo, audio, imágenes, colecciones de miniaturas, texto realiza un seguimiento y subtítulos archivos (y Hola metadatos acerca de estos archivos.) Una vez que se cargan archivos de hello, el contenido está almacenado en forma segura en nube de Hola para su posterior procesamiento y transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="aca33-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="aca33-111">[StorSimple de Azure](https://docs.microsoft.com/azure/storsimple/) usa almacenamiento en nube como solución local de una extensión de hello y automáticamente de capas de datos a través de un almacenamiento local hello y almacenamiento en la nube.</span><span class="sxs-lookup"><span data-stu-id="aca33-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="aca33-112">dispositivo de StorSimple de Hello dedupes y comprime los datos antes de enviarlo en la nube toohello lo que muy eficaz para el envío de nube de toohello de archivos de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="aca33-112">hello StorSimple device dedupes and compresses your data before sending it toohello cloud making it very efficient for sending large files toohello cloud.</span></span> <span data-ttu-id="aca33-113">Hola [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) servicio proporciona las API que permiten tooextract de datos de StorSimple y presentan como activos de AMS.</span><span class="sxs-lookup"><span data-stu-id="aca33-113">hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service provides APIs that enable you tooextract data from StorSimple and present it as AMS assets.</span></span>

## <a name="get-started"></a><span data-ttu-id="aca33-114">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="aca33-114">Get started</span></span>

1. <span data-ttu-id="aca33-115">[Crear una cuenta de servicios multimedia](media-services-portal-create-account.md) en la que desea que los activos de hello tootransfer.</span><span class="sxs-lookup"><span data-stu-id="aca33-115">[Create a Media Services account](media-services-portal-create-account.md) into which you want tootransfer hello assets.</span></span>
2. <span data-ttu-id="aca33-116">Registrarse para la vista previa de administrador de datos, como se describe en hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="aca33-116">Sign up for Data Manager preview, as described in hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) article.</span></span>
3. <span data-ttu-id="aca33-117">Cree una cuenta de StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="aca33-117">Create a StorSimple Data Manager account.</span></span>
4. <span data-ttu-id="aca33-118">Cree un trabajo de transformación de datos que, cuando se ejecute, extraiga datos de un dispositivo de StorSimple y los transfiera como recursos a una cuenta de AMS.</span><span class="sxs-lookup"><span data-stu-id="aca33-118">Create a data transformation job that when runs, extracts data from a StorSimple device and transfers it into an AMS account as assets.</span></span> 

    <span data-ttu-id="aca33-119">Cuando el trabajo de hello empieza a ejecutarse, se crea una cola de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="aca33-119">When hello job starts running, a storage queue is created.</span></span> <span data-ttu-id="aca33-120">Esta cola se rellena con mensajes de los blobs transformados a medida que están listos.</span><span class="sxs-lookup"><span data-stu-id="aca33-120">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="aca33-121">nombre de Hola de esta cola es Hola igual que el nombre de Hola Hola de definición de trabajo.</span><span class="sxs-lookup"><span data-stu-id="aca33-121">hello name of this queue is hello same as hello name of hello job definition.</span></span> <span data-ttu-id="aca33-122">Puede usar este toodetermine de cola cuando como activo es listos y llamar a su toorun deseado de operación de servicios multimedia de ella.</span><span class="sxs-lookup"><span data-stu-id="aca33-122">You can use this queue toodetermine when as asset is ready and call your desired Media Services operation toorun on it.</span></span> <span data-ttu-id="aca33-123">Por ejemplo, puede usar este tootrigger cola una función de Azure que tiene código de servicios multimedia necesario hello en ella.</span><span class="sxs-lookup"><span data-stu-id="aca33-123">For example, you can use this queue tootrigger an Azure Function that has hello necessary Media Services code in it.</span></span>

## <a name="see-also"></a><span data-ttu-id="aca33-124">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="aca33-124">See also</span></span>

[<span data-ttu-id="aca33-125">Use Hola .net SDK tootrigger trabajos Hola Data Manager</span><span class="sxs-lookup"><span data-stu-id="aca33-125">Use hello .Net SDK tootrigger jobs in hello Data Manager</span></span>](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="aca33-126">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="aca33-126">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="aca33-127">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="aca33-127">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="aca33-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aca33-128">Next steps</span></span>

<span data-ttu-id="aca33-129">Ahora puede codificar los recursos cargados.</span><span class="sxs-lookup"><span data-stu-id="aca33-129">You can now encode your uploaded assets.</span></span> <span data-ttu-id="aca33-130">Para más información, consulte [Encode an asset using Media Encoder Standard with the Azure portal](media-services-portal-encode.md)(Codificación de recursos mediante el estándar de codificador multimedia con el Portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="aca33-130">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>
