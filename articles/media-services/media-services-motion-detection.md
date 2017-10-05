---
title: "Detección de movimientos con Análisis multimedia de Azure | Microsoft Docs"
description: "El procesador de multimedia (MP) Detector de movimiento multimedia de Azure permite identificar de manera eficaz las secciones de interés dentro de un vídeo que, de lo contrario, sería extenso y monótono."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 115ad9dfd88062f23d5d17eed8897ce5d2ca8484
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="1f95c-103">Detección de movimientos con Análisis multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="1f95c-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="1f95c-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1f95c-104">Overview</span></span>
<span data-ttu-id="1f95c-105">El procesador de multimedia (MP) **Detector de movimiento multimedia de Azure** permite identificar de manera eficaz las secciones de interés dentro de un vídeo que, de lo contrario, sería extenso y monótono.</span><span class="sxs-lookup"><span data-stu-id="1f95c-105">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="1f95c-106">La detección de movimiento se puede usar en grabaciones con cámara estática para identificar las secciones del vídeo donde se produjo el movimiento.</span><span class="sxs-lookup"><span data-stu-id="1f95c-106">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="1f95c-107">Genera un archivo JSON que contiene metadatos con marcas de tiempo y la región delimitadora donde se produjo el evento.</span><span class="sxs-lookup"><span data-stu-id="1f95c-107">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="1f95c-108">Orientada a las fuentes de vídeo de seguridad, esta tecnología puede clasificar el movimiento en eventos relevantes y falsos positivos, como sombras y cambios en la iluminación.</span><span class="sxs-lookup"><span data-stu-id="1f95c-108">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="1f95c-109">Esto le permite generar alertas de seguridad a partir de las fuentes de las cámaras sin recibir correos no deseados con una cantidad interminable de eventos irrelevantes, a la vez que puede extraer momentos de interés a partir vídeos de vigilancia considerablemente extensos.</span><span class="sxs-lookup"><span data-stu-id="1f95c-109">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="1f95c-110">El MP **Detector de movimiento multimedia de Azure** está actualmente en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="1f95c-110">The **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="1f95c-111">Este tema proporciona detalles sobre **Azure Media Motion Detector** y muestra cómo se usa con el SDK de Media Services para .NET</span><span class="sxs-lookup"><span data-stu-id="1f95c-111">This topic gives details about  **Azure Media Motion Detector** and shows how to use it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="1f95c-112">Archivos de entrada del Detector de movimiento</span><span class="sxs-lookup"><span data-stu-id="1f95c-112">Motion Detector input files</span></span>
<span data-ttu-id="1f95c-113">Archivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="1f95c-113">Video files.</span></span> <span data-ttu-id="1f95c-114">Actualmente, se admiten los siguientes formatos: MP4, MOV y WMV.</span><span class="sxs-lookup"><span data-stu-id="1f95c-114">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="1f95c-115">Configuración de tareas (valor predeterminado)</span><span class="sxs-lookup"><span data-stu-id="1f95c-115">Task configuration (preset)</span></span>
<span data-ttu-id="1f95c-116">Cuando cree una tarea con **Azure Media Motion Detector**, tiene que especificar una configuración preestablecida.</span><span class="sxs-lookup"><span data-stu-id="1f95c-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="1f95c-117">Parámetros</span><span class="sxs-lookup"><span data-stu-id="1f95c-117">Parameters</span></span>
<span data-ttu-id="1f95c-118">Puede usar los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="1f95c-118">You can use the following parameters:</span></span>

