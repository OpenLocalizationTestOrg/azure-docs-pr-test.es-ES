---
title: "aaaGet se inició con la entrega de VoD mediante Hola portal de Azure | Documentos de Microsoft"
description: "Este tutorial le guiará por los pasos de saludo de la implementación de un servicio de entrega de contenido de vídeo bajo demanda (VoD) básico con aplicación de servicios de multimedia de Azure (AMS) mediante Hola portal de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a><span data-ttu-id="646ac-103">Introducción a la entrega de contenido a petición con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="646ac-103">Get started with delivering content on demand using hello Azure portal</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="646ac-104">Este tutorial le guiará por los pasos de saludo de la implementación de un servicio de entrega de contenido de vídeo bajo demanda (VoD) básico con aplicación de servicios de multimedia de Azure (AMS) mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="646ac-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="646ac-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="646ac-105">Prerequisites</span></span>
<span data-ttu-id="646ac-106">tutorial de hello toocomplete necesarios son las siguientes de Hello:</span><span class="sxs-lookup"><span data-stu-id="646ac-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="646ac-107">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="646ac-107">An Azure account.</span></span> <span data-ttu-id="646ac-108">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="646ac-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="646ac-109">Una cuenta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="646ac-109">A Media Services account.</span></span> <span data-ttu-id="646ac-110">toocreate una cuenta de servicios multimedia, consulte [cómo tooCreate una cuenta de servicios multimedia](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="646ac-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="646ac-111">Este tutorial incluye Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="646ac-111">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="646ac-112">Inicie el punto de conexión de streaming.</span><span class="sxs-lookup"><span data-stu-id="646ac-112">Start streaming endpoint.</span></span>
2. <span data-ttu-id="646ac-113">Carga de un archivo de vídeo.</span><span class="sxs-lookup"><span data-stu-id="646ac-113">Upload a video file.</span></span>
3. <span data-ttu-id="646ac-114">Codificar el archivo de código fuente de hello en un conjunto de archivos MP4 de velocidad de bits adaptativa.</span><span class="sxs-lookup"><span data-stu-id="646ac-114">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="646ac-115">Publicar los activos de Hola y get de transmisión por secuencias y direcciones URL de descarga progresiva.</span><span class="sxs-lookup"><span data-stu-id="646ac-115">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="646ac-116">Reproduzca el contenido.</span><span class="sxs-lookup"><span data-stu-id="646ac-116">Play your content.</span></span>

## <a name="start-streaming-endpoints"></a><span data-ttu-id="646ac-117">Inicio de los puntos de conexión de streaming</span><span class="sxs-lookup"><span data-stu-id="646ac-117">Start streaming endpoints</span></span> 

<span data-ttu-id="646ac-118">Cuando se trabaja con uno de los escenarios más comunes de hello es entregar vídeo a través de la velocidad de bits de transmisión por secuencias adaptativa de servicios de multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="646ac-118">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="646ac-119">Servicios multimedia proporciona empaquetado dinámico, lo que permite toodeliver la velocidad de bits adaptativa MP4 codificados contenido de transmisión por secuencias formatos admitidos por servicios multimedia (MPEG DASH, HLS, Smooth Streaming) just-in-time, sin necesidad de toostore preempaquetado versiones de cada uno de estos formatos de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="646ac-119">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="646ac-120">Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado.</span><span class="sxs-lookup"><span data-stu-id="646ac-120">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="646ac-121">toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado.</span><span class="sxs-lookup"><span data-stu-id="646ac-121">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

<span data-ttu-id="646ac-122">toostart Hola extremo de streaming, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="646ac-122">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="646ac-123">Inicie sesión en hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="646ac-123">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="646ac-124">En la ventana de configuración de hello, haga clic en los puntos de conexión de la transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="646ac-124">In hello Settings window, click Streaming endpoints.</span></span> 
3. <span data-ttu-id="646ac-125">Haga clic en predeterminada Hola extremo de streaming.</span><span class="sxs-lookup"><span data-stu-id="646ac-125">Click hello default streaming endpoint.</span></span> 

    <span data-ttu-id="646ac-126">Aparecerá la ventana de detalles predeterminada del extremo de transmisión por secuencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="646ac-126">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="646ac-127">Haga clic en el icono de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="646ac-127">Click hello Start icon.</span></span>
5. <span data-ttu-id="646ac-128">Haga clic en botón toosave de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="646ac-128">Click hello Save button toosave your changes.</span></span>

## <a name="upload-files"></a><span data-ttu-id="646ac-129">Carga de archivos</span><span class="sxs-lookup"><span data-stu-id="646ac-129">Upload files</span></span>
<span data-ttu-id="646ac-130">toostream vídeos con servicios multimedia de Azure, necesita vídeos de origen de tooupload hello, codificarlos en varias velocidades de bits y publicar resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="646ac-130">toostream videos using Azure Media Services, you need tooupload hello source videos, encode them into multiple bitrates, and publish hello result.</span></span> <span data-ttu-id="646ac-131">primer paso de Hola se trata en esta sección.</span><span class="sxs-lookup"><span data-stu-id="646ac-131">hello first step is covered in this section.</span></span> 

1. <span data-ttu-id="646ac-132">Hola **configuración** ventana, haga clic en **activos**.</span><span class="sxs-lookup"><span data-stu-id="646ac-132">In hello **Setting** window, click **Assets**.</span></span>
   
    ![Carga de archivos](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. <span data-ttu-id="646ac-134">Haga clic en hello **cargar** botón.</span><span class="sxs-lookup"><span data-stu-id="646ac-134">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="646ac-135">Hola **cargar un recurso de vídeo** aparecerá la ventana.</span><span class="sxs-lookup"><span data-stu-id="646ac-135">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="646ac-136">No hay ninguna limitación de tamaño de archivo.</span><span class="sxs-lookup"><span data-stu-id="646ac-136">There is no file size limitation.</span></span>
   > 
   > 
3. <span data-ttu-id="646ac-137">Examinar vídeo toohello deseado en el equipo, selecciónelo y haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="646ac-137">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="646ac-138">inicia la carga de Hola y puede ver progreso de hello en nombre de archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="646ac-138">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="646ac-139">Una vez completada la carga de hello, vea activo nuevo Hola enumerado en hello **activos** ventana.</span><span class="sxs-lookup"><span data-stu-id="646ac-139">Once hello upload completes, you see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="encode-assets"></a><span data-ttu-id="646ac-140">Codificación de recursos</span><span class="sxs-lookup"><span data-stu-id="646ac-140">Encode assets</span></span>

<span data-ttu-id="646ac-141">Cuando se trabaja con servicios de multimedia de Azure, uno de los escenarios más comunes de hello entrega a clientes tooyour streaming de velocidad de bits adaptativa.</span><span class="sxs-lookup"><span data-stu-id="646ac-141">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="646ac-142">Servicios multimedia admite Hola siguiendo las tecnologías de streaming de velocidad de bits adaptativa: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="646ac-142">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="646ac-143">tooprepare los vídeos de streaming de velocidad de bits adaptativa, necesita tooencode el origen de vídeo en archivos de varias velocidades de bits.</span><span class="sxs-lookup"><span data-stu-id="646ac-143">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="646ac-144">Debe usar hello **Media Encoder estándar** codificador tooencode sus vídeos.</span><span class="sxs-lookup"><span data-stu-id="646ac-144">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="646ac-145">Servicios multimedia también proporciona el empaquetado dinámico, lo que permite toodeliver su MP4s velocidades de bits en los siguientes formatos de streaming de Hola: MPEG DASH, HLS, Smooth Streaming, sin necesidad de toorepackage en estos formatos de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="646ac-145">Media Services also provides dynamic packaging, which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toorepackage into these streaming formats.</span></span> <span data-ttu-id="646ac-146">Con el empaquetado dinámico, solo tendrá toostore y pago para archivos de hello en formato de almacenamiento único y servicios multimedia genera y actúa según las solicitudes de un cliente de respuesta adecuada Hola.</span><span class="sxs-lookup"><span data-stu-id="646ac-146">With dynamic packaging, you only need toostore and pay for hello files in single storage format and Media Services builds and serves hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="646ac-147">tootake ventaja del empaquetado dinámico, debe tooencode el archivo de origen en un conjunto de archivos MP4 de velocidad de bits múltiple (pasos de codificación de Hola se muestran más adelante en esta sección).</span><span class="sxs-lookup"><span data-stu-id="646ac-147">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

### <a name="toouse-hello-portal-tooencode"></a><span data-ttu-id="646ac-148">toouse Hola portal tooencode</span><span class="sxs-lookup"><span data-stu-id="646ac-148">toouse hello portal tooencode</span></span>
<span data-ttu-id="646ac-149">Esta sección describen los pasos de Hola que puede seguir tooencode el contenido con Media Encoder estándar.</span><span class="sxs-lookup"><span data-stu-id="646ac-149">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="646ac-150">Hola **configuración** ventana, seleccione **activos**.</span><span class="sxs-lookup"><span data-stu-id="646ac-150">In hello **Settings** window, select **Assets**.</span></span>  
2. <span data-ttu-id="646ac-151">Hola **activos** (ventana), activo Hola select que desearía tooencode.</span><span class="sxs-lookup"><span data-stu-id="646ac-151">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
3. <span data-ttu-id="646ac-152">Hola presione **Encode** botón.</span><span class="sxs-lookup"><span data-stu-id="646ac-152">Press hello **Encode** button.</span></span>
4. <span data-ttu-id="646ac-153">Hola **codificar un activo** ventana, procesador "Media Encoder" estándar"hello select y un valor preestablecido.</span><span class="sxs-lookup"><span data-stu-id="646ac-153">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="646ac-154">Para más información acerca de los valores preestablecidos, consulte [Generación automática de una escalera de velocidad de bits](media-services-autogen-bitrate-ladder-with-mes.md) y [Valores preestablecidos de tarea para MES](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="646ac-154">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="646ac-155">Si tiene previsto toocontrol se utiliza el valor predeterminado de codificación, Téngalo en cuenta: es importante tooselect Hola preestablecido que sea más adecuado para el vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="646ac-155">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="646ac-156">Por ejemplo, si sabe que el vídeo de entrada tiene una resolución de 1920 x 1080 píxeles, a continuación, podría utilizar Hola "H264 1080p de velocidad de bits múltiple" preestablecido.</span><span class="sxs-lookup"><span data-stu-id="646ac-156">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="646ac-157">Si tiene un vídeo de baja resolución (640 x 360), no debería utilizar el valor preestablecido "H264 Multiple Bitrate 1080p".</span><span class="sxs-lookup"><span data-stu-id="646ac-157">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="646ac-158">Para facilitar la administración, tendrá una opción de edición nombre Hola de recurso de salida de hello y nombre de Hola de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="646ac-158">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![Codificación de recursos](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="646ac-160">Pulse **Crear**.</span><span class="sxs-lookup"><span data-stu-id="646ac-160">Press **Create**.</span></span>

### <a name="monitor-encoding-job-progress"></a><span data-ttu-id="646ac-161">Supervisión del progreso del trabajo de codificación</span><span class="sxs-lookup"><span data-stu-id="646ac-161">Monitor encoding job progress</span></span>
<span data-ttu-id="646ac-162">progreso de hello toomonitor de hello codificación de trabajo, haga clic en **configuración** (al principio de Hola de página de hello) y, a continuación, seleccione **trabajos**.</span><span class="sxs-lookup"><span data-stu-id="646ac-162">toomonitor hello progress of hello encoding job, click **Settings** (at hello top of hello page) and then select **Jobs**.</span></span>

![Trabajos](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a><span data-ttu-id="646ac-164">Publicación de contenido</span><span class="sxs-lookup"><span data-stu-id="646ac-164">Publish content</span></span>
<span data-ttu-id="646ac-165">tooprovide el usuario con una dirección URL que puede ser toostream usado o descargar el contenido, primero necesita demasiado "publicar" su activo mediante la creación de un localizador.</span><span class="sxs-lookup"><span data-stu-id="646ac-165">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="646ac-166">Los localizadores proporcionan toofiles de acceso que contiene el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="646ac-166">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="646ac-167">Media Services admite dos tipos de localizadores:</span><span class="sxs-lookup"><span data-stu-id="646ac-167">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="646ac-168">Transmisión por secuencias localizadores (OnDemandOrigin), que se usan para streaming adaptable (por ejemplo, toostream MPEG DASH, HLS o Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="646ac-168">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="646ac-169">toocreate un localizador de streaming el activo debe contener un archivo .ism.</span><span class="sxs-lookup"><span data-stu-id="646ac-169">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="646ac-170">Localizadores (SAS) progresivos, utilizados para la entrega de vídeo mediante descarga progresiva.</span><span class="sxs-lookup"><span data-stu-id="646ac-170">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="646ac-171">Una dirección URL de streaming tiene Hola siguiendo el formato y se pueden usar recursos de Smooth Streaming tooplay.</span><span class="sxs-lookup"><span data-stu-id="646ac-171">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="646ac-172">Anexar toobuild una transmisión por secuencias de dirección URL, de HLS (formato = m3u8-aapl) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="646ac-172">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="646ac-173">Anexar toobuild una dirección URL de streaming de MPEG DASH (formato = mpd: tiempo-csf) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="646ac-173">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="646ac-174">Una dirección URL SAS tiene Hola siguiendo el formato.</span><span class="sxs-lookup"><span data-stu-id="646ac-174">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> <span data-ttu-id="646ac-175">Si utiliza los localizadores de hello toocreate portal antes de marzo de 2015, se crearon localizadores con una fecha de expiración de dos años.</span><span class="sxs-lookup"><span data-stu-id="646ac-175">If you used hello portal toocreate locators before March 2015, locators with a two-year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="646ac-176">tooupdate una fecha de caducidad en un localizador, utilice [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) o [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API.</span><span class="sxs-lookup"><span data-stu-id="646ac-176">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="646ac-177">Cuando se actualiza la fecha de expiración de Hola de un localizador SAS, cambia la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="646ac-177">When you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="646ac-178">toouse Hola portal toopublish un activo</span><span class="sxs-lookup"><span data-stu-id="646ac-178">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="646ac-179">toouse Hola portal toopublish un activo, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="646ac-179">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="646ac-180">Seleccione **Configuración** > **Activos**.</span><span class="sxs-lookup"><span data-stu-id="646ac-180">Select **Settings** > **Assets**.</span></span>
2. <span data-ttu-id="646ac-181">Seleccione activo de Hola que desea toopublish.</span><span class="sxs-lookup"><span data-stu-id="646ac-181">Select hello asset that you want toopublish.</span></span>
3. <span data-ttu-id="646ac-182">Haga clic en hello **publicar** botón.</span><span class="sxs-lookup"><span data-stu-id="646ac-182">Click hello **Publish** button.</span></span>
4. <span data-ttu-id="646ac-183">Seleccione el tipo de localizador de Hola.</span><span class="sxs-lookup"><span data-stu-id="646ac-183">Select hello locator type.</span></span>
5. <span data-ttu-id="646ac-184">Presione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="646ac-184">Press **Add**.</span></span>
   
    ![Publicar](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="646ac-186">dirección URL de Hola se agrega la lista de toohello de **publicado direcciones URL**.</span><span class="sxs-lookup"><span data-stu-id="646ac-186">hello URL is added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="646ac-187">Reproducir contenido del portal de Hola</span><span class="sxs-lookup"><span data-stu-id="646ac-187">Play content from hello portal</span></span>
<span data-ttu-id="646ac-188">Hello portal de Azure proporciona un Reproductor de contenido que se puede usar tootest el vídeo.</span><span class="sxs-lookup"><span data-stu-id="646ac-188">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="646ac-189">Haga clic en vídeo de hello deseado y, a continuación, haga clic en hello **reproducir** botón.</span><span class="sxs-lookup"><span data-stu-id="646ac-189">Click hello desired video and then click hello **Play** button.</span></span>

![Publicar](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="646ac-191">Se aplican algunas consideraciones:</span><span class="sxs-lookup"><span data-stu-id="646ac-191">Some considerations apply:</span></span>

* <span data-ttu-id="646ac-192">toobegin transmisión por secuencias, iniciar la ejecución hello **predeterminado** extremo de streaming.</span><span class="sxs-lookup"><span data-stu-id="646ac-192">toobegin streaming, start running hello **default** streaming endpoint.</span></span>
* <span data-ttu-id="646ac-193">Asegúrese de que se ha publicado Hola vídeo.</span><span class="sxs-lookup"><span data-stu-id="646ac-193">Make sure hello video has been published.</span></span>
* <span data-ttu-id="646ac-194">Esto **Reproductor** reproduce desde predeterminado Hola extremo de streaming.</span><span class="sxs-lookup"><span data-stu-id="646ac-194">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="646ac-195">Si desea que tooplay de un valor no predeterminado del origen, haga clic en la dirección URL de hello toocopy y utilice otro reproductor.</span><span class="sxs-lookup"><span data-stu-id="646ac-195">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="646ac-196">Por ejemplo, [Reproductor de Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="646ac-196">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="646ac-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="646ac-197">Next steps</span></span>
<span data-ttu-id="646ac-198">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="646ac-198">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="646ac-199">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="646ac-199">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

