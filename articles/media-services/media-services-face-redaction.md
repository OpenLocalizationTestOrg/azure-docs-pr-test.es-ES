---
title: "aaaRedact caras con análisis de multimedia de Azure | Documentos de Microsoft"
description: "Este tema muestra cómo se enfrenta a tooredact con análisis de multimedia de Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="403f8-103">Censura de rostros con Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="403f8-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="403f8-104">Información general</span><span class="sxs-lookup"><span data-stu-id="403f8-104">Overview</span></span>
<span data-ttu-id="403f8-105">**Redactor de Azure Media** es un [análisis de multimedia de Azure](media-services-analytics-overview.md) procesador multimedia (MP) que ofrece la redacción de cara escalable en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="403f8-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="403f8-106">Redacción de cara permite toomodify el vídeo en caras de tooblur de orden de los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="403f8-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="403f8-107">Puede desear toouse Hola el servicio de redacción de cara en escenarios de seguridad y medios de noticias públicos.</span><span class="sxs-lookup"><span data-stu-id="403f8-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="403f8-108">Unos pocos minutos después de material de archivo que contiene varios tipos pueden tardar horas tooredact manualmente, pero con esta imagen de hello servicio proceso de redacción requiere unos pocos pasos sencillos.</span><span class="sxs-lookup"><span data-stu-id="403f8-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="403f8-109">Para más información, consulte [este blog](https://azure.microsoft.com/blog/azure-media-redactor/).</span><span class="sxs-lookup"><span data-stu-id="403f8-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="403f8-110">Este tema proporciona detalles acerca de **Redactor de multimedia de Azure** y muestra cómo toouse con el SDK de servicios multimedia para. NET.</span><span class="sxs-lookup"><span data-stu-id="403f8-110">This topic gives details about **Azure Media Redactor** and shows how toouse it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="403f8-111">Hola **Redactor de multimedia de Azure** MP está actualmente en vista previa.</span><span class="sxs-lookup"><span data-stu-id="403f8-111">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="403f8-112">Está disponible en todas las regiones de Azure públicas, así como en los centros de datos de China y el gobierno de Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="403f8-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="403f8-113">Actualmente, esta versión preliminar es gratuita.</span><span class="sxs-lookup"><span data-stu-id="403f8-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="403f8-114">Modos de censura de rostros</span><span class="sxs-lookup"><span data-stu-id="403f8-114">Face redaction modes</span></span>
<span data-ttu-id="403f8-115">Redacción facial funciona mediante la detección de caras en cada fotograma de vídeo y seguimiento cara Hola objeto tanto hacia delante y hacia atrás en el tiempo, para que hello misma persona puede ser borrosa desde otros ángulos así.</span><span class="sxs-lookup"><span data-stu-id="403f8-115">Facial redaction works by detecting faces in every frame of video and tracking hello face object both forwards and backwards in time, so that hello same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="403f8-116">Hola proceso automatizado de redacción es muy compleja y no genera siempre el 100% del resultado deseado, por este motivo que análisis multimedia proporciona con un par de formas de obtener el resultado final hello toomodify.</span><span class="sxs-lookup"><span data-stu-id="403f8-116">hello automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways toomodify hello final output.</span></span>

<span data-ttu-id="403f8-117">En suma tooa totalmente el modo automático, hay un flujo de trabajo de dos pasos que permite Hola selección/desinstalación-selection de caras se encuentra a través de una lista de identificadores.</span><span class="sxs-lookup"><span data-stu-id="403f8-117">In addition tooa fully automatic mode, there is a two-pass workflow which allows hello selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="403f8-118">Además, toomake arbitrario por Hola de ajustes de marco MP usa un archivo de metadatos en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="403f8-118">Also, toomake arbitrary per frame adjustments hello MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="403f8-119">Este flujo de trabajo se divide en los modos **Analyze** (Analizar) y **Redact** (Censurar).</span><span class="sxs-lookup"><span data-stu-id="403f8-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="403f8-120">Puede combinar los dos modos de hello en un único paso que ejecuta dos tareas en un trabajo; este modo se denomina **Combined**.</span><span class="sxs-lookup"><span data-stu-id="403f8-120">You can combine hello two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="403f8-121">Modo combinado</span><span class="sxs-lookup"><span data-stu-id="403f8-121">Combined mode</span></span>
<span data-ttu-id="403f8-122">Se generará un mp4 censurado automáticamente sin necesidad de intervención manual.</span><span class="sxs-lookup"><span data-stu-id="403f8-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="403f8-123">Fase</span><span class="sxs-lookup"><span data-stu-id="403f8-123">Stage</span></span> | <span data-ttu-id="403f8-124">Nombre de archivo</span><span class="sxs-lookup"><span data-stu-id="403f8-124">File Name</span></span> | <span data-ttu-id="403f8-125">Notas</span><span class="sxs-lookup"><span data-stu-id="403f8-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="403f8-126">Recurso de entrada</span><span class="sxs-lookup"><span data-stu-id="403f8-126">Input asset</span></span> |<span data-ttu-id="403f8-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="403f8-127">foo.bar</span></span> |<span data-ttu-id="403f8-128">Vídeo en formato WMV, MOV o MP4</span><span class="sxs-lookup"><span data-stu-id="403f8-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="403f8-129">Configuración de entrada</span><span class="sxs-lookup"><span data-stu-id="403f8-129">Input config</span></span> |<span data-ttu-id="403f8-130">Configuración predeterminada de trabajo</span><span class="sxs-lookup"><span data-stu-id="403f8-130">Job configuration preset</span></span> |<span data-ttu-id="403f8-131">{'version':'1.0', 'options': {'mode':'combined'}}</span><span class="sxs-lookup"><span data-stu-id="403f8-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="403f8-132">Recurso de salida</span><span class="sxs-lookup"><span data-stu-id="403f8-132">Output asset</span></span> |<span data-ttu-id="403f8-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="403f8-133">foo_redacted.mp4</span></span> |<span data-ttu-id="403f8-134">Vídeo con difuminado aplicado</span><span class="sxs-lookup"><span data-stu-id="403f8-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="403f8-135">Ejemplo de entrada:</span><span class="sxs-lookup"><span data-stu-id="403f8-135">Input example:</span></span>
[<span data-ttu-id="403f8-136">Vea este vídeo</span><span class="sxs-lookup"><span data-stu-id="403f8-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="403f8-137">Ejemplo de salida:</span><span class="sxs-lookup"><span data-stu-id="403f8-137">Output example:</span></span>
[<span data-ttu-id="403f8-138">Vea este vídeo</span><span class="sxs-lookup"><span data-stu-id="403f8-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="403f8-139">Modo Analyze (Análisis)</span><span class="sxs-lookup"><span data-stu-id="403f8-139">Analyze mode</span></span>
<span data-ttu-id="403f8-140">Hola **analizar** paso del flujo de trabajo de dos pasos Hola toma una entrada de vídeo y genera un archivo JSON de ubicaciones de cara y jpg imágenes de cada detectan cara.</span><span class="sxs-lookup"><span data-stu-id="403f8-140">hello **analyze** pass of hello two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="403f8-141">Fase</span><span class="sxs-lookup"><span data-stu-id="403f8-141">Stage</span></span> | <span data-ttu-id="403f8-142">Nombre de archivo</span><span class="sxs-lookup"><span data-stu-id="403f8-142">File Name</span></span> | <span data-ttu-id="403f8-143">Notas</span><span class="sxs-lookup"><span data-stu-id="403f8-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="403f8-144">Recurso de entrada</span><span class="sxs-lookup"><span data-stu-id="403f8-144">Input asset</span></span> |<span data-ttu-id="403f8-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="403f8-145">foo.bar</span></span> |<span data-ttu-id="403f8-146">Vídeo en formato WMV, MOV o MP4</span><span class="sxs-lookup"><span data-stu-id="403f8-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="403f8-147">Configuración de entrada</span><span class="sxs-lookup"><span data-stu-id="403f8-147">Input config</span></span> |<span data-ttu-id="403f8-148">Configuración predeterminada de trabajo</span><span class="sxs-lookup"><span data-stu-id="403f8-148">Job configuration preset</span></span> |<span data-ttu-id="403f8-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span><span class="sxs-lookup"><span data-stu-id="403f8-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="403f8-150">Recurso de salida</span><span class="sxs-lookup"><span data-stu-id="403f8-150">Output asset</span></span> |<span data-ttu-id="403f8-151">foo_annotations.JSON</span><span class="sxs-lookup"><span data-stu-id="403f8-151">foo_annotations.json</span></span> |<span data-ttu-id="403f8-152">Datos de anotación de ubicaciones de rostros en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="403f8-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="403f8-153">Esto se puede editar mediante Hola usuario toomodify Hola de desenfoque cuadros de límite.</span><span class="sxs-lookup"><span data-stu-id="403f8-153">This can be edited by hello user toomodify hello blurring bounding boxes.</span></span> <span data-ttu-id="403f8-154">Vea el ejemplo a continuación.</span><span class="sxs-lookup"><span data-stu-id="403f8-154">See sample below.</span></span> |
| <span data-ttu-id="403f8-155">Recurso de salida</span><span class="sxs-lookup"><span data-stu-id="403f8-155">Output asset</span></span> |<span data-ttu-id="403f8-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="403f8-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="403f8-157">Un jpg recortado de cada detectado cara, donde el número de hello indica labelId Hola de cara de Hola</span><span class="sxs-lookup"><span data-stu-id="403f8-157">A cropped jpg of each detected face, where hello number indicates hello labelId of hello face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="403f8-158">Ejemplo de salida:</span><span class="sxs-lookup"><span data-stu-id="403f8-158">Output example:</span></span>

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a><span data-ttu-id="403f8-159">Modo Redact (Censurar)</span><span class="sxs-lookup"><span data-stu-id="403f8-159">Redact mode</span></span>
<span data-ttu-id="403f8-160">segundo pase de Hola de flujo de trabajo de hello tiene un mayor número de entradas que deben combinarse en un solo activo.</span><span class="sxs-lookup"><span data-stu-id="403f8-160">hello second pass of hello workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="403f8-161">Esto incluye una lista de identificadores de tooblur, vídeo original de Hola y anotaciones Hola JSON.</span><span class="sxs-lookup"><span data-stu-id="403f8-161">This includes a list of IDs tooblur, hello original video, and hello annotations JSON.</span></span> <span data-ttu-id="403f8-162">Este modo utiliza Hola anotaciones tooapply desenfoque en vídeo de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="403f8-162">This mode uses hello annotations tooapply blurring on hello input video.</span></span>

<span data-ttu-id="403f8-163">salida de paso de analizar Hola Hello no incluye la vídeo original de Hola.</span><span class="sxs-lookup"><span data-stu-id="403f8-163">hello output from hello Analyze pass does not include hello original video.</span></span> <span data-ttu-id="403f8-164">Hola vídeo debe toobe cargado en el recurso de entrada de hello para la tarea de modo de hello Redact y seleccionado como archivo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="403f8-164">hello video needs toobe uploaded into hello input asset for hello Redact mode task and selected as hello primary file.</span></span>

| <span data-ttu-id="403f8-165">Fase</span><span class="sxs-lookup"><span data-stu-id="403f8-165">Stage</span></span> | <span data-ttu-id="403f8-166">Nombre de archivo</span><span class="sxs-lookup"><span data-stu-id="403f8-166">File Name</span></span> | <span data-ttu-id="403f8-167">Notas</span><span class="sxs-lookup"><span data-stu-id="403f8-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="403f8-168">Recurso de entrada</span><span class="sxs-lookup"><span data-stu-id="403f8-168">Input asset</span></span> |<span data-ttu-id="403f8-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="403f8-169">foo.bar</span></span> |<span data-ttu-id="403f8-170">Vídeo en formato WMV, MOV o MP4.</span><span class="sxs-lookup"><span data-stu-id="403f8-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="403f8-171">El mismo vídeo que en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="403f8-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="403f8-172">Recurso de entrada</span><span class="sxs-lookup"><span data-stu-id="403f8-172">Input asset</span></span> |<span data-ttu-id="403f8-173">foo_annotations.JSON</span><span class="sxs-lookup"><span data-stu-id="403f8-173">foo_annotations.json</span></span> |<span data-ttu-id="403f8-174">archivo de metadatos de anotaciones de la fase uno, con modificaciones opcionales.</span><span class="sxs-lookup"><span data-stu-id="403f8-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="403f8-175">Recurso de entrada</span><span class="sxs-lookup"><span data-stu-id="403f8-175">Input asset</span></span> |<span data-ttu-id="403f8-176">foo_IDList.txt (opcional)</span><span class="sxs-lookup"><span data-stu-id="403f8-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="403f8-177">Nueva línea opcional lista separada de cara tooredact de identificadores.</span><span class="sxs-lookup"><span data-stu-id="403f8-177">Optional new line separated list of face IDs tooredact.</span></span> <span data-ttu-id="403f8-178">Si se deja en blanco, se difuminarán todas las caras.</span><span class="sxs-lookup"><span data-stu-id="403f8-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="403f8-179">Configuración de entrada</span><span class="sxs-lookup"><span data-stu-id="403f8-179">Input config</span></span> |<span data-ttu-id="403f8-180">Configuración predeterminada de trabajo</span><span class="sxs-lookup"><span data-stu-id="403f8-180">Job configuration preset</span></span> |<span data-ttu-id="403f8-181">{'version':'1.0', 'options': {'mode':'analyze'}}</span><span class="sxs-lookup"><span data-stu-id="403f8-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="403f8-182">Recurso de salida</span><span class="sxs-lookup"><span data-stu-id="403f8-182">Output asset</span></span> |<span data-ttu-id="403f8-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="403f8-183">foo_redacted.mp4</span></span> |<span data-ttu-id="403f8-184">Vídeo con difuminado aplicado en base a las anotaciones</span><span class="sxs-lookup"><span data-stu-id="403f8-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="403f8-185">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="403f8-185">Example output</span></span>
<span data-ttu-id="403f8-186">Este es el resultado de hello desde un Lista_id con un Id. de seleccionado.</span><span class="sxs-lookup"><span data-stu-id="403f8-186">This is hello output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="403f8-187">Vea este vídeo</span><span class="sxs-lookup"><span data-stu-id="403f8-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="403f8-188">foo_IDList.txt de ejemplo</span><span class="sxs-lookup"><span data-stu-id="403f8-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="403f8-189">Tipos de desenfoque</span><span class="sxs-lookup"><span data-stu-id="403f8-189">Blur types</span></span>

<span data-ttu-id="403f8-190">Hola **Combined** o **Redact** modo, hay 5 modos desenfoque diferentes posibles a través de la configuración de entrada de JSON de hello: **bajo**, **Med**, **Alta**, **depurar**, y **negro**.</span><span class="sxs-lookup"><span data-stu-id="403f8-190">In hello **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via hello JSON input configuration: **Low**, **Med**, **High**, **Debug**, and **Black**.</span></span> <span data-ttu-id="403f8-191">Se usa **Medio** de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="403f8-191">By default **Med** is used.</span></span>

<span data-ttu-id="403f8-192">Puede encontrar ejemplos de hello desenfoque tipos siguiente.</span><span class="sxs-lookup"><span data-stu-id="403f8-192">You can find samples of hello blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="403f8-193">Ejemplo de JSON:</span><span class="sxs-lookup"><span data-stu-id="403f8-193">Example JSON:</span></span>

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a><span data-ttu-id="403f8-194">Bajo</span><span class="sxs-lookup"><span data-stu-id="403f8-194">Low</span></span>

![Bajo](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="403f8-196">Medio</span><span class="sxs-lookup"><span data-stu-id="403f8-196">Med</span></span>

![Medio](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="403f8-198">Alto</span><span class="sxs-lookup"><span data-stu-id="403f8-198">High</span></span>

![Alto](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a><span data-ttu-id="403f8-200">Depurar</span><span class="sxs-lookup"><span data-stu-id="403f8-200">Debug</span></span>

![Depurar](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="403f8-202">Negro</span><span class="sxs-lookup"><span data-stu-id="403f8-202">Black</span></span>

![Negro](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="403f8-204">Elementos Hola JSON del archivo de salida</span><span class="sxs-lookup"><span data-stu-id="403f8-204">Elements of hello output JSON file</span></span>

<span data-ttu-id="403f8-205">Hola MP de redacción proporciona detección de ubicación de cara de alta precisión y el seguimiento que puede detectar una too64 caras humana en un fotograma de vídeo.</span><span class="sxs-lookup"><span data-stu-id="403f8-205">hello Redaction MP provides high precision face location detection and tracking that can detect up too64 human faces in a video frame.</span></span> <span data-ttu-id="403f8-206">Caras frontales proporcionan Hola los mejores resultados, mientras caras laterales y caras pequeñas (menor que o igual a too24x24 píxeles) son un desafío.</span><span class="sxs-lookup"><span data-stu-id="403f8-206">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="403f8-207">Código de ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="403f8-207">.NET sample code</span></span>

<span data-ttu-id="403f8-208">siguiente de Hello programa muestra cómo:</span><span class="sxs-lookup"><span data-stu-id="403f8-208">hello following program shows how to:</span></span>

1. <span data-ttu-id="403f8-209">Crear un activo y cargar un archivo multimedia en activo de Hola.</span><span class="sxs-lookup"><span data-stu-id="403f8-209">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="403f8-210">Crear un trabajo con una tarea de redacción de cara basada en un archivo de configuración que contiene el siguiente valor preestablecido de json de Hola.</span><span class="sxs-lookup"><span data-stu-id="403f8-210">Create a job with a face redaction task based on a configuration file that contains hello following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="403f8-211">Descargar archivos de hello salida JSON.</span><span class="sxs-lookup"><span data-stu-id="403f8-211">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="403f8-212">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="403f8-212">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="403f8-213">Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="403f8-213">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="403f8-214">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="403f8-214">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceRedaction
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

            // Use hello following event handler toocheck job progress.  
            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch hello job.
            job.Submit();

            // Check job execution and wait for job toofinish.
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

            progressJobTask.Wait();

            // If job state is Error, hello event handling
            // method for job progress should log errors.  Here we check
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
            ErrorDetail error = job.Tasks.First().ErrorDetails.First();
            Console.WriteLine(string.Format("Error: {0}. {1}",
                            error.Code,
                            error.Message));
            return null;
            }

            return job.OutputMediaAssets[0];
        }

        static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
        {
            IAsset asset = _context.Assets.Create(assetName, options);

            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);

            return asset;
        }

        static void DownloadAsset(IAsset asset, string outputDirectory)
        {
            foreach (IAssetFile file in asset.AssetFiles)
            {
            file.Download(Path.Combine(outputDirectory, file.Name));
            }
        }

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

        static private void StateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);

            switch (e.CurrentState)
            {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished.");
                Console.WriteLine();
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
            case JobState.Error:
                // Cast sender as a job.
                IJob job = (IJob)sender;
                // Display or log error details as needed.
                // LogJobStop(job.Id);
                break;
            default:
                break;
            }
        }
        }
    }

## <a name="next-steps"></a><span data-ttu-id="403f8-215">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="403f8-215">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="403f8-216">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="403f8-216">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="403f8-217">Vínculos relacionados</span><span class="sxs-lookup"><span data-stu-id="403f8-217">Related links</span></span>
[<span data-ttu-id="403f8-218">Azure Media Services Analytics Overview (Información general sobre análisis de Servicios multimedia de Azure)</span><span class="sxs-lookup"><span data-stu-id="403f8-218">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="403f8-219">Demostraciones de Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="403f8-219">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

