---
title: "Introducción a la entrega de VoD mediante Azure Portal | Microsoft Docs"
description: "Este tutorial le guiará por los pasos necesarios para implementar un servicio básico de entrega de contenido de vídeo bajo demanda (VoD) con la aplicación de Azure Media Services (AMS) mediante Azure Portal."
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
ms.openlocfilehash: a8eeeeff412837acba14b441a3c590edf7e3597a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-the-azure-portal"></a><span data-ttu-id="5fd69-103">Introducción a la entrega de contenido a petición mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5fd69-103">Get started with delivering content on demand using the Azure portal</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="5fd69-104">Este tutorial le guiará por los pasos necesarios para implementar un servicio básico de entrega de contenido de vídeo bajo demanda (VoD) con la aplicación de Azure Media Services (AMS) mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5fd69-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fd69-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5fd69-105">Prerequisites</span></span>
<span data-ttu-id="5fd69-106">Estos son los requisitos previos para completar el tutorial.</span><span class="sxs-lookup"><span data-stu-id="5fd69-106">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="5fd69-107">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="5fd69-107">An Azure account.</span></span> <span data-ttu-id="5fd69-108">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5fd69-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="5fd69-109">Una cuenta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="5fd69-109">A Media Services account.</span></span> <span data-ttu-id="5fd69-110">Para crear una cuenta de Media Services, consulte el tema [Creación de una cuenta de Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="5fd69-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="5fd69-111">Este tutorial incluye las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="5fd69-111">This tutorial includes the following tasks:</span></span>

1. <span data-ttu-id="5fd69-112">Inicie el punto de conexión de streaming.</span><span class="sxs-lookup"><span data-stu-id="5fd69-112">Start streaming endpoint.</span></span>
2. <span data-ttu-id="5fd69-113">Carga de un archivo de vídeo.</span><span class="sxs-lookup"><span data-stu-id="5fd69-113">Upload a video file.</span></span>
3. <span data-ttu-id="5fd69-114">Codificación del archivo de origen en un conjunto de archivos MP4 de velocidad de bits adaptativa</span><span class="sxs-lookup"><span data-stu-id="5fd69-114">Encode the source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="5fd69-115">Publicación del recurso y obtención de direcciones URL de descarga progresiva y streaming.</span><span class="sxs-lookup"><span data-stu-id="5fd69-115">Publish the asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="5fd69-116">Reproduzca el contenido.</span><span class="sxs-lookup"><span data-stu-id="5fd69-116">Play your content.</span></span>

## <a name="start-streaming-endpoints"></a><span data-ttu-id="5fd69-117">Inicio de los puntos de conexión de streaming</span><span class="sxs-lookup"><span data-stu-id="5fd69-117">Start streaming endpoints</span></span> 

<span data-ttu-id="5fd69-118">Cuando se trabaja con Azure Media Services, uno de los escenarios más comunes es entregar contenido de vídeo a los clientes mediante streaming con velocidad de bits adaptable.</span><span class="sxs-lookup"><span data-stu-id="5fd69-118">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="5fd69-119">Media Services proporciona empaquetado dinámico que permite entregar contenido codificado MP4 con velocidad de bits adaptable en formatos de streaming admitidos por Media Services (MPEG DASH, HLS, Smooth Streaming) justo a tiempo, sin tener que almacenar versiones previamente empaquetadas de cada uno de estos formatos.</span><span class="sxs-lookup"><span data-stu-id="5fd69-119">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="5fd69-120">Cuando se crea la cuenta de AMS, se agrega un punto de conexión de streaming **predeterminado** a la cuenta en estado **Stopped** (Detenido).</span><span class="sxs-lookup"><span data-stu-id="5fd69-120">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="5fd69-121">Para iniciar la transmisión del contenido y aprovechar el empaquetado dinámico y el cifrado dinámico, el punto de conexión de streaming desde el que va a transmitir el contenido debe estar en estado **Running** (En ejecución).</span><span class="sxs-lookup"><span data-stu-id="5fd69-121">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

<span data-ttu-id="5fd69-122">Para iniciar el punto de conexión de streaming, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5fd69-122">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="5fd69-123">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5fd69-123">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5fd69-124">En la ventana Settings (Configuración), haga clic en Streaming endpoints (Puntos de conexión de streaming).</span><span class="sxs-lookup"><span data-stu-id="5fd69-124">In the Settings window, click Streaming endpoints.</span></span> 
3. <span data-ttu-id="5fd69-125">Haga clic en el punto de conexión de streaming predeterminado.</span><span class="sxs-lookup"><span data-stu-id="5fd69-125">Click the default streaming endpoint.</span></span> 

    <span data-ttu-id="5fd69-126">Aparecerá la ventana de detalles del punto de conexión de streaming predeterminado.</span><span class="sxs-lookup"><span data-stu-id="5fd69-126">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="5fd69-127">Haga clic en el icono de inicio.</span><span class="sxs-lookup"><span data-stu-id="5fd69-127">Click the Start icon.</span></span>
5. <span data-ttu-id="5fd69-128">Haga clic en el botón Save (Guardar) para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="5fd69-128">Click the Save button to save your changes.</span></span>

## <a name="upload-files"></a><span data-ttu-id="5fd69-129">Carga de archivos</span><span class="sxs-lookup"><span data-stu-id="5fd69-129">Upload files</span></span>
<span data-ttu-id="5fd69-130">Para transmitir vídeos mediante Azure Media Services, es preciso cargar los vídeos de origen, codificarlos en varias velocidades de bits y publicar el resultado.</span><span class="sxs-lookup"><span data-stu-id="5fd69-130">To stream videos using Azure Media Services, you need to upload the source videos, encode them into multiple bitrates, and publish the result.</span></span> <span data-ttu-id="5fd69-131">En esta sección se describe el primer paso.</span><span class="sxs-lookup"><span data-stu-id="5fd69-131">The first step is covered in this section.</span></span> 

1. <span data-ttu-id="5fd69-132">En la ventana **Configuración**, haga clic en **Activos**.</span><span class="sxs-lookup"><span data-stu-id="5fd69-132">In the **Setting** window, click **Assets**.</span></span>
   
    ![Carga de archivos](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. <span data-ttu-id="5fd69-134">Haga clic en el botón **Upload** .</span><span class="sxs-lookup"><span data-stu-id="5fd69-134">Click the **Upload** button.</span></span>
   
    <span data-ttu-id="5fd69-135">Aparecerá la ventana **Upload a video asset** (Cargar un recurso de vídeo).</span><span class="sxs-lookup"><span data-stu-id="5fd69-135">The **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5fd69-136">No hay ninguna limitación de tamaño de archivo.</span><span class="sxs-lookup"><span data-stu-id="5fd69-136">There is no file size limitation.</span></span>
   > 
   > 
3. <span data-ttu-id="5fd69-137">Busque el vídeo deseado en su equipo, selecciónelo y haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="5fd69-137">Browse to the desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="5fd69-138">La carga se inicia y puede ver el progreso en el nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="5fd69-138">The upload starts and you can see the progress under the file name.</span></span>  

<span data-ttu-id="5fd69-139">Una vez que la carga se haya completado, verá el nuevo recurso en la ventana **Activos** .</span><span class="sxs-lookup"><span data-stu-id="5fd69-139">Once the upload completes, you see the new asset listed in the **Assets** window.</span></span> 

## <a name="encode-assets"></a><span data-ttu-id="5fd69-140">Codificación de recursos</span><span class="sxs-lookup"><span data-stu-id="5fd69-140">Encode assets</span></span>

<span data-ttu-id="5fd69-141">Cuando se trabaja con Azure Media Services, uno de los escenarios más comunes es entregar streaming de velocidad de bits adaptable a los clientes.</span><span class="sxs-lookup"><span data-stu-id="5fd69-141">When working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="5fd69-142">Media Services admite las siguientes tecnologías de streaming con velocidad de bits adaptable: HTTP Live Streaming (HLS), Smooth Streaming y MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="5fd69-142">Media Services supports the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="5fd69-143">Para preparar vídeos para streaming con velocidad de bits adaptable, debe codificar el vídeo de origen en archivos de varias velocidades de bits.</span><span class="sxs-lookup"><span data-stu-id="5fd69-143">To prepare your videos for adaptive bitrate streaming, you need to encode your source video into multi-bitrate files.</span></span> <span data-ttu-id="5fd69-144">Debe utilizar el **Codificador multimedia estándar** para codificar sus vídeos.</span><span class="sxs-lookup"><span data-stu-id="5fd69-144">You should use the **Media Encoder Standard** encoder to encode your videos.</span></span>  

<span data-ttu-id="5fd69-145">Media Services también proporciona empaquetado dinámico, que permite entregar archivos MP4 de velocidad de bits múltiple en los siguientes formatos de streaming: MPEG DASH, HLS o Smooth Streaming sin tener que volver a empaquetar en dichos formatos.</span><span class="sxs-lookup"><span data-stu-id="5fd69-145">Media Services also provides dynamic packaging, which allows you to deliver your multi-bitrate MP4s in the following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having to repackage into these streaming formats.</span></span> <span data-ttu-id="5fd69-146">Con el empaquetado dinámico, solo necesita almacenar y pagar por los archivos en formato de almacenamiento sencillo y Media Services creará y servirá la respuesta adecuada en función de las solicitudes del cliente.</span><span class="sxs-lookup"><span data-stu-id="5fd69-146">With dynamic packaging, you only need to store and pay for the files in single storage format and Media Services builds and serves the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="5fd69-147">Para sacar partido del empaquetado dinámico, tiene que codificar su archivo de origen en un conjunto de archivos MP4 de velocidad de bits múltiple (los pasos de codificación se muestran más adelante en esta sección).</span><span class="sxs-lookup"><span data-stu-id="5fd69-147">To take advantage of dynamic packaging, you need to encode your source file into a set of multi-bitrate MP4 files (the encoding steps are demonstrated later in this section).</span></span>

### <a name="to-use-the-portal-to-encode"></a><span data-ttu-id="5fd69-148">Uso del portal para codificar</span><span class="sxs-lookup"><span data-stu-id="5fd69-148">To use the portal to encode</span></span>
<span data-ttu-id="5fd69-149">En esta sección se describen los pasos que puede seguir para codificar el contenido con Estándar de codificador multimedia.</span><span class="sxs-lookup"><span data-stu-id="5fd69-149">This section describes the steps you can take to encode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="5fd69-150">En la ventana **Configuración**, seleccione **Activos**.</span><span class="sxs-lookup"><span data-stu-id="5fd69-150">In the **Settings** window, select **Assets**.</span></span>  
2. <span data-ttu-id="5fd69-151">En la ventana **Activos** , seleccione el recurso que desea codificar.</span><span class="sxs-lookup"><span data-stu-id="5fd69-151">In the **Assets** window, select the asset that you would like to encode.</span></span>
3. <span data-ttu-id="5fd69-152">Presione el botón **Codificar** .</span><span class="sxs-lookup"><span data-stu-id="5fd69-152">Press the **Encode** button.</span></span>
4. <span data-ttu-id="5fd69-153">En la ventana **Encode an asset** (Codificar un recurso), seleccione el procesador "Codificador multimedia estándar" y un valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="5fd69-153">In the **Encode an asset** window, select the "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="5fd69-154">Para más información acerca de los valores preestablecidos, consulte [Generación automática de una escalera de velocidad de bits](media-services-autogen-bitrate-ladder-with-mes.md) y [Valores preestablecidos de tarea para MES](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5fd69-154">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="5fd69-155">Si tiene previsto controlar qué valor preestablecido de codificación se usa, tenga en cuenta: es importante seleccionar el valor preestablecido más adecuado para la entrada de vídeo.</span><span class="sxs-lookup"><span data-stu-id="5fd69-155">If you plan to control which encoding preset is used, keep this in mind: it is important to select the preset that is most appropriate for your input video.</span></span> <span data-ttu-id="5fd69-156">Por ejemplo, si sabe que el vídeo de entrada tiene una resolución de 1920 x 1080 píxeles, se podría utilizar el valor predeterminado "H264 Multiple Bitrate 1080p".</span><span class="sxs-lookup"><span data-stu-id="5fd69-156">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use the "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="5fd69-157">Si tiene un vídeo de baja resolución (640 x 360), no debería utilizar el valor preestablecido "H264 Multiple Bitrate 1080p".</span><span class="sxs-lookup"><span data-stu-id="5fd69-157">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="5fd69-158">Para facilitar la administración, se puede editar el nombre del recurso de salida y el nombre del trabajo.</span><span class="sxs-lookup"><span data-stu-id="5fd69-158">For easier management, you have an option of editing the name of the output asset, and the name of the job.</span></span>
   
   ![Codificación de recursos](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="5fd69-160">Pulse **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5fd69-160">Press **Create**.</span></span>

### <a name="monitor-encoding-job-progress"></a><span data-ttu-id="5fd69-161">Supervisión del progreso del trabajo de codificación</span><span class="sxs-lookup"><span data-stu-id="5fd69-161">Monitor encoding job progress</span></span>
<span data-ttu-id="5fd69-162">Para supervisar el progreso del trabajo de codificación, haga clic en **Configuración** (en la parte superior de la página) y, después, seleccione **Trabajos**.</span><span class="sxs-lookup"><span data-stu-id="5fd69-162">To monitor the progress of the encoding job, click **Settings** (at the top of the page) and then select **Jobs**.</span></span>

![Trabajos](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a><span data-ttu-id="5fd69-164">Publicación de contenido</span><span class="sxs-lookup"><span data-stu-id="5fd69-164">Publish content</span></span>
<span data-ttu-id="5fd69-165">Para proporcionar al usuario una dirección URL que pueda utilizarse para transmitir o descargar su contenido, primero necesitará "publicar" su recurso mediante la creación de un localizador.</span><span class="sxs-lookup"><span data-stu-id="5fd69-165">To provide your user with a  URL that can be used to stream or download your content, you first need to "publish" your asset by creating a locator.</span></span> <span data-ttu-id="5fd69-166">Los localizadores proporcionan acceso a los archivos contenidos en el recurso.</span><span class="sxs-lookup"><span data-stu-id="5fd69-166">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="5fd69-167">Media Services admite dos tipos de localizadores:</span><span class="sxs-lookup"><span data-stu-id="5fd69-167">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="5fd69-168">Los localizadores de streaming (OnDemandOrigin), que se usan en el streaming adaptable (por ejemplo, para transmitir MPEG DASH, HLS o Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="5fd69-168">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, to stream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="5fd69-169">Para crear un localizador de streaming el recurso debe contener un archivo .ism.</span><span class="sxs-lookup"><span data-stu-id="5fd69-169">To create a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="5fd69-170">Localizadores (SAS) progresivos, utilizados para la entrega de vídeo mediante descarga progresiva.</span><span class="sxs-lookup"><span data-stu-id="5fd69-170">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="5fd69-171">Una dirección URL de streaming tiene el siguiente formato y se puede usar para reproducir los recursos de Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="5fd69-171">A streaming URL has the following format and you can use it to play Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="5fd69-172">Para generar una dirección URL de streaming de HLS, anexe (format=m3u8-aapl) a la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="5fd69-172">To build an HLS streaming URL, append (format=m3u8-aapl) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="5fd69-173">Para generar una dirección URL de streaming de MPEG DASH, anexe (format=mpd-time-csf) a la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="5fd69-173">To build an  MPEG DASH streaming URL, append (format=mpd-time-csf) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="5fd69-174">Una dirección URL de SAS tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="5fd69-174">A SAS URL has the following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> <span data-ttu-id="5fd69-175">Si usó el portal para crear localizadores antes de marzo de 2015, se crearon localizadores con una fecha de caducidad de dos años.</span><span class="sxs-lookup"><span data-stu-id="5fd69-175">If you used the portal to create locators before March 2015, locators with a two-year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="5fd69-176">Para actualizar la fecha de caducidad de un localizador, use las API de [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) o de [.NET](http://go.microsoft.com/fwlink/?LinkID=533259).</span><span class="sxs-lookup"><span data-stu-id="5fd69-176">To update an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="5fd69-177">Cuando se actualiza la fecha de caducidad de un localizador de SAS, cambia la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="5fd69-177">When you update the expiration date of a SAS locator, the URL changes.</span></span>

### <a name="to-use-the-portal-to-publish-an-asset"></a><span data-ttu-id="5fd69-178">Uso del portal para publicar un recurso</span><span class="sxs-lookup"><span data-stu-id="5fd69-178">To use the portal to publish an asset</span></span>
<span data-ttu-id="5fd69-179">Para usar el portal para publicar un recurso, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5fd69-179">To use the portal to publish an asset, do the following:</span></span>

1. <span data-ttu-id="5fd69-180">Seleccione **Configuración** > **Activos**.</span><span class="sxs-lookup"><span data-stu-id="5fd69-180">Select **Settings** > **Assets**.</span></span>
2. <span data-ttu-id="5fd69-181">Seleccione el recurso que desea publicar.</span><span class="sxs-lookup"><span data-stu-id="5fd69-181">Select the asset that you want to publish.</span></span>
3. <span data-ttu-id="5fd69-182">Haga clic en el botón **Publicar** .</span><span class="sxs-lookup"><span data-stu-id="5fd69-182">Click the **Publish** button.</span></span>
4. <span data-ttu-id="5fd69-183">Seleccione el tipo de localizador.</span><span class="sxs-lookup"><span data-stu-id="5fd69-183">Select the locator type.</span></span>
5. <span data-ttu-id="5fd69-184">Presione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5fd69-184">Press **Add**.</span></span>
   
    ![Publicar](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="5fd69-186">La dirección URL se agrega a la lista de **direcciones URL publicadas**.</span><span class="sxs-lookup"><span data-stu-id="5fd69-186">The URL is added to the list of **Published URLs**.</span></span>

## <a name="play-content-from-the-portal"></a><span data-ttu-id="5fd69-187">contenido desde el portal</span><span class="sxs-lookup"><span data-stu-id="5fd69-187">Play content from the portal</span></span>
<span data-ttu-id="5fd69-188">Azure Portal proporciona un reproductor de contenido que puede usar para probar el vídeo.</span><span class="sxs-lookup"><span data-stu-id="5fd69-188">The Azure portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="5fd69-189">Haga clic en el vídeo deseado y, luego, en el botón **Reproducir** .</span><span class="sxs-lookup"><span data-stu-id="5fd69-189">Click the desired video and then click the **Play** button.</span></span>

![Publicar](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="5fd69-191">Se aplican algunas consideraciones:</span><span class="sxs-lookup"><span data-stu-id="5fd69-191">Some considerations apply:</span></span>

* <span data-ttu-id="5fd69-192">Para iniciar el streaming, comience a ejecutar el punto de conexión de streaming **predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="5fd69-192">To begin streaming, start running the **default** streaming endpoint.</span></span>
* <span data-ttu-id="5fd69-193">Asegúrese de que se ha publicado el vídeo.</span><span class="sxs-lookup"><span data-stu-id="5fd69-193">Make sure the video has been published.</span></span>
* <span data-ttu-id="5fd69-194">**Media player** reproduce desde el punto de conexión de streaming predeterminado.</span><span class="sxs-lookup"><span data-stu-id="5fd69-194">This **Media player** plays from the default streaming endpoint.</span></span> <span data-ttu-id="5fd69-195">Si desea reproducir desde un punto de conexión de streaming que no esté predeterminado, haga clic para copiar la dirección URL y use otro reproductor.</span><span class="sxs-lookup"><span data-stu-id="5fd69-195">If you want to play from a non-default streaming endpoint, click to copy the URL and use another player.</span></span> <span data-ttu-id="5fd69-196">Por ejemplo, [Reproductor de Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="5fd69-196">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fd69-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5fd69-197">Next steps</span></span>
<span data-ttu-id="5fd69-198">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="5fd69-198">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5fd69-199">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="5fd69-199">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

