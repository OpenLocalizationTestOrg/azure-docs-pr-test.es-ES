---
title: "Digitalización de texto con OCR de Análisis multimedia de Azure | Microsoft Docs"
description: "Gracias al OCR (reconocimiento óptico de caracteres) de Análisis multimedia de Azure, podrá convertir el contenido de texto de archivos de vídeo en texto digital modificable y utilizable en búsquedas.  De este modo, se puede automatizar la extracción de metadatos significativos de la señal de vídeo de los elementos multimedia."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 43f5b3a9bbec243e668c79702045094fcfedbdda
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-media-analytics-to-convert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="d0bce-104">Uso de Análisis multimedia de Azure para convertir el contenido de texto de archivos de vídeo en texto digital</span><span class="sxs-lookup"><span data-stu-id="d0bce-104">Use Azure Media Analytics to convert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="d0bce-105">Información general</span><span class="sxs-lookup"><span data-stu-id="d0bce-105">Overview</span></span>
<span data-ttu-id="d0bce-106">Si necesita extraer el contenido de texto de los archivos de vídeo y generar un texto digital que se pueda editar y en el que se pueda buscar, utilice OCR (reconocimiento óptico de caracteres) de Análisis multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="d0bce-106">If you need to extract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="d0bce-107">Este procesador multimedia de Azure detecta contenido de texto en los archivos de vídeo y genera archivos de texto para su uso.</span><span class="sxs-lookup"><span data-stu-id="d0bce-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span></span> <span data-ttu-id="d0bce-108">El OCR le permite automatizar la extracción de metadatos significativos a partir de la señal de vídeo de los elementos multimedia.</span><span class="sxs-lookup"><span data-stu-id="d0bce-108">OCR enables you to automate the extraction of meaningful metadata from the video signal of your media.</span></span>

