---
title: "Movimientos de aaaDetect con análisis de multimedia de Azure | Documentos de Microsoft"
description: "Hola habilita el Detector de movimiento de multimedia de Azure media procesador (MP) tooefficiently se identifican las secciones de interés dentro de un vídeo largo y sin incidentes en caso contrario."
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
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="1989d-103">Detección de movimientos con Análisis multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="1989d-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="1989d-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1989d-104">Overview</span></span>
<span data-ttu-id="1989d-105">Hola **Detector de movimiento de multimedia de Azure** habilita el procesador (MP) media tooefficiently se identifican las secciones de interés dentro de un vídeo largo y sin incidentes en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="1989d-105">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="1989d-106">Detección de movimiento puede usarse en secciones de tooidentify grabaciones de cámaras estáticas de vídeo de Hola donde se produce un movimiento.</span><span class="sxs-lookup"><span data-stu-id="1989d-106">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="1989d-107">Genera un archivo JSON que contiene un metadatos con hello límite región donde se produjo el evento de Hola y marcas de tiempo.</span><span class="sxs-lookup"><span data-stu-id="1989d-107">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="1989d-108">Destinado fuentes de vídeo de seguridad, esta tecnología es capaz de toocategorize movimiento en los eventos relevantes y falsos positivos, como los cambios de iluminación y sombras.</span><span class="sxs-lookup"><span data-stu-id="1989d-108">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="1989d-109">Esto permite toogenerate alertas de seguridad de las fuentes de cámara sin que se va a spam con eventos irrelevantes infinitos, al que se va a momentos tooextract capaz de interés de vídeos de vigilancia muy largos.</span><span class="sxs-lookup"><span data-stu-id="1989d-109">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="1989d-110">Hola **Detector de movimiento de multimedia de Azure** MP está actualmente en vista previa.</span><span class="sxs-lookup"><span data-stu-id="1989d-110">hello **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="1989d-111">Este tema proporciona detalles acerca de **Detector de movimiento de multimedia de Azure** y muestra cómo toouse con el SDK de servicios multimedia para .NET</span><span class="sxs-lookup"><span data-stu-id="1989d-111">This topic gives details about  **Azure Media Motion Detector** and shows how toouse it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="1989d-112">Archivos de entrada del Detector de movimiento</span><span class="sxs-lookup"><span data-stu-id="1989d-112">Motion Detector input files</span></span>
<span data-ttu-id="1989d-113">Archivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="1989d-113">Video files.</span></span> <span data-ttu-id="1989d-114">Actualmente, se admite Hola siguientes formatos: MP4, MOV y WMV.</span><span class="sxs-lookup"><span data-stu-id="1989d-114">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="1989d-115">Configuración de tareas (valor preestablecido)</span><span class="sxs-lookup"><span data-stu-id="1989d-115">Task configuration (preset)</span></span>
<span data-ttu-id="1989d-116">Cuando cree una tarea con **Azure Media Motion Detector**, tiene que especificar una configuración preestablecida.</span><span class="sxs-lookup"><span data-stu-id="1989d-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="1989d-117">parameters</span><span class="sxs-lookup"><span data-stu-id="1989d-117">Parameters</span></span>
<span data-ttu-id="1989d-118">Puede usar Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="1989d-118">You can use hello following parameters:</span></span>

