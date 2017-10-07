---
title: "texto de aaaDigitize con Azure Media análisis OCR | Documentos de Microsoft"
description: "Azure Media análisis OCR (reconocimiento óptico de caracteres) le permite tooconvert el contenido de texto en archivos de vídeo en modificable, puede buscar texto digital.  Esto permite la extracción de hello tooautomate de metadatos significativo de señal de vídeo de Hola de los medios."
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
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="32eb2-104">Usar el contenido de texto de tooconvert de análisis de multimedia de Azure en archivos de vídeo en textos digitales</span><span class="sxs-lookup"><span data-stu-id="32eb2-104">Use Azure Media Analytics tooconvert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="32eb2-105">Información general</span><span class="sxs-lookup"><span data-stu-id="32eb2-105">Overview</span></span>
<span data-ttu-id="32eb2-106">Si necesita tooextract texto contenido desde los archivos de vídeo y generar un texto digital editable, búsquedo, debe usar Azure Media análisis OCR (reconocimiento óptico de caracteres).</span><span class="sxs-lookup"><span data-stu-id="32eb2-106">If you need tooextract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="32eb2-107">Este procesador multimedia de Azure detecta contenido de texto en los archivos de vídeo y genera archivos de texto para su uso.</span><span class="sxs-lookup"><span data-stu-id="32eb2-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span></span> <span data-ttu-id="32eb2-108">OCR permite tooautomate Hola extracción de metadatos significativo de señal de vídeo de Hola de los medios.</span><span class="sxs-lookup"><span data-stu-id="32eb2-108">OCR enables you tooautomate hello extraction of meaningful metadata from hello video signal of your media.</span></span>