| <span data-ttu-id="1f95c-119">Nombre</span><span class="sxs-lookup"><span data-stu-id="1f95c-119">Name</span></span> | <span data-ttu-id="1f95c-120">Opciones</span><span class="sxs-lookup"><span data-stu-id="1f95c-120">Options</span></span> | <span data-ttu-id="1f95c-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="1f95c-121">Description</span></span> | <span data-ttu-id="1f95c-122">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="1f95c-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1f95c-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="1f95c-123">sensitivityLevel</span></span> |<span data-ttu-id="1f95c-124">Cadena: 'bajo', 'medio', 'alto'</span><span class="sxs-lookup"><span data-stu-id="1f95c-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="1f95c-125">Establece el nivel de sensibilidad que se usa para notificar los movimientos.</span><span class="sxs-lookup"><span data-stu-id="1f95c-125">Sets the sensitivity level at which motions is reported.</span></span> <span data-ttu-id="1f95c-126">Es necesario ajustarlo bien para controlar la cantidad de falsos positivos.</span><span class="sxs-lookup"><span data-stu-id="1f95c-126">Adjust this to adjust amount of false positives.</span></span> |<span data-ttu-id="1f95c-127">'medio'</span><span class="sxs-lookup"><span data-stu-id="1f95c-127">'medium'</span></span> |
| <span data-ttu-id="1f95c-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="1f95c-128">frameSamplingValue</span></span> |<span data-ttu-id="1f95c-129">Un número entero positivo</span><span class="sxs-lookup"><span data-stu-id="1f95c-129">Positive integer</span></span> |<span data-ttu-id="1f95c-130">Establece la frecuencia con la que se ejecuta el algoritmo.</span><span class="sxs-lookup"><span data-stu-id="1f95c-130">Sets the frequency at which algorithm runs.</span></span> <span data-ttu-id="1f95c-131">1 es en cada fotograma, 2 significa en uno de cada dos fotogramas y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="1f95c-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="1f95c-132">1</span><span class="sxs-lookup"><span data-stu-id="1f95c-132">1</span></span> |
| <span data-ttu-id="1f95c-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="1f95c-133">detectLightChange</span></span> |<span data-ttu-id="1f95c-134">Valor booleano: 'true', 'false'</span><span class="sxs-lookup"><span data-stu-id="1f95c-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="1f95c-135">Establece si se notifican los cambios de luz en los resultados</span><span class="sxs-lookup"><span data-stu-id="1f95c-135">Sets whether light changes are reported in the results</span></span> |<span data-ttu-id="1f95c-136">'False'</span><span class="sxs-lookup"><span data-stu-id="1f95c-136">'False'</span></span> |
| <span data-ttu-id="1f95c-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="1f95c-137">mergeTimeThreshold</span></span> |<span data-ttu-id="1f95c-138">Xs-time: hh:mm:ss</span><span class="sxs-lookup"><span data-stu-id="1f95c-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="1f95c-139">Ejemplo: 00:00:03</span><span class="sxs-lookup"><span data-stu-id="1f95c-139">Example: 00:00:03</span></span> |<span data-ttu-id="1f95c-140">Especifica el período de tiempo entre eventos de movimiento donde 2 eventos se combinarán y se notifican como 1.</span><span class="sxs-lookup"><span data-stu-id="1f95c-140">Specifies the time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="1f95c-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="1f95c-141">00:00:00</span></span> |
| <span data-ttu-id="1f95c-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="1f95c-142">detectionZones</span></span> |<span data-ttu-id="1f95c-143">Una matriz de zonas de detección:</span><span class="sxs-lookup"><span data-stu-id="1f95c-143">An array of detection zones:</span></span><br/><span data-ttu-id="1f95c-144">-La zona de detección es un array de 3 o más puntos</span><span class="sxs-lookup"><span data-stu-id="1f95c-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="1f95c-145">-punto es una coordenada x y de 0 a 1.</span><span class="sxs-lookup"><span data-stu-id="1f95c-145">- Point is a x and y coordinate from 0 to 1.</span></span> |<span data-ttu-id="1f95c-146">Describe la lista de zonas de detección poligonal que se usan.</span><span class="sxs-lookup"><span data-stu-id="1f95c-146">Describes the list of polygonal detection zones to be used.</span></span><br/><span data-ttu-id="1f95c-147">Los resultados aparecerán con las zonas como un identificador, siendo el primero 'id': 0</span><span class="sxs-lookup"><span data-stu-id="1f95c-147">Results will be reported with the zones as an ID, with the first one being 'id':0</span></span> |<span data-ttu-id="1f95c-148">Zona única que abarca todo el marco.</span><span class="sxs-lookup"><span data-stu-id="1f95c-148">Single zone which covers the entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="1f95c-149">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1f95c-149">JSON example</span></span>
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a><span data-ttu-id="1f95c-150">Archivos de salida del Detector de movimiento</span><span class="sxs-lookup"><span data-stu-id="1f95c-150">Motion Detector output files</span></span>
<span data-ttu-id="1f95c-151">Un trabajo de detección de movimiento devolverá un archivo JSON en el recurso de salida, el que describe las alertas de movimiento y sus categorías dentro del vídeo.</span><span class="sxs-lookup"><span data-stu-id="1f95c-151">A motion detection job will return a JSON file in the output asset which describes the motion alerts, and their categories, within the video.</span></span> <span data-ttu-id="1f95c-152">El archivo contendrá información sobre el tiempo y la duración del movimiento detectado en el vídeo.</span><span class="sxs-lookup"><span data-stu-id="1f95c-152">The file will contain information about the time and duration of motion detected in the video.</span></span>