| <span data-ttu-id="1989d-119">Nombre</span><span class="sxs-lookup"><span data-stu-id="1989d-119">Name</span></span> | <span data-ttu-id="1989d-120">Opciones</span><span class="sxs-lookup"><span data-stu-id="1989d-120">Options</span></span> | <span data-ttu-id="1989d-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="1989d-121">Description</span></span> | <span data-ttu-id="1989d-122">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="1989d-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1989d-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="1989d-123">sensitivityLevel</span></span> |<span data-ttu-id="1989d-124">Cadena: 'bajo', 'medio', 'alto'</span><span class="sxs-lookup"><span data-stu-id="1989d-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="1989d-125">Establecen sensibilidad Hola nivel como se indica qué movimientos.</span><span class="sxs-lookup"><span data-stu-id="1989d-125">Sets hello sensitivity level at which motions is reported.</span></span> <span data-ttu-id="1989d-126">Ajustar esta cantidad tooadjust de falsos positivos.</span><span class="sxs-lookup"><span data-stu-id="1989d-126">Adjust this tooadjust amount of false positives.</span></span> |<span data-ttu-id="1989d-127">'medio'</span><span class="sxs-lookup"><span data-stu-id="1989d-127">'medium'</span></span> |
| <span data-ttu-id="1989d-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="1989d-128">frameSamplingValue</span></span> |<span data-ttu-id="1989d-129">Un número entero positivo</span><span class="sxs-lookup"><span data-stu-id="1989d-129">Positive integer</span></span> |<span data-ttu-id="1989d-130">Establece la frecuencia de hello en el que se ejecuta el algoritmo.</span><span class="sxs-lookup"><span data-stu-id="1989d-130">Sets hello frequency at which algorithm runs.</span></span> <span data-ttu-id="1989d-131">1 es en cada fotograma, 2 significa en uno de cada dos fotogramas y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="1989d-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="1989d-132">1</span><span class="sxs-lookup"><span data-stu-id="1989d-132">1</span></span> |
| <span data-ttu-id="1989d-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="1989d-133">detectLightChange</span></span> |<span data-ttu-id="1989d-134">Valor booleano: 'true', 'false'</span><span class="sxs-lookup"><span data-stu-id="1989d-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="1989d-135">Establece si se notifican los cambios de luz en los resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="1989d-135">Sets whether light changes are reported in hello results</span></span> |<span data-ttu-id="1989d-136">'False'</span><span class="sxs-lookup"><span data-stu-id="1989d-136">'False'</span></span> |
| <span data-ttu-id="1989d-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="1989d-137">mergeTimeThreshold</span></span> |<span data-ttu-id="1989d-138">Xs-time: hh:mm:ss</span><span class="sxs-lookup"><span data-stu-id="1989d-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="1989d-139">Ejemplo: 00:00:03</span><span class="sxs-lookup"><span data-stu-id="1989d-139">Example: 00:00:03</span></span> |<span data-ttu-id="1989d-140">Especifica el período de tiempo de hello entre eventos de movimiento donde 2 eventos se combinarán y se notifican como 1.</span><span class="sxs-lookup"><span data-stu-id="1989d-140">Specifies hello time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="1989d-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="1989d-141">00:00:00</span></span> |
| <span data-ttu-id="1989d-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="1989d-142">detectionZones</span></span> |<span data-ttu-id="1989d-143">Una matriz de zonas de detección:</span><span class="sxs-lookup"><span data-stu-id="1989d-143">An array of detection zones:</span></span><br/><span data-ttu-id="1989d-144">-La zona de detección es un array de 3 o más puntos</span><span class="sxs-lookup"><span data-stu-id="1989d-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="1989d-145">-Punto es una x e y coordenadas de too1 0.</span><span class="sxs-lookup"><span data-stu-id="1989d-145">- Point is a x and y coordinate from 0 too1.</span></span> |<span data-ttu-id="1989d-146">Describe la lista de Hola de detección poligonal zonas toobe usa.</span><span class="sxs-lookup"><span data-stu-id="1989d-146">Describes hello list of polygonal detection zones toobe used.</span></span><br/><span data-ttu-id="1989d-147">Resultados aparecerán con zonas de Hola como un identificador, con hello en primer lugar un es 'identificador': 0</span><span class="sxs-lookup"><span data-stu-id="1989d-147">Results will be reported with hello zones as an ID, with hello first one being 'id':0</span></span> |<span data-ttu-id="1989d-148">Zona único que cubre a marco completo Hola.</span><span class="sxs-lookup"><span data-stu-id="1989d-148">Single zone which covers hello entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="1989d-149">Ejemplo JSON</span><span class="sxs-lookup"><span data-stu-id="1989d-149">JSON example</span></span>
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


## <a name="motion-detector-output-files"></a><span data-ttu-id="1989d-150">Archivos de salida del Detector de movimiento</span><span class="sxs-lookup"><span data-stu-id="1989d-150">Motion Detector output files</span></span>
<span data-ttu-id="1989d-151">Un trabajo de detección de movimiento devolverá un archivo JSON de recurso de salida de hello que describe las alertas de movimiento de Hola y sus categorías, dentro de hello vídeo.</span><span class="sxs-lookup"><span data-stu-id="1989d-151">A motion detection job will return a JSON file in hello output asset which describes hello motion alerts, and their categories, within hello video.</span></span> <span data-ttu-id="1989d-152">archivo Hello contendrá información sobre el tiempo de Hola y duración de movimiento detectado en hello vídeo.</span><span class="sxs-lookup"><span data-stu-id="1989d-152">hello file will contain information about hello time and duration of motion detected in hello video.</span></span>

