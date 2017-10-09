---
title: "aaaDetect cara y las emociones con análisis de multimedia de Azure | Documentos de Microsoft"
description: "Este tema muestra cómo se enfrenta a toodetect y emociones con análisis de multimedia de Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a><span data-ttu-id="60e75-103">Detección de caras y emociones con Análisis multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="60e75-103">Detect Face and Emotion with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="60e75-104">Información general</span><span class="sxs-lookup"><span data-stu-id="60e75-104">Overview</span></span>
<span data-ttu-id="60e75-105">Hola **Detector de caras de multimedia de Azure** procesador multimedia (MP) le permite toocount, movimientos de seguimiento y participación de la audiencia de medidor incluso y reacción a través de expresiones faciales.</span><span class="sxs-lookup"><span data-stu-id="60e75-105">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="60e75-106">Este servicio contiene dos características:</span><span class="sxs-lookup"><span data-stu-id="60e75-106">This service contains two features:</span></span> 

* <span data-ttu-id="60e75-107">**Detección de caras**</span><span class="sxs-lookup"><span data-stu-id="60e75-107">**Face detection**</span></span>
  
    <span data-ttu-id="60e75-108">La detección de caras busca y realiza el seguimiento de caras humanas dentro de un vídeo.</span><span class="sxs-lookup"><span data-stu-id="60e75-108">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="60e75-109">Varias caras pueden detectarse y posteriormente se realiza el seguimiento de medida que se mueven, con metadatos de tiempo y la ubicación de hello devueltos en un archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="60e75-109">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="60e75-110">Durante el seguimiento, tratará de toogive un toohello identificador coherente mismo enfrentan mientras está moviendo persona Hola en pantalla, incluso si se puede ver obstruidos o brevemente deje marco Hola.</span><span class="sxs-lookup"><span data-stu-id="60e75-110">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="60e75-111">Este servicio no lleva a cabo el reconocimiento facial.</span><span class="sxs-lookup"><span data-stu-id="60e75-111">This service does not perform facial recognition.</span></span> <span data-ttu-id="60e75-112">Una persona que sale del marco de Hola o deja de estar obstruida para demasiado larga se le asignará un nuevo identificador cuando devuelven.</span><span class="sxs-lookup"><span data-stu-id="60e75-112">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="60e75-113">**Detección de emociones**</span><span class="sxs-lookup"><span data-stu-id="60e75-113">**Emotion detection**</span></span>
  
    <span data-ttu-id="60e75-114">Detección de emoción es un componente opcional de hello procesador de multimedia de detección de cara que devuelve el análisis en varios atributos emoción de caras de hello detectados, incluida la satisfacción, tristeza, temor, ira y mucho más.</span><span class="sxs-lookup"><span data-stu-id="60e75-114">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

<span data-ttu-id="60e75-115">Hola **Detector de caras de multimedia de Azure** MP está actualmente en vista previa.</span><span class="sxs-lookup"><span data-stu-id="60e75-115">hello **Azure Media Face Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="60e75-116">Este tema proporciona detalles acerca de **Detector de caras de multimedia de Azure** y muestra cómo toouse con el SDK de servicios multimedia para. NET.</span><span class="sxs-lookup"><span data-stu-id="60e75-116">This topic gives details about  **Azure Media Face Detector** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="face-detector-input-files"></a><span data-ttu-id="60e75-117">Archivos de entrada de Face Detector (Detector de caras)</span><span class="sxs-lookup"><span data-stu-id="60e75-117">Face Detector input files</span></span>
<span data-ttu-id="60e75-118">Archivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="60e75-118">Video files.</span></span> <span data-ttu-id="60e75-119">Actualmente, se admite Hola siguientes formatos: MP4, MOV y WMV.</span><span class="sxs-lookup"><span data-stu-id="60e75-119">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="face-detector-output-files"></a><span data-ttu-id="60e75-120">Archivos de salida de Face Detector (Detector de caras)</span><span class="sxs-lookup"><span data-stu-id="60e75-120">Face Detector output files</span></span>
<span data-ttu-id="60e75-121">API de detección y seguimiento de cara de Hello proporciona detección de ubicación de cara de alta precisión y el seguimiento que puede detectar una too64 caras humana en un vídeo.</span><span class="sxs-lookup"><span data-stu-id="60e75-121">hello face detection and tracking API provides high precision face location detection and tracking that can detect up too64 human faces in a video.</span></span> <span data-ttu-id="60e75-122">Caras frontales proporcionan Hola los mejores resultados, al lado caras y caras pequeños (menor que o igual a too24x24 píxeles) no sea lo más preciso.</span><span class="sxs-lookup"><span data-stu-id="60e75-122">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) might not be as accurate.</span></span>