<span data-ttu-id="d0bce-109">Cuando se utiliza junto con un motor de búsqueda, puede indexar fácilmente el contenido multimedia por texto y mejorar la detectabilidad de su contenido.</span><span class="sxs-lookup"><span data-stu-id="d0bce-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance the discoverability of your content.</span></span> <span data-ttu-id="d0bce-110">Esto es muy útil en vídeos con gran cantidad de texto, como una grabación de vídeo o una captura de pantalla de una presentación de diapositivas.</span><span class="sxs-lookup"><span data-stu-id="d0bce-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span></span> <span data-ttu-id="d0bce-111">El procesador multimedia de OCR de Azure está optimizado para texto digital.</span><span class="sxs-lookup"><span data-stu-id="d0bce-111">The Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="d0bce-112">El procesador multimedia **Azure Media OCR** está actualmente en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="d0bce-112">The **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="d0bce-113">En este tema se proporcionan detalles sobre **Azure Media OCR** y se muestra cómo se usa con el SDK de Media Services para .NET.</span><span class="sxs-lookup"><span data-stu-id="d0bce-113">This topic gives details about  **Azure Media OCR** and shows how to use it with Media Services SDK for .NET.</span></span> <span data-ttu-id="d0bce-114">Para obtener información adicional y ejemplos, consulte [este blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span><span class="sxs-lookup"><span data-stu-id="d0bce-114">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="d0bce-115">Archivos de entrada para OCR</span><span class="sxs-lookup"><span data-stu-id="d0bce-115">OCR input files</span></span>
<span data-ttu-id="d0bce-116">Archivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="d0bce-116">Video files.</span></span> <span data-ttu-id="d0bce-117">Actualmente, se admiten los siguientes formatos: MP4, MOV y WMV.</span><span class="sxs-lookup"><span data-stu-id="d0bce-117">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="d0bce-118">Configuración de tareas</span><span class="sxs-lookup"><span data-stu-id="d0bce-118">Task configuration</span></span>
<span data-ttu-id="d0bce-119">Configuración de tareas (valor predeterminado)</span><span class="sxs-lookup"><span data-stu-id="d0bce-119">Task configuration (preset).</span></span> <span data-ttu-id="d0bce-120">Cuando se crea una tarea con **Azure Media OCR**, debe especificar una configuración preestablecida mediante JSON o XML.</span><span class="sxs-lookup"><span data-stu-id="d0bce-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="d0bce-121">El motor de OCR solo toma una área de imagen con un mínimo de 40 píxeles hasta un máximo de 32 000 píxeles como entrada válida en los valores alto y ancho.</span><span class="sxs-lookup"><span data-stu-id="d0bce-121">The OCR engine only takes an image region with minimum 40 pixels to maximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="d0bce-122">Descripciones de atributos</span><span class="sxs-lookup"><span data-stu-id="d0bce-122">Attribute descriptions</span></span>
| <span data-ttu-id="d0bce-123">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="d0bce-123">Attribute name</span></span> | <span data-ttu-id="d0bce-124">Descripción</span><span class="sxs-lookup"><span data-stu-id="d0bce-124">Description</span></span> |
| --- | --- |
|<span data-ttu-id="d0bce-125">AdvancedOutput</span><span class="sxs-lookup"><span data-stu-id="d0bce-125">AdvancedOutput</span></span>| <span data-ttu-id="d0bce-126">Si establece AdvancedOutput en true, la salida JSON contendrá datos posicionales para cada palabra única (además de frases y regiones).</span><span class="sxs-lookup"><span data-stu-id="d0bce-126">If you set AdvancedOutput to true, the JSON output will contain positional data for every single word (in addition to phrases and regions).</span></span> <span data-ttu-id="d0bce-127">Si no desea ver estos detalles, establezca la marca en false.</span><span class="sxs-lookup"><span data-stu-id="d0bce-127">If you do not want to see these details, set the flag to false.</span></span> <span data-ttu-id="d0bce-128">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="d0bce-128">The default value is false.</span></span> <span data-ttu-id="d0bce-129">Para más información, vea [este blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span><span class="sxs-lookup"><span data-stu-id="d0bce-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span></span>|
| <span data-ttu-id="d0bce-130">language</span><span class="sxs-lookup"><span data-stu-id="d0bce-130">Language</span></span> |<span data-ttu-id="d0bce-131">(Opcional) Describe el idioma del texto que desea buscar.</span><span class="sxs-lookup"><span data-stu-id="d0bce-131">(optional) describes the language of text for which to look.</span></span> <span data-ttu-id="d0bce-132">Está disponible en los idiomas siguientes: Detección automática (predeterminado), alemán, árabe, chino (simplificado y tradicional), checo, coreano, danés, español, finés, francés, griego, húngaro, inglés, italiano, japonés, neerlandés, noruego, polaco, portugués, rumano, ruso, serbio cirílico, serbio latino, eslovaco, sueco, turco.</span><span class="sxs-lookup"><span data-stu-id="d0bce-132">One of the following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="d0bce-133">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="d0bce-133">TextOrientation</span></span> |<span data-ttu-id="d0bce-134">(Opcional) Describe la orientación del texto que desea buscar.</span><span class="sxs-lookup"><span data-stu-id="d0bce-134">(optional) describes the orientation of text for which to look.</span></span>  <span data-ttu-id="d0bce-135">"Izquierda" significa que la parte superior de todas las letras apunta a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="d0bce-135">"Left" means that the top of all letters are pointed towards the left.</span></span>  <span data-ttu-id="d0bce-136">El texto predeterminado (similar al que se encuentra en un libro) se puede denominar orientado "hacia arriba".</span><span class="sxs-lookup"><span data-stu-id="d0bce-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="d0bce-137">Uno de los siguientes: detección automática (valor predeterminado), arriba, derecha, abajo, izquierda.</span><span class="sxs-lookup"><span data-stu-id="d0bce-137">One of the following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="d0bce-138">TimeInterval</span><span class="sxs-lookup"><span data-stu-id="d0bce-138">TimeInterval</span></span> |<span data-ttu-id="d0bce-139">(Opcional) Describe la frecuencia de muestreo.</span><span class="sxs-lookup"><span data-stu-id="d0bce-139">(optional) describes the sampling rate.</span></span>  <span data-ttu-id="d0bce-140">El valor predeterminado es cada 1/2 segundo.</span><span class="sxs-lookup"><span data-stu-id="d0bce-140">Default is every 1/2 second.</span></span><br/><span data-ttu-id="d0bce-141">Formato JSON: HH:mm:ss.SSS (predeterminado 00:00:00.500)</span><span class="sxs-lookup"><span data-stu-id="d0bce-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="d0bce-142">Formato XML – primitiva de duración W3C XSD (valor predeterminado PT0.5)</span><span class="sxs-lookup"><span data-stu-id="d0bce-142">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="d0bce-143">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="d0bce-143">DetectRegions</span></span> |<span data-ttu-id="d0bce-144">(Opcional) Una matriz de objetos DetectRegion que especifica regiones dentro del marco de vídeo en el que se va a detectar el texto.</span><span class="sxs-lookup"><span data-stu-id="d0bce-144">(optional) An array of DetectRegion objects specifying regions within the video frame in which to detect text.</span></span><br/><span data-ttu-id="d0bce-145">Un objeto DetectRegion consta de los siguientes cuatro valores enteros:</span><span class="sxs-lookup"><span data-stu-id="d0bce-145">A DetectRegion object is made of the following four integer values:</span></span><br/><span data-ttu-id="d0bce-146">Izquierda: píxeles desde el margen izquierdo</span><span class="sxs-lookup"><span data-stu-id="d0bce-146">Left – pixels from the left-margin</span></span><br/><span data-ttu-id="d0bce-147">Parte superior: píxeles desde el margen superior</span><span class="sxs-lookup"><span data-stu-id="d0bce-147">Top – pixels from the top-margin</span></span><br/><span data-ttu-id="d0bce-148">Ancho: ancho de la región en píxeles</span><span class="sxs-lookup"><span data-stu-id="d0bce-148">Width – width of the region in pixels</span></span><br/><span data-ttu-id="d0bce-149">Alto: el alto de la región en píxeles</span><span class="sxs-lookup"><span data-stu-id="d0bce-149">Height – height of the region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="d0bce-150">Ejemplo de JSON preestablecido</span><span class="sxs-lookup"><span data-stu-id="d0bce-150">JSON preset example</span></span>

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a><span data-ttu-id="d0bce-151">Ejemplo de XML preestablecido</span><span class="sxs-lookup"><span data-stu-id="d0bce-151">XML preset example</span></span>
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a><span data-ttu-id="d0bce-152">Archivos de salida OCR</span><span class="sxs-lookup"><span data-stu-id="d0bce-152">OCR output files</span></span>
<span data-ttu-id="d0bce-153">La salida del procesador multimedia OCR es un archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="d0bce-153">The output of the OCR media processor is a JSON file.</span></span>

### <a name="elements-of-the-output-json-file"></a><span data-ttu-id="d0bce-154">Elementos del archivo JSON de salida</span><span class="sxs-lookup"><span data-stu-id="d0bce-154">Elements of the output JSON file</span></span>
<span data-ttu-id="d0bce-155">La salida de vídeo OCR proporciona datos segmentados en tiempo en los caracteres que se encuentran en el vídeo.</span><span class="sxs-lookup"><span data-stu-id="d0bce-155">The Video OCR output provides time-segmented data on the characters found in your video.</span></span>  <span data-ttu-id="d0bce-156">Puede utilizar atributos tales como el idioma o la orientación para afinar exactamente las palabras en las que está interesado para analizar.</span><span class="sxs-lookup"><span data-stu-id="d0bce-156">You can use attributes such as language or orientation to hone-in on exactly the words that you are interested in analyzing.</span></span> 

<span data-ttu-id="d0bce-157">La salida contiene los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="d0bce-157">The output contains the following attributes:</span></span>

| <span data-ttu-id="d0bce-158">Elemento</span><span class="sxs-lookup"><span data-stu-id="d0bce-158">Element</span></span> | <span data-ttu-id="d0bce-159">Description</span><span class="sxs-lookup"><span data-stu-id="d0bce-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d0bce-160">Escala de tiempo</span><span class="sxs-lookup"><span data-stu-id="d0bce-160">Timescale</span></span> |<span data-ttu-id="d0bce-161">"Tics" por segundo del vídeo</span><span class="sxs-lookup"><span data-stu-id="d0bce-161">"ticks" per second of the video</span></span> |
| <span data-ttu-id="d0bce-162">Offset</span><span class="sxs-lookup"><span data-stu-id="d0bce-162">Offset</span></span> |<span data-ttu-id="d0bce-163">Diferencia de tiempo para las marcas de tiempo</span><span class="sxs-lookup"><span data-stu-id="d0bce-163">time offset for timestamps.</span></span> <span data-ttu-id="d0bce-164">En la versión 1.0 de las API de vídeo, será siempre 0.</span><span class="sxs-lookup"><span data-stu-id="d0bce-164">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="d0bce-165">Framerate</span><span class="sxs-lookup"><span data-stu-id="d0bce-165">Framerate</span></span> |<span data-ttu-id="d0bce-166">Fotogramas por segundo del vídeo</span><span class="sxs-lookup"><span data-stu-id="d0bce-166">Frames per second of the video</span></span> |
| <span data-ttu-id="d0bce-167">width</span><span class="sxs-lookup"><span data-stu-id="d0bce-167">width</span></span> |<span data-ttu-id="d0bce-168">Ancho del vídeo en píxeles</span><span class="sxs-lookup"><span data-stu-id="d0bce-168">width of the video in pixels</span></span> |
| <span data-ttu-id="d0bce-169">height</span><span class="sxs-lookup"><span data-stu-id="d0bce-169">height</span></span> |<span data-ttu-id="d0bce-170">Alto del vídeo en píxeles</span><span class="sxs-lookup"><span data-stu-id="d0bce-170">height of the video in pixels</span></span> |
| <span data-ttu-id="d0bce-171">Fragments</span><span class="sxs-lookup"><span data-stu-id="d0bce-171">Fragments</span></span> |<span data-ttu-id="d0bce-172">Matriz de fragmentos de vídeo basados en tiempo en los que están fragmentados los metadatos</span><span class="sxs-lookup"><span data-stu-id="d0bce-172">array of time-based chunks of video into which the metadata is chunked</span></span> |
| <span data-ttu-id="d0bce-173">start</span><span class="sxs-lookup"><span data-stu-id="d0bce-173">start</span></span> |<span data-ttu-id="d0bce-174">Hora de inicio de un fragmento en "tics"</span><span class="sxs-lookup"><span data-stu-id="d0bce-174">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="d0bce-175">duration</span><span class="sxs-lookup"><span data-stu-id="d0bce-175">duration</span></span> |<span data-ttu-id="d0bce-176">Duración de un fragmento en "tics"</span><span class="sxs-lookup"><span data-stu-id="d0bce-176">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="d0bce-177">interval</span><span class="sxs-lookup"><span data-stu-id="d0bce-177">interval</span></span> |<span data-ttu-id="d0bce-178">Intervalo de cada evento en el fragmento determinado</span><span class="sxs-lookup"><span data-stu-id="d0bce-178">interval of each event within the given fragment</span></span> |
| <span data-ttu-id="d0bce-179">events</span><span class="sxs-lookup"><span data-stu-id="d0bce-179">events</span></span> |<span data-ttu-id="d0bce-180">La matriz que contiene las regiones</span><span class="sxs-lookup"><span data-stu-id="d0bce-180">array containing regions</span></span> |
| <span data-ttu-id="d0bce-181">region</span><span class="sxs-lookup"><span data-stu-id="d0bce-181">region</span></span> |<span data-ttu-id="d0bce-182">Objeto que representa las palabras o frases detectadas</span><span class="sxs-lookup"><span data-stu-id="d0bce-182">object representing detected words or phrases</span></span> |
| <span data-ttu-id="d0bce-183">Idioma</span><span class="sxs-lookup"><span data-stu-id="d0bce-183">language</span></span> |<span data-ttu-id="d0bce-184">Idioma del texto detectado en una región</span><span class="sxs-lookup"><span data-stu-id="d0bce-184">language of the text detected within a region</span></span> |
| <span data-ttu-id="d0bce-185">orientation</span><span class="sxs-lookup"><span data-stu-id="d0bce-185">orientation</span></span> |<span data-ttu-id="d0bce-186">Orientación del texto detectado en una región</span><span class="sxs-lookup"><span data-stu-id="d0bce-186">orientation of the text detected within a region</span></span> |
| <span data-ttu-id="d0bce-187">lines</span><span class="sxs-lookup"><span data-stu-id="d0bce-187">lines</span></span> |<span data-ttu-id="d0bce-188">Matriz de líneas de texto detectadas en una región</span><span class="sxs-lookup"><span data-stu-id="d0bce-188">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="d0bce-189">text</span><span class="sxs-lookup"><span data-stu-id="d0bce-189">text</span></span> |<span data-ttu-id="d0bce-190">El texto real</span><span class="sxs-lookup"><span data-stu-id="d0bce-190">the actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="d0bce-191">Ejemplo de salida JSON</span><span class="sxs-lookup"><span data-stu-id="d0bce-191">JSON output example</span></span>
<span data-ttu-id="d0bce-192">En el siguiente ejemplo de salida contiene la información general de vídeo y varios fragmentos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="d0bce-192">The following output example contains the general video information and several video fragments.</span></span> <span data-ttu-id="d0bce-193">En cada fragmento de vídeo, se encuentran las regiones detectadas por el módulo de administración del reconocimiento óptico de caracteres, con el idioma y la orientación del texto.</span><span class="sxs-lookup"><span data-stu-id="d0bce-193">In every video fragment, it contains every region which is detected by OCR MP with the language and its text orientation.</span></span> <span data-ttu-id="d0bce-194">La región también contiene las líneas de palabras en esta región con el texto de la línea, la posición de la línea y cualquier otra información de las palabras (contenido de palabras, posición y confianza) de esta línea.</span><span class="sxs-lookup"><span data-stu-id="d0bce-194">The region also contains every word line in this region with the line’s text, the line’s position, and every word information (word content, position and confidence) in this line.</span></span> <span data-ttu-id="d0bce-195">El siguiente es un ejemplo y he agregado algunos comentarios entre líneas.</span><span class="sxs-lookup"><span data-stu-id="d0bce-195">The following is an example, and I put some comments inline.</span></span>

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // the time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // the detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including the text and the position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a><span data-ttu-id="d0bce-196">Código de ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="d0bce-196">.NET sample code</span></span>

<span data-ttu-id="d0bce-197">El programa siguiente muestra cómo:</span><span class="sxs-lookup"><span data-stu-id="d0bce-197">The following program shows how to:</span></span>

1. <span data-ttu-id="d0bce-198">Crear un recurso y cargar un archivo multimedia en dicho recurso.</span><span class="sxs-lookup"><span data-stu-id="d0bce-198">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="d0bce-199">Cree un trabajo con un archivo de configuración o valores preestablecidos de OCR.</span><span class="sxs-lookup"><span data-stu-id="d0bce-199">Create a job with an OCR configuration/preset file.</span></span>
3. <span data-ttu-id="d0bce-200">Descargar los archivos JSON de salida.</span><span class="sxs-lookup"><span data-stu-id="d0bce-200">Download the output JSON files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="d0bce-201">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d0bce-201">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="d0bce-202">Configure el entorno de desarrollo y rellene el archivo app.config con la información de la conexión, como se describe en [Desarrollo de Media Services con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d0bce-202">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="d0bce-203">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="d0bce-203">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace OCR
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

                // Run the OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference to Azure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="d0bce-204">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="d0bce-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d0bce-205">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="d0bce-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="d0bce-206">Vínculos relacionados</span><span class="sxs-lookup"><span data-stu-id="d0bce-206">Related links</span></span>
[<span data-ttu-id="d0bce-207">Azure Media Services Analytics Overview (Información general sobre análisis de Servicios multimedia de Azure)</span><span class="sxs-lookup"><span data-stu-id="d0bce-207">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

