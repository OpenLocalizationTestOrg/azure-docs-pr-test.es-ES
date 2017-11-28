---
title: Censura de rostros con Azure Media Analytics | Microsoft Docs
description: "Este tema muestra cómo censurar caras con Análisis multimedia de Azure."
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
ms.openlocfilehash: 747f3ae1a7484515083c590942de3da22568cd39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="89183-103">Censura de rostros con Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="89183-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="89183-104">Información general</span><span class="sxs-lookup"><span data-stu-id="89183-104">Overview</span></span>
<span data-ttu-id="89183-105">**Redactor multimedia de Azure** es un procesador multimedia (MP) de [Análisis multimedia de Azure](media-services-analytics-overview.md) que ofrece censura de rostros escalable en la nube.</span><span class="sxs-lookup"><span data-stu-id="89183-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="89183-106">La censura de rostros le permite modificar un vídeo con el fin de difuminar las caras de personas seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="89183-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="89183-107">Puede usar el servicio de censura de rostros en escenarios de seguridad pública y de noticias en los medios de comunicación.</span><span class="sxs-lookup"><span data-stu-id="89183-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="89183-108">Unos minutos de material de archivo que contenga varias caras puede tardar horas en censurarse manualmente, pero con este servicio, el proceso de censura de caras requiere solamente unos pocos pasos sencillos.</span><span class="sxs-lookup"><span data-stu-id="89183-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="89183-109">Para más información, consulte [este blog](https://azure.microsoft.com/blog/azure-media-redactor/).</span><span class="sxs-lookup"><span data-stu-id="89183-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="89183-110">En este tema se proporcionan detalles sobre **Redactor multimedia de Azure** y se muestra cómo se usa con el SDK de Media Services para .NET.</span><span class="sxs-lookup"><span data-stu-id="89183-110">This topic gives details about **Azure Media Redactor** and shows how to use it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="89183-111">El procesador de multimedia **Redactor multimedia de Azure** está actualmente en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="89183-111">The **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="89183-112">Está disponible en todas las regiones de Azure públicas, así como en los centros de datos de China y el gobierno de Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="89183-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="89183-113">Actualmente, esta versión preliminar es gratuita.</span><span class="sxs-lookup"><span data-stu-id="89183-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="89183-114">Modos de censura de rostros</span><span class="sxs-lookup"><span data-stu-id="89183-114">Face redaction modes</span></span>
<span data-ttu-id="89183-115">La censura facial funciona detectando caras en cada fotograma de vídeo y realizando un seguimiento del objeto de cara tanto hacia delante como hacia atrás en el tiempo, para que la imagen de la misma persona pueda difuminarse también desde otros ángulos.</span><span class="sxs-lookup"><span data-stu-id="89183-115">Facial redaction works by detecting faces in every frame of video and tracking the face object both forwards and backwards in time, so that the same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="89183-116">El proceso de censura automatizada es muy complejo y no siempre genera los resultados deseados al 100 %, por este motivo, Análisis multimedia de Azure le ofrece un par de métodos para modificar el resultado final.</span><span class="sxs-lookup"><span data-stu-id="89183-116">The automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways to modify the final output.</span></span>

<span data-ttu-id="89183-117">Además de un modo totalmente automático, hay un flujo de trabajo de dos pasos que permite la selección y deselección de caras encontradas a través de una lista de identificadores.</span><span class="sxs-lookup"><span data-stu-id="89183-117">In addition to a fully automatic mode, there is a two-pass workflow which allows the selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="89183-118">Igualmente, para realizar ajustes arbitrarios por fotograma, el procesador multimedia utiliza un archivo de metadatos en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="89183-118">Also, to make arbitrary per frame adjustments the MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="89183-119">Este flujo de trabajo se divide en los modos **Analyze** (Analizar) y **Redact** (Censurar).</span><span class="sxs-lookup"><span data-stu-id="89183-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="89183-120">Puede combinar los dos modos en un único paso que ejecuta las tareas de un trabajo; este modo se denomina **Combinado**.</span><span class="sxs-lookup"><span data-stu-id="89183-120">You can combine the two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="89183-121">Modo combinado</span><span class="sxs-lookup"><span data-stu-id="89183-121">Combined mode</span></span>
<span data-ttu-id="89183-122">Se generará un mp4 censurado automáticamente sin necesidad de intervención manual.</span><span class="sxs-lookup"><span data-stu-id="89183-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="89183-123">Fase</span><span class="sxs-lookup"><span data-stu-id="89183-123">Stage</span></span> | <span data-ttu-id="89183-124">Nombre de archivo</span><span class="sxs-lookup"><span data-stu-id="89183-124">File Name</span></span> | <span data-ttu-id="89183-125">Notas</span><span class="sxs-lookup"><span data-stu-id="89183-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="89183-126">Recurso de entrada</span><span class="sxs-lookup"><span data-stu-id="89183-126">Input asset</span></span> |<span data-ttu-id="89183-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="89183-127">foo.bar</span></span> |<span data-ttu-id="89183-128">Vídeo en formato WMV, MOV o MP4</span><span class="sxs-lookup"><span data-stu-id="89183-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="89183-129">Configuración de entrada</span><span class="sxs-lookup"><span data-stu-id="89183-129">Input config</span></span> |<span data-ttu-id="89183-130">Configuración predeterminada de trabajo</span><span class="sxs-lookup"><span data-stu-id="89183-130">Job configuration preset</span></span> |<span data-ttu-id="89183-131">{'version':'1.0', 'options': {'mode':'combined'}}</span><span class="sxs-lookup"><span data-stu-id="89183-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="89183-132">Recurso de salida</span><span class="sxs-lookup"><span data-stu-id="89183-132">Output asset</span></span> |<span data-ttu-id="89183-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="89183-133">foo_redacted.mp4</span></span> |<span data-ttu-id="89183-134">Vídeo con difuminado aplicado</span><span class="sxs-lookup"><span data-stu-id="89183-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="89183-135">Ejemplo de entrada:</span><span class="sxs-lookup"><span data-stu-id="89183-135">Input example:</span></span>
[<span data-ttu-id="89183-136">Vea este vídeo</span><span class="sxs-lookup"><span data-stu-id="89183-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="89183-137">Ejemplo de salida:</span><span class="sxs-lookup"><span data-stu-id="89183-137">Output example:</span></span>
[<span data-ttu-id="89183-138">Vea este vídeo</span><span class="sxs-lookup"><span data-stu-id="89183-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="89183-139">Modo Analyze (Análisis)</span><span class="sxs-lookup"><span data-stu-id="89183-139">Analyze mode</span></span>
<span data-ttu-id="89183-140">El paso **analizar** del flujo de trabajo de dos pasos toma una entrada de vídeo y genera un archivo JSON de ubicaciones de rostros e imágenes jpg de cada rostro detectado.</span><span class="sxs-lookup"><span data-stu-id="89183-140">The **analyze** pass of the two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="89183-141">Fase</span><span class="sxs-lookup"><span data-stu-id="89183-141">Stage</span></span> | <span data-ttu-id="89183-142">Nombre de archivo</span><span class="sxs-lookup"><span data-stu-id="89183-142">File Name</span></span> | <span data-ttu-id="89183-143">Notas</span><span class="sxs-lookup"><span data-stu-id="89183-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="89183-144">Recurso de entrada</span><span class="sxs-lookup"><span data-stu-id="89183-144">Input asset</span></span> |<span data-ttu-id="89183-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="89183-145">foo.bar</span></span> |<span data-ttu-id="89183-146">Vídeo en formato WMV, MOV o MP4</span><span class="sxs-lookup"><span data-stu-id="89183-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="89183-147">Configuración de entrada</span><span class="sxs-lookup"><span data-stu-id="89183-147">Input config</span></span> |<span data-ttu-id="89183-148">Configuración predeterminada de trabajo</span><span class="sxs-lookup"><span data-stu-id="89183-148">Job configuration preset</span></span> |<span data-ttu-id="89183-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span><span class="sxs-lookup"><span data-stu-id="89183-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="89183-150">Recurso de salida</span><span class="sxs-lookup"><span data-stu-id="89183-150">Output asset</span></span> |<span data-ttu-id="89183-151">foo_annotations.JSON</span><span class="sxs-lookup"><span data-stu-id="89183-151">foo_annotations.json</span></span> |<span data-ttu-id="89183-152">Datos de anotación de ubicaciones de rostros en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="89183-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="89183-153">El usuario puede editarlo para modificar los rectángulos de selección para el difuminado.</span><span class="sxs-lookup"><span data-stu-id="89183-153">This can be edited by the user to modify the blurring bounding boxes.</span></span> <span data-ttu-id="89183-154">Vea el ejemplo a continuación.</span><span class="sxs-lookup"><span data-stu-id="89183-154">See sample below.</span></span> |
| <span data-ttu-id="89183-155">Recurso de salida</span><span class="sxs-lookup"><span data-stu-id="89183-155">Output asset</span></span> |<span data-ttu-id="89183-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="89183-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="89183-157">Un jpg recortado de cada rostro detectado, donde el número indica el identificador (labelId) de la cara</span><span class="sxs-lookup"><span data-stu-id="89183-157">A cropped jpg of each detected face, where the number indicates the labelId of the face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="89183-158">Ejemplo de salida:</span><span class="sxs-lookup"><span data-stu-id="89183-158">Output example:</span></span>

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

### <a name="redact-mode"></a><span data-ttu-id="89183-159">Modo Redact (Censurar)</span><span class="sxs-lookup"><span data-stu-id="89183-159">Redact mode</span></span>
<span data-ttu-id="89183-160">El segundo paso del flujo de trabajo tiene un mayor número de entradas que tienen que combinarse en un solo recurso.</span><span class="sxs-lookup"><span data-stu-id="89183-160">The second pass of the workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="89183-161">Esto incluye una lista de identificadores para difuminar, el vídeo original y las anotaciones JSON.</span><span class="sxs-lookup"><span data-stu-id="89183-161">This includes a list of IDs to blur, the original video, and the annotations JSON.</span></span> <span data-ttu-id="89183-162">Este modo usa las anotaciones para aplicar difuminado en el vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="89183-162">This mode uses the annotations to apply blurring on the input video.</span></span>

<span data-ttu-id="89183-163">El resultado de la fase de análisis no incluye el vídeo original.</span><span class="sxs-lookup"><span data-stu-id="89183-163">The output from the Analyze pass does not include the original video.</span></span> <span data-ttu-id="89183-164">El vídeo tiene que estar cargado en el recurso de entrada para la tarea de modo Redact (Censurar) y seleccionado como el archivo principal.</span><span class="sxs-lookup"><span data-stu-id="89183-164">The video needs to be uploaded into the input asset for the Redact mode task and selected as the primary file.</span></span>

| <span data-ttu-id="89183-165">Fase</span><span class="sxs-lookup"><span data-stu-id="89183-165">Stage</span></span> | <span data-ttu-id="89183-166">Nombre de archivo</span><span class="sxs-lookup"><span data-stu-id="89183-166">File Name</span></span> | <span data-ttu-id="89183-167">Notas</span><span class="sxs-lookup"><span data-stu-id="89183-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="89183-168">Recurso de entrada</span><span class="sxs-lookup"><span data-stu-id="89183-168">Input asset</span></span> |<span data-ttu-id="89183-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="89183-169">foo.bar</span></span> |<span data-ttu-id="89183-170">Vídeo en formato WMV, MOV o MP4.</span><span class="sxs-lookup"><span data-stu-id="89183-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="89183-171">El mismo vídeo que en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="89183-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="89183-172">Recurso de entrada</span><span class="sxs-lookup"><span data-stu-id="89183-172">Input asset</span></span> |<span data-ttu-id="89183-173">foo_annotations.JSON</span><span class="sxs-lookup"><span data-stu-id="89183-173">foo_annotations.json</span></span> |<span data-ttu-id="89183-174">archivo de metadatos de anotaciones de la fase uno, con modificaciones opcionales.</span><span class="sxs-lookup"><span data-stu-id="89183-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="89183-175">Recurso de entrada</span><span class="sxs-lookup"><span data-stu-id="89183-175">Input asset</span></span> |<span data-ttu-id="89183-176">foo_IDList.txt (opcional)</span><span class="sxs-lookup"><span data-stu-id="89183-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="89183-177">Nueva lista opcional separada por líneas de identificadores de rostro para censurar.</span><span class="sxs-lookup"><span data-stu-id="89183-177">Optional new line separated list of face IDs to redact.</span></span> <span data-ttu-id="89183-178">Si se deja en blanco, se difuminarán todas las caras.</span><span class="sxs-lookup"><span data-stu-id="89183-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="89183-179">Configuración de entrada</span><span class="sxs-lookup"><span data-stu-id="89183-179">Input config</span></span> |<span data-ttu-id="89183-180">Configuración predeterminada de trabajo</span><span class="sxs-lookup"><span data-stu-id="89183-180">Job configuration preset</span></span> |<span data-ttu-id="89183-181">{'version':'1.0', 'options': {'mode':'analyze'}}</span><span class="sxs-lookup"><span data-stu-id="89183-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="89183-182">Recurso de salida</span><span class="sxs-lookup"><span data-stu-id="89183-182">Output asset</span></span> |<span data-ttu-id="89183-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="89183-183">foo_redacted.mp4</span></span> |<span data-ttu-id="89183-184">Vídeo con difuminado aplicado en base a las anotaciones</span><span class="sxs-lookup"><span data-stu-id="89183-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="89183-185">Salida de ejemplo</span><span class="sxs-lookup"><span data-stu-id="89183-185">Example output</span></span>
<span data-ttu-id="89183-186">Este es el resultado de una lista de identificadores con un identificador seleccionado.</span><span class="sxs-lookup"><span data-stu-id="89183-186">This is the output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="89183-187">Vea este vídeo</span><span class="sxs-lookup"><span data-stu-id="89183-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="89183-188">foo_IDList.txt de ejemplo</span><span class="sxs-lookup"><span data-stu-id="89183-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="89183-189">Tipos de desenfoque</span><span class="sxs-lookup"><span data-stu-id="89183-189">Blur types</span></span>

<span data-ttu-id="89183-190">En el modo **Combined** (Combinado) o **Redact** (Censurar), hay cinco modos de desenfoque diferentes entre los que puede elegir en la configuración de la entrada JSON: **Bajo**, **Medio**, **Alto**, **Depurar** y **Negro**.</span><span class="sxs-lookup"><span data-stu-id="89183-190">In the **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via the JSON input configuration: **Low**, **Med**, **High**, **Debug**, and **Black**.</span></span> <span data-ttu-id="89183-191">Se usa **Medio** de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="89183-191">By default **Med** is used.</span></span>

<span data-ttu-id="89183-192">Puede encontrar ejemplos de los tipos de desenfoque a continuación.</span><span class="sxs-lookup"><span data-stu-id="89183-192">You can find samples of the blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="89183-193">Ejemplo de JSON:</span><span class="sxs-lookup"><span data-stu-id="89183-193">Example JSON:</span></span>

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a><span data-ttu-id="89183-194">Bajo</span><span class="sxs-lookup"><span data-stu-id="89183-194">Low</span></span>

![Bajo](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="89183-196">Medio</span><span class="sxs-lookup"><span data-stu-id="89183-196">Med</span></span>

![Medio](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="89183-198">Alto</span><span class="sxs-lookup"><span data-stu-id="89183-198">High</span></span>

![Alto](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a><span data-ttu-id="89183-200">Depurar</span><span class="sxs-lookup"><span data-stu-id="89183-200">Debug</span></span>

![Depurar](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="89183-202">Negro</span><span class="sxs-lookup"><span data-stu-id="89183-202">Black</span></span>

![Negro](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-the-output-json-file"></a><span data-ttu-id="89183-204">Elementos del archivo JSON de salida</span><span class="sxs-lookup"><span data-stu-id="89183-204">Elements of the output JSON file</span></span>

<span data-ttu-id="89183-205">El procesador multimedia de censura proporciona detección de ubicación y seguimiento de rostros de alta precisión que puede detectar hasta 64 caras humanas en un fotograma de vídeo.</span><span class="sxs-lookup"><span data-stu-id="89183-205">The Redaction MP provides high precision face location detection and tracking that can detect up to 64 human faces in a video frame.</span></span> <span data-ttu-id="89183-206">Las caras de frente ofrecen los mejores resultados, mientras que las que se encuentran de lado y las caras pequeñas (inferiores o iguales a 24x24 píxeles) podrían no ser tan precisas.</span><span class="sxs-lookup"><span data-stu-id="89183-206">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="89183-207">Código de ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="89183-207">.NET sample code</span></span>

<span data-ttu-id="89183-208">El programa siguiente muestra cómo:</span><span class="sxs-lookup"><span data-stu-id="89183-208">The following program shows how to:</span></span>

1. <span data-ttu-id="89183-209">Crear un recurso y cargar un archivo multimedia en dicho recurso.</span><span class="sxs-lookup"><span data-stu-id="89183-209">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="89183-210">Crear un trabajo con una tarea de censura de rostros basándose en un archivo de configuración que contiene el siguiente valor predeterminado de JSON.</span><span class="sxs-lookup"><span data-stu-id="89183-210">Create a job with a face redaction task based on a configuration file that contains the following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="89183-211">Descargar los archivos JSON de salida.</span><span class="sxs-lookup"><span data-stu-id="89183-211">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="89183-212">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="89183-212">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="89183-213">Configure el entorno de desarrollo y rellene el archivo app.config con la información de la conexión, como se describe en [Desarrollo de Media Services con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="89183-213">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="89183-214">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="89183-214">Example</span></span>

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
        // Read values from the App.config file.
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

            // Run the FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download the job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload the input media file to storage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference to Azure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from the specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with the encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify the input asset.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

            // Use the following event handler to check job progress.  
            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch the job.
            job.Submit();

            // Check job execution and wait for job to finish.
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

            progressJobTask.Wait();

            // If job state is Error, the event handling
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

## <a name="next-steps"></a><span data-ttu-id="89183-215">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="89183-215">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="89183-216">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="89183-216">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="89183-217">Vínculos relacionados</span><span class="sxs-lookup"><span data-stu-id="89183-217">Related links</span></span>
[<span data-ttu-id="89183-218">Azure Media Services Analytics Overview (Información general sobre Azure Media Services Analytics)</span><span class="sxs-lookup"><span data-stu-id="89183-218">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="89183-219">Demostraciones de Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="89183-219">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