<span data-ttu-id="60e75-123">Hello caras detectadas y de seguimiento se devuelven con las coordenadas (izquierda, superior, ancho y alto) que indica la ubicación de Hola de caras de imagen de hello en píxeles, así como una cara identificador numérico que indica Hola seguimiento de ese individuo.</span><span class="sxs-lookup"><span data-stu-id="60e75-123">hello detected and tracked faces are returned with coordinates (left, top, width, and height) indicating hello location of faces in hello image in pixels, as well as a face ID number indicating hello tracking of that individual.</span></span> <span data-ttu-id="60e75-124">Números de Id. de cara son propensas a tooreset en circunstancias cuando cara frontal Hola se pierde o superpuesta en el marco de hello, lo que da lugar a algunas personas al asignarse a varios identificadores.</span><span class="sxs-lookup"><span data-stu-id="60e75-124">Face ID numbers are prone tooreset under circumstances when hello frontal face is lost or overlapped in hello frame, resulting in some individuals getting assigned multiple IDs.</span></span>

## <span data-ttu-id="60e75-125"><a id="output_elements"></a>Elementos Hola JSON del archivo de salida</span><span class="sxs-lookup"><span data-stu-id="60e75-125"><a id="output_elements"></a>Elements of hello output JSON file</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

<span data-ttu-id="60e75-126">Detector de caras usa técnicas de fragmentación (donde hello metadatos se pueden dividir en fragmentos basados en tiempo y se puede descargar sólo lo que necesita) y la segmentación (donde los eventos de Hola se dividen en caso de aumenten demasiados).</span><span class="sxs-lookup"><span data-stu-id="60e75-126">Face Detector uses techniques of fragmentation (where hello metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where hello events are broken up in case they get too large).</span></span> <span data-ttu-id="60e75-127">Algunos cálculos sencillos pueden ayudarle a transformar datos Hola.</span><span class="sxs-lookup"><span data-stu-id="60e75-127">Some simple calculations can help you transform hello data.</span></span> <span data-ttu-id="60e75-128">Por ejemplo, si un evento se inició en 6300 (tics), con una escala de tiempo de 2997 (tics/segundo) y una velocidad de fotogramas de 29,97 (fotogramas/segundo), entonces:</span><span class="sxs-lookup"><span data-stu-id="60e75-128">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span></span>

* <span data-ttu-id="60e75-129">Inicio/Escala de tiempo = 2,1 segundos</span><span class="sxs-lookup"><span data-stu-id="60e75-129">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="60e75-130">Segundos x Framerate = 63 marcos</span><span class="sxs-lookup"><span data-stu-id="60e75-130">Seconds x Framerate = 63 frames</span></span>