<span data-ttu-id="1f95c-153">La API del Detector de movimiento brinda indicadores una vez que hay objetos en movimiento en un vídeo de fondo fijo (por ejemplo, un vídeo de vigilancia).</span><span class="sxs-lookup"><span data-stu-id="1f95c-153">The Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="1f95c-154">El Detector de movimiento está entrenado para disminuir las alarmas falsas, como cambios de iluminación y sombras.</span><span class="sxs-lookup"><span data-stu-id="1f95c-154">The Motion Detector is trained to reduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="1f95c-155">Las limitaciones actuales de los algoritmos incluyen vídeos con visión nocturna, objetos semitransparentes y objetos pequeños.</span><span class="sxs-lookup"><span data-stu-id="1f95c-155">Current limitations of the algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="1f95c-156"><a id="output_elements"></a>Elementos del archivo JSON de salida</span><span class="sxs-lookup"><span data-stu-id="1f95c-156"><a id="output_elements"></a>Elements of the output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="1f95c-157">En la versión más reciente, el formato JSON de salida ha cambiado y puede representar un cambio importante para algunos clientes.</span><span class="sxs-lookup"><span data-stu-id="1f95c-157">In the latest release, the Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="1f95c-158">En la tabla siguiente, se describen elementos del archivo JSON de salida.</span><span class="sxs-lookup"><span data-stu-id="1f95c-158">The following table describes elements of the output JSON file.</span></span>