<span data-ttu-id="1989d-153">Hola movimiento Detector API proporciona indicadores cuando hay objetos en movimiento en un plano fijo vídeo (por ejemplo, un vídeo de vigilancia).</span><span class="sxs-lookup"><span data-stu-id="1989d-153">hello Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="1989d-154">Hola Detector de movimiento es tooreduce entrenado falsas alarmas, como los cambios de instantáneas y la iluminación.</span><span class="sxs-lookup"><span data-stu-id="1989d-154">hello Motion Detector is trained tooreduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="1989d-155">Las limitaciones actuales de algoritmos de hello incluyen vídeos de visión de la noche, objetos semitransparentes y objetos pequeños.</span><span class="sxs-lookup"><span data-stu-id="1989d-155">Current limitations of hello algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="1989d-156"><a id="output_elements"></a>Elementos Hola JSON del archivo de salida</span><span class="sxs-lookup"><span data-stu-id="1989d-156"><a id="output_elements"></a>Elements of hello output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="1989d-157">En la versión más reciente de hello, formato de salida JSON de hello ha cambiado y puede representar un cambio importante para algunos clientes.</span><span class="sxs-lookup"><span data-stu-id="1989d-157">In hello latest release, hello Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="1989d-158">Hello tabla siguiente describe elementos Hola JSON del archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="1989d-158">hello following table describes elements of hello output JSON file.</span></span>

