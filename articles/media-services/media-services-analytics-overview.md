---
title: "aaaMedia análisis en la plataforma de servicios multimedia de hello | Documentos de Microsoft"
description: "Información general sobre la versión preliminar pública de Análisis multimedia, una colección de servicios de voz y visión informática a escala empresarial, cumplimiento, seguridad y alcance global"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a><span data-ttu-id="a6aa7-103">Análisis de multimedia en la plataforma de servicios multimedia de Hola</span><span class="sxs-lookup"><span data-stu-id="a6aa7-103">Media Analytics on hello Media Services platform</span></span>
## <a name="overview"></a><span data-ttu-id="a6aa7-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a6aa7-104">Overview</span></span>
<span data-ttu-id="a6aa7-105">Las organizaciones más están utilizando vídeo como Hola preferido tootrain intermedio sus empleados, captar sus clientes y las funciones de negocio de documento.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-105">More organizations are using video as hello preferred medium tootrain their employees, engage their customers, and document business functions.</span></span> <span data-ttu-id="a6aa7-106">Proporciona una manera toostore, la informática en nube transmitir por secuencias y tener acceso a estos archivos multimedia de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-106">Cloud computing provides a way toostore, stream, and access these large media files.</span></span> <span data-ttu-id="a6aa7-107">Pero a medida que crece la biblioteca de la compañía de contenido de vídeo, necesita un medio igualmente eficaz de extraer información de contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-107">But as a company's library of video content grows, it needs an equally effective means of extracting insights from hello content.</span></span> 

<span data-ttu-id="a6aa7-108">tooaddress esta necesidad creciente, servicios multimedia de Azure ofrece análisis de multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-108">tooaddress this growing need, Azure Media Services offers Azure Media Analytics.</span></span> <span data-ttu-id="a6aa7-109">Análisis multimedia es una colección de componentes de voz y visión que resulta más fácil para las organizaciones y empresas información procesable tooderive de sus archivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-109">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="a6aa7-110">Creado mediante el uso de componentes de la plataforma de servicios multimedia de hello core, análisis multimedia puede controlar a escala en el primer día de procesamiento de medios.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-110">Built by using hello core Media Services platform components, Media Analytics can handle media processing at scale on day one.</span></span>

<span data-ttu-id="a6aa7-111">Con Análisis multimedia, los desarrolladores pueden integrar funcionalidad de vídeo avanzada en las aplicaciones rápidamente.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-111">With Media Analytics, developers can quickly bring advanced video functionality into applications.</span></span> <span data-ttu-id="a6aa7-112">Proporciona entornos empresariales con escala completa hello, cumplimiento, seguridad y alcance global requerido las grandes organizaciones.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-112">It provides enterprise environments with hello full scale, compliance, security, and global reach required by large organizations.</span></span>

<span data-ttu-id="a6aa7-113">Hello siguiente diagrama muestra análisis multimedia y otros componentes principales de la plataforma de servicios multimedia de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-113">hello following diagram shows Media Analytics and other major parts of hello Media Services platform.</span></span> 