| <span data-ttu-id="1f95c-159">Elemento</span><span class="sxs-lookup"><span data-stu-id="1f95c-159">Element</span></span> | <span data-ttu-id="1f95c-160">Descripción</span><span class="sxs-lookup"><span data-stu-id="1f95c-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1f95c-161">Versión</span><span class="sxs-lookup"><span data-stu-id="1f95c-161">Version</span></span> |<span data-ttu-id="1f95c-162">Esto se refiere a la versión de la API de vídeo.</span><span class="sxs-lookup"><span data-stu-id="1f95c-162">This refers to the version of the Video API.</span></span> <span data-ttu-id="1f95c-163">La versión actual es 2.</span><span class="sxs-lookup"><span data-stu-id="1f95c-163">The current version is 2.</span></span> |
| <span data-ttu-id="1f95c-164">Escala de tiempo</span><span class="sxs-lookup"><span data-stu-id="1f95c-164">Timescale</span></span> |<span data-ttu-id="1f95c-165">"Tics" por segundo del vídeo.</span><span class="sxs-lookup"><span data-stu-id="1f95c-165">"Ticks" per second of the video.</span></span> |
| <span data-ttu-id="1f95c-166">Offset</span><span class="sxs-lookup"><span data-stu-id="1f95c-166">Offset</span></span> |<span data-ttu-id="1f95c-167">La diferencia de tiempo para las marcas de tiempo en "tics".</span><span class="sxs-lookup"><span data-stu-id="1f95c-167">The time offset for timestamps in "ticks".</span></span> <span data-ttu-id="1f95c-168">En la versión 1.0 de las API de vídeo, será siempre 0.</span><span class="sxs-lookup"><span data-stu-id="1f95c-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="1f95c-169">En los escenarios futuros que se admitan, este valor puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="1f95c-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="1f95c-170">Framerate</span><span class="sxs-lookup"><span data-stu-id="1f95c-170">Framerate</span></span> |<span data-ttu-id="1f95c-171">Fotogramas por segundo del vídeo.</span><span class="sxs-lookup"><span data-stu-id="1f95c-171">Frames per second of the video.</span></span> |
| <span data-ttu-id="1f95c-172">Ancho, alto</span><span class="sxs-lookup"><span data-stu-id="1f95c-172">Width, Height</span></span> |<span data-ttu-id="1f95c-173">Se refiere al ancho y alto del vídeo en píxeles.</span><span class="sxs-lookup"><span data-stu-id="1f95c-173">Refers to the width and height of the video in pixels.</span></span> |
| <span data-ttu-id="1f95c-174">Iniciar</span><span class="sxs-lookup"><span data-stu-id="1f95c-174">Start</span></span> |<span data-ttu-id="1f95c-175">La marca de tiempo de inicio en "tics".</span><span class="sxs-lookup"><span data-stu-id="1f95c-175">The start timestamp in "ticks".</span></span> |
| <span data-ttu-id="1f95c-176">Duración</span><span class="sxs-lookup"><span data-stu-id="1f95c-176">Duration</span></span> |<span data-ttu-id="1f95c-177">La longitud del evento, en "tics".</span><span class="sxs-lookup"><span data-stu-id="1f95c-177">The length of the event, in "ticks".</span></span> |
| <span data-ttu-id="1f95c-178">Intervalo</span><span class="sxs-lookup"><span data-stu-id="1f95c-178">Interval</span></span> |<span data-ttu-id="1f95c-179">El intervalo de cada entrada del evento, en "tics".</span><span class="sxs-lookup"><span data-stu-id="1f95c-179">The interval of each entry in the event, in "ticks".</span></span> |
| <span data-ttu-id="1f95c-180">Eventos</span><span class="sxs-lookup"><span data-stu-id="1f95c-180">Events</span></span> |<span data-ttu-id="1f95c-181">Cada fragmento de evento contiene el movimiento detectado dentro de esa duración.</span><span class="sxs-lookup"><span data-stu-id="1f95c-181">Each event fragment contains the motion detected within that time duration.</span></span> |
| <span data-ttu-id="1f95c-182">Tipo</span><span class="sxs-lookup"><span data-stu-id="1f95c-182">Type</span></span> |<span data-ttu-id="1f95c-183">En la versión actual, este valor siempre es "2" para el movimiento genérico.</span><span class="sxs-lookup"><span data-stu-id="1f95c-183">In the current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="1f95c-184">Esta etiqueta brinda a las API de vídeo la flexibilidad para clasificar el movimiento en las versiones futuras.</span><span class="sxs-lookup"><span data-stu-id="1f95c-184">This label gives Video APIs the flexibility to categorize motion in future versions.</span></span> |
| <span data-ttu-id="1f95c-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="1f95c-185">RegionID</span></span> |<span data-ttu-id="1f95c-186">Tal como se explicó anteriormente, este valor siempre será 0 en esta versión.</span><span class="sxs-lookup"><span data-stu-id="1f95c-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="1f95c-187">Esta etiqueta brinda a la API de vídeo la flexibilidad para encontrar el movimiento en diversas regiones en las versiones futuras.</span><span class="sxs-lookup"><span data-stu-id="1f95c-187">This label gives Video API the flexibility to find motion in various regions in future versions.</span></span> |
| <span data-ttu-id="1f95c-188">Regiones</span><span class="sxs-lookup"><span data-stu-id="1f95c-188">Regions</span></span> |<span data-ttu-id="1f95c-189">Se refiere al área del vídeo donde le interesa el movimiento.</span><span class="sxs-lookup"><span data-stu-id="1f95c-189">Refers to the area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="1f95c-190">-"id" representa el área de la región: en esta versión es solo una, Id. 0.</span><span class="sxs-lookup"><span data-stu-id="1f95c-190">-"id" represents the region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="1f95c-191">-"tipo" representa la forma de la región que le interesa para un movimiento.</span><span class="sxs-lookup"><span data-stu-id="1f95c-191">-"type" represents the shape of the region you care about for motion.</span></span> <span data-ttu-id="1f95c-192">Actualmente, se admiten los valores "rectángulo" y "polígono".</span><span class="sxs-lookup"><span data-stu-id="1f95c-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="1f95c-193">Si especifica "rectángulo", las dimensiones de la región son X, Y, ancho y alto.</span><span class="sxs-lookup"><span data-stu-id="1f95c-193">If you specified "rectangle", the region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="1f95c-194">Las coordenadas X e Y representan las coordenadas XY del lado superior izquierdo de la región en una escala normalizada de 0,0 a 1,0.</span><span class="sxs-lookup"><span data-stu-id="1f95c-194">The X and Y coordinates represent the upper left hand XY coordinates of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="1f95c-195">El ancho y el alto representan el tamaño de la región en una escala normalizada de 0,0 a 1,0.</span><span class="sxs-lookup"><span data-stu-id="1f95c-195">The width and height represent the size of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="1f95c-196">En la versión actual, X, Y, ancho y alto son valores fijos siempre en 0, 0 y 1, 1.</span><span class="sxs-lookup"><span data-stu-id="1f95c-196">In the current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="1f95c-197">Si especifica "polígono", la región tiene dimensiones en puntos.</span><span class="sxs-lookup"><span data-stu-id="1f95c-197">If you specified "polygon", the region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="1f95c-198">Fragments</span><span class="sxs-lookup"><span data-stu-id="1f95c-198">Fragments</span></span> |<span data-ttu-id="1f95c-199">Los metadatos se separan en diferentes segmentos denominados fragmentos.</span><span class="sxs-lookup"><span data-stu-id="1f95c-199">The metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="1f95c-200">Cada fragmento contiene un inicio, una duración, un número de intervalo y eventos.</span><span class="sxs-lookup"><span data-stu-id="1f95c-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="1f95c-201">Un fragmento sin eventos significa que no se detectó movimiento durante esa hora de inicio y la duración.</span><span class="sxs-lookup"><span data-stu-id="1f95c-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="1f95c-202">Corchetes []</span><span class="sxs-lookup"><span data-stu-id="1f95c-202">Brackets []</span></span> |<span data-ttu-id="1f95c-203">Cada corchete representa un intervalo del evento.</span><span class="sxs-lookup"><span data-stu-id="1f95c-203">Each bracket represents one interval in the event.</span></span> <span data-ttu-id="1f95c-204">Si ese intervalo contiene corchetes vacíos, significa que no se detectó movimiento.</span><span class="sxs-lookup"><span data-stu-id="1f95c-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="1f95c-205">Ubicaciones</span><span class="sxs-lookup"><span data-stu-id="1f95c-205">locations</span></span> |<span data-ttu-id="1f95c-206">Esta nueva entrada de eventos muestra la ubicación donde se produjo el movimiento.</span><span class="sxs-lookup"><span data-stu-id="1f95c-206">This new entry under events lists the location where the motion occurred.</span></span> <span data-ttu-id="1f95c-207">Se trata de un valor más específico que las zonas de detección.</span><span class="sxs-lookup"><span data-stu-id="1f95c-207">This is more specific than the detection zones.</span></span> |