| <span data-ttu-id="1989d-159">Elemento</span><span class="sxs-lookup"><span data-stu-id="1989d-159">Element</span></span> | <span data-ttu-id="1989d-160">Descripción</span><span class="sxs-lookup"><span data-stu-id="1989d-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1989d-161">Versión</span><span class="sxs-lookup"><span data-stu-id="1989d-161">Version</span></span> |<span data-ttu-id="1989d-162">Esto refiere toohello versión de hello API de vídeo.</span><span class="sxs-lookup"><span data-stu-id="1989d-162">This refers toohello version of hello Video API.</span></span> <span data-ttu-id="1989d-163">versión actual de Hello es 2.</span><span class="sxs-lookup"><span data-stu-id="1989d-163">hello current version is 2.</span></span> |
| <span data-ttu-id="1989d-164">Escala de tiempo</span><span class="sxs-lookup"><span data-stu-id="1989d-164">Timescale</span></span> |<span data-ttu-id="1989d-165">"Tics" de vídeo de Hola por segundo.</span><span class="sxs-lookup"><span data-stu-id="1989d-165">"Ticks" per second of hello video.</span></span> |
| <span data-ttu-id="1989d-166">Offset</span><span class="sxs-lookup"><span data-stu-id="1989d-166">Offset</span></span> |<span data-ttu-id="1989d-167">desplazamiento de hora de Hola para las marcas de hora "tics".</span><span class="sxs-lookup"><span data-stu-id="1989d-167">hello time offset for timestamps in "ticks".</span></span> <span data-ttu-id="1989d-168">En la versión 1.0 de las API de vídeo, será siempre 0.</span><span class="sxs-lookup"><span data-stu-id="1989d-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="1989d-169">En los escenarios futuros que se admitan, este valor puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="1989d-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="1989d-170">Framerate</span><span class="sxs-lookup"><span data-stu-id="1989d-170">Framerate</span></span> |<span data-ttu-id="1989d-171">Fotogramas por segundo de hello vídeo.</span><span class="sxs-lookup"><span data-stu-id="1989d-171">Frames per second of hello video.</span></span> |
| <span data-ttu-id="1989d-172">Ancho, alto</span><span class="sxs-lookup"><span data-stu-id="1989d-172">Width, Height</span></span> |<span data-ttu-id="1989d-173">Se refiere toohello ancho y alto de hello vídeo en píxeles.</span><span class="sxs-lookup"><span data-stu-id="1989d-173">Refers toohello width and height of hello video in pixels.</span></span> |
| <span data-ttu-id="1989d-174">Iniciar</span><span class="sxs-lookup"><span data-stu-id="1989d-174">Start</span></span> |<span data-ttu-id="1989d-175">Hola iniciar marca de tiempo en "tics".</span><span class="sxs-lookup"><span data-stu-id="1989d-175">hello start timestamp in "ticks".</span></span> |
| <span data-ttu-id="1989d-176">Duration</span><span class="sxs-lookup"><span data-stu-id="1989d-176">Duration</span></span> |<span data-ttu-id="1989d-177">longitud de Hola de evento hello, "tics".</span><span class="sxs-lookup"><span data-stu-id="1989d-177">hello length of hello event, in "ticks".</span></span> |
| <span data-ttu-id="1989d-178">Intervalo</span><span class="sxs-lookup"><span data-stu-id="1989d-178">Interval</span></span> |<span data-ttu-id="1989d-179">intervalo de saludo de cada entrada de evento de hello, en "tics".</span><span class="sxs-lookup"><span data-stu-id="1989d-179">hello interval of each entry in hello event, in "ticks".</span></span> |
| <span data-ttu-id="1989d-180">Eventos</span><span class="sxs-lookup"><span data-stu-id="1989d-180">Events</span></span> |<span data-ttu-id="1989d-181">Cada fragmento de evento contiene movimiento Hola detectado durante ese período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="1989d-181">Each event fragment contains hello motion detected within that time duration.</span></span> |
| <span data-ttu-id="1989d-182">Tipo</span><span class="sxs-lookup"><span data-stu-id="1989d-182">Type</span></span> |<span data-ttu-id="1989d-183">En la versión actual de hello, siempre es '2' para el movimiento genérico.</span><span class="sxs-lookup"><span data-stu-id="1989d-183">In hello current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="1989d-184">Esta etiqueta proporciona movimiento de las API de vídeo Hola flexibilidad toocategorize en versiones futuras.</span><span class="sxs-lookup"><span data-stu-id="1989d-184">This label gives Video APIs hello flexibility toocategorize motion in future versions.</span></span> |
| <span data-ttu-id="1989d-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="1989d-185">RegionID</span></span> |<span data-ttu-id="1989d-186">Tal como se explicó anteriormente, este valor siempre será 0 en esta versión.</span><span class="sxs-lookup"><span data-stu-id="1989d-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="1989d-187">Esta etiqueta proporciona movimiento de API de vídeo Hola flexibilidad toofind en diversas regiones en versiones futuras.</span><span class="sxs-lookup"><span data-stu-id="1989d-187">This label gives Video API hello flexibility toofind motion in various regions in future versions.</span></span> |
| <span data-ttu-id="1989d-188">Regiones</span><span class="sxs-lookup"><span data-stu-id="1989d-188">Regions</span></span> |<span data-ttu-id="1989d-189">Se refiere toohello área del vídeo que le interese movimiento.</span><span class="sxs-lookup"><span data-stu-id="1989d-189">Refers toohello area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="1989d-190">-"id" representa el área de la región de hello: en esta versión solo hay un, Id. 0.</span><span class="sxs-lookup"><span data-stu-id="1989d-190">-"id" represents hello region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="1989d-191">-"tipo" representa la forma de Hola de región de Hola que le interesa para el movimiento.</span><span class="sxs-lookup"><span data-stu-id="1989d-191">-"type" represents hello shape of hello region you care about for motion.</span></span> <span data-ttu-id="1989d-192">Actualmente, se admiten los valores "rectángulo" y "polígono".</span><span class="sxs-lookup"><span data-stu-id="1989d-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="1989d-193">Si especifica "rectángulo", región de hello con dimensiones de X, Y, ancho y alto.</span><span class="sxs-lookup"><span data-stu-id="1989d-193">If you specified "rectangle", hello region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="1989d-194">Hola X y coordenadas representan coordenadas XY superior izquierda de Hola de región de hello en una escala normalizada de too1.0 0,0.</span><span class="sxs-lookup"><span data-stu-id="1989d-194">hello X and Y coordinates represent hello upper left hand XY coordinates of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="1989d-195">alto y ancho de hello representan tamaño Hola de región de hello en una escala normalizada de too1.0 0,0.</span><span class="sxs-lookup"><span data-stu-id="1989d-195">hello width and height represent hello size of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="1989d-196">En la versión actual de hello, X, Y, ancho y alto están fijos siempre en 0, 0 y 1, 1.</span><span class="sxs-lookup"><span data-stu-id="1989d-196">In hello current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="1989d-197">Si especifica "polygon", región de hello tiene dimensiones en puntos.</span><span class="sxs-lookup"><span data-stu-id="1989d-197">If you specified "polygon", hello region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="1989d-198">Fragments</span><span class="sxs-lookup"><span data-stu-id="1989d-198">Fragments</span></span> |<span data-ttu-id="1989d-199">metadatos de Hello está fragmentado seguridad en diferentes segmentos denominados fragmentos.</span><span class="sxs-lookup"><span data-stu-id="1989d-199">hello metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="1989d-200">Cada fragmento contiene un inicio, una duración, un número de intervalo y eventos.</span><span class="sxs-lookup"><span data-stu-id="1989d-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="1989d-201">Un fragmento sin eventos significa que no se detectó movimiento durante esa hora de inicio y la duración.</span><span class="sxs-lookup"><span data-stu-id="1989d-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="1989d-202">Corchetes []</span><span class="sxs-lookup"><span data-stu-id="1989d-202">Brackets []</span></span> |<span data-ttu-id="1989d-203">Cada corchete de cierre representa un intervalo en eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1989d-203">Each bracket represents one interval in hello event.</span></span> <span data-ttu-id="1989d-204">Si ese intervalo contiene corchetes vacíos, significa que no se detectó movimiento.</span><span class="sxs-lookup"><span data-stu-id="1989d-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="1989d-205">Ubicaciones</span><span class="sxs-lookup"><span data-stu-id="1989d-205">locations</span></span> |<span data-ttu-id="1989d-206">Esta nueva entrada en eventos contiene ubicaciones de Hola donde se produjo el movimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="1989d-206">This new entry under events lists hello location where hello motion occurred.</span></span> <span data-ttu-id="1989d-207">Esto es más específico que las zonas de detección de Hola.</span><span class="sxs-lookup"><span data-stu-id="1989d-207">This is more specific than hello detection zones.</span></span> |