<span data-ttu-id="32eb2-109">Cuando se usa junto con un motor de búsqueda, puede fácilmente indexar los medios por texto y mejorar la detectabilidad de hello del contenido.</span><span class="sxs-lookup"><span data-stu-id="32eb2-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance hello discoverability of your content.</span></span> <span data-ttu-id="32eb2-110">Esto es muy útil en vídeos con gran cantidad de texto, como una grabación de vídeo o una captura de pantalla de una presentación de diapositivas.</span><span class="sxs-lookup"><span data-stu-id="32eb2-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span></span> <span data-ttu-id="32eb2-111">Hola procesador multimedia de Azure OCR está optimizado para texto digital.</span><span class="sxs-lookup"><span data-stu-id="32eb2-111">hello Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="32eb2-112">Hola **Azure Media OCR** procesador multimedia está actualmente en vista previa.</span><span class="sxs-lookup"><span data-stu-id="32eb2-112">hello **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="32eb2-113">Este tema proporciona detalles acerca de **Azure Media OCR** y muestra cómo toouse con el SDK de servicios multimedia para. NET.</span><span class="sxs-lookup"><span data-stu-id="32eb2-113">This topic gives details about  **Azure Media OCR** and shows how toouse it with Media Services SDK for .NET.</span></span> <span data-ttu-id="32eb2-114">Para obtener información adicional y ejemplos, consulte [este blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span><span class="sxs-lookup"><span data-stu-id="32eb2-114">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="32eb2-115">Archivos de entrada para OCR</span><span class="sxs-lookup"><span data-stu-id="32eb2-115">OCR input files</span></span>
<span data-ttu-id="32eb2-116">Archivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="32eb2-116">Video files.</span></span> <span data-ttu-id="32eb2-117">Actualmente, se admite Hola siguientes formatos: MP4, MOV y WMV.</span><span class="sxs-lookup"><span data-stu-id="32eb2-117">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="32eb2-118">Configuración de tareas</span><span class="sxs-lookup"><span data-stu-id="32eb2-118">Task configuration</span></span>
<span data-ttu-id="32eb2-119">Configuración de tareas (valor predeterminado)</span><span class="sxs-lookup"><span data-stu-id="32eb2-119">Task configuration (preset).</span></span> <span data-ttu-id="32eb2-120">Cuando se crea una tarea con **Azure Media OCR**, debe especificar una configuración preestablecida mediante JSON o XML.</span><span class="sxs-lookup"><span data-stu-id="32eb2-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="32eb2-121">motor de OCR Hola solo toma un área de imagen a mínimo 40 toomaximum 32000 píxeles como una entrada válida en ambos alto y ancho.</span><span class="sxs-lookup"><span data-stu-id="32eb2-121">hello OCR engine only takes an image region with minimum 40 pixels toomaximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="32eb2-122">Descripciones de atributos</span><span class="sxs-lookup"><span data-stu-id="32eb2-122">Attribute descriptions</span></span>
| <span data-ttu-id="32eb2-123">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="32eb2-123">Attribute name</span></span> | <span data-ttu-id="32eb2-124">Descripción</span><span class="sxs-lookup"><span data-stu-id="32eb2-124">Description</span></span> |
| --- | --- |
|<span data-ttu-id="32eb2-125">AdvancedOutput</span><span class="sxs-lookup"><span data-stu-id="32eb2-125">AdvancedOutput</span></span>| <span data-ttu-id="32eb2-126">Si establece AdvancedOutput tootrue, salida JSON de hello contendrá datos posicionales cada palabra única (en suma toophrases y regiones).</span><span class="sxs-lookup"><span data-stu-id="32eb2-126">If you set AdvancedOutput tootrue, hello JSON output will contain positional data for every single word (in addition toophrases and regions).</span></span> <span data-ttu-id="32eb2-127">Si no desea toosee estos detalles, establezca Hola marca toofalse.</span><span class="sxs-lookup"><span data-stu-id="32eb2-127">If you do not want toosee these details, set hello flag toofalse.</span></span> <span data-ttu-id="32eb2-128">valor predeterminado de Hello es false.</span><span class="sxs-lookup"><span data-stu-id="32eb2-128">hello default value is false.</span></span> <span data-ttu-id="32eb2-129">Para más información, vea [este blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span><span class="sxs-lookup"><span data-stu-id="32eb2-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span></span>|
| <span data-ttu-id="32eb2-130">language</span><span class="sxs-lookup"><span data-stu-id="32eb2-130">Language</span></span> |<span data-ttu-id="32eb2-131">(opcional) describe lenguaje Hola de texto para que toolook.</span><span class="sxs-lookup"><span data-stu-id="32eb2-131">(optional) describes hello language of text for which toolook.</span></span> <span data-ttu-id="32eb2-132">Uno de los siguientes hello: detección automática (valor predeterminado), árabe, chino, chino tradicional, checo danés, neerlandés, inglés, finés, francés, alemán, griego, húngaro, italiano, japonés, coreano, noruego, polaco, portugués, rumano, ruso, SerbianCyrillic, SerbianLatin, eslovaco, español, sueco, turco.</span><span class="sxs-lookup"><span data-stu-id="32eb2-132">One of hello following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="32eb2-133">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="32eb2-133">TextOrientation</span></span> |<span data-ttu-id="32eb2-134">(opcional) describe la orientación de hello del texto para que toolook.</span><span class="sxs-lookup"><span data-stu-id="32eb2-134">(optional) describes hello orientation of text for which toolook.</span></span>  <span data-ttu-id="32eb2-135">"Izquierda" significa que Hola parte superior de todas las letras se señala hacia la izquierda de Hola.</span><span class="sxs-lookup"><span data-stu-id="32eb2-135">"Left" means that hello top of all letters are pointed towards hello left.</span></span>  <span data-ttu-id="32eb2-136">El texto predeterminado (similar al que se encuentra en un libro) se puede denominar orientado "hacia arriba".</span><span class="sxs-lookup"><span data-stu-id="32eb2-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="32eb2-137">Uno de los siguientes hello: detección automática (valor predeterminado), hasta izquierda, derecha, abajo.</span><span class="sxs-lookup"><span data-stu-id="32eb2-137">One of hello following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="32eb2-138">TimeInterval</span><span class="sxs-lookup"><span data-stu-id="32eb2-138">TimeInterval</span></span> |<span data-ttu-id="32eb2-139">(opcional) describe la frecuencia de muestreo de Hola.</span><span class="sxs-lookup"><span data-stu-id="32eb2-139">(optional) describes hello sampling rate.</span></span>  <span data-ttu-id="32eb2-140">El valor predeterminado es cada 1/2 segundo.</span><span class="sxs-lookup"><span data-stu-id="32eb2-140">Default is every 1/2 second.</span></span><br/><span data-ttu-id="32eb2-141">Formato JSON: HH:mm:ss.SSS (predeterminado 00:00:00.500)</span><span class="sxs-lookup"><span data-stu-id="32eb2-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="32eb2-142">Formato XML – primitiva de duración W3C XSD (valor predeterminado PT0.5)</span><span class="sxs-lookup"><span data-stu-id="32eb2-142">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="32eb2-143">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="32eb2-143">DetectRegions</span></span> |<span data-ttu-id="32eb2-144">(opcional) Una matriz de objetos de DetectRegion especificando las regiones dentro de fotograma de vídeo de hello en texto para que toodetect.</span><span class="sxs-lookup"><span data-stu-id="32eb2-144">(optional) An array of DetectRegion objects specifying regions within hello video frame in which toodetect text.</span></span><br/><span data-ttu-id="32eb2-145">Un objeto DetectRegion consta de hello después de cuatro valores enteros:</span><span class="sxs-lookup"><span data-stu-id="32eb2-145">A DetectRegion object is made of hello following four integer values:</span></span><br/><span data-ttu-id="32eb2-146">Izquierda: píxeles desde el margen izquierdo de Hola</span><span class="sxs-lookup"><span data-stu-id="32eb2-146">Left – pixels from hello left-margin</span></span><br/><span data-ttu-id="32eb2-147">Parte superior: píxeles del margen superior de Hola</span><span class="sxs-lookup"><span data-stu-id="32eb2-147">Top – pixels from hello top-margin</span></span><br/><span data-ttu-id="32eb2-148">Ancho: el ancho del área de hello en píxeles</span><span class="sxs-lookup"><span data-stu-id="32eb2-148">Width – width of hello region in pixels</span></span><br/><span data-ttu-id="32eb2-149">Alto: el alto del área de hello en píxeles</span><span class="sxs-lookup"><span data-stu-id="32eb2-149">Height – height of hello region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="32eb2-150">Ejemplo de JSON preestablecido</span><span class="sxs-lookup"><span data-stu-id="32eb2-150">JSON preset example</span></span>

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


#### <a name="xml-preset-example"></a><span data-ttu-id="32eb2-151">Ejemplo de XML preestablecido</span><span class="sxs-lookup"><span data-stu-id="32eb2-151">XML preset example</span></span>
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

## <a name="ocr-output-files"></a><span data-ttu-id="32eb2-152">Archivos de salida OCR</span><span class="sxs-lookup"><span data-stu-id="32eb2-152">OCR output files</span></span>
<span data-ttu-id="32eb2-153">salida de Hello de procesador de multimedia de hello OCR es un archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="32eb2-153">hello output of hello OCR media processor is a JSON file.</span></span>

### <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="32eb2-154">Elementos Hola JSON del archivo de salida</span><span class="sxs-lookup"><span data-stu-id="32eb2-154">Elements of hello output JSON file</span></span>
<span data-ttu-id="32eb2-155">salida de vídeo OCR Hello proporciona segmentada en tiempo de datos en caracteres de Hola que se encuentren en el vídeo.</span><span class="sxs-lookup"><span data-stu-id="32eb2-155">hello Video OCR output provides time-segmented data on hello characters found in your video.</span></span>  <span data-ttu-id="32eb2-156">Puede usar atributos como el idioma o la orientación en toohone en exactamente las palabras hello que está interesado en analizar.</span><span class="sxs-lookup"><span data-stu-id="32eb2-156">You can use attributes such as language or orientation toohone-in on exactly hello words that you are interested in analyzing.</span></span> 

<span data-ttu-id="32eb2-157">salida de Hello contiene Hola siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="32eb2-157">hello output contains hello following attributes:</span></span>

| <span data-ttu-id="32eb2-158">Elemento</span><span class="sxs-lookup"><span data-stu-id="32eb2-158">Element</span></span> | <span data-ttu-id="32eb2-159">Description</span><span class="sxs-lookup"><span data-stu-id="32eb2-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="32eb2-160">Escala de tiempo</span><span class="sxs-lookup"><span data-stu-id="32eb2-160">Timescale</span></span> |<span data-ttu-id="32eb2-161">"tics" de vídeo de Hola por segundo</span><span class="sxs-lookup"><span data-stu-id="32eb2-161">"ticks" per second of hello video</span></span> |
| <span data-ttu-id="32eb2-162">Offset</span><span class="sxs-lookup"><span data-stu-id="32eb2-162">Offset</span></span> |<span data-ttu-id="32eb2-163">Diferencia de tiempo para las marcas de tiempo</span><span class="sxs-lookup"><span data-stu-id="32eb2-163">time offset for timestamps.</span></span> <span data-ttu-id="32eb2-164">En la versión 1.0 de las API de vídeo, será siempre 0.</span><span class="sxs-lookup"><span data-stu-id="32eb2-164">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="32eb2-165">Framerate</span><span class="sxs-lookup"><span data-stu-id="32eb2-165">Framerate</span></span> |<span data-ttu-id="32eb2-166">Fotogramas por segundo de hello vídeo</span><span class="sxs-lookup"><span data-stu-id="32eb2-166">Frames per second of hello video</span></span> |
| <span data-ttu-id="32eb2-167">width</span><span class="sxs-lookup"><span data-stu-id="32eb2-167">width</span></span> |<span data-ttu-id="32eb2-168">ancho del vídeo en píxeles Hola</span><span class="sxs-lookup"><span data-stu-id="32eb2-168">width of hello video in pixels</span></span> |
| <span data-ttu-id="32eb2-169">height</span><span class="sxs-lookup"><span data-stu-id="32eb2-169">height</span></span> |<span data-ttu-id="32eb2-170">alto de vídeo en píxeles Hola</span><span class="sxs-lookup"><span data-stu-id="32eb2-170">height of hello video in pixels</span></span> |
| <span data-ttu-id="32eb2-171">Fragments</span><span class="sxs-lookup"><span data-stu-id="32eb2-171">Fragments</span></span> |<span data-ttu-id="32eb2-172">matriz de fragmentos basado en tiempo de vídeo en qué Hola está fragmentado metadatos</span><span class="sxs-lookup"><span data-stu-id="32eb2-172">array of time-based chunks of video into which hello metadata is chunked</span></span> |
| <span data-ttu-id="32eb2-173">start</span><span class="sxs-lookup"><span data-stu-id="32eb2-173">start</span></span> |<span data-ttu-id="32eb2-174">Hora de inicio de un fragmento en "tics"</span><span class="sxs-lookup"><span data-stu-id="32eb2-174">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="32eb2-175">duration</span><span class="sxs-lookup"><span data-stu-id="32eb2-175">duration</span></span> |<span data-ttu-id="32eb2-176">Duración de un fragmento en "tics"</span><span class="sxs-lookup"><span data-stu-id="32eb2-176">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="32eb2-177">interval</span><span class="sxs-lookup"><span data-stu-id="32eb2-177">interval</span></span> |<span data-ttu-id="32eb2-178">intervalo de cada evento de hello dado fragmento</span><span class="sxs-lookup"><span data-stu-id="32eb2-178">interval of each event within hello given fragment</span></span> |
| <span data-ttu-id="32eb2-179">events</span><span class="sxs-lookup"><span data-stu-id="32eb2-179">events</span></span> |<span data-ttu-id="32eb2-180">La matriz que contiene las regiones</span><span class="sxs-lookup"><span data-stu-id="32eb2-180">array containing regions</span></span> |
| <span data-ttu-id="32eb2-181">region</span><span class="sxs-lookup"><span data-stu-id="32eb2-181">region</span></span> |<span data-ttu-id="32eb2-182">Objeto que representa las palabras o frases detectadas</span><span class="sxs-lookup"><span data-stu-id="32eb2-182">object representing detected words or phrases</span></span> |
| <span data-ttu-id="32eb2-183">Idioma</span><span class="sxs-lookup"><span data-stu-id="32eb2-183">language</span></span> |<span data-ttu-id="32eb2-184">idioma del texto hello detectado dentro de una región</span><span class="sxs-lookup"><span data-stu-id="32eb2-184">language of hello text detected within a region</span></span> |
| <span data-ttu-id="32eb2-185">orientation</span><span class="sxs-lookup"><span data-stu-id="32eb2-185">orientation</span></span> |<span data-ttu-id="32eb2-186">orientación del texto hello detectado dentro de una región</span><span class="sxs-lookup"><span data-stu-id="32eb2-186">orientation of hello text detected within a region</span></span> |
| <span data-ttu-id="32eb2-187">lines</span><span class="sxs-lookup"><span data-stu-id="32eb2-187">lines</span></span> |<span data-ttu-id="32eb2-188">Matriz de líneas de texto detectadas en una región</span><span class="sxs-lookup"><span data-stu-id="32eb2-188">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="32eb2-189">text</span><span class="sxs-lookup"><span data-stu-id="32eb2-189">text</span></span> |<span data-ttu-id="32eb2-190">texto real de Hola</span><span class="sxs-lookup"><span data-stu-id="32eb2-190">hello actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="32eb2-191">Ejemplo de salida JSON</span><span class="sxs-lookup"><span data-stu-id="32eb2-191">JSON output example</span></span>
<span data-ttu-id="32eb2-192">Hello siguiente ejemplo de salida contiene información de vídeo general hello y varios fragmentos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="32eb2-192">hello following output example contains hello general video information and several video fragments.</span></span> <span data-ttu-id="32eb2-193">En cada fragmento de vídeo, contiene todas las regiones que se ha detectado por MP de OCR con lenguaje de Hola y su orientación del texto.</span><span class="sxs-lookup"><span data-stu-id="32eb2-193">In every video fragment, it contains every region which is detected by OCR MP with hello language and its text orientation.</span></span> <span data-ttu-id="32eb2-194">región de Hello también contiene cada línea de word en esta región con el texto de la línea hello, posición de la línea hello y cada información de word (contenido de word, posición y confianza) en esta línea.</span><span class="sxs-lookup"><span data-stu-id="32eb2-194">hello region also contains every word line in this region with hello line’s text, hello line’s position, and every word information (word content, position and confidence) in this line.</span></span> <span data-ttu-id="32eb2-195">Hola siguiente es un ejemplo y colocan algunos comentarios entre líneas.</span><span class="sxs-lookup"><span data-stu-id="32eb2-195">hello following is an example, and I put some comments inline.</span></span>

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
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
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

## <a name="net-sample-code"></a><span data-ttu-id="32eb2-196">Código de ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="32eb2-196">.NET sample code</span></span>

<span data-ttu-id="32eb2-197">siguiente de Hello programa muestra cómo:</span><span class="sxs-lookup"><span data-stu-id="32eb2-197">hello following program shows how to:</span></span>

1. <span data-ttu-id="32eb2-198">Crear un activo y cargar un archivo multimedia en activo de Hola.</span><span class="sxs-lookup"><span data-stu-id="32eb2-198">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="32eb2-199">Cree un trabajo con un archivo de configuración o valores preestablecidos de OCR.</span><span class="sxs-lookup"><span data-stu-id="32eb2-199">Create a job with an OCR configuration/preset file.</span></span>
3. <span data-ttu-id="32eb2-200">Descargar archivos de hello salida JSON.</span><span class="sxs-lookup"><span data-stu-id="32eb2-200">Download hello output JSON files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="32eb2-201">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="32eb2-201">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="32eb2-202">Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="32eb2-202">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="32eb2-203">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="32eb2-203">Example</span></span>

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

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="32eb2-204">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="32eb2-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="32eb2-205">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="32eb2-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="32eb2-206">Vínculos relacionados</span><span class="sxs-lookup"><span data-stu-id="32eb2-206">Related links</span></span>
[<span data-ttu-id="32eb2-207">Azure Media Services Analytics Overview (Información general sobre análisis de Servicios multimedia de Azure)</span><span class="sxs-lookup"><span data-stu-id="32eb2-207">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