<span data-ttu-id="1f95c-208">El siguiente es un ejemplo de salida JSON</span><span class="sxs-lookup"><span data-stu-id="1f95c-208">The following is a JSON output example</span></span>

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a><span data-ttu-id="1f95c-209">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="1f95c-209">Limitations</span></span>
* <span data-ttu-id="1f95c-210">Los formatos de vídeo de entrada admitidos incluyen MP4, MOV y WMV.</span><span class="sxs-lookup"><span data-stu-id="1f95c-210">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="1f95c-211">La detección de movimiento está optimizada para los vídeos de fondo fijos.</span><span class="sxs-lookup"><span data-stu-id="1f95c-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="1f95c-212">El algoritmo se centra en disminuir las alarmas falsas, como cambios en la iluminación y sombras.</span><span class="sxs-lookup"><span data-stu-id="1f95c-212">The algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="1f95c-213">Es posible que no se detecten ciertos movimientos debido a desafíos técnicos; por ejemplo, vídeos con visión nocturna, objetos semitransparentes y objetos pequeños.</span><span class="sxs-lookup"><span data-stu-id="1f95c-213">Some motion may not be detected due to technical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="1f95c-214">Código de ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="1f95c-214">.NET sample code</span></span>

<span data-ttu-id="1f95c-215">El programa siguiente muestra cómo:</span><span class="sxs-lookup"><span data-stu-id="1f95c-215">The following program shows how to:</span></span>

1. <span data-ttu-id="1f95c-216">Crear un recurso y cargar un archivo multimedia en dicho recurso.</span><span class="sxs-lookup"><span data-stu-id="1f95c-216">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="1f95c-217">Crear un trabajo con una tarea de detección de movimiento de vídeo basada en un archivo de configuración que contiene el siguiente valor predeterminado JSON.</span><span class="sxs-lookup"><span data-stu-id="1f95c-217">Create a job with a video motion detection task based on a configuration file that contains the following json preset.</span></span> 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
        }
3. <span data-ttu-id="1f95c-218">Descargar los archivos JSON de salida.</span><span class="sxs-lookup"><span data-stu-id="1f95c-218">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="1f95c-219">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f95c-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="1f95c-220">Configure el entorno de desarrollo y rellene el archivo app.config con la información de la conexión, como se describe en [Desarrollo de Media Services con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="1f95c-220">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="1f95c-221">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1f95c-221">Example</span></span>


    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoMotionDetection
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

                // Run the VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference to Azure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="1f95c-222">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="1f95c-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1f95c-223">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="1f95c-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="1f95c-224">Vínculos relacionados</span><span class="sxs-lookup"><span data-stu-id="1f95c-224">Related links</span></span>
[<span data-ttu-id="1f95c-225">Blog de Azure Media Services Motion Detector</span><span class="sxs-lookup"><span data-stu-id="1f95c-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="1f95c-226">Información general de análisis de Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="1f95c-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="1f95c-227">Demostraciones de Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="1f95c-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