![Flujo de trabajo de VoD](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

<span data-ttu-id="a6aa7-115">Los procesadores multimedia de Análisis multimedia generan archivos MP4 o JSON.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-115">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="a6aa7-116">Si un procesador multimedia genera un archivo MP4, puede descargar progresivamente archivo hello.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-116">If a media processor produces an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="a6aa7-117">Si un procesador multimedia genera un archivo JSON, puede descargar el archivo hello desde el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-117">If a media processor produces a JSON file, you can download hello file from Azure Blob storage.</span></span> 

## <a name="media-analytics-services"></a><span data-ttu-id="a6aa7-118">Servicios de Análisis multimedia</span><span class="sxs-lookup"><span data-stu-id="a6aa7-118">Media Analytics services</span></span>

### <a name="indexer"></a><span data-ttu-id="a6aa7-119">Indexer</span><span class="sxs-lookup"><span data-stu-id="a6aa7-119">Indexer</span></span>
<span data-ttu-id="a6aa7-120">Con Azure Media Indexer puede realizar búsquedas en el contenido, así como generar pistas de subtítulos.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-120">With Azure Media Indexer, you can make content searchable and generate closed-captioning tracks.</span></span> <span data-ttu-id="a6aa7-121">La versión anterior de toohello comparados, vista previa de Azure Media Indexer 2 es indización rápida y más amplia de lenguaje compatible con.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-121">Compared toohello previous version, Azure Media Indexer 2 Preview has faster indexing and broader language support.</span></span> <span data-ttu-id="a6aa7-122">Los idiomas compatibles son alemán, árabe, chino, español, francés, inglés, italiano y portugués.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-122">Supported languages include English, Spanish, French, German, Italian, Chinese, Portuguese, and Arabic.</span></span> <span data-ttu-id="a6aa7-123">Para obtener información detallada y ejemplos, vea [Process videos with Azure Media Indexer 2 (Procesar vídeos con Azure Media Indexer 2)](media-services-process-content-with-indexer2.md).</span><span class="sxs-lookup"><span data-stu-id="a6aa7-123">For detailed information and examples, see [Process videos with Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span></span>
### <a name="hyperlapse"></a><span data-ttu-id="a6aa7-124">Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="a6aa7-124">Hyperlapse</span></span>
<span data-ttu-id="a6aa7-125">Microsoft Hyperlapse combina estabilización del vídeo y capacidad lapso de tiempo toocreate rápido, puede usar vídeos desde el contenido de formato largo.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-125">Microsoft Hyperlapse combines video stabilization and time-lapse capability toocreate quick, consumable videos from your long-form content.</span></span> <span data-ttu-id="a6aa7-126">Además de la creación de vídeo de lapso de tiempo, puede usar Hyperlapse toocreate estables vídeos de vídeos cambiante de captura a través de teléfonos y cámaras de vídeo.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-126">Besides creating time-lapse video, you can use Hyperlapse toocreate stable videos from shaky videos captured via cell phones and camcorders.</span></span> <span data-ttu-id="a6aa7-127">Para obtener información detallada y ejemplos, vea [Archivos multimedia de Hyperlapse con Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span><span class="sxs-lookup"><span data-stu-id="a6aa7-127">For detailed information and examples, see [Hyperlapse media files with Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span></span>
### <a name="motion-detector"></a><span data-ttu-id="a6aa7-128">Detector de movimientos</span><span class="sxs-lookup"><span data-stu-id="a6aa7-128">Motion Detector</span></span>
<span data-ttu-id="a6aa7-129">Puede usar el movimiento de toodetect Detector de movimiento en un vídeo con fondos estacionarios.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-129">You can use Motion Detector toodetect motion in a video with stationary backgrounds.</span></span> <span data-ttu-id="a6aa7-130">Esto hace posible toocheck de falsos positivos en eventos de movimiento detectados por las cámaras de vigilancia.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-130">This makes it possible toocheck for false positives on motion events detected by surveillance cameras.</span></span> <span data-ttu-id="a6aa7-131">Para obtener información detallada y ejemplos, vea [Motion Detection for Azure Media Analytics (Detección de movimiento para Análisis multimedia de Azure)](media-services-motion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="a6aa7-131">For detailed information and examples, see [Motion detection for Azure Media Analytics](media-services-motion-detection.md).</span></span>
### <a name="face-detector"></a><span data-ttu-id="a6aa7-132">Detector de caras</span><span class="sxs-lookup"><span data-stu-id="a6aa7-132">Face Detector</span></span>
<span data-ttu-id="a6aa7-133">Con Face Detector puede detectar las caras y las emociones de las personas, lo que incluye felicidad, tristeza y sorpresa.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-133">By using Face Detector, you can detect people’s faces and their emotions, including happiness, sadness, and surprise.</span></span> <span data-ttu-id="a6aa7-134">Esto tiene varias aplicaciones útiles para el sector, que se describen más adelante, como la adición y el análisis de reacciones de personas que asisten a un evento.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-134">This has several useful industry applications, described later, including aggregating and analyzing reactions of people attending an event.</span></span> <span data-ttu-id="a6aa7-135">Para obtener información detallada y ejemplos, vea [Face and Emotion Detection for Azure Media Analytics (Detección de caras y emociones para Análisis multimedia de Azure)](media-services-face-and-emotion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="a6aa7-135">For detailed information and examples, see [Face and emotion detection for Azure Media Analytics](media-services-face-and-emotion-detection.md).</span></span>
### <a name="video-summarization"></a><span data-ttu-id="a6aa7-136">Resumen de vídeo</span><span class="sxs-lookup"><span data-stu-id="a6aa7-136">Video summarization</span></span>
<span data-ttu-id="a6aa7-137">Resumen de vídeo puede ayudar a crear resúmenes de los vídeos largos seleccionando automáticamente interesantes fragmentos de vídeo de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-137">Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="a6aa7-138">Esta capacidad es útil cuando se desea una introducción rápida de qué tooexpect en un vídeo largo tooprovide.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-138">This ability is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="a6aa7-139">Para obtener información detallada y ejemplos, vea [resumen vídeo de miniaturas de vídeo de multimedia de Azure de uso toocreate](media-services-video-summarization.md).</span><span class="sxs-lookup"><span data-stu-id="a6aa7-139">For detailed information and examples, see [Use Azure Media Video Thumbnails toocreate video summarization](media-services-video-summarization.md).</span></span>
### <a name="optical-character-recognition"></a><span data-ttu-id="a6aa7-140">Reconocimiento óptico de caracteres</span><span class="sxs-lookup"><span data-stu-id="a6aa7-140">Optical character recognition</span></span>
<span data-ttu-id="a6aa7-141">Con Azure Media OCR (reconocimiento óptico de caracteres), puede convertir el contenido de texto de archivos de vídeo en texto digital modificable y utilizable en búsquedas.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-141">With Azure Media OCR (optical character recognition), you can convert text content in video files into editable, searchable digital text.</span></span> <span data-ttu-id="a6aa7-142">A continuación, puede automatizar extracción Hola de metadatos significativo de señal de vídeo de Hola de los medios.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-142">You can then automate hello extraction of meaningful metadata from hello video signal of your media.</span></span>
### <a name="scalable-face-redaction"></a><span data-ttu-id="a6aa7-143">Censura de rostros escalable</span><span class="sxs-lookup"><span data-stu-id="a6aa7-143">Scalable face redaction</span></span>
<span data-ttu-id="a6aa7-144">Redactor de multimedia de Azure es un procesador de multimedia de análisis multimedia que ofrece la redacción de cara escalable en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-144">Azure Media Redactor is a Media Analytics media processor that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="a6aa7-145">Mediante el uso de redacción de cara, puede modificar sus caras tooblur vídeo de los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-145">By using face redaction, you can modify your video tooblur faces of selected individuals.</span></span> <span data-ttu-id="a6aa7-146">Puede ser conveniente servicio de redacción de cara de toouse hello en los medios de noticias o cuando está implicada seguridad pública.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-146">You might want toouse hello face redaction service in news media or when public safety is involved.</span></span> <span data-ttu-id="a6aa7-147">Unos pocos minutos después de material de archivo que contiene varios tipos pueden tardar horas tooredact manualmente, pero con este servicio, redacción de cara tarda unos pocos pasos sencillos.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-147">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service, face redaction takes just a few simple steps.</span></span> <span data-ttu-id="a6aa7-148">Para obtener más información, vea hello [censurar caras con análisis de multimedia de Azure](media-services-face-redaction.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-148">For more information, see hello [Redact faces with Azure Media Analytics](media-services-face-redaction.md) article.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="a6aa7-149">Escenarios comunes</span><span class="sxs-lookup"><span data-stu-id="a6aa7-149">Common scenarios</span></span>
<span data-ttu-id="a6aa7-150">Análisis multimedia puede ayudar a las organizaciones y empresas a recopilar nuevos datos relevantes a partir del vídeo y a administrar más eficazmente grandes volúmenes de contenido de vídeo.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-150">Media Analytics can help organizations and enterprises glean new insights from video and more effectively manage large volumes of video content.</span></span> <span data-ttu-id="a6aa7-151">Estos son algunos escenarios:</span><span class="sxs-lookup"><span data-stu-id="a6aa7-151">Here are several scenarios:</span></span>

* <span data-ttu-id="a6aa7-152">**Centros de atención al cliente**.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-152">**Call centers**.</span></span> <span data-ttu-id="a6aa7-153">Incluso con la llegada de Hola de redes sociales, centros de llamadas de cliente todavía facilitan un porcentaje elevado de transacciones de servicio al cliente.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-153">Even with hello advent of social media, customer call centers still facilitate a large percentage of customer-service transactions.</span></span> <span data-ttu-id="a6aa7-154">Codificados en estos datos de audio es una gran cantidad de información del cliente que se pueden analiza tooachieve mayor satisfacción del cliente.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-154">Encoded in this audio data is a large amount of customer information that can be analyzed tooachieve higher customer satisfaction.</span></span> <span data-ttu-id="a6aa7-155">Con Media Indexer, las organizaciones pueden extraer texto y crear índices y paneles de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-155">By using Media Indexer, organizations can extract text and build search indexes and dashboards.</span></span> <span data-ttu-id="a6aa7-156">Luego pueden extraer inteligencia de las quejas habituales, los orígenes de las quejas y otros datos relevantes.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-156">Then they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span></span>
* <span data-ttu-id="a6aa7-157">**Moderación de contenido generado por el usuario**.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-157">**User-generated content moderation**.</span></span> <span data-ttu-id="a6aa7-158">De departamentos de toopolice de distribuidores de medios de noticias, muchas organizaciones tienen portales de acceso público que aceptan multimedia generado por el usuario, como imágenes y vídeos.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-158">From news media outlets toopolice departments, many organizations have public-facing portals that accept user-generated media such as videos and images.</span></span> <span data-ttu-id="a6aa7-159">volumen de Hola de contenido puede tener picos debido toounexpected eventos.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-159">hello volume of content can spike due toounexpected events.</span></span> <span data-ttu-id="a6aa7-160">En estos casos, resulta difícil tooconduct las revisiones del manual efectiva del contenido de idoneidad.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-160">In these scenarios, it is difficult tooconduct effective manual reviews of content for appropriateness.</span></span> <span data-ttu-id="a6aa7-161">Los clientes pueden basarse en hello toofocus de servicio de moderación de contenido en el contenido que es adecuado.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-161">Customers can rely on hello content-moderation service toofocus on content that is appropriate.</span></span>
* <span data-ttu-id="a6aa7-162">**Vigilancia**.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-162">**Surveillance**.</span></span> <span data-ttu-id="a6aa7-163">Hola crecimiento del uso de cámaras IP conlleva un inventario creciente de vídeo de vigilancia.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-163">With hello growth in use of IP cameras comes a growing inventory of surveillance video.</span></span> <span data-ttu-id="a6aa7-164">Revisar manualmente vídeo vigilancia es toohuman intensivo y propensa a errores en tiempo de.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-164">Manually reviewing surveillance video is time intensive and prone toohuman error.</span></span> <span data-ttu-id="a6aa7-165">Análisis multimedia proporciona servicios como la detección de movimiento y detección de cara, proceso de Hyperlapse toomake Hola de revisar, administrar y crear los derivados más fácil.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-165">Media Analytics provides services such as motion detection, face detection, and Hyperlapse toomake hello process of reviewing, managing, and creating derivatives easier.</span></span>

## <a name="media-analytics-media-processors"></a><span data-ttu-id="a6aa7-166">Procesadores de multimedia de Análisis multimedia</span><span class="sxs-lookup"><span data-stu-id="a6aa7-166">Media Analytics media processors</span></span>
<span data-ttu-id="a6aa7-167">Esta sección procesadores de multimedia de listas Hola análisis multimedia y muestra cómo toouse .NET o REST tooget un objeto de procesador (MP) de medios.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-167">This section lists hello Media Analytics media processors and shows how toouse .NET or REST tooget a media processor (MP) object.</span></span>

### <a name="mp-names"></a><span data-ttu-id="a6aa7-168">Nombres de MP</span><span class="sxs-lookup"><span data-stu-id="a6aa7-168">MP names</span></span>
* <span data-ttu-id="a6aa7-169">Azure Media Indexer 2 Preview</span><span class="sxs-lookup"><span data-stu-id="a6aa7-169">Azure Media Indexer 2 Preview</span></span>
* <span data-ttu-id="a6aa7-170">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="a6aa7-170">Azure Media Indexer</span></span>
* <span data-ttu-id="a6aa7-171">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="a6aa7-171">Azure Media Hyperlapse</span></span>
* <span data-ttu-id="a6aa7-172">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="a6aa7-172">Azure Media Face Detector</span></span>
* <span data-ttu-id="a6aa7-173">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="a6aa7-173">Azure Media Motion Detector</span></span>
* <span data-ttu-id="a6aa7-174">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="a6aa7-174">Azure Media Video Thumbnails</span></span>
* <span data-ttu-id="a6aa7-175">Azure Media OCR</span><span class="sxs-lookup"><span data-stu-id="a6aa7-175">Azure Media OCR</span></span>

### <a name="net"></a><span data-ttu-id="a6aa7-176">.NET</span><span class="sxs-lookup"><span data-stu-id="a6aa7-176">.NET</span></span>
<span data-ttu-id="a6aa7-177">Hola después de la función toma uno del programa Hola a especifica nombres de módulo de administración y devuelve un objeto de módulo de administración.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-177">hello following function takes one of hello specified MP names and returns an MP object.</span></span>

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }


### <a name="rest"></a><span data-ttu-id="a6aa7-178">REST</span><span class="sxs-lookup"><span data-stu-id="a6aa7-178">REST</span></span>
<span data-ttu-id="a6aa7-179">Solicitud:</span><span class="sxs-lookup"><span data-stu-id="a6aa7-179">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

<span data-ttu-id="a6aa7-180">Respuesta:</span><span class="sxs-lookup"><span data-stu-id="a6aa7-180">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a><span data-ttu-id="a6aa7-181">Demostraciones</span><span class="sxs-lookup"><span data-stu-id="a6aa7-181">Demos</span></span>
<span data-ttu-id="a6aa7-182">Vea [Demostraciones de Análisis multimedia de Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span><span class="sxs-lookup"><span data-stu-id="a6aa7-182">See [Azure Media Analytics demos](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6aa7-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a6aa7-183">Next steps</span></span>
<span data-ttu-id="a6aa7-184">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="a6aa7-184">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a6aa7-185">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="a6aa7-185">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="a6aa7-186">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="a6aa7-186">Related articles</span></span>
<span data-ttu-id="a6aa7-187">Vea [Media Services Analytics announcement (Anuncio de análisis de Media Services)](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span><span class="sxs-lookup"><span data-stu-id="a6aa7-187">See [Media Services Analytics announcement](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span></span>

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