## <a name="face-detection-input-and-output-example"></a><span data-ttu-id="60e75-131">Ejemplo de entrada y salida de detección de caras</span><span class="sxs-lookup"><span data-stu-id="60e75-131">Face detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="60e75-132">Vídeo de entrada</span><span class="sxs-lookup"><span data-stu-id="60e75-132">Input video</span></span>
[<span data-ttu-id="60e75-133">Vídeo de entrada</span><span class="sxs-lookup"><span data-stu-id="60e75-133">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="60e75-134">Configuración de tareas (valor preestablecido)</span><span class="sxs-lookup"><span data-stu-id="60e75-134">Task configuration (preset)</span></span>
<span data-ttu-id="60e75-135">Al crear una tarea con **Azure Media Face Detector**(Detector de caras multimedia de Azure), debe especificar un valor predeterminado de configuración.</span><span class="sxs-lookup"><span data-stu-id="60e75-135">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="60e75-136">Hola siguiente valor preestablecido de configuración es solo para la detección de cara.</span><span class="sxs-lookup"><span data-stu-id="60e75-136">hello following configuration preset is just for face detection.</span></span>

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a><span data-ttu-id="60e75-137">Descripciones de atributos</span><span class="sxs-lookup"><span data-stu-id="60e75-137">Attribute descriptions</span></span>
| <span data-ttu-id="60e75-138">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="60e75-138">Attribute name</span></span> | <span data-ttu-id="60e75-139">Description</span><span class="sxs-lookup"><span data-stu-id="60e75-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="60e75-140">Mode</span><span class="sxs-lookup"><span data-stu-id="60e75-140">Mode</span></span> |<span data-ttu-id="60e75-141">Rápido: procesamiento rápido, pero menos preciso (valor predeterminado).</span><span class="sxs-lookup"><span data-stu-id="60e75-141">Fast - fast processing speed, but less accurate (default).</span></span>|

### <a name="json-output"></a><span data-ttu-id="60e75-142">Salida de JSON</span><span class="sxs-lookup"><span data-stu-id="60e75-142">JSON output</span></span>
<span data-ttu-id="60e75-143">se truncaron Hola siguiente ejemplo de salida JSON.</span><span class="sxs-lookup"><span data-stu-id="60e75-143">hello following example of JSON output was truncated.</span></span>

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a><span data-ttu-id="60e75-144">Ejemplo de entrada y salida de detección de emociones</span><span class="sxs-lookup"><span data-stu-id="60e75-144">Emotion detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="60e75-145">Vídeo de entrada</span><span class="sxs-lookup"><span data-stu-id="60e75-145">Input video</span></span>
[<span data-ttu-id="60e75-146">Vídeo de entrada</span><span class="sxs-lookup"><span data-stu-id="60e75-146">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="60e75-147">Configuración de tareas (valor preestablecido)</span><span class="sxs-lookup"><span data-stu-id="60e75-147">Task configuration (preset)</span></span>
<span data-ttu-id="60e75-148">Al crear una tarea con **Azure Media Face Detector**(Detector de caras multimedia de Azure), debe especificar un valor predeterminado de configuración.</span><span class="sxs-lookup"><span data-stu-id="60e75-148">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="60e75-149">Hola siguiente valor preestablecido de configuración especifica toocreate que JSON en función de detección de hello emociones.</span><span class="sxs-lookup"><span data-stu-id="60e75-149">hello following configuration preset specifies toocreate JSON based on hello emotion detection.</span></span>

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a><span data-ttu-id="60e75-150">Descripciones de atributos</span><span class="sxs-lookup"><span data-stu-id="60e75-150">Attribute descriptions</span></span>
| <span data-ttu-id="60e75-151">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="60e75-151">Attribute name</span></span> | <span data-ttu-id="60e75-152">Description</span><span class="sxs-lookup"><span data-stu-id="60e75-152">Description</span></span> |
| --- | --- |
| <span data-ttu-id="60e75-153">Mode</span><span class="sxs-lookup"><span data-stu-id="60e75-153">Mode</span></span> |<span data-ttu-id="60e75-154">Faces: solo detección de caras.</span><span class="sxs-lookup"><span data-stu-id="60e75-154">Faces: Only face detection.</span></span><br/><span data-ttu-id="60e75-155">PerFaceEmotion: devolver emociones independientemente para cada detección de cara.</span><span class="sxs-lookup"><span data-stu-id="60e75-155">PerFaceEmotion: Return emotion independently for each face detection.</span></span><br/><span data-ttu-id="60e75-156">AggregateEmotion: Devolver valores de emociones medios para todas las caras del fotograma.</span><span class="sxs-lookup"><span data-stu-id="60e75-156">AggregateEmotion: Return average emotion values for all faces in frame.</span></span> |
| <span data-ttu-id="60e75-157">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="60e75-157">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="60e75-158">Utilizar si se selecciona el modo AggregateEmotion.</span><span class="sxs-lookup"><span data-stu-id="60e75-158">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="60e75-159">Especifica longitud Hola de vídeo tooproduce utilizado cada resultado agregado, en milisegundos.</span><span class="sxs-lookup"><span data-stu-id="60e75-159">Specifies hello length of video used tooproduce each aggregate result, in milliseconds.</span></span> |
| <span data-ttu-id="60e75-160">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="60e75-160">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="60e75-161">Utilizar si se selecciona el modo AggregateEmotion.</span><span class="sxs-lookup"><span data-stu-id="60e75-161">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="60e75-162">Especifica con qué agregado de tooproduce frecuencia da como resultado.</span><span class="sxs-lookup"><span data-stu-id="60e75-162">Specifies with what frequency tooproduce aggregate results.</span></span> |

#### <a name="aggregate-defaults"></a><span data-ttu-id="60e75-163">Agregar valores predeterminados</span><span class="sxs-lookup"><span data-stu-id="60e75-163">Aggregate defaults</span></span>
<span data-ttu-id="60e75-164">A continuación se recomiendan los valores de ventana agregada de Hola y la configuración de intervalos.</span><span class="sxs-lookup"><span data-stu-id="60e75-164">Below are recommended values for hello aggregate window and interval settings.</span></span> <span data-ttu-id="60e75-165">AggregateEmotionWindowMs debe ser mayor que AggregateEmotionIntervalMs.</span><span class="sxs-lookup"><span data-stu-id="60e75-165">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span></span>

|| <span data-ttu-id="60e75-166">Valores predeterminados</span><span class="sxs-lookup"><span data-stu-id="60e75-166">Defaults(s)</span></span> | <span data-ttu-id="60e75-167">Mínimos</span><span class="sxs-lookup"><span data-stu-id="60e75-167">Min(s)</span></span> | <span data-ttu-id="60e75-168">Máximos</span><span class="sxs-lookup"><span data-stu-id="60e75-168">Max(s)</span></span> |
|--- | --- | --- | --- |
| <span data-ttu-id="60e75-169">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="60e75-169">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="60e75-170">0,5</span><span class="sxs-lookup"><span data-stu-id="60e75-170">0.5</span></span> |<span data-ttu-id="60e75-171">2</span><span class="sxs-lookup"><span data-stu-id="60e75-171">2</span></span> |<span data-ttu-id="60e75-172">0,25</span><span class="sxs-lookup"><span data-stu-id="60e75-172">0.25</span></span>|
| <span data-ttu-id="60e75-173">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="60e75-173">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="60e75-174">0,5</span><span class="sxs-lookup"><span data-stu-id="60e75-174">0.5</span></span> |<span data-ttu-id="60e75-175">1</span><span class="sxs-lookup"><span data-stu-id="60e75-175">1</span></span> |<span data-ttu-id="60e75-176">0,25</span><span class="sxs-lookup"><span data-stu-id="60e75-176">0.25</span></span>|

### <a name="json-output"></a><span data-ttu-id="60e75-177">Salida de JSON</span><span class="sxs-lookup"><span data-stu-id="60e75-177">JSON output</span></span>
<span data-ttu-id="60e75-178">Salida de JSON para la emoción agregada (truncada):</span><span class="sxs-lookup"><span data-stu-id="60e75-178">JSON output for aggregate emotion (truncated):</span></span>

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a><span data-ttu-id="60e75-179">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="60e75-179">Limitations</span></span>
* <span data-ttu-id="60e75-180">formatos de vídeo de entrada de Hello compatibles incluyen MP4, MOV y WMV.</span><span class="sxs-lookup"><span data-stu-id="60e75-180">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="60e75-181">intervalo de tamaño de cara detectables de Hello es too2048x2048 de 24 x 24 píxeles.</span><span class="sxs-lookup"><span data-stu-id="60e75-181">hello detectable face size range is 24x24 too2048x2048 pixels.</span></span> <span data-ttu-id="60e75-182">no se detectarán las caras de Hello fuera de este intervalo.</span><span class="sxs-lookup"><span data-stu-id="60e75-182">hello faces out of this range will not be detected.</span></span>
* <span data-ttu-id="60e75-183">Para cada vídeo, número máximo de Hola de caras devuelto es 64.</span><span class="sxs-lookup"><span data-stu-id="60e75-183">For each video, hello maximum number of faces returned is 64.</span></span>
* <span data-ttu-id="60e75-184">Algunas caras podrían no detectarse debido a problemas de tootechnical; Por ejemplo, un gran ángulos de cara (head postura) y oclusión grande.</span><span class="sxs-lookup"><span data-stu-id="60e75-184">Some faces may not be detected due tootechnical challenges; e.g. very large face angles (head-pose), and large occlusion.</span></span> <span data-ttu-id="60e75-185">Caras frontales y cerca frontal tienen los mejores resultados Hola.</span><span class="sxs-lookup"><span data-stu-id="60e75-185">Frontal and near-frontal faces have hello best results.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="60e75-186">Código de ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="60e75-186">.NET sample code</span></span>

<span data-ttu-id="60e75-187">siguiente de Hello programa muestra cómo:</span><span class="sxs-lookup"><span data-stu-id="60e75-187">hello following program shows how to:</span></span>

1. <span data-ttu-id="60e75-188">Crear un activo y cargar un archivo multimedia en activo de Hola.</span><span class="sxs-lookup"><span data-stu-id="60e75-188">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="60e75-189">Crear un trabajo con una tarea de detección de la cara basada en un archivo de configuración que contiene Hola siguiente valor preestablecido de json.</span><span class="sxs-lookup"><span data-stu-id="60e75-189">Create a job with a face detection task based on a configuration file that contains hello following json preset.</span></span> 
   
        {
            "version": "1.0"
        }
3. <span data-ttu-id="60e75-190">Descargar archivos de hello salida JSON.</span><span class="sxs-lookup"><span data-stu-id="60e75-190">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="60e75-191">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="60e75-191">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="60e75-192">Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="60e75-192">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="60e75-193">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="60e75-193">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceDetection
    {
        class Program
        {
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

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="60e75-194">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="60e75-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="60e75-195">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="60e75-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="60e75-196">Vínculos relacionados</span><span class="sxs-lookup"><span data-stu-id="60e75-196">Related links</span></span>
[<span data-ttu-id="60e75-197">Azure Media Services Analytics Overview (Información general sobre análisis de Servicios multimedia de Azure)</span><span class="sxs-lookup"><span data-stu-id="60e75-197">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="60e75-198">Demostraciones de Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="60e75-198">Azure Media Analytics demos</span></span>](http://amslabs.azurewebsites.net/demos/Analytics.html)

