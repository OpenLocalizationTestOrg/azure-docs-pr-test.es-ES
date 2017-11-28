---
title: aaaAnalyze los medios que utilizan Hola portal de Azure | Documentos de Microsoft
description: "Este tema se describe cómo tooprocess multimedia con procesadores de multimedia de análisis multimedia (MP) mediante Hola portal de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a><span data-ttu-id="54454-103">Analizar el contenido multimedia mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="54454-103">Analyze your media using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="54454-104">toocomplete este tutorial, necesita una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="54454-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="54454-105">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54454-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="54454-106">Información general</span><span class="sxs-lookup"><span data-stu-id="54454-106">Overview</span></span>
<span data-ttu-id="54454-107">Análisis de servicios multimedia de Azure es una colección de componentes de voz y visión (en escala empresarial, cumplimiento de normas, seguridad y alcance global) que resulte más fácil para las organizaciones y empresas información procesable tooderive de sus archivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="54454-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="54454-108">Para obtener información más detallada de Análisis de Azure Media Services, consulte [este](media-services-analytics-overview.md) tema.</span><span class="sxs-lookup"><span data-stu-id="54454-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="54454-109">Este tema se describe cómo tooprocess multimedia con procesadores de multimedia de análisis multimedia (MP) mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="54454-109">This topic discusses how tooprocess your media with Media Analytics media processors (MPs) using hello Azure portal.</span></span> <span data-ttu-id="54454-110">Los procesadores de multimedia de Análisis multimedia generan archivos MP4 o JSON.</span><span class="sxs-lookup"><span data-stu-id="54454-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="54454-111">Si un procesador multimedia genera un archivo MP4, puede descargar progresivamente archivo hello.</span><span class="sxs-lookup"><span data-stu-id="54454-111">If a media processor produced an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="54454-112">Si un procesador multimedia genera un archivo JSON, puede descargar el archivo hello de hello almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="54454-112">If a media processor produced a JSON file, you can download hello file from hello Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a><span data-ttu-id="54454-113">Elija un recurso que desea tooanalyze</span><span class="sxs-lookup"><span data-stu-id="54454-113">Choose an asset that you want tooanalyze</span></span>
1. <span data-ttu-id="54454-114">Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="54454-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="54454-115">Hola **configuración** ventana, seleccione **activos**.</span><span class="sxs-lookup"><span data-stu-id="54454-115">In hello **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="54454-116">.</span><span class="sxs-lookup"><span data-stu-id="54454-116">.</span></span>
    <span data-ttu-id="54454-117">![Análisis de vídeos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="54454-117">![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="54454-118">Activos de hello SELECT que le gustaría hello tooanalyze y presione **analizar** botón.</span><span class="sxs-lookup"><span data-stu-id="54454-118">Select hello asset that you would like tooanalyze and press hello **Analyze** button.</span></span>
   
    ![Análisis de vídeos](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="54454-120">Hola **activo multimedia de proceso con análisis multimedia** (ventana), el procesador de hello seleccione.</span><span class="sxs-lookup"><span data-stu-id="54454-120">In hello **Process media asset with  Media Analytics** window, select hello processor.</span></span> 
   
    <span data-ttu-id="54454-121">resto de Hello del artículo de hello explica por qué y cómo toouse cada procesador.</span><span class="sxs-lookup"><span data-stu-id="54454-121">hello rest of hello article explains why and how toouse each processor.</span></span> 
5. <span data-ttu-id="54454-122">Presione **crear** toohello iniciar un trabajo.</span><span class="sxs-lookup"><span data-stu-id="54454-122">Press **Create** toohello start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="54454-123">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="54454-123">Azure Media Indexer</span></span>
<span data-ttu-id="54454-124">Hola **Azure Media Indexer** procesador multimedia permite toomake los archivos multimedia y contenido para la búsqueda, así como generar pistas de subtítulos.</span><span class="sxs-lookup"><span data-stu-id="54454-124">hello **Azure Media Indexer** media processor enables you toomake media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="54454-125">En esta sección se proporcionan algunos detalles sobre las opciones que puede especificar para este MP.</span><span class="sxs-lookup"><span data-stu-id="54454-125">This sections gives some details about options that you can specify for this MP.</span></span>

![Análisis de vídeos](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="54454-127">language</span><span class="sxs-lookup"><span data-stu-id="54454-127">Language</span></span>
<span data-ttu-id="54454-128">Hola toobe de lenguaje natural que se reconocen en el archivo multimedia de hello.</span><span class="sxs-lookup"><span data-stu-id="54454-128">hello natural language toobe recognized in hello multimedia file.</span></span> <span data-ttu-id="54454-129">Por ejemplo, inglés o español.</span><span class="sxs-lookup"><span data-stu-id="54454-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="54454-130">Subtítulos</span><span class="sxs-lookup"><span data-stu-id="54454-130">Captions</span></span>
<span data-ttu-id="54454-131">Puede elegir un formato de subtitulado que se generará a partir del contenido.</span><span class="sxs-lookup"><span data-stu-id="54454-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="54454-132">Un trabajo de indización puede generar archivos de subtítulos de hello siguientes formatos:</span><span class="sxs-lookup"><span data-stu-id="54454-132">An indexing job can generate closed caption files in hello following formats:</span></span>  

* <span data-ttu-id="54454-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="54454-133">**SAMI**</span></span>
* <span data-ttu-id="54454-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="54454-134">**TTML**</span></span>
* <span data-ttu-id="54454-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="54454-135">**WebVTT**</span></span>

<span data-ttu-id="54454-136">Archivos cerrados de subtítulos (CC) en estos formatos pueden ser usado toomake audio y archivos de vídeo toopeople accesible con discapacidades auditivas.</span><span class="sxs-lookup"><span data-stu-id="54454-136">Closed Caption (CC) files in these formats can be used toomake audio and video files accessible toopeople with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="54454-137">Archivo AIB</span><span class="sxs-lookup"><span data-stu-id="54454-137">AIB file</span></span>
<span data-ttu-id="54454-138">Seleccione esta opción si se como archivo de Blob de índice de Audio de hello toogenerate para su uso con el Hola IFilter personalizada de servidor de SQL.</span><span class="sxs-lookup"><span data-stu-id="54454-138">Select this option if you would like toogenerate hello Audio Index Blob file for use with hello custom SQL Server IFilter.</span></span> <span data-ttu-id="54454-139">Para más información, consulte [este blog](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) .</span><span class="sxs-lookup"><span data-stu-id="54454-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="54454-140">Palabras clave</span><span class="sxs-lookup"><span data-stu-id="54454-140">Keywords</span></span>
<span data-ttu-id="54454-141">Seleccione esta opción si desea que toogenerate un archivo XML de palabras clave.</span><span class="sxs-lookup"><span data-stu-id="54454-141">Select this option if you would like toogenerate a keywords XML file.</span></span> <span data-ttu-id="54454-142">Este archivo contiene palabras clave extraídas de contenidos de hello orales, con frecuencia y la información de desplazamiento.</span><span class="sxs-lookup"><span data-stu-id="54454-142">This file contains keywords extracted from hello speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="54454-143">Nombre del trabajo</span><span class="sxs-lookup"><span data-stu-id="54454-143">Job name</span></span>
<span data-ttu-id="54454-144">Un nombre descriptivo que le permite identificar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="54454-144">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="54454-145">[Esto](media-services-portal-check-job-progress.md) artículo describe cómo puede supervisar el progreso de Hola de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="54454-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="54454-146">Archivo de salida</span><span class="sxs-lookup"><span data-stu-id="54454-146">Output file</span></span>
<span data-ttu-id="54454-147">Un nombre descriptivo que le permite identificar el contenido de la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="54454-147">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="54454-148">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="54454-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="54454-149">Azure Media Hyperlapse es un MP que crea vídeos fluidos con la técnica time-lapse a partir de contenido generado en primera persona o con una cámara de acción.</span><span class="sxs-lookup"><span data-stu-id="54454-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="54454-150">Para obtener más información, consulte [este tema](media-services-hyperlapse-content.md) .</span><span class="sxs-lookup"><span data-stu-id="54454-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="54454-151">En esta sección se proporcionan algunos detalles sobre las opciones que puede especificar para este MP.</span><span class="sxs-lookup"><span data-stu-id="54454-151">This sections gives some details about options that you can specify for this MP.</span></span>

![Análisis de vídeos](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="54454-153">Velocidad</span><span class="sxs-lookup"><span data-stu-id="54454-153">Speed</span></span>
<span data-ttu-id="54454-154">Especifica la velocidad de hello con qué toospeed el vídeo de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="54454-154">Specify hello speed with which toospeed up hello input video.</span></span> <span data-ttu-id="54454-155">salida de Hello es una copia estabilizar y vencido de tiempo del vídeo de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="54454-155">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="54454-156">Nombre del trabajo</span><span class="sxs-lookup"><span data-stu-id="54454-156">Job name</span></span>
<span data-ttu-id="54454-157">Un nombre descriptivo que le permite identificar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="54454-157">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="54454-158">[Esto](media-services-portal-check-job-progress.md) artículo describe cómo puede supervisar el progreso de Hola de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="54454-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="54454-159">Archivo de salida</span><span class="sxs-lookup"><span data-stu-id="54454-159">Output file</span></span>
<span data-ttu-id="54454-160">Un nombre descriptivo que le permite identificar el contenido de la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="54454-160">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="54454-161">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="54454-161">Azure Media Face Detector</span></span>
<span data-ttu-id="54454-162">Hola **Detector de caras de multimedia de Azure** procesador multimedia (MP) le permite toocount, movimientos de seguimiento y participación de la audiencia de medidor incluso y reacción a través de expresiones faciales.</span><span class="sxs-lookup"><span data-stu-id="54454-162">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="54454-163">Este servicio contiene dos características:</span><span class="sxs-lookup"><span data-stu-id="54454-163">This service contains two features:</span></span> 

* <span data-ttu-id="54454-164">**Detección de caras**</span><span class="sxs-lookup"><span data-stu-id="54454-164">**Face detection**</span></span>
  
    <span data-ttu-id="54454-165">La detección de caras busca y realiza el seguimiento de caras humanas dentro de un vídeo.</span><span class="sxs-lookup"><span data-stu-id="54454-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="54454-166">Varias caras pueden detectarse y posteriormente se realiza el seguimiento de medida que se mueven, con metadatos de tiempo y la ubicación de hello devueltos en un archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="54454-166">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="54454-167">Durante el seguimiento, tratará de toogive un toohello identificador coherente mismo enfrentan mientras está moviendo persona Hola en pantalla, incluso si se puede ver obstruidos o brevemente deje marco Hola.</span><span class="sxs-lookup"><span data-stu-id="54454-167">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="54454-168">Este servicio no lleva a cabo el reconocimiento facial.</span><span class="sxs-lookup"><span data-stu-id="54454-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="54454-169">Una persona que sale del marco de Hola o deja de estar obstruida para demasiado larga se le asignará un nuevo identificador cuando devuelven.</span><span class="sxs-lookup"><span data-stu-id="54454-169">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="54454-170">**Detección de emociones**</span><span class="sxs-lookup"><span data-stu-id="54454-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="54454-171">Detección de emoción es un componente opcional de hello procesador de multimedia de detección de cara que devuelve el análisis en varios atributos emoción de caras de hello detectados, incluida la satisfacción, tristeza, temor, ira y mucho más.</span><span class="sxs-lookup"><span data-stu-id="54454-171">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![Análisis de vídeos](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="54454-173">Modo de detección</span><span class="sxs-lookup"><span data-stu-id="54454-173">Detection mode</span></span>
<span data-ttu-id="54454-174">Uno de los siguientes modos de hello puede usarse por procesador hello:</span><span class="sxs-lookup"><span data-stu-id="54454-174">One of hello following modes can be used by hello processor:</span></span>

* <span data-ttu-id="54454-175">Detección de caras</span><span class="sxs-lookup"><span data-stu-id="54454-175">face detection</span></span>
* <span data-ttu-id="54454-176">Detección de emociones por cara</span><span class="sxs-lookup"><span data-stu-id="54454-176">per face emotion detection</span></span>
* <span data-ttu-id="54454-177">Detección de emociones agregadas</span><span class="sxs-lookup"><span data-stu-id="54454-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="54454-178">Nombre del trabajo</span><span class="sxs-lookup"><span data-stu-id="54454-178">Job name</span></span>
<span data-ttu-id="54454-179">Un nombre descriptivo que le permite identificar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="54454-179">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="54454-180">[Esto](media-services-portal-check-job-progress.md) artículo describe cómo puede supervisar el progreso de Hola de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="54454-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="54454-181">Archivo de salida</span><span class="sxs-lookup"><span data-stu-id="54454-181">Output file</span></span>
<span data-ttu-id="54454-182">Un nombre descriptivo que le permite identificar el contenido de la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="54454-182">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="54454-183">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="54454-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="54454-184">Hola **Detector de movimiento de multimedia de Azure** habilita el procesador (MP) media tooefficiently se identifican las secciones de interés dentro de un vídeo largo y sin incidentes en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="54454-184">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="54454-185">Detección de movimiento puede usarse en secciones de tooidentify grabaciones de cámaras estáticas de vídeo de Hola donde se produce un movimiento.</span><span class="sxs-lookup"><span data-stu-id="54454-185">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="54454-186">Genera un archivo JSON que contiene un metadatos con hello límite región donde se produjo el evento de Hola y marcas de tiempo.</span><span class="sxs-lookup"><span data-stu-id="54454-186">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="54454-187">Destinado fuentes de vídeo de seguridad, esta tecnología es capaz de toocategorize movimiento en los eventos relevantes y falsos positivos, como los cambios de iluminación y sombras.</span><span class="sxs-lookup"><span data-stu-id="54454-187">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="54454-188">Esto permite toogenerate alertas de seguridad de las fuentes de cámara sin que se va a spam con eventos irrelevantes infinitos, al que se va a momentos tooextract capaz de interés de vídeos de vigilancia muy largos.</span><span class="sxs-lookup"><span data-stu-id="54454-188">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

![Análisis de vídeos](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="54454-190">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="54454-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="54454-191">Este procesador puede ayudarle a crear resúmenes de los vídeos largos seleccionando automáticamente interesantes fragmentos de vídeo de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="54454-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="54454-192">Esto es útil cuando se desea una introducción rápida de qué tooexpect en un vídeo largo tooprovide.</span><span class="sxs-lookup"><span data-stu-id="54454-192">This is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="54454-193">Para obtener información detallada y ejemplos, vea [tooCreate de miniaturas de vídeo de multimedia de Azure Use un resumen de vídeo](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="54454-193">For detailed information and examples, see [Use Azure Media Video Thumbnails tooCreate a Video Summarization](media-services-video-summarization.md)</span></span>

![Análisis de vídeos](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="54454-195">Nombre del trabajo</span><span class="sxs-lookup"><span data-stu-id="54454-195">Job name</span></span>
<span data-ttu-id="54454-196">Un nombre descriptivo que le permite identificar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="54454-196">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="54454-197">[Esto](media-services-portal-check-job-progress.md) artículo describe cómo puede supervisar el progreso de Hola de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="54454-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="54454-198">Archivo de salida</span><span class="sxs-lookup"><span data-stu-id="54454-198">Output file</span></span>
<span data-ttu-id="54454-199">Un nombre descriptivo que le permite identificar el contenido de la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="54454-199">A friendly name that lets you identify hello output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="54454-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="54454-200">Next steps</span></span>
<span data-ttu-id="54454-201">Ver las rutas de aprendizaje de Media Services</span><span class="sxs-lookup"><span data-stu-id="54454-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="54454-202">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="54454-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