<span data-ttu-id="1989d-208">Hola aquí te mostramos un ejemplo de salida JSON</span><span class="sxs-lookup"><span data-stu-id="1989d-208">hello following is a JSON output example</span></span>

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
## <a name="limitations"></a><span data-ttu-id="1989d-209">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="1989d-209">Limitations</span></span>
* <span data-ttu-id="1989d-210">formatos de vídeo de entrada de Hello compatibles incluyen MP4, MOV y WMV.</span><span class="sxs-lookup"><span data-stu-id="1989d-210">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="1989d-211">La detección de movimiento está optimizada para los vídeos de fondo fijos.</span><span class="sxs-lookup"><span data-stu-id="1989d-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="1989d-212">algoritmo de Hola se centra en la reducción de falsas alarmas, como cambios de iluminación y sombras.</span><span class="sxs-lookup"><span data-stu-id="1989d-212">hello algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="1989d-213">Algunos movimiento podrían no detectarse debido a problemas de tootechnical; Por ejemplo, vídeos de visión de la noche, objetos semitransparentes y objetos pequeños.</span><span class="sxs-lookup"><span data-stu-id="1989d-213">Some motion may not be detected due tootechnical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="1989d-214">Código de ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="1989d-214">.NET sample code</span></span>

<span data-ttu-id="1989d-215">siguiente de Hello programa muestra cómo:</span><span class="sxs-lookup"><span data-stu-id="1989d-215">hello following program shows how to:</span></span>

1. <span data-ttu-id="1989d-216">Crear un activo y cargar un archivo multimedia en activo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1989d-216">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="1989d-217">Crear un trabajo con una tarea de detección de movimiento de vídeo basada en un archivo de configuración que contiene Hola siguiente valor preestablecido de json.</span><span class="sxs-lookup"><span data-stu-id="1989d-217">Create a job with a video motion detection task based on a configuration file that contains hello following json preset.</span></span> 
   
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
3. <span data-ttu-id="1989d-218">Descargar archivos de hello salida JSON.</span><span class="sxs-lookup"><span data-stu-id="1989d-218">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="1989d-219">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1989d-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="1989d-220">Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="1989d-220">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="1989d-221">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1989d-221">Example</span></span>


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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="1989d-222">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="1989d-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1989d-223">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="1989d-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="1989d-224">Vínculos relacionados</span><span class="sxs-lookup"><span data-stu-id="1989d-224">Related links</span></span>
[<span data-ttu-id="1989d-225">Blog de Azure Media Services Motion Detector</span><span class="sxs-lookup"><span data-stu-id="1989d-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="1989d-226">Información general de análisis de Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="1989d-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="1989d-227">Demostraciones de Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="1989d-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

