---
title: "tutoriales de flujo de trabajo de Premium de codificación de medios aaaAvanced"
description: "Este documento contiene tutoriales que muestran cómo tooperform avanzada tareas con flujo de trabajo de Premium de codificación de medios y también cómo toocreate flujos de trabajo complejos con el Diseñador de flujo de trabajo."
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a><span data-ttu-id="294f9-103">Tutoriales avanzados sobre el flujo de trabajo premium del codificador multimedia</span><span class="sxs-lookup"><span data-stu-id="294f9-103">Advanced Media Encoder Premium Workflow tutorials</span></span>
## <a name="overview"></a><span data-ttu-id="294f9-104">Información general</span><span class="sxs-lookup"><span data-stu-id="294f9-104">Overview</span></span>
<span data-ttu-id="294f9-105">Este documento contiene tutoriales que muestran cómo los flujos de trabajo de toocustomize con **Workflow Designer**.</span><span class="sxs-lookup"><span data-stu-id="294f9-105">This document contains walkthroughs that show how toocustomize workflows with  **Workflow Designer**.</span></span> <span data-ttu-id="294f9-106">Puede encontrar archivos de flujo de trabajo real hello [aquí](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span><span class="sxs-lookup"><span data-stu-id="294f9-106">You can find hello actual workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span></span>  

## <a name="toc"></a><span data-ttu-id="294f9-107">TABLA DE CONTENIDO</span><span class="sxs-lookup"><span data-stu-id="294f9-107">TOC</span></span>
<span data-ttu-id="294f9-108">se trata Hola temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="294f9-108">hello following topics are covered:</span></span>

* [<span data-ttu-id="294f9-109">Codificación de MXF en un MP4 de velocidad de bits única</span><span class="sxs-lookup"><span data-stu-id="294f9-109">Encoding MXF into a single bitrate MP4</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [<span data-ttu-id="294f9-110">Inicio de un nuevo flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="294f9-110">Starting a new workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [<span data-ttu-id="294f9-111">Uso de hello entrada de archivo de medios</span><span class="sxs-lookup"><span data-stu-id="294f9-111">Using hello Media File Input</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [<span data-ttu-id="294f9-112">Inspección de transmisiones multimedia</span><span class="sxs-lookup"><span data-stu-id="294f9-112">Inspecting media streams</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [<span data-ttu-id="294f9-113">Incorporación de un codificador de vídeo para la generación de archivos .MP4</span><span class="sxs-lookup"><span data-stu-id="294f9-113">Adding a video encoder for .MP4 file generation</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [<span data-ttu-id="294f9-114">Secuencia de audio de codificación Hola</span><span class="sxs-lookup"><span data-stu-id="294f9-114">Encoding hello audio stream</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [<span data-ttu-id="294f9-115">Multiplexación de secuencias de audio y vídeo en un contenedor MP4</span><span class="sxs-lookup"><span data-stu-id="294f9-115">Multiplexing Audio and Video streams into an MP4 container</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [<span data-ttu-id="294f9-116">Escribir el archivo MP4 de Hola</span><span class="sxs-lookup"><span data-stu-id="294f9-116">Writing hello MP4 file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [<span data-ttu-id="294f9-117">Crear un recurso de servicios multimedia de archivo de salida de hello</span><span class="sxs-lookup"><span data-stu-id="294f9-117">Creating a Media Services Asset from hello output file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [<span data-ttu-id="294f9-118">Hola de prueba terminado localmente el flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="294f9-118">Test hello finished workflow locally</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [<span data-ttu-id="294f9-119">Codificación de MXF en archivos MP4 de varias velocidades de bits: empaquetado dinámico habilitado</span><span class="sxs-lookup"><span data-stu-id="294f9-119">Encoding MXF into multibitrate MP4s - dynamic packaging enabled</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [<span data-ttu-id="294f9-120">Incorporación de una o más salidas MP4 adicionales</span><span class="sxs-lookup"><span data-stu-id="294f9-120">Adding one or more additional MP4 outputs</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [<span data-ttu-id="294f9-121">Nombres de salida de archivo de configuración Hola</span><span class="sxs-lookup"><span data-stu-id="294f9-121">Configuring hello file output names</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [<span data-ttu-id="294f9-122">Incorporación de una pista de audio independiente</span><span class="sxs-lookup"><span data-stu-id="294f9-122">Adding a separate Audio Track</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [<span data-ttu-id="294f9-123">Agregar Hola. Archivo SMIL ISM</span><span class="sxs-lookup"><span data-stu-id="294f9-123">Adding hello .ISM SMIL File</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [<span data-ttu-id="294f9-124">Codificación de MXF en archivos MP4 de varias velocidades de bits: plano mejorado</span><span class="sxs-lookup"><span data-stu-id="294f9-124">Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [<span data-ttu-id="294f9-125">Flujo de trabajo información general sobre tooenhance</span><span class="sxs-lookup"><span data-stu-id="294f9-125">Workflow overview tooenhance</span></span>](#workflow-overview-to-enhance)
  * [<span data-ttu-id="294f9-126">Convenciones de nomenclatura de los archivos</span><span class="sxs-lookup"><span data-stu-id="294f9-126">File Naming Conventions</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [<span data-ttu-id="294f9-127">Propiedades de componente en la raíz del flujo de trabajo de Hola de publicación</span><span class="sxs-lookup"><span data-stu-id="294f9-127">Publishing component properties onto hello workflow root</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [<span data-ttu-id="294f9-128">Se han generado nombres de archivo de salida que se basan en los valores de propiedad publicados</span><span class="sxs-lookup"><span data-stu-id="294f9-128">Have generated output file names rely on published property values</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [<span data-ttu-id="294f9-129">Agregar la salida de las miniaturas toomultibitrate MP4</span><span class="sxs-lookup"><span data-stu-id="294f9-129">Adding thumbnails toomultibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [<span data-ttu-id="294f9-130">Vistas en miniatura de flujo de trabajo información general sobre tooadd a</span><span class="sxs-lookup"><span data-stu-id="294f9-130">Workflow overview tooadd thumbnails to</span></span>](#workflow-overview-to-add-thumbnails-to)
  * [<span data-ttu-id="294f9-131">Incorporación de codificación JPG</span><span class="sxs-lookup"><span data-stu-id="294f9-131">Adding JPG Encoding</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [<span data-ttu-id="294f9-132">Relación con la conversión de espacio de colores</span><span class="sxs-lookup"><span data-stu-id="294f9-132">Dealing with Color Space conversion</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [<span data-ttu-id="294f9-133">Miniaturas de Hola de escritura</span><span class="sxs-lookup"><span data-stu-id="294f9-133">Writing hello thumbnails</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [<span data-ttu-id="294f9-134">Detección de errores en un flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="294f9-134">Detecting errors in a workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [<span data-ttu-id="294f9-135">Flujo de trabajo finalizado</span><span class="sxs-lookup"><span data-stu-id="294f9-135">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [<span data-ttu-id="294f9-136">Recorte basado en tiempo de salida MP4 de varias velocidades de bits</span><span class="sxs-lookup"><span data-stu-id="294f9-136">Time-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [<span data-ttu-id="294f9-137">Flujo de trabajo información general sobre toostart Agregar recorte</span><span class="sxs-lookup"><span data-stu-id="294f9-137">Workflow overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [<span data-ttu-id="294f9-138">Uso de hello secuencia recortador</span><span class="sxs-lookup"><span data-stu-id="294f9-138">Using hello Stream Trimmer</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [<span data-ttu-id="294f9-139">Flujo de trabajo finalizado</span><span class="sxs-lookup"><span data-stu-id="294f9-139">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [<span data-ttu-id="294f9-140">Introducción a Hola componente de la secuencia de comandos</span><span class="sxs-lookup"><span data-stu-id="294f9-140">Introducing hello Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [<span data-ttu-id="294f9-141">Scripting en un flujo de trabajo: hola a todos</span><span class="sxs-lookup"><span data-stu-id="294f9-141">Scripting within a workflow: hello world</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [<span data-ttu-id="294f9-142">Recorte basado en fotogramas de salida MP4 de varias velocidades de bits</span><span class="sxs-lookup"><span data-stu-id="294f9-142">Frame-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [<span data-ttu-id="294f9-143">Plano técnico toostart de información general sobre la adición de recorte para</span><span class="sxs-lookup"><span data-stu-id="294f9-143">Blueprint overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [<span data-ttu-id="294f9-144">Uso de hello XML de la lista de imágenes</span><span class="sxs-lookup"><span data-stu-id="294f9-144">Using hello Clip List XML</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [<span data-ttu-id="294f9-145">Modificar lista de clip Hola desde un componente de la secuencia de comandos</span><span class="sxs-lookup"><span data-stu-id="294f9-145">Modifying hello clip list from a Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [<span data-ttu-id="294f9-146">Incorporación de una propiedad de conveniencia ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="294f9-146">Adding a ClippingEnabled convenience property</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <span data-ttu-id="294f9-147"><a id="MXF_to_MP4"></a>Codificación de MXF en un MP4 de velocidad de bits única</span><span class="sxs-lookup"><span data-stu-id="294f9-147"><a id="MXF_to_MP4"></a>Encoding MXF into a single bitrate MP4</span></span>
<span data-ttu-id="294f9-148">En este tutorial crearemos un archivo .MP4 de velocidad de bits única con audio codificado AAC-HE a partir de un archivo de entrada .MXF.</span><span class="sxs-lookup"><span data-stu-id="294f9-148">In this walkthrough we'll create a single bitrate .MP4 file with AAC-HE encoded audio from an .MXF input file.</span></span>

### <span data-ttu-id="294f9-149"><a id="MXF_to_MP4_start_new"></a>Inicio de un nuevo flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="294f9-149"><a id="MXF_to_MP4_start_new"></a>Starting a new workflow</span></span>
<span data-ttu-id="294f9-150">Abra el Diseñador de flujo de trabajo y seleccione "File" (Archivo), "New Workspace" (Nueva área de trabajo), "Transcode Blueprint" (Transcodificar plano)</span><span class="sxs-lookup"><span data-stu-id="294f9-150">Open Workflow Designer and select "File"-"New Workspace"-"Transcode Blueprint"</span></span>

<span data-ttu-id="294f9-151">nuevo flujo de trabajo Hola mostrará 3 elementos:</span><span class="sxs-lookup"><span data-stu-id="294f9-151">hello new workflow will show 3 elements:</span></span>

* <span data-ttu-id="294f9-152">Primary Source File (Archivo de origen principal)</span><span class="sxs-lookup"><span data-stu-id="294f9-152">Primary Source File</span></span>
* <span data-ttu-id="294f9-153">Clip List XML (XML de la lista de clips)</span><span class="sxs-lookup"><span data-stu-id="294f9-153">Clip List XML</span></span>
* <span data-ttu-id="294f9-154">Output File/Asset (Recurso/Archivo de salida)</span><span class="sxs-lookup"><span data-stu-id="294f9-154">Output File/Asset</span></span>  

![Nuevo flujo de trabajo de codificación](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

<span data-ttu-id="294f9-156">*Nuevo flujo de trabajo de codificación*</span><span class="sxs-lookup"><span data-stu-id="294f9-156">*New Encoding Workflow*</span></span>

### <span data-ttu-id="294f9-157"><a id="MXF_to_MP4_with_file_input"></a>Uso de hello entrada de archivo de medios</span><span class="sxs-lookup"><span data-stu-id="294f9-157"><a id="MXF_to_MP4_with_file_input"></a>Using hello Media File Input</span></span>
<span data-ttu-id="294f9-158">En orden tooaccept nuestro archivo multimedia de entrada, uno se inicia con la adición de un componente de entrada de archivo de medios.</span><span class="sxs-lookup"><span data-stu-id="294f9-158">In order tooaccept our input media file, one starts with adding a Media File Input component.</span></span> <span data-ttu-id="294f9-159">tooadd un flujo de trabajo de toohello de componente, busque en el cuadro de búsqueda de repositorio de Hola y arrastre entrada Hola deseado en el panel del diseñador Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-159">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span> <span data-ttu-id="294f9-160">Hacer esto para entrada de archivo de medios hello y conéctese pin de la entrada de nombre de archivo archivo de código fuente principal componente toohello de Hola desde Hola entrada de archivo de medios.</span><span class="sxs-lookup"><span data-stu-id="294f9-160">Do this for hello Media File Input and connect hello Primary Source File component toohello Filename input pin from hello Media File Input.</span></span>

![Entrada de archivo multimedia conectada](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

<span data-ttu-id="294f9-162">*Entrada de archivo multimedia conectada*</span><span class="sxs-lookup"><span data-stu-id="294f9-162">*Connected Media File Input*</span></span>

<span data-ttu-id="294f9-163">Antes de que podemos hacer mucho más, en primer lugar necesitaremos el Diseñador de flujo de trabajo de tooindicate toohello qué archivo de ejemplo nos gustaría toouse toodesign con nuestro flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="294f9-163">Before we can do much else, we'll first need tooindicate toohello workflow designer what sample file we'd like toouse toodesign our workflow with.</span></span> <span data-ttu-id="294f9-164">toodo por lo tanto, haga clic en fondo del panel del Diseñador de Hola y busque la propiedad de archivo de origen principal de hello en el panel derecho de propiedad de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-164">toodo so, click hello designer pane background and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="294f9-165">Haga clic en el icono de carpeta de Hola y Hola seleccione deseado de flujo de trabajo de Hola de tootest archivo con.</span><span class="sxs-lookup"><span data-stu-id="294f9-165">Click hello folder icon and select hello desired file tootest hello workflow with.</span></span> <span data-ttu-id="294f9-166">En cuanto se haga esto, componente de entrada de archivo multimedia de hello inspeccionar el archivo hello y rellenar el archivo de hello tooreflect de PIN de salida que se inspeccionar.</span><span class="sxs-lookup"><span data-stu-id="294f9-166">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file it inspected.</span></span>

![Entrada de archivo multimedia rellena](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

<span data-ttu-id="294f9-168">*Entrada de archivo multimedia rellena*</span><span class="sxs-lookup"><span data-stu-id="294f9-168">*Populated Media File Input*</span></span>

<span data-ttu-id="294f9-169">Mientras que esto se especifica con lo que nos gustaría toowork con de entrada, no indica aún donde debe hacia la salida de hello codificado.</span><span class="sxs-lookup"><span data-stu-id="294f9-169">While this specifies with what input we'd like toowork with, it doesn't tell yet where hello encoded output should go to.</span></span> <span data-ttu-id="294f9-170">Similar hello toohow se ha configurado el archivo de origen principal, ahora configurar Hola propiedad variables de carpeta de salida, justo debajo de él.</span><span class="sxs-lookup"><span data-stu-id="294f9-170">Similar toohow hello Primary Source File was configured, now configure hello Output Folder Variable property, just below it.</span></span>

![Propiedades de entrada y salida configuradas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

<span data-ttu-id="294f9-172">*Propiedades de entrada y salida configuradas*</span><span class="sxs-lookup"><span data-stu-id="294f9-172">*Configured Input and Output properties*</span></span>

### <span data-ttu-id="294f9-173"><a id="MXF_to_MP4_streams"></a>Inspección de transmisiones multimedia</span><span class="sxs-lookup"><span data-stu-id="294f9-173"><a id="MXF_to_MP4_streams"></a>Inspecting media streams</span></span>
<span data-ttu-id="294f9-174">A menudo se desea tooknow cómo flujo Hola parece probable que fluye a través de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-174">Often it's desired tooknow how hello stream looks like that flows through hello workflow.</span></span> <span data-ttu-id="294f9-175">tooinspect una secuencia en cualquier punto en el flujo de trabajo de hello, simplemente haga clic en una salida o entrada pin en cualquiera de los componentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-175">tooinspect a stream at any point in hello workflow, just click an output or input pin on any of hello components.</span></span> <span data-ttu-id="294f9-176">En este caso, intente hacer clic en el pin de salida de vídeo sin comprimir Hola a partir de nuestros datos de archivo multimedia.</span><span class="sxs-lookup"><span data-stu-id="294f9-176">In this case, try clicking on hello Uncompressed Video output pin from our Media File Input.</span></span> <span data-ttu-id="294f9-177">Se abrirá un cuadro de diálogo que permite el vídeo de salida de hello tooinspect.</span><span class="sxs-lookup"><span data-stu-id="294f9-177">A dialog will open up that allows tooinspect hello outbound video.</span></span>

![Inspeccionar Hola pin de salida de vídeo sin comprimir](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

<span data-ttu-id="294f9-179">*Inspeccionar Hola pin de salida de vídeo sin comprimir*</span><span class="sxs-lookup"><span data-stu-id="294f9-179">*Inspecting hello Uncompressed Video output pin*</span></span>

<span data-ttu-id="294f9-180">En nuestro caso, nos dice por ejemplo que estamos trabajando con una entrada de 1920 x 1080 a 24 fotogramas por segundo en un muestreo 4:2:2 para ver un vídeo de casi 2 minutos.</span><span class="sxs-lookup"><span data-stu-id="294f9-180">In our case, it tells us for example that we're dealing with a 1920x1080 input at 24 frames per second in 4:2:2 sampling for a video of almost 2 minutes.</span></span>

### <span data-ttu-id="294f9-181"><a id="MXF_to_MP4_file_generation"></a>Incorporación de un codificador de vídeo para la generación de archivos .MP4</span><span class="sxs-lookup"><span data-stu-id="294f9-181"><a id="MXF_to_MP4_file_generation"></a>Adding a video encoder for .MP4 file generation</span></span>
<span data-ttu-id="294f9-182">Tenga en cuenta que ahora, una clavija de salida de vídeo sin comprimir y varias de audio sin comprimir están disponibles para su utilización en la entrada de archivo multimedia.</span><span class="sxs-lookup"><span data-stu-id="294f9-182">Note that now, an Uncompressed Video and multiple Uncompressed Audio output pins are available for use on our Media File Input.</span></span> <span data-ttu-id="294f9-183">En orden tooencode Hola vídeo entrante, necesitamos un componente de codificación - en este caso para la generación. Archivos MP4.</span><span class="sxs-lookup"><span data-stu-id="294f9-183">In order tooencode hello inbound video, we need an encoding component - in this case for generating .MP4 files.</span></span>

<span data-ttu-id="294f9-184">tooencode Hola tooH.264 de secuencia de vídeo, agregue la superficie del Diseñador de hello codificador de vídeo AVC componente toohello.</span><span class="sxs-lookup"><span data-stu-id="294f9-184">tooencode hello video stream tooH.264, add hello AVC Video Encoder component toohello designer surface.</span></span> <span data-ttu-id="294f9-185">Este componente toma una secuencia de vídeo sin comprimir como entrada y entrega una secuencia de vídeo comprimida AVC en su clavija de salida.</span><span class="sxs-lookup"><span data-stu-id="294f9-185">This component takes an uncompress video stream as input and delivers an AVC compressed video stream on its output pin.</span></span>

![Codificador de AVC no conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

<span data-ttu-id="294f9-187">*Codificador de AVC no conectado*</span><span class="sxs-lookup"><span data-stu-id="294f9-187">*Unconnected AVC Encoder*</span></span>

<span data-ttu-id="294f9-188">Sus propiedades determinan cómo exactamente Hola codificación ocurre.</span><span class="sxs-lookup"><span data-stu-id="294f9-188">Its properties determine how hello encoding exactly happens.</span></span> <span data-ttu-id="294f9-189">Echemos un vistazo a algunas de hello configuraciones más importantes:</span><span class="sxs-lookup"><span data-stu-id="294f9-189">Let's have a look at some of hello more important settings:</span></span>

* <span data-ttu-id="294f9-190">Ancho de salida y el alto de salida: estos determinan la resolución de Hola de vídeo de hello codificado.</span><span class="sxs-lookup"><span data-stu-id="294f9-190">Output width and Output height: these determine hello resolution of hello encoded video.</span></span> <span data-ttu-id="294f9-191">En nuestro caso seleccionaremos 640 x 360</span><span class="sxs-lookup"><span data-stu-id="294f9-191">In our case let's go with 640x360</span></span>
* <span data-ttu-id="294f9-192">Velocidad de fotogramas: cuando toopassthrough conjunto será simplemente adopten la velocidad de fotogramas de origen de hello, es posible toooverride aunque este.</span><span class="sxs-lookup"><span data-stu-id="294f9-192">Frame Rate: when set toopassthrough it will just adopt hello source frame rate, it's possible toooverride this though.</span></span> <span data-ttu-id="294f9-193">Tenga en cuenta que esa conversión de velocidad de fotogramas no está compensada por el movimiento.</span><span class="sxs-lookup"><span data-stu-id="294f9-193">Note that such framerate conversion is not motion-compensated.</span></span>
* <span data-ttu-id="294f9-194">Perfil y nivel: determinan perfil Hola AVC y nivel.</span><span class="sxs-lookup"><span data-stu-id="294f9-194">Profile and Level: these determine hello AVC profile and level.</span></span> <span data-ttu-id="294f9-195">tooconveniently obtener más información acerca de diferentes niveles de Hola y perfiles, haga clic en el icono de signo de interrogación de hello en el componente de codificador de vídeo AVC hello y página de Ayuda de hello mostrará información más detallada sobre cada uno de los niveles de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-195">tooconveniently get more information about hello different levels and profiles, click hello question mark icon on hello AVC Video Encoder component and hello help page will show more detail about each of hello levels.</span></span> <span data-ttu-id="294f9-196">Para nuestro ejemplo, vamos a Main Profile en nivel 3.2 (valor predeterminado de hello).</span><span class="sxs-lookup"><span data-stu-id="294f9-196">For our sample, let's go with Main Profile at level 3.2 (hello default).</span></span>
* <span data-ttu-id="294f9-197">Velocidad de bits (kbps) y modo de control de velocidad: en nuestro escenario optamos por una salida de velocidad de bits constante (CBR) a 1200 kbps</span><span class="sxs-lookup"><span data-stu-id="294f9-197">Rate Control Mode and Bitrate (kbps): in our scenario we opt for a constant bitrate (CBR) output at 1200 kbps</span></span>
* <span data-ttu-id="294f9-198">Formato de vídeo: este tema trata sobre Hola VUI (información de facilidad de uso de vídeo) que se escriba en la secuencia de hello H.264 (información del lado del que puede ser utilizada por un descodificador tooenhance Hola la visualización pero no es esencial toocorrectly descodificar):</span><span class="sxs-lookup"><span data-stu-id="294f9-198">Video Format: this is about hello VUI (Video Usability Information) that gets written into hello H.264 stream (side information that might be used by a decoder tooenhance hello display but not essential toocorrectly decode):</span></span>
* <span data-ttu-id="294f9-199">NTSC (habitual en Estados Unidos o Japón, utiliza 30 fps)</span><span class="sxs-lookup"><span data-stu-id="294f9-199">NTSC (typical for US or Japan, using 30 fps)</span></span>
* <span data-ttu-id="294f9-200">PAL (típica en Europa, utiliza 25 fps)</span><span class="sxs-lookup"><span data-stu-id="294f9-200">PAL (typical for Europe, using 25 fps)</span></span>
* <span data-ttu-id="294f9-201">Modo de cambiar el tamaño de GOP: vamos a configurar un tamaño fijo de GOP para nuestros fines con un intervalo de clave de 2 segundos con GOP cerrados.</span><span class="sxs-lookup"><span data-stu-id="294f9-201">GOP Size Mode: we'll configure Fixed GOP Size for our purposes with a Key Interval of 2 seconds with Closed GOPs.</span></span> <span data-ttu-id="294f9-202">Esto asegura la compatibilidad con hello que proporciona servicios de multimedia de Azure de empaquetado dinámico.</span><span class="sxs-lookup"><span data-stu-id="294f9-202">This ensures compatibility with hello dynamic packaging Azure Media Services provides.</span></span>

<span data-ttu-id="294f9-203">toofeed nuestro codificador AVC, conectarse pin de salida de vídeo sin comprimir de Hola desde Hola medios archivo componente toohello vídeo sin comprimir entrada pin de entrada de codificador de hello AVC.</span><span class="sxs-lookup"><span data-stu-id="294f9-203">toofeed our AVC encoder, connect hello Uncompressed Video output pin from hello Media File Input component toohello Uncompressed Video input pin from hello AVC encoder.</span></span>

![Codificador AVC conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

<span data-ttu-id="294f9-205">*Codificador principal AVC conectado*</span><span class="sxs-lookup"><span data-stu-id="294f9-205">*Connected AVC Main encoder*</span></span>

### <span data-ttu-id="294f9-206"><a id="MXF_to_MP4_audio"></a>Secuencia de audio de codificación Hola</span><span class="sxs-lookup"><span data-stu-id="294f9-206"><a id="MXF_to_MP4_audio"></a>Encoding hello audio stream</span></span>
<span data-ttu-id="294f9-207">En este punto, nos hemos codificado vídeo pero secuencia de audio sin comprimir original Hola aún debe toobe comprimido.</span><span class="sxs-lookup"><span data-stu-id="294f9-207">At this point, we have encoded video but hello original uncompressed audio stream still needs toobe compressed.</span></span> <span data-ttu-id="294f9-208">Para esto decidimos con AAC codificación por hello componente de codificador AAC (Dolby).</span><span class="sxs-lookup"><span data-stu-id="294f9-208">For this we'll go with AAC encoding by hello AAC Encoder (Dolby) component.</span></span> <span data-ttu-id="294f9-209">Agregar flujo de trabajo de toohello.</span><span class="sxs-lookup"><span data-stu-id="294f9-209">Add it toohello workflow.</span></span>

![Codificador de AVC no conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

<span data-ttu-id="294f9-211">*Codificador de AAC no conectado*</span><span class="sxs-lookup"><span data-stu-id="294f9-211">*Unconnected AAC encoder*</span></span>

<span data-ttu-id="294f9-212">Ahora hay una incompatibilidad: hay solo un único sin comprimir audio entrado pin de hello AAC codificador mientras más probable Hola de entrada de archivo de medios tendrán diferentes no lo está disponible de la secuencia de audio: uno para hello dejado canales de audio y otra para Hola Correcto.</span><span class="sxs-lookup"><span data-stu-id="294f9-212">Now there's an incompatibility: there's only a single uncompressed audio input pin from hello AAC Encoder while more than likely hello Media File Input will have two different uncompressed audio stream available: one for hello left audio channel and one for hello right.</span></span> <span data-ttu-id="294f9-213">(Si está trabajando con sonido envolvente, eso suma 6 canales). Por lo que no es posible toodirectly conéctelos audio Hola de origen de datos proporcionados por el archivo multimedia de hello codificador de audio AAC Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-213">(If you're dealing with surround sound, that's 6 channels.) So it's not possible toodirectly connect hello audio from hello Media File Input source into hello AAC audio encoder.</span></span> <span data-ttu-id="294f9-214">componente AAC Hello espera una secuencia de audio como los denominados "intercalada": un solo flujo que presente ambos Hola hello e izquierda canales correctos intercalados entre sí.</span><span class="sxs-lookup"><span data-stu-id="294f9-214">hello AAC component expects a so-called "interleaved" audio stream: a single stream that has both hello left and hello right channels interleaved with each other.</span></span> <span data-ttu-id="294f9-215">Una vez que sepamos de nuestro archivo de medios de origen las pistas de audio en la posición en el origen de hello, podemos generar esa secuencia de audio intercalada con hello correctamente tienen posiciones de los altavoces para izquierda y derecha.</span><span class="sxs-lookup"><span data-stu-id="294f9-215">Once we know from our source media file which audio tracks are on what position in hello source, we can generate such interleaved audio stream with hello correctly assigned speaker positions for left and right.</span></span>

<span data-ttu-id="294f9-216">En primer lugar una desearán toogenerated una secuencia intercalada de canales de audio de origen de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="294f9-216">First one will want toogenerated an interleaved stream from hello required source audio channels.</span></span> <span data-ttu-id="294f9-217">componente de Hello Interleaver de secuencia de Audio controlará esto para que podamos.</span><span class="sxs-lookup"><span data-stu-id="294f9-217">hello Audio Stream Interleaver component will handle this for us.</span></span> <span data-ttu-id="294f9-218">Agregar flujo de trabajo toohello y conéctese salidas de audio de Hola de hello proporcionados por el archivo multimedia en él.</span><span class="sxs-lookup"><span data-stu-id="294f9-218">Add it toohello workflow and connect hello audio outputs from hello Media File Input into it.</span></span>

![Entrelazador de secuencias de audio conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

<span data-ttu-id="294f9-220">*Entrelazador de secuencias de audio conectado*</span><span class="sxs-lookup"><span data-stu-id="294f9-220">*Connected Audio Stream Interleaver*</span></span>

<span data-ttu-id="294f9-221">Ahora que tenemos una secuencia de audio intercalada, todavía no especificamos donde coloca los altavoces de izquierdo o derecho de hello tooassign a.</span><span class="sxs-lookup"><span data-stu-id="294f9-221">Now that we have an interleaved audio stream, we still didn't specify where tooassign hello left or right speaker positions to.</span></span> <span data-ttu-id="294f9-222">En orden toospecify esto, podemos aprovechar Hola asignador de posición de altavoces.</span><span class="sxs-lookup"><span data-stu-id="294f9-222">In order toospecify this, we can leverage hello Speaker Position Assigner.</span></span>

![Incorporación de un asignador de posiciones de altavoz](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

<span data-ttu-id="294f9-224">*Incorporación de un asignador de posiciones de altavoz*</span><span class="sxs-lookup"><span data-stu-id="294f9-224">*Adding a Speaker Position Assigner*</span></span>

<span data-ttu-id="294f9-225">Configurar Hola asignador de posición de altavoces para su uso con un flujo de entrada estéreo a través de un filtro de valor preestablecido de codificador de "Custom" y Hola canal preestablecido denominado "2.0 (L, R)".</span><span class="sxs-lookup"><span data-stu-id="294f9-225">Configure hello Speaker Position Assigner for use with a stereo input stream through an Encoder Preset Filter of "Custom" and hello Channel Preset called "2.0 (L,R)".</span></span> <span data-ttu-id="294f9-226">(Esto asignará Hola altavoz izquierdo posición toochannel 1 y Hola altavoz derecho posición toochannel 2.)</span><span class="sxs-lookup"><span data-stu-id="294f9-226">(This will assign hello left speaker position toochannel 1 and hello right speaker position toochannel 2.)</span></span>

<span data-ttu-id="294f9-227">Conecte la salida de hello de entrada de toohello Hola altavoz posición asignador de hello AAC codificador.</span><span class="sxs-lookup"><span data-stu-id="294f9-227">Connect hello output of hello Speaker Position Assigner toohello input of hello AAC Encoder.</span></span> <span data-ttu-id="294f9-228">A continuación, indicar Hola AAC codificador toowork con un "2.0 (L, R)" predefinidos de canal, para que sepa toodeal con audio estéreo como entrada.</span><span class="sxs-lookup"><span data-stu-id="294f9-228">Then, tell hello AAC Encoder toowork with a "2.0 (L,R)" Channel Preset, so it knows toodeal with stereo audio as input.</span></span>

### <span data-ttu-id="294f9-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexación de secuencias de audio y vídeo en un contenedor MP4</span><span class="sxs-lookup"><span data-stu-id="294f9-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing Audio and Video streams into an MP4 container</span></span>
<span data-ttu-id="294f9-230">Una vez que tenemos nuestra secuencia de vídeo codificado AVC y nuestra secuencia de audio codificada AAC, podemos capturar ambas en un contenedor .MP4.</span><span class="sxs-lookup"><span data-stu-id="294f9-230">Given our AVC encoded video stream and our AAC encoded audio stream, we can capture both into an .MP4 container.</span></span> <span data-ttu-id="294f9-231">proceso de Hola de mezclar secuencias diferentes en una sola instrucción se denomina "multiplexación" (o "muxing").</span><span class="sxs-lookup"><span data-stu-id="294f9-231">hello process of mixing different streams into a single one is called "multiplexing" (or "muxing").</span></span> <span data-ttu-id="294f9-232">En este caso se estamos intercalación audio hello y secuencias de vídeo de hello en una sola coherente. Paquete de MP4.</span><span class="sxs-lookup"><span data-stu-id="294f9-232">In this case we're interleaving hello audio and hello video streams in a single coherent .MP4 package.</span></span> <span data-ttu-id="294f9-233">componente de Hola que coordina esto por una. Contenedor de MP4 se denomina hello multiplexor de ISO MPEG-4.</span><span class="sxs-lookup"><span data-stu-id="294f9-233">hello component that coordinates this for an .MP4 container is called hello ISO MPEG-4 Multiplexer.</span></span> <span data-ttu-id="294f9-234">Agregue una superficie del diseñador toohello y conecte Hola codificador de vídeo AVC y entradas de hello AAC codificador tooits.</span><span class="sxs-lookup"><span data-stu-id="294f9-234">Add one toohello designer surface and connect both hello AVC Video Encoder and hello AAC Encoder tooits inputs.</span></span>

![Multiplexor MPEG4 conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

<span data-ttu-id="294f9-236">*Multiplexor MPEG4 conectado*</span><span class="sxs-lookup"><span data-stu-id="294f9-236">*Connected MPEG4 Multiplexer*</span></span>

### <span data-ttu-id="294f9-237"><a id="MXF_to_MP4_writing_mp4"></a>Escribir el archivo MP4 de Hola</span><span class="sxs-lookup"><span data-stu-id="294f9-237"><a id="MXF_to_MP4_writing_mp4"></a>Writing hello MP4 file</span></span>
<span data-ttu-id="294f9-238">Al escribir un archivo de salida, se utiliza el componente de archivo de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="294f9-238">When writing an output file, hello File Output component is used.</span></span> <span data-ttu-id="294f9-239">Para que la salida se escriba toodisk se podemos conectar este resultado toohello de hello multiplexor de ISO MPEG-4.</span><span class="sxs-lookup"><span data-stu-id="294f9-239">We can connect this toohello output of hello ISO MPEG-4 Multiplexer so that its output gets written toodisk.</span></span> <span data-ttu-id="294f9-240">toodo, conectar Hola contenedor (MPEG-4) pin toohello escritura entrada conexión de salida del programa Hola a archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="294f9-240">toodo this, connect hello Container (MPEG-4) output pin toohello Write input pin of hello File Output.</span></span>

![Salida de archivo conectada](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

<span data-ttu-id="294f9-242">*Salida de archivo conectada*</span><span class="sxs-lookup"><span data-stu-id="294f9-242">*Connected File Output*</span></span>

<span data-ttu-id="294f9-243">Hola filename que se usará viene determinado por hello propiedad de archivo.</span><span class="sxs-lookup"><span data-stu-id="294f9-243">hello filename that will be used is determined by hello File property.</span></span> <span data-ttu-id="294f9-244">Mientras que esa propiedad puede ser tooa codificado valor, más probablemente una desearán tooset a través de una expresión en su lugar.</span><span class="sxs-lookup"><span data-stu-id="294f9-244">While that property can be hardcoded tooa given value, most likely one will want tooset it through an expression instead.</span></span>

<span data-ttu-id="294f9-245">flujo de trabajo de hello toohave determinar automáticamente la salida de hello propiedad de nombre de una expresión de archivo, haga clic en hello botón siguiente toohello nombre de archivo (icono de carpeta de toohello siguiente).</span><span class="sxs-lookup"><span data-stu-id="294f9-245">toohave hello workflow automatically determine hello output File name property from an expression, click hello buton next toohello File name (next toohello folder icon).</span></span> <span data-ttu-id="294f9-246">De hello menú desplegable, haga clic en "Expression".</span><span class="sxs-lookup"><span data-stu-id="294f9-246">From hello drop down menu then select "Expression".</span></span> <span data-ttu-id="294f9-247">Se abrirá el editor de expresiones Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-247">This will bring up hello expression editor.</span></span> <span data-ttu-id="294f9-248">Borrar contenido de hello del editor de hello en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="294f9-248">Clear hello contents of hello editor first.</span></span>

![Editor de expresiones vacío](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

<span data-ttu-id="294f9-250">*Editor de expresiones vacío*</span><span class="sxs-lookup"><span data-stu-id="294f9-250">*Empty Expression Editor*</span></span>

<span data-ttu-id="294f9-251">editor de expresiones de Hello permite tooenter cualquier valor literal, combinado con una o más variables.</span><span class="sxs-lookup"><span data-stu-id="294f9-251">hello expression editor allows tooenter any literal value, mixed with one or more variables.</span></span> <span data-ttu-id="294f9-252">Las variables comienzan con un signo de dólar.</span><span class="sxs-lookup"><span data-stu-id="294f9-252">Variables start with a dollar sign.</span></span> <span data-ttu-id="294f9-253">Tal y como se presionar la tecla de $ de hello, editor de hello mostrará un cuadro de lista desplegable con una variedad de las variables disponibles.</span><span class="sxs-lookup"><span data-stu-id="294f9-253">As you hit hello $ key, hello editor will show a dropdown box with a choice of available variables.</span></span> <span data-ttu-id="294f9-254">En nuestro caso, vamos a usar una combinación de variables de directorio de salida de hello y variable de nombre de archivo de entrada de base de hello:</span><span class="sxs-lookup"><span data-stu-id="294f9-254">In our case we'll use a combination of hello output directory variable and hello base input file name variable:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Editor de expresiones relleno](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

<span data-ttu-id="294f9-256">*Editor de expresiones relleno*</span><span class="sxs-lookup"><span data-stu-id="294f9-256">*Filled out Expression Editor*</span></span>

> [!NOTE]
> <span data-ttu-id="294f9-257">En orden toosee ver un archivo de salida de su trabajo de codificación en Azure, debe proporcionar un valor en el editor de expresiones Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-257">In order toosee see an output file of your encoding job in Azure, you must provide a value in hello expression editor.</span></span>
>
>

<span data-ttu-id="294f9-258">Cuando se confirma la expresión de hello presionando Aceptar, ventana de propiedades de hello obtendrá una vista previa toowhat valor Hola archivo propiedad resuelve en este momento.</span><span class="sxs-lookup"><span data-stu-id="294f9-258">When you confirm hello expression by hitting ok, hello property window will preview toowhat value hello File property resolves at this point in time.</span></span>

![La expresión de archivo resuelve el directorio de salida](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

<span data-ttu-id="294f9-260">*La expresión de archivo resuelve el directorio de salida*</span><span class="sxs-lookup"><span data-stu-id="294f9-260">*File Expression resolves output dir*</span></span>

### <span data-ttu-id="294f9-261"><a id="MXF_to_MP4_asset_from_output"></a>Crear un recurso de servicios multimedia de archivo de salida de hello</span><span class="sxs-lookup"><span data-stu-id="294f9-261"><a id="MXF_to_MP4_asset_from_output"></a>Creating a Media Services Asset from hello output file</span></span>
<span data-ttu-id="294f9-262">Mientras lo hemos incluido un archivo de salida MP4, todavía necesitamos tooindicate que pertenece este archivo toohello asset qué servicios de multimedia se generarán como resultado de ejecutar este flujo de trabajo de salida.</span><span class="sxs-lookup"><span data-stu-id="294f9-262">While we have written an MP4 output file, we still need tooindicate that this file belongs toohello output asset which media services will generate as a result of executing this workflow.</span></span> <span data-ttu-id="294f9-263">se utiliza toothis final, nodo de recurso de archivo de salida de hello en el lienzo de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-263">toothis end, hello Output File/Asset node on hello workflow canvas is used.</span></span> <span data-ttu-id="294f9-264">Todos los archivos entrantes en este nodo, formará parte del activo de servicios multimedia de Azure de hello resultante.</span><span class="sxs-lookup"><span data-stu-id="294f9-264">All incoming files into this node will make part of hello resulting Azure Media Services asset.</span></span>

<span data-ttu-id="294f9-265">Conectar Hola salida del archivo componente toohello recurso de archivo de salida componente toofinish Hola flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="294f9-265">Connect hello File Output component toohello Output File/Asset component toofinish hello workflow.</span></span>

![Flujo de trabajo finalizado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

<span data-ttu-id="294f9-267">*Flujo de trabajo finalizado*</span><span class="sxs-lookup"><span data-stu-id="294f9-267">*Finished Workflow*</span></span>

### <span data-ttu-id="294f9-268"><a id="MXF_to_MP4_test"></a>Hola de prueba terminado localmente el flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="294f9-268"><a id="MXF_to_MP4_test"></a>Test hello finished workflow locally</span></span>
<span data-ttu-id="294f9-269">tootest Hola flujo de trabajo localmente, pulse el botón de reproducción de hello en barra de herramientas de hello en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-269">tootest hello workflow locally, hit hello play button in hello toolbar at hello top.</span></span> <span data-ttu-id="294f9-270">Cuando finalice la ejecución del flujo de trabajo de hello, inspeccionar el resultado de hello generado en la carpeta de salida de hello configurado.</span><span class="sxs-lookup"><span data-stu-id="294f9-270">When hello workflow finished executing, inspect hello output generated in hello configured output folder.</span></span> <span data-ttu-id="294f9-271">Podrá ver Hola terminado de archivo de salida de MP4 que se codificó de archivo de origen de entrada de hello MXF.</span><span class="sxs-lookup"><span data-stu-id="294f9-271">You'll see hello finished MP4 output file that was encoded from hello MXF input source file.</span></span>

## <span data-ttu-id="294f9-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Codificación de MXF en archivos MP4: empaquetado dinámico de varias velocidades de bits habilitado</span><span class="sxs-lookup"><span data-stu-id="294f9-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Encoding MXF into MP4 - multibitrate dynamic packaging enabled</span></span>
<span data-ttu-id="294f9-273">En este tutorial crearemos un conjunto de archivos .MP4 de varias velocidades de bits con audio codificado AAC a partir de un archivo de entrada .MXF.</span><span class="sxs-lookup"><span data-stu-id="294f9-273">In this walkthrough we'll create a set of multiple bitrate MP4 files with AAC encoded audio from a single .MXF input file.</span></span>

<span data-ttu-id="294f9-274">Cuando se desea una salida de activos de velocidades de bits para su uso en combinación con las características de empaquetado dinámico de Hola que ofrece servicios de multimedia de Azure, varios archivos MP4 alineados con GOP de cada una velocidad de bits diferente y resolución deberán toobe generado.</span><span class="sxs-lookup"><span data-stu-id="294f9-274">When a multi-bitrate asset output is desired for use in combination with hello Dynamic Packaging features offered by Azure Media Services, multiple GOP-aligned MP4 files of each a different bitrate and resolution will need toobe generated.</span></span> <span data-ttu-id="294f9-275">por lo tanto, Hola toodo [codificación MXF en una velocidad de bits única MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) tutorial proporciona un buen punto de partida.</span><span class="sxs-lookup"><span data-stu-id="294f9-275">toodo so, hello [Encoding MXF into a single bitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) walkthrough provides us with a good starting point.</span></span>

![Inicio del flujo de trabajo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

<span data-ttu-id="294f9-277">*Inicio del flujo de trabajo*</span><span class="sxs-lookup"><span data-stu-id="294f9-277">*Starting Workflow*</span></span>

### <span data-ttu-id="294f9-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Incorporación de una o más salidas MP4 adicionales</span><span class="sxs-lookup"><span data-stu-id="294f9-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adding one or more additional MP4 outputs</span></span>
<span data-ttu-id="294f9-279">Cada archivo MP4 en el recurso resultante de Servicios multimedia de Azure será compatible con una velocidad de bits y resolución diferentes.</span><span class="sxs-lookup"><span data-stu-id="294f9-279">Every MP4 file in our resulting Azure Media Services asset will support a different bitrate and resolution.</span></span> <span data-ttu-id="294f9-280">Vamos a agregar uno o varios MP4 salida archivos toohello flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="294f9-280">Let's add one or more MP4 output files toohello workflow.</span></span>

<span data-ttu-id="294f9-281">toomake seguro tenemos todos nuestros codificadores de vídeo creados con Hola misma configuración, es más conveniente tooduplicate Hola codificador de vídeo AVC ya existente y configurar otra combinación de resolución y velocidad de bits (vamos a agregar uno de 960 x 540 en 25 fotogramas por segundo en 2,5 Mbps).</span><span class="sxs-lookup"><span data-stu-id="294f9-281">toomake sure we have all our video encoders created with hello same settings, it's most convenient tooduplicate hello already existing AVC Video Encoder and configure another combination of resolution and bitrate (let's add one of 960 x 540 at 25 frames per second at 2,5 Mbps).</span></span> <span data-ttu-id="294f9-282">tooduplicate del codificador existentes hello, copia pegarla en la superficie del Diseñador de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-282">tooduplicate hello existing encoder, copy paste it on hello designer surface.</span></span>

<span data-ttu-id="294f9-283">Conectar la conexión de salida de vídeo sin comprimir de Hola de hello entrada de archivo de medios en nuestro nuevo componente AVC.</span><span class="sxs-lookup"><span data-stu-id="294f9-283">Connect hello Uncompressed Video output pin of hello Media File Input into our new AVC component.</span></span>

![Segundo codificador AVC conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

<span data-ttu-id="294f9-285">*Segundo codificador AVC conectado*</span><span class="sxs-lookup"><span data-stu-id="294f9-285">*Second AVC encoder connected*</span></span>

<span data-ttu-id="294f9-286">Ahora se adaptan configuración Hola para nuestro nuevo toooutput de codificador AVC 960 x 540 a 2,5 Mbps.</span><span class="sxs-lookup"><span data-stu-id="294f9-286">Now adapt hello configuration for our new AVC encoder toooutput 960x540 at 2,5 Mbps.</span></span> <span data-ttu-id="294f9-287">(Utilice sus propiedades "Output width" (ancho de salida), "Output height" (Altura de salida) y "Bitrate (kbps)" (Velocidad de bits (kbps) para esto).</span><span class="sxs-lookup"><span data-stu-id="294f9-287">(Use its properties "Output width", "Output height", and "Bitrate (kbps)" for this.)</span></span>

<span data-ttu-id="294f9-288">Dado que deseamos asset resultante de hello toouse junto con el empaquetado dinámico de servicios multimedia de Azure, Hola extremo de streaming debe toobe capaz de generar a partir de estos archivos MP4 de fragmentos de MP4 HLS/fragmentado/DASH que son exactamente alineado tooeach otro de forma que los clientes que al cambian entre distintas velocidades de bits obtienen una sola experiencia sin problemas continua audio y vídeo.</span><span class="sxs-lookup"><span data-stu-id="294f9-288">Given we want toouse hello resulting asset together with Azure Media Services' dynamic packaging, hello streaming endpoint needs toobe capable of generating from these MP4 files HLS/Fragmented MP4/DASH fragments that are exactly aligned tooeach other in a way that clients that are switching between different bitrates get a single smooth continuous video and audio experience.</span></span> <span data-ttu-id="294f9-289">toomake que se producen, necesitamos tooensure que, en Propiedades de Hola de codificadores AVC se establece Hola tamaño GOP ("grupo de imágenes") para ambos archivos MP4 too2 segundos, lo que pueden hacer por:</span><span class="sxs-lookup"><span data-stu-id="294f9-289">toomake that happen, we need tooensure that, in hello properties of both AVC encoders hello GOP ("group of pictures") size for both MP4 files is set too2 seconds, which can be done by:</span></span>

* <span data-ttu-id="294f9-290">establecer el tamaño de GOP de tooFixed de modo de tamaño de GOP hello y</span><span class="sxs-lookup"><span data-stu-id="294f9-290">setting hello GOP Size Mode tooFixed GOP size and</span></span>
* <span data-ttu-id="294f9-291">segundos de tootwo de Hello intervalo de fotogramas clave.</span><span class="sxs-lookup"><span data-stu-id="294f9-291">hello Key Frame Interval tootwo seconds.</span></span>
* <span data-ttu-id="294f9-292">establecer Hola GOP IDR Control tooClosed GOP tooensure se permanente todos los GOP en sus propias sin dependencias</span><span class="sxs-lookup"><span data-stu-id="294f9-292">also set hello GOP IDR Control tooClosed GOP tooensure all GOP's are standing on their own without dependencies</span></span>

<span data-ttu-id="294f9-293">toomake nuestra toounderstand adecuada del flujo de trabajo, cambiar el nombre de codificador de hello primera AVC demasiado "codificador de vídeo AVC 640 x 360 1.200 kbps" y Hola segundo codificador AVC "codificador de vídeo AVC 960 x 540 kbps 2500".</span><span class="sxs-lookup"><span data-stu-id="294f9-293">toomake our workflow convenient toounderstand, rename hello first AVC encoder too"AVC Video Encoder 640x360 1200kbps" and hello second AVC encoder "AVC Video Encoder 960x540 2500 kbps".</span></span>

<span data-ttu-id="294f9-294">Ahora, agregue un segundo multiplexor ISO MPEG-4 y una segunda salida de archivo.</span><span class="sxs-lookup"><span data-stu-id="294f9-294">Now add a second ISO MPEG-4 Multiplexer and a second File Output.</span></span> <span data-ttu-id="294f9-295">Conecte Hola multiplexor toohello nueva AVC codificador y asegúrese de que se dirige la salida en el archivo de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="294f9-295">Connect hello multiplexer toohello new AVC encoder and make sure its output is directed into hello File Output.</span></span> <span data-ttu-id="294f9-296">A continuación, conecte también nueva de toohello de salida del codificador de audio de AAC Hola entrada de multiplexor.</span><span class="sxs-lookup"><span data-stu-id="294f9-296">Then also connect hello AAC audio encoder output toohello new multiplexer's input.</span></span> <span data-ttu-id="294f9-297">Hola archivo de salida a su vez, a continuación, puede ser tooadd de nodo de recurso de archivo de salida toohello conectado se toohello activo de servicios multimedia que va a crear.</span><span class="sxs-lookup"><span data-stu-id="294f9-297">hello File Output in turn can then be connected toohello Output File/Asset node tooadd it toohello Media Services Asset that will be created.</span></span>

![Segundo multiplexor y salida de archivo conectados](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

<span data-ttu-id="294f9-299">*Segundo multiplexor y salida de archivo conectados*</span><span class="sxs-lookup"><span data-stu-id="294f9-299">*Second Muxer and File Output connected*</span></span>

<span data-ttu-id="294f9-300">Por compatibilidad con el empaquetado dinámico de servicios multimedia de Azure, configure tooGOP recuento de hello del multiplexor modo de fragmento o la duración y establezca GOP Hola por fragmento too1.</span><span class="sxs-lookup"><span data-stu-id="294f9-300">For compatibility with Azure Media Services dynamic packaging, configure hello multiplexer's Chunk Mode tooGOP count or duration and set hello GOPs per chunk too1.</span></span> <span data-ttu-id="294f9-301">(Esto debe ser Hola predeterminada.)</span><span class="sxs-lookup"><span data-stu-id="294f9-301">(This should be hello default.)</span></span>

![Modos de fragmento del multiplexor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

<span data-ttu-id="294f9-303">*Modos de fragmento del multiplexor*</span><span class="sxs-lookup"><span data-stu-id="294f9-303">*Muxer Chunk Modes*</span></span>

<span data-ttu-id="294f9-304">Nota: puede que desee toorepeat este proceso para cualquier otro de velocidad de bits y la resolución combinaciones que desee toohave agregan una salida de activos toohello.</span><span class="sxs-lookup"><span data-stu-id="294f9-304">Note: you may want toorepeat this process for any other bitrate and resolution combinations you want toohave added toohello asset output.</span></span>

### <span data-ttu-id="294f9-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Nombres de salida de archivo de configuración Hola</span><span class="sxs-lookup"><span data-stu-id="294f9-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configuring hello file output names</span></span>
<span data-ttu-id="294f9-306">Contamos con más de un recurso de salida toohello único archivo agregado.</span><span class="sxs-lookup"><span data-stu-id="294f9-306">We have more than one single file added toohello output asset.</span></span> <span data-ttu-id="294f9-307">Esto proporciona una necesidad toomake seguro hello, nombres de archivo para cada uno de Hola archivos difieren entre sí y quizás incluso aplican una convención de nomenclatura de archivos para lo que usted está tratando con queda claro Hola nombre de archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="294f9-307">This provides a need toomake sure hello filenames for each of hello output files are different from each other and maybe even apply a file-naming convention so it becomes clear from hello file name what you're dealing with.</span></span>

<span data-ttu-id="294f9-308">Nomenclatura de salida de archivos se puede controlar a través de expresiones en el Diseñador de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-308">File output naming can be controlled through expressions in hello designer.</span></span> <span data-ttu-id="294f9-309">Abrir Panel de propiedades de Hola para uno de los componentes del archivo de salida de hello y abra el editor de expresiones de Hola para hello propiedad de archivo.</span><span class="sxs-lookup"><span data-stu-id="294f9-309">Open hello property pane for one of hello File Output components and open hello expression editor for hello File property.</span></span> <span data-ttu-id="294f9-310">Nuestro primer archivo de salida se configura a través de la siguiente expresión de hello (vea tutorial Hola para pasar de [velocidad de bits MXF tooa única salida MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span><span class="sxs-lookup"><span data-stu-id="294f9-310">Our first output file was configured through hello following expression (see hello tutorial for going from [MXF tooa single bitrate MP4 output](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

<span data-ttu-id="294f9-311">Esto significa que el nombre de archivo viene determinado por dos variables: Hola output directory toowrite en y hello nombre base del archivo de origen.</span><span class="sxs-lookup"><span data-stu-id="294f9-311">This means that our filename is determined by two variables: hello output directory toowrite in and hello source file base name.</span></span> <span data-ttu-id="294f9-312">primero Hola se expone como una propiedad en la raíz del flujo de trabajo de Hola y Hola este último viene determinado por el archivo de entrada de hello.</span><span class="sxs-lookup"><span data-stu-id="294f9-312">hello former is exposed as a property on hello workflow root and hello latter is determined by hello incoming file.</span></span> <span data-ttu-id="294f9-313">Tenga en cuenta ese directorio de salida de hello es lo que se utiliza para realizar pruebas locales; motor de flujo de trabajo de hello reemplazará esta propiedad cuando se ejecuta el flujo de trabajo de Hola por procesador de multimedia en la nube de hello en los servicios de multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="294f9-313">Note that hello output directory is what you use for local testing; this property will be overridden by hello workflow engine when hello workflow is executed by hello cloud-based media processor in Azure Media Services.</span></span>
<span data-ttu-id="294f9-314">toogive ambos archivos de nuestro salida un resultado coherente de nomenclatura, cambio Hola primero archivo nomenclatura expresión para:</span><span class="sxs-lookup"><span data-stu-id="294f9-314">toogive both our output files a consistent output naming, change hello first file naming expression to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="294f9-315">y en segundo lugar Hola para:</span><span class="sxs-lookup"><span data-stu-id="294f9-315">and hello second to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="294f9-316">Ejecutar una prueba intermedia ejecutar toomake seguro ambos archivos MP4 de salida se generan correctamente.</span><span class="sxs-lookup"><span data-stu-id="294f9-316">Execute an intermediate test run toomake sure both MP4 output files are properly generated.</span></span>

### <span data-ttu-id="294f9-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Incorporación de una pista de audio independiente</span><span class="sxs-lookup"><span data-stu-id="294f9-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adding a separate Audio Track</span></span>
<span data-ttu-id="294f9-318">Como veremos más adelante cuando se genera un toogo de archivo .ism con nuestros archivos MP4 de salida, se también necesitará un archivo MP4 de solo audio como pista de audio de hello para el streaming adaptable.</span><span class="sxs-lookup"><span data-stu-id="294f9-318">As we'll see later when we generate an .ism file toogo with our MP4 output files, we will also require a audio-only MP4 file as hello audio track for our adaptive streaming.</span></span> <span data-ttu-id="294f9-319">toocreate este archivo, agregue un flujo de trabajo de toohello muxer adicionales (multiplexor de ISO-MPEG-4) y conéctese pin de salida del codificador de hello AAC con su pin de entrada de seguimiento 1.</span><span class="sxs-lookup"><span data-stu-id="294f9-319">toocreate this file, add an additional muxer toohello workflow (ISO-MPEG-4 Multiplexer) and connect hello AAC encoder's output pin with its input pin for Track 1.</span></span>

![Multiplexor de audio agregado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

<span data-ttu-id="294f9-321">*Multiplexor de audio agregado*</span><span class="sxs-lookup"><span data-stu-id="294f9-321">*Audio Muxer Added*</span></span>

<span data-ttu-id="294f9-322">Cree un tercer flujo de salida de salida del archivo componente toooutput Hola de hello muxer y configure la expresión de asignación de nombres de archivo hello como:</span><span class="sxs-lookup"><span data-stu-id="294f9-322">Create a third File Output component toooutput hello outbound stream from hello muxer and configure hello file naming expression as:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Multiplexor de audio creando una salida de archivo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

<span data-ttu-id="294f9-324">*Multiplexor de audio creando una salida de archivo*</span><span class="sxs-lookup"><span data-stu-id="294f9-324">*Audio Muxer creating File Output*</span></span>

### <span data-ttu-id="294f9-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Agregar Hola. Archivo SMIL ISM</span><span class="sxs-lookup"><span data-stu-id="294f9-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adding hello .ISM SMIL File</span></span>
<span data-ttu-id="294f9-326">Hola empaquetado dinámico toowork en combinación con ambos MP4 en archivos (y Hola solo audio MP4) en el recurso de servicios multimedia, también es necesario un archivo de manifiesto (también denominado archivo de "SMIL": lenguaje de integración Multimedia sincronizada).</span><span class="sxs-lookup"><span data-stu-id="294f9-326">For hello dynamic packaging toowork in combination with both MP4 files (and hello audio-only MP4) in our Media Services asset, we also need a manifest file (also called a "SMIL" file: Synchronized Multimedia Integration Language).</span></span> <span data-ttu-id="294f9-327">Este archivo indica los servicios multimedia tooAzure qué archivos MP4 están disponibles para el empaquetado dinámico y cuáles de esos tooconsider para hello audio de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="294f9-327">This file indicates tooAzure Media Services what MP4 files are available for dynamic packaging and which of those tooconsider for hello audio streaming.</span></span> <span data-ttu-id="294f9-328">Un archivo de manifiesto típico para un conjunto de archivos MP4 con una única secuencia de audio tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="294f9-328">A typical manifest file for a set of MP4's with a single audio stream looks like this:</span></span>

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

<span data-ttu-id="294f9-329">archivo .ism de Hello contiene dentro de una instrucción switch, una tooeach de referencia de archivos de vídeo de MP4 individuales hello y además tooan MP4 que solo contiene audio Hola hace referencia a archivo de audio de toothose también una (o más).</span><span class="sxs-lookup"><span data-stu-id="294f9-329">hello .ism file contains within a switch statement, a reference tooeach of hello individual MP4 video files and in addition toothose also one (or more) audio file references tooan MP4 that only contains hello audio.</span></span>

<span data-ttu-id="294f9-330">Generar archivo de manifiesto de Hola para nuestro conjunto de MP4 puede realizarse a través de un componente denominado Hola "AMS manifiesto Writer".</span><span class="sxs-lookup"><span data-stu-id="294f9-330">Generating hello manifest file for our set of MP4's can be done through a component called hello "AMS Manifest Writer".</span></span> <span data-ttu-id="294f9-331">toouse, arrástrelo hasta la superficie de Hola y conecte clavijas de salida "Escritura finalizada" Hola desde Hola tres archivos salida componentes toohello el escritor de manifiesto de AMS de entrada.</span><span class="sxs-lookup"><span data-stu-id="294f9-331">toouse it, drag it onto hello surface and connect hello "Write Complete" output pins from hello three File Output components toohello AMS Manifest Writer input.</span></span> <span data-ttu-id="294f9-332">A continuación, asegúrese de salida de hello tooconnect seguro de hello AMS manifiesto escritor toohello recurso de archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="294f9-332">Then make sure tooconnect hello output of hello AMS Manifest Writer toohello Output File/Asset.</span></span>

<span data-ttu-id="294f9-333">Al igual que con nuestros otros componentes de salida archivo, configurar Hola .ism el nombre de salida de archivo con una expresión:</span><span class="sxs-lookup"><span data-stu-id="294f9-333">As with our other file output components, configure hello .ism file output name with an expression:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

<span data-ttu-id="294f9-334">El flujo de trabajo terminado es similar a Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="294f9-334">Our finished workflow looks like hello below:</span></span>

![El flujo de trabajo terminado MXF toomultibitrate MP4](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

<span data-ttu-id="294f9-336">*El flujo de trabajo terminado MXF toomultibitrate MP4*</span><span class="sxs-lookup"><span data-stu-id="294f9-336">*Finished MXF toomultibitrate MP4 workflow*</span></span>

## <span data-ttu-id="294f9-337"><a id="MXF_to__multibitrate_MP4"></a>Codificación de MXF en archivos MP4 de varias velocidades de bits: plano mejorado</span><span class="sxs-lookup"><span data-stu-id="294f9-337"><a id="MXF_to__multibitrate_MP4"></a>Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>
<span data-ttu-id="294f9-338">Hola [tutorial de flujo de trabajo anterior](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) hemos visto cómo se puede convertir un solo activo de entrada de MXF en un recurso de salida con archivos MP4 de varias velocidades de bits, un archivo MP4 de solo audio y un archivo de manifiesto para su uso junto con multimedia de Azure Servicios de empaquetado dinámico.</span><span class="sxs-lookup"><span data-stu-id="294f9-338">In hello [previous workflow walkthrough](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we've seen how a single MXF input asset can be converted into an output asset with multi-bitrate MP4 files, an audio-only MP4 file and a manifest file for use in conjunction with Azure Media Services dynamic packaging.</span></span>

<span data-ttu-id="294f9-339">Este tutorial le mostrará cómo pueden mejorar y algunos de los aspectos de hello pueden realizar más cómodo.</span><span class="sxs-lookup"><span data-stu-id="294f9-339">This walkthrough will show how some of hello aspects can be enhanced and made more convenient.</span></span>

### <span data-ttu-id="294f9-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Flujo de trabajo información general sobre tooenhance</span><span class="sxs-lookup"><span data-stu-id="294f9-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Workflow overview tooenhance</span></span>
![Multibitrate MP4 tooenhance de flujo de trabajo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

<span data-ttu-id="294f9-342">*Multibitrate MP4 tooenhance de flujo de trabajo*</span><span class="sxs-lookup"><span data-stu-id="294f9-342">*Multibitrate MP4 workflow tooenhance*</span></span>

### <span data-ttu-id="294f9-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>Convenciones de nomenclatura de los archivos</span><span class="sxs-lookup"><span data-stu-id="294f9-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>File Naming Conventions</span></span>
<span data-ttu-id="294f9-344">En el flujo de trabajo anterior Hola se especificó una expresión simple como base de Hola para generar nombres de archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="294f9-344">In hello previous workflow we specified a simple expression as hello basis for generating output file names.</span></span> <span data-ttu-id="294f9-345">Tenemos algunos duplicación aunque: todos los componentes de archivo de salida individual de Hola Hola de dicha expresión especificada.</span><span class="sxs-lookup"><span data-stu-id="294f9-345">We have some duplication though: all of hello hello individual output file components specified such expression.</span></span>

<span data-ttu-id="294f9-346">Por ejemplo, el componente de salida de archivo hello primer archivo de vídeo se configura con esta expresión:</span><span class="sxs-lookup"><span data-stu-id="294f9-346">For example, our file output component for hello first video file is configured with this expression:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="294f9-347">Mientras que para la segunda salida de hello vídeo, tenemos una expresión como:</span><span class="sxs-lookup"><span data-stu-id="294f9-347">While for hello second output video, we have an expression like:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="294f9-348">¿No sería más claro, menos propenso a errores y más fácil que pudiéramos eliminar parte de esta duplicación y hacer las cosas más configurables en su lugar?</span><span class="sxs-lookup"><span data-stu-id="294f9-348">Wouldn't it be cleaner, less error prone and more convenient if we could remove some of this duplication and make things more configurable instead?</span></span> <span data-ttu-id="294f9-349">Por suerte podemos: capacidades de expresión del Diseñador de hello en combinación con toocreate de propiedades personalizadas en la raíz del flujo de trabajo para la capacidad Hola nos ofrecen un nivel adicional de comodidad.</span><span class="sxs-lookup"><span data-stu-id="294f9-349">Luckily we can: hello designer's expression capabilities in combination with hello ability toocreate custom properties on our workflow root will give us an added layer of convenience.</span></span>

<span data-ttu-id="294f9-350">Supongamos que se obtendrá de unidades de configuración de nombre de archivo de hello velocidades de bits de archivos MP4 individuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-350">Let's assume we'll drive filename configuration from hello bitrates of hello individual MP4 files.</span></span> <span data-ttu-id="294f9-351">Estas velocidades de bits se deberá tratar de conseguir tooconfigure en un centro colocar (en raíz Hola de nuestro gráfico), desde donde podrá ser acceso generación del nombre de archivo tooconfigure y la unidad.</span><span class="sxs-lookup"><span data-stu-id="294f9-351">These bitrates we'll aim tooconfigure in one central place (on hello root of our graph), from where they'll be accessed tooconfigure and drive file name generation.</span></span> <span data-ttu-id="294f9-352">toodo, comenzamos mediante la publicación de la propiedad de velocidad de bits de Hola desde ambos raíz AVC codificadores toohello nuestro flujo de trabajo, para que sea accesible desde ambos raíz hello también a partir de los codificadores Hola AVC.</span><span class="sxs-lookup"><span data-stu-id="294f9-352">toodo this, we start by publishing hello bitrate property from both AVC encoders toohello root of our workflow, so that it becomes accessible from both hello root as well as from hello AVC encoders.</span></span> <span data-ttu-id="294f9-353">(Incluso aunque se muestren en dos lugares diferentes, hay solo un valor subyacente).</span><span class="sxs-lookup"><span data-stu-id="294f9-353">(Even if displayed in two different spots, there's only one underlying value.)</span></span>

### <span data-ttu-id="294f9-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Propiedades de componente en la raíz del flujo de trabajo de Hola de publicación</span><span class="sxs-lookup"><span data-stu-id="294f9-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Publishing component properties onto hello workflow root</span></span>
<span data-ttu-id="294f9-355">Abra codificador de hello primera AVC, vaya toohello propiedad de velocidad de bits (kbps) y de lista desplegable de hello elija Publicar.</span><span class="sxs-lookup"><span data-stu-id="294f9-355">Open hello first AVC encoder, go toohello Bitrate (kbps) property and from hello dropdown choose Publish.</span></span>

![Propiedad de velocidad de bits de publicación Hola](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

<span data-ttu-id="294f9-357">*Propiedad de velocidad de bits de publicación Hola*</span><span class="sxs-lookup"><span data-stu-id="294f9-357">*Publishing hello bitrate property*</span></span>

<span data-ttu-id="294f9-358">Configurar Hola publicar diálogo toopublish toohello raíz de nuestro gráfico de flujo de trabajo, con un nombre publicado de "video1bitrate" y un nombre para mostrar legible de "Velocidad de bits de vídeo 1".</span><span class="sxs-lookup"><span data-stu-id="294f9-358">Configure hello publish dialog toopublish toohello root of our workflow graph, with a published name of "video1bitrate" and a readable display name of "Video 1 Bitrate".</span></span> <span data-ttu-id="294f9-359">Configure un grupo personalizado denominado "Velocidades de bits de streaming" y haga clic en Publish (Publicar).</span><span class="sxs-lookup"><span data-stu-id="294f9-359">Configure a custom group name called "Streaming Bitrates" and hit Publish.</span></span>

![Propiedad de velocidad de bits de publicación Hola](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

<span data-ttu-id="294f9-361">*Cuadro de diálogo de publicación para la propiedad de velocidad de bits*</span><span class="sxs-lookup"><span data-stu-id="294f9-361">*Publishing dialog for bitrate property*</span></span>

<span data-ttu-id="294f9-362">Repita el proceso Hola mismo para la propiedad de velocidad de bits de Hola de hello en segundo lugar codificador AVC y asígnele el nombre "video2bitrate" con un nombre para mostrar de "Velocidad de bits de vídeo 2", en hello misma personalizado de grupo "Velocidades de bits de transmisión por secuencias".</span><span class="sxs-lookup"><span data-stu-id="294f9-362">Repeat hello same for hello bitrate property of hello second AVC encoder and name it "video2bitrate" with a display name of "Video 2 Bitrate", in hello same custom group "Streaming Bitrates".</span></span>

<span data-ttu-id="294f9-363">Si ahora se inspeccionar las propiedades de raíz del flujo de trabajo de hello, veremos nuestro grupo personalizado con hello aparecen dos propiedades publicados.</span><span class="sxs-lookup"><span data-stu-id="294f9-363">If we now inspect hello workflow root properties, we'll see our custom group with hello two published properties show up.</span></span> <span data-ttu-id="294f9-364">Ambos son reflejar el valor de Hola de su respectivo AVC codificador de velocidad de bits.</span><span class="sxs-lookup"><span data-stu-id="294f9-364">Both are reflecting hello value of their respective AVC encoder bitrate.</span></span>

![Propiedades de velocidad de bits publicadas en la raíz del flujo de trabajo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

<span data-ttu-id="294f9-366">Siempre que se desee tooaccess estas propiedades desde el código o desde una expresión, por lo que podemos similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="294f9-366">Whenever we want tooaccess these properties from code or from an expression, we can do so like this:</span></span>

* <span data-ttu-id="294f9-367">desde el código en línea de un componente justo debajo de la raíz de hello: node.getPropertyAsString('.. / video1bitrate', null)</span><span class="sxs-lookup"><span data-stu-id="294f9-367">from inline code from a component right below hello root: node.getPropertyAsString('../video1bitrate',null)</span></span>
* <span data-ttu-id="294f9-368">dentro de una expresión: ${ROOT_video1bitrate}</span><span class="sxs-lookup"><span data-stu-id="294f9-368">within an expression: ${ROOT_video1bitrate}</span></span>

<span data-ttu-id="294f9-369">Vamos a completar grupo de "Velocidades de bits de transmisión por secuencias" hello mediante la publicación de nuestro velocidad pista de audio en él.</span><span class="sxs-lookup"><span data-stu-id="294f9-369">Let's complete hello "Streaming Bitrates" group by publishing our audio track bitrate on it as well.</span></span> <span data-ttu-id="294f9-370">Dentro de las propiedades de Hola de hello AAC codificador, busque la configuración de velocidad de bits de Hola y seleccione Publicar de hello desplegable siguiente tooit.</span><span class="sxs-lookup"><span data-stu-id="294f9-370">Within hello properties of hello AAC Encoder, search for hello Bitrate setting and select Publish from hello dropdown next tooit.</span></span> <span data-ttu-id="294f9-371">Publicar toohello raíz del gráfico de hello con nombre "audio1bitrate" y el nombre "Velocidad de bits de Audio 1" dentro de nuestro grupo personalizado "Velocidades de bits de transmisión por secuencias" para mostrar.</span><span class="sxs-lookup"><span data-stu-id="294f9-371">Publish toohello root of hello graph with name "audio1bitrate" and display name "Audio 1 Bitrate" within our custom group "Streaming Bitrates".</span></span>

![Cuadro de diálogo de publicación para la velocidad de bits de archivos de audio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

<span data-ttu-id="294f9-373">*Cuadro de diálogo de publicación para la velocidad de bits de archivos de audio*</span><span class="sxs-lookup"><span data-stu-id="294f9-373">*Publishing dialog for audio bitrate*</span></span>

![Propiedades resultantes de audio y vídeo en la raíz](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

<span data-ttu-id="294f9-375">*Propiedades resultantes de audio y vídeo en la raíz*</span><span class="sxs-lookup"><span data-stu-id="294f9-375">*Resulting video and audio props on root*</span></span>

<span data-ttu-id="294f9-376">Tenga en cuenta que si se cambia cualquiera de los tres valores también vuelve a configurar y cambios Hola valores en los componentes respectivos Hola se vinculan con (y donde publicado desde).</span><span class="sxs-lookup"><span data-stu-id="294f9-376">Note that changing any of those three values also re-configures and changes hello values on hello respective components they are linked with (and where published from).</span></span>

### <span data-ttu-id="294f9-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Se han generado nombres de archivo de salida que se basan en los valores de propiedad publicados</span><span class="sxs-lookup"><span data-stu-id="294f9-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Have generated output file names rely on published property values</span></span>
<span data-ttu-id="294f9-378">En lugar de codificar nuestros nombres de archivo generado, podemos cambiar ahora la expresión de nombre de archivo en cada uno de los componentes toorely de archivo de salida de hello en las propiedades de la velocidad de bits de Hola que se acaba de publicar en la raíz del gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-378">Instead of hardcoding our generated file names, we can now change our filename expression on each of hello File Output components toorely on hello bitrate properties we just published on hello graph root.</span></span> <span data-ttu-id="294f9-379">A partir de la primera salida de archivo, buscar la propiedad de archivo de Hola y Editar expresión Hola similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="294f9-379">Starting with our first file output, find hello File property and edit hello expression like this:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

<span data-ttu-id="294f9-380">pueden obtener acceso y escritos cuando se alcanza el signo de dólar Hola teclado Hola mientras esté en la ventana de la expresión de hello distintos parámetros de Hello en esta expresión.</span><span class="sxs-lookup"><span data-stu-id="294f9-380">hello different parameters in this expression can be accessed and entered by hitting hello dollar sign on hello keyboard while in hello expression window.</span></span> <span data-ttu-id="294f9-381">Uno de los parámetros disponibles de hello es nuestra propiedad video1bitrate que se publicó con anterioridad.</span><span class="sxs-lookup"><span data-stu-id="294f9-381">One of hello available parameters is our video1bitrate property which we published earlier.</span></span>

![Acceso a los parámetros de una expresión](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

<span data-ttu-id="294f9-383">*Acceso a los parámetros de una expresión*</span><span class="sxs-lookup"><span data-stu-id="294f9-383">*Accessing parameters within an expression*</span></span>

<span data-ttu-id="294f9-384">Hola mismo para la salida de archivo de Hola para nuestro vídeo segundo:</span><span class="sxs-lookup"><span data-stu-id="294f9-384">Do hello same for hello file output for our second video:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

<span data-ttu-id="294f9-385">y para la salida de archivo de solo audio hello:</span><span class="sxs-lookup"><span data-stu-id="294f9-385">and for hello audio-only file output:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

<span data-ttu-id="294f9-386">Si ahora cambiamos la velocidad de bits de Hola para cualquiera de los archivos de audio o de vídeo de hello, codificador respectivos Hola se volverá a configurar y convención del nombre de archivo basado en la velocidad de bits Hola respetará todos los automática.</span><span class="sxs-lookup"><span data-stu-id="294f9-386">If we now change hello bitrate for any of hello video or audio files, hello respective encoder will be reconfigured and hello bitrate-based file name convention will be honored all automatic.</span></span>

## <span data-ttu-id="294f9-387"><a id="thumbnails_to__multibitrate_MP4"></a>Agregar la salida de las miniaturas toomultibitrate MP4</span><span class="sxs-lookup"><span data-stu-id="294f9-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adding thumbnails toomultibitrate MP4 output</span></span>
<span data-ttu-id="294f9-388">A partir de un flujo de trabajo que genera [una salida de archivos MP4 de una entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), nos encargaremos ahora en Agregar salida toohello de las miniaturas.</span><span class="sxs-lookup"><span data-stu-id="294f9-388">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into adding thumbnails toohello output.</span></span>

### <span data-ttu-id="294f9-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Vistas en miniatura de flujo de trabajo información general sobre tooadd a</span><span class="sxs-lookup"><span data-stu-id="294f9-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Workflow overview tooadd thumbnails to</span></span>
![Multibitrate MP4 toostart de flujo de trabajo de](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

<span data-ttu-id="294f9-391">*Multibitrate MP4 toostart de flujo de trabajo de*</span><span class="sxs-lookup"><span data-stu-id="294f9-391">*Multibitrate MP4 workflow toostart from*</span></span>

### <span data-ttu-id="294f9-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Incorporación de codificación JPG</span><span class="sxs-lookup"><span data-stu-id="294f9-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adding JPG Encoding</span></span>
<span data-ttu-id="294f9-393">núcleo de Hello de la generación de miniaturas será componente de codificador JPG hello, toooutput capaz de los archivos JPG.</span><span class="sxs-lookup"><span data-stu-id="294f9-393">hello heart of our thumbnail generation will be hello JPG Encoder component, able toooutput JPG files.</span></span>

![Codificador JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

<span data-ttu-id="294f9-395">*Codificador JPG*</span><span class="sxs-lookup"><span data-stu-id="294f9-395">*JPG Encoder*</span></span>

<span data-ttu-id="294f9-396">No podemos directamente sin embargo nos conectamos la secuencia de vídeo sin comprimir de hello entrada de archivo de medios en el codificador de hello JPG.</span><span class="sxs-lookup"><span data-stu-id="294f9-396">We cannot however directly connect our Uncompressed Video stream from hello Media File Input into hello JPG encoder.</span></span> <span data-ttu-id="294f9-397">En su lugar, se espera que va a pasar toobe fotogramas individuales.</span><span class="sxs-lookup"><span data-stu-id="294f9-397">Instead, it expects toobe handed individual frames.</span></span> <span data-ttu-id="294f9-398">Esto, podemos hacer mediante un componente de puerta de fotograma de vídeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-398">This, we can do through hello Video Frame Gate component.</span></span>

![Conectar un codificador de marco puerta toohello JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

<span data-ttu-id="294f9-400">*Conectar un codificador de marco puerta toohello JPG*</span><span class="sxs-lookup"><span data-stu-id="294f9-400">*Connecting a frame gate toohello JPG encoder*</span></span>

<span data-ttu-id="294f9-401">puerta de marco de Hello, una vez cada tantas segundos o marcos permite un toopass de fotograma de vídeo.</span><span class="sxs-lookup"><span data-stu-id="294f9-401">hello frame gate once every so many seconds or frames allows a video frame toopass.</span></span> <span data-ttu-id="294f9-402">tiempo de Hola y el intervalo de Hello desfase que esto sucede es configurable en las propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-402">hello interval and hello time offset with which this happens is configurable in hello properties.</span></span>

![Propiedades de puerta de fotogramas de vídeo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

<span data-ttu-id="294f9-404">*Propiedades de puerta de fotogramas de vídeo*</span><span class="sxs-lookup"><span data-stu-id="294f9-404">*Video Frame Gate properties*</span></span>

<span data-ttu-id="294f9-405">Vamos a crear una vista en miniatura de cada minuto estableciendo el modo de hello tooTime (segundos) y Hola too60 de intervalo.</span><span class="sxs-lookup"><span data-stu-id="294f9-405">Let's create a thumbnail every minute by setting hello mode tooTime (seconds) and hello Interval too60.</span></span>

### <span data-ttu-id="294f9-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Relación con la conversión de espacio de colores</span><span class="sxs-lookup"><span data-stu-id="294f9-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Dealing with Color Space conversion</span></span>
<span data-ttu-id="294f9-407">Aunque podría parecer lógico tanto ahora se pueden conectar los terminales de vídeo sin comprimir de puerta de marco de Hola y Hola entrada de archivo multimedia, se obtendría una advertencia si se debería hacerlo.</span><span class="sxs-lookup"><span data-stu-id="294f9-407">While it would seem logical both Uncompressed Video pins of hello frame gate and hello Media File Input can now be connected, we would get a warning if we would do so.</span></span>

![Error de espacio de colores de entrada](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

<span data-ttu-id="294f9-409">*Error de espacio de colores de entrada*</span><span class="sxs-lookup"><span data-stu-id="294f9-409">*Input color space error*</span></span>

<span data-ttu-id="294f9-410">Esto es porque la manera de hello en qué color se representa información en nuestro original sin formato sin comprimir secuencia de vídeo, procedentes de nuestro MXF es diferente de qué Hola JPG codificador está esperando.</span><span class="sxs-lookup"><span data-stu-id="294f9-410">This is because hello way in which colour information is represented in our original raw uncompressed video stream, coming from our MXF, is different from what hello JPG Encoder is expecting.</span></span> <span data-ttu-id="294f9-411">Más específicamente, una denominada "espacio de color" de "RGB" o "Escala de grises" es lo esperado tooflow en.</span><span class="sxs-lookup"><span data-stu-id="294f9-411">More specifically, a so-called "color space" of "RGB" or "Grayscale" is expected tooflow in.</span></span> <span data-ttu-id="294f9-412">Esto significa la que secuencia de vídeo entrante del que Hola vídeo fotograma puerta deberá toohave una conversión que se aplican en primer lugar con respecto a su espacio de color.</span><span class="sxs-lookup"><span data-stu-id="294f9-412">This means that hello Video Frame Gate's inbound video stream will need toohave a conversion applied regarding its color space first.</span></span>

<span data-ttu-id="294f9-413">Arrastre Hola de flujo de trabajo de hello convertidor de espacio de Color - Intel y conectar la puerta de marco tooour.</span><span class="sxs-lookup"><span data-stu-id="294f9-413">Drag onto hello workflow hello Color Space Converter - Intel and connect it tooour frame gate.</span></span>

![Conexión con un convertidor de espacio de colores](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

<span data-ttu-id="294f9-415">*Conexión con un convertidor de espacio de colores*</span><span class="sxs-lookup"><span data-stu-id="294f9-415">*Connecting a Color Space Convertor*</span></span>

<span data-ttu-id="294f9-416">En la ventana de propiedades de hello, elija entrada Hola BGR de 24 de hello valor preestablecido de lista.</span><span class="sxs-lookup"><span data-stu-id="294f9-416">In hello properties window, pick hello BGR 24 entry from hello Preset list.</span></span>

### <span data-ttu-id="294f9-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Miniaturas de Hola de escritura</span><span class="sxs-lookup"><span data-stu-id="294f9-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Writing hello thumbnails</span></span>
<span data-ttu-id="294f9-418">A diferencia de nuestro vídeo de MP4, Hola codificador JPG componente dará como resultado más de un archivo.</span><span class="sxs-lookup"><span data-stu-id="294f9-418">Different from our MP4 video's, hello JPG Encoder component will output more than one file.</span></span> <span data-ttu-id="294f9-419">En orden toodeal con esto, se puede usar un componente de sistema de escritura de archivo de escena búsqueda JPG: tomará miniaturas de Hola entrantes JPG y escribirlos, cada nombre de archivo que se va a seguidos de un número diferente.</span><span class="sxs-lookup"><span data-stu-id="294f9-419">In order toodeal with this, a Scene Search JPG File Writer component can be used: it will take hello incoming JPG thumbnails and write them out, each filename being suffixed by a different number.</span></span> <span data-ttu-id="294f9-420">(número de hello normalmente indica el número de Hola de segundos/unidades en flujo de Hola que Hola miniatura se extraen del).</span><span class="sxs-lookup"><span data-stu-id="294f9-420">(hello number typically indicating hello number of seconds/units in hello stream which hello thumbnail was drawn from.)</span></span>

![Introducción a Hola escena búsqueda JPG archivo escritor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

<span data-ttu-id="294f9-422">*Introducción a Hola escena búsqueda JPG archivo escritor*</span><span class="sxs-lookup"><span data-stu-id="294f9-422">*Introducing hello Scene Search JPG File Writer*</span></span>

<span data-ttu-id="294f9-423">Configurar la propiedad de ruta de acceso de carpeta de salida de hello con expresión hello: ${ROOT_outputWriteDirectory}</span><span class="sxs-lookup"><span data-stu-id="294f9-423">Configure hello Output Folder Path property with hello expression: ${ROOT_outputWriteDirectory}</span></span>

<span data-ttu-id="294f9-424">y Hola la propiedad con el prefijo de nombre de archivo:</span><span class="sxs-lookup"><span data-stu-id="294f9-424">and hello Filename Prefix property with:</span></span>

    ${ROOT_sourceFileBaseName}_thumb_

<span data-ttu-id="294f9-425">prefijo de Hello determinarán cómo se se denominan archivos de miniaturas de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-425">hello prefix will determine how hello thumbnail files are being named.</span></span> <span data-ttu-id="294f9-426">Se agregará como sufijo con posición de un número que indica Hola general flujo de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-426">They will be suffixed with a number indicating hello thumb's position in hello stream.</span></span>

![Propiedades de la escritura de archivos JPG de búsqueda de escenas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

<span data-ttu-id="294f9-428">*Propiedades de la escritura de archivos JPG de búsqueda de escenas*</span><span class="sxs-lookup"><span data-stu-id="294f9-428">*Scene Search JPG File Writer properties*</span></span>

<span data-ttu-id="294f9-429">Conecte el nodo de recurso de archivo de salida de hello escena búsqueda JPG archivo escritor toohello.</span><span class="sxs-lookup"><span data-stu-id="294f9-429">Connect hello Scene Search JPG File Writer toohello Output File/Asset node.</span></span>

### <span data-ttu-id="294f9-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detección de errores en un flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="294f9-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detecting errors in a workflow</span></span>
<span data-ttu-id="294f9-431">Conectar entrada Hola Hola color espacio convertidor toohello sin formato sin comprimir salida de vídeo.</span><span class="sxs-lookup"><span data-stu-id="294f9-431">Connect hello input of hello color space converter toohello raw uncompressed video output.</span></span> <span data-ttu-id="294f9-432">Ahora, ejecutar una prueba local para el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-432">Now perform a local test run for hello workflow.</span></span> <span data-ttu-id="294f9-433">Hay un flujo de trabajo de hello muchas posibilidades repentinamente se deje de ejecutarse y se indican con un contorno de color rojo en el componente de Hola que encontró un error:</span><span class="sxs-lookup"><span data-stu-id="294f9-433">There's a good chance hello workflow will suddenly stop executing and indicate with a red outline on hello component that encountered an error:</span></span>

![Error de convertidor de espacio de colores](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

<span data-ttu-id="294f9-435">*Error de convertidor de espacio de colores*</span><span class="sxs-lookup"><span data-stu-id="294f9-435">*Color Space Converter error*</span></span>

<span data-ttu-id="294f9-436">Haga clic en icono de "E" hello poco rojo en hello superior derecho de hello convertidor de espacio de Color componente toosee ¿cuál es el motivo de hello error al tratar de codificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-436">Click hello little red "E" icon in hello top right corner of hello Color Space Converter component toosee what's hello reason hello encoding attempt failed.</span></span>

![Cuadro de diálogo de error del convertidor de espacio de colores](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

<span data-ttu-id="294f9-438">*Cuadro de diálogo de error del convertidor de espacio de colores*</span><span class="sxs-lookup"><span data-stu-id="294f9-438">*Color Space Converter error dialog*</span></span>

<span data-ttu-id="294f9-439">Esto resulta, como puede ver, que espacio de colores entrante de hello estándar para los convertidores de espacio de color de hello tiene toobe rec601 para la conversión solicitada de YUV tooRGB.</span><span class="sxs-lookup"><span data-stu-id="294f9-439">It turns out, as you can see, that hello incoming color space standard for hello color space converter has toobe rec601 for our requested conversion of YUV tooRGB.</span></span> <span data-ttu-id="294f9-440">Aparentemente, nuestra secuencia no indica que fuera rec601.</span><span class="sxs-lookup"><span data-stu-id="294f9-440">Apparently our stream doesn't indicate it's rec601.</span></span> <span data-ttu-id="294f9-441">(Rec 601 es un estándar para codificar señales de vídeo analógicas entrelazadas en formato de vídeo digital.</span><span class="sxs-lookup"><span data-stu-id="294f9-441">(Rec 601 is a standard for encoding interlaced analog video signals in digital video form.</span></span> <span data-ttu-id="294f9-442">Especifica una región activa que abarcan 720 muestras de luminancia y 360 muestras cromáticas por línea.</span><span class="sxs-lookup"><span data-stu-id="294f9-442">It specifies an active region covering 720 luminance samples and 360 chrominance samples per line.</span></span> <span data-ttu-id="294f9-443">sistema de codificación de color de Hola se conoce como YCbCr 4:2:2.)</span><span class="sxs-lookup"><span data-stu-id="294f9-443">hello color encoding system is known as YCbCr 4:2:2.)</span></span>

<span data-ttu-id="294f9-444">toofix esto, se deberá indicar en los metadatos de Hola de nuestro flujo que estamos trabajando con contenido de rec601.</span><span class="sxs-lookup"><span data-stu-id="294f9-444">toofix this, we'll indicate on hello metadata of our stream that we're dealing with rec601 content.</span></span> <span data-ttu-id="294f9-445">toodo por lo que vamos a usar un componente actualizador de tipo de datos de vídeo, que colocamos entre nuestro raw hello y origen color espacio componente de conversión.</span><span class="sxs-lookup"><span data-stu-id="294f9-445">toodo so we'll use a Video Data Type Updater component, which we'll put in between our raw source and hello color space conversion component.</span></span> <span data-ttu-id="294f9-446">Esta actualización del tipo de datos permite la actualización manual de Hola de determinados datos de vídeo propiedades de tipo.</span><span class="sxs-lookup"><span data-stu-id="294f9-446">This data type updater allows for hello manual update of certain video data type properties.</span></span> <span data-ttu-id="294f9-447">Configurar un espacio de Color estándar de "Rec 601" tooindicate.</span><span class="sxs-lookup"><span data-stu-id="294f9-447">Configure it tooindicate a Color Space Standard of "Rec 601".</span></span> <span data-ttu-id="294f9-448">Esto hará que flujo de hello actualizador de tipo de datos de vídeo tootag Hola con espacio de colores de Hola "Rec 601" Si no hay ningún espacio de color definido todavía.</span><span class="sxs-lookup"><span data-stu-id="294f9-448">This will cause hello Video Data Type Updater tootag hello stream with hello "Rec 601" color space if there was no color space defined yet.</span></span> <span data-ttu-id="294f9-449">(No reemplazará los metadatos existentes, a menos que se activa la casilla de invalidación de Hola.)</span><span class="sxs-lookup"><span data-stu-id="294f9-449">(It will not override any existing metadata, unless hello Override checkbox was checked.)</span></span>

![Actualizar espacio de Color estándar en hello actualizador de tipo de datos](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

<span data-ttu-id="294f9-451">*Actualizar espacio de Color estándar en hello actualizador de tipo de datos*</span><span class="sxs-lookup"><span data-stu-id="294f9-451">*Updating Color Space Standard on hello Data Type Updater*</span></span>

### <span data-ttu-id="294f9-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Flujo de trabajo finalizado</span><span class="sxs-lookup"><span data-stu-id="294f9-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Finished Workflow</span></span>
<span data-ttu-id="294f9-453">Ahora que nuestro finaliza el flujo de trabajo, realice otra toosee de ejecución de pruebas que pasar.</span><span class="sxs-lookup"><span data-stu-id="294f9-453">Now that our our workflow is finished, do another test run toosee it pass.</span></span>

![Flujo de trabajo terminado para varias salidas MP4 con miniaturas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

<span data-ttu-id="294f9-455">*Flujo de trabajo terminado para varias salidas MP4 con miniaturas*</span><span class="sxs-lookup"><span data-stu-id="294f9-455">*Finished workflow for multi-mp4 output with thumbnails*</span></span>

## <span data-ttu-id="294f9-456"><a id="time_based_trim"></a>Recorte basado en tiempo de salida MP4 de varias velocidades de bits</span><span class="sxs-lookup"><span data-stu-id="294f9-456"><a id="time_based_trim"></a>Time-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="294f9-457">A partir de un flujo de trabajo que genera [una salida de archivos MP4 de una entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), ahora nos encargaremos en Recortar el vídeo de origen de hello en función de marcas de tiempo.</span><span class="sxs-lookup"><span data-stu-id="294f9-457">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on time-stamps.</span></span>

### <span data-ttu-id="294f9-458"><a id="time_based_trim_start"></a>Flujo de trabajo información general sobre toostart Agregar recorte</span><span class="sxs-lookup"><span data-stu-id="294f9-458"><a id="time_based_trim_start"></a>Workflow overview toostart adding trimming to</span></span>
![A partir de recorte de tooadd de flujo de trabajo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

<span data-ttu-id="294f9-460">*A partir de recorte de tooadd de flujo de trabajo*</span><span class="sxs-lookup"><span data-stu-id="294f9-460">*Starting workflow tooadd trimming to*</span></span>

### <span data-ttu-id="294f9-461"><a id="time_based_trim_use_stream_trimmer"></a>Uso de hello secuencia recortador</span><span class="sxs-lookup"><span data-stu-id="294f9-461"><a id="time_based_trim_use_stream_trimmer"></a>Using hello Stream Trimmer</span></span>
<span data-ttu-id="294f9-462">componente de flujo recortador Hola permite tootrim Hola principio y al final de un flujo de entrada que se base en información de tiempo (segundos, minutos,...). Recortador Hello no admite basada en el marco de recorte.</span><span class="sxs-lookup"><span data-stu-id="294f9-462">hello Stream Trimmer component allows tootrim hello beginning and ending of an input stream base on timing information (seconds, minutes, ...). hello trimmer does not support frame-based trimming.</span></span>

![Recortador de transmisiones](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

<span data-ttu-id="294f9-464">*Recortador de transmisiones*</span><span class="sxs-lookup"><span data-stu-id="294f9-464">*Stream Trimmer*</span></span>

<span data-ttu-id="294f9-465">En lugar de vincular directamente los codificadores de hello AVC y altavoces posición asignador toohello entrada de archivo multimedia, colocamos entre esos Recortador de flujo de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-465">Instead of linking hello AVC encoders and speaker position assigner toohello Media File Input directly, we'll put in between those hello stream trimmer.</span></span> <span data-ttu-id="294f9-466">(Uno para señal de vídeo de hello y otro para hello intercalan la señal de audio.)</span><span class="sxs-lookup"><span data-stu-id="294f9-466">(One for hello video signal and one for hello interleaved audio signal.)</span></span>

![Coloque el recortador de transmisiones entre ellos](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

<span data-ttu-id="294f9-468">*Coloque el recortador de transmisiones entre ellos*</span><span class="sxs-lookup"><span data-stu-id="294f9-468">*Put Stream Trimmer in between*</span></span>

<span data-ttu-id="294f9-469">Vamos a configurar recortador Hola para que sólo se procesará de vídeo y audio entre 15 y 60 segundos en vídeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-469">Let's configure hello trimmer so that we will only process video and audio between 15 seconds and 60 seconds in hello video.</span></span>

<span data-ttu-id="294f9-470">Vaya toohello propiedades de hello Recortador de secuencia de vídeo y configure la hora de inicio (15s) y propiedades de la hora de finalización (60 s).</span><span class="sxs-lookup"><span data-stu-id="294f9-470">Go toohello properties of hello Video Stream Trimmer and configure both Start Time (15s) and End Time (60s) properties.</span></span> <span data-ttu-id="294f9-471">toomake seguro tanto nuestro Recortador de audio y vídeo es siempre configurado toohello mismo empezar y terminar valores, se publicará esos raíz toohello de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-471">toomake sure both our audio and video trimmer are always configured toohello same start and end values, we will publish those toohello root of hello workflow.</span></span>

![Publique la propiedad de tiempo de inicio del recortador de transmisiones](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

<span data-ttu-id="294f9-473">*Publique la propiedad de tiempo de inicio del recortador de transmisiones*</span><span class="sxs-lookup"><span data-stu-id="294f9-473">*Publish start time property from Stream Trimmer*</span></span>

![Cuadro de diálogo de propiedades de publicación para el tiempo de inicio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

<span data-ttu-id="294f9-475">*Cuadro de diálogo de propiedades de publicación para el tiempo de inicio*</span><span class="sxs-lookup"><span data-stu-id="294f9-475">*Publish property dialog for start time*</span></span>

![Cuadro de diálogo de propiedades de publicación para el tiempo de finalización](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

<span data-ttu-id="294f9-477">*Cuadro de diálogo de propiedades de publicación para el tiempo de finalización*</span><span class="sxs-lookup"><span data-stu-id="294f9-477">*Publish property dialog for end time*</span></span>

<span data-ttu-id="294f9-478">Si ahora se inspecciona raíz Hola nuestro flujo de trabajo, ambas propiedades será claridad mostrada y se puede configurar a partir de ahí.</span><span class="sxs-lookup"><span data-stu-id="294f9-478">If we now inspect hello root of our workflow, both properties will be neatly displayed and configurable from there.</span></span>

![Propiedades publicadas disponibles en la raíz](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

<span data-ttu-id="294f9-480">*Propiedades publicadas disponibles en la raíz*</span><span class="sxs-lookup"><span data-stu-id="294f9-480">*Published properties available on root*</span></span>

<span data-ttu-id="294f9-481">Abrir propiedades de recorte de Hola desde recortador audio Hola ahora y configurar horas de inicio y final con una expresión que hace referencia toohello publicado propiedades en la raíz de Hola de nuestro flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="294f9-481">Now open hello trimming properties from hello audio trimmer and configure both start and end times with an expression that refers toohello published properties on hello root of our workflow.</span></span>

<span data-ttu-id="294f9-482">Para hello recorte audio hora de inicio:</span><span class="sxs-lookup"><span data-stu-id="294f9-482">For hello audio trimming start time:</span></span>

    ${ROOT_TrimmingStartTime}

<span data-ttu-id="294f9-483">y para el tiempo de finalización:</span><span class="sxs-lookup"><span data-stu-id="294f9-483">and for its end time:</span></span>

    ${ROOT_TrimmingEndTime}

### <span data-ttu-id="294f9-484"><a id="time_based_trim_finish"></a>Flujo de trabajo finalizado</span><span class="sxs-lookup"><span data-stu-id="294f9-484"><a id="time_based_trim_finish"></a>Finished Workflow</span></span>
![Flujo de trabajo finalizado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

<span data-ttu-id="294f9-486">*Flujo de trabajo finalizado*</span><span class="sxs-lookup"><span data-stu-id="294f9-486">*Finished Workflow*</span></span>

## <span data-ttu-id="294f9-487"><a id="scripting"></a>Introducción a Hola componente de la secuencia de comandos</span><span class="sxs-lookup"><span data-stu-id="294f9-487"><a id="scripting"></a>Introducing hello Scripted Component</span></span>
<span data-ttu-id="294f9-488">Componentes de script pueden ejecutar secuencias de comandos arbitrarias durante las fases de ejecución de Hola de nuestro flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="294f9-488">Scripted Components can execute arbitrary scripts during hello execution phases of our workflow.</span></span> <span data-ttu-id="294f9-489">Hay cuatro secuencias de comandos diferentes que se pueden ejecutar, cada uno con su propio contexto de ciclo de vida de flujo de trabajo Hola y de características específicas:</span><span class="sxs-lookup"><span data-stu-id="294f9-489">There are four different scripts that can be executed, each with specific characteristics and their own place in hello workflow life-cycle:</span></span>

* <span data-ttu-id="294f9-490">**commandScript**</span><span class="sxs-lookup"><span data-stu-id="294f9-490">**commandScript**</span></span>
* <span data-ttu-id="294f9-491">**realizeScript**</span><span class="sxs-lookup"><span data-stu-id="294f9-491">**realizeScript**</span></span>
* <span data-ttu-id="294f9-492">**processInputScript**</span><span class="sxs-lookup"><span data-stu-id="294f9-492">**processInputScript**</span></span>
* <span data-ttu-id="294f9-493">**lifeCycleScript**</span><span class="sxs-lookup"><span data-stu-id="294f9-493">**lifeCycleScript**</span></span>

<span data-ttu-id="294f9-494">documentación de Hola de hello componente incluye en el script va con más detalle para cada uno de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="294f9-494">hello documentation of hello Scripted Component goes in more detail for each of hello above.</span></span> <span data-ttu-id="294f9-495">En [Hola después de la sección](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** componente scripting es tooconstruct usa un xml cliplist en marcha de hello cuando se inicia el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-495">In [hello following section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** scripting component is used tooconstruct a cliplist xml on hello fly when hello workflow starts.</span></span> <span data-ttu-id="294f9-496">Este script se llama durante la instalación de componente de hello, lo que sucede solo una vez en su ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="294f9-496">This script is called during hello component setup, which happens only once in it's lifecycle.</span></span>

### <span data-ttu-id="294f9-497"><a id="scripting_hello_world"></a>Scripting en un flujo de trabajo: hola a todos</span><span class="sxs-lookup"><span data-stu-id="294f9-497"><a id="scripting_hello_world"></a>Scripting within a workflow: hello world</span></span>
<span data-ttu-id="294f9-498">Arrastre un componente de la secuencia de comandos en la superficie del Diseñador de Hola y cambie su nombre (por ejemplo, "SetClipListXML").</span><span class="sxs-lookup"><span data-stu-id="294f9-498">Drag a Scripted Component onto hello designer surface and rename it (for example, "SetClipListXML").</span></span>

![Incorporación de un componente generado por script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="294f9-500">*Incorporación de un componente generado por script*</span><span class="sxs-lookup"><span data-stu-id="294f9-500">*Adding a Scripted Component*</span></span>

<span data-ttu-id="294f9-501">Al examinar las propiedades de Hola de Hola componente de la secuencia de comandos, hello se muestran cuatro tipos diferentes de la secuencia de comandos, cada secuencia de comandos distintos de tooa configurable.</span><span class="sxs-lookup"><span data-stu-id="294f9-501">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Propiedades de componente generado por script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="294f9-503">*Propiedades de componente generado por script*</span><span class="sxs-lookup"><span data-stu-id="294f9-503">*Scripted Component properties*</span></span>

<span data-ttu-id="294f9-504">Desactive Hola processInputScript y abra el editor de Hola para hello realizeScript.</span><span class="sxs-lookup"><span data-stu-id="294f9-504">Clear hello processInputScript and open hello editor for hello realizeScript.</span></span> <span data-ttu-id="294f9-505">Ahora se está configuradas y listo toostart de scripting.</span><span class="sxs-lookup"><span data-stu-id="294f9-505">Now we're set up and ready toostart scripting.</span></span>

<span data-ttu-id="294f9-506">Las secuencias de comandos se escriben en Groovy, un lenguaje de scripting compilado dinámicamente para la plataforma Java de Hola que conserva la compatibilidad con Java.</span><span class="sxs-lookup"><span data-stu-id="294f9-506">Scripts are written in Groovy, a dynamically compiled scripting language for hello Java platform that retains compatibility with Java.</span></span> <span data-ttu-id="294f9-507">En realidad, la mayoría del código Java es también código Groovy válido.</span><span class="sxs-lookup"><span data-stu-id="294f9-507">Actually, most Java code is valid Groovy code.</span></span>

<span data-ttu-id="294f9-508">Vamos a escribir una secuencia de comandos simple hello world muy bueno en contexto de Hola de nuestra realizeScript.</span><span class="sxs-lookup"><span data-stu-id="294f9-508">Let's write a simple hello world groovy script in hello context of our realizeScript.</span></span> <span data-ttu-id="294f9-509">Escriba Hola siguiente en el editor de hello:</span><span class="sxs-lookup"><span data-stu-id="294f9-509">Enter hello following in hello editor:</span></span>

    node.log("hello world");

<span data-ttu-id="294f9-510">A continuación, ejecute una prueba de forma local.</span><span class="sxs-lookup"><span data-stu-id="294f9-510">Now execute a local test run.</span></span> <span data-ttu-id="294f9-511">Después de esta ejecución, inspeccionar (a través de la ficha de sistema de hello en Hola componente de la secuencia de comandos) Hola propiedad registros.</span><span class="sxs-lookup"><span data-stu-id="294f9-511">After this run, inspect (through hello System tab on hello Scripted Component) hello Logs property.</span></span>

![Salida de registro Hola a todos](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

<span data-ttu-id="294f9-513">*Salida de registro Hola a todos*</span><span class="sxs-lookup"><span data-stu-id="294f9-513">*Hello world log output*</span></span>

<span data-ttu-id="294f9-514">objeto de nodo de Hola se llame al método de registro de hello, hace referencia tooour actual "node" o un componente de hello nos estamos scripting dentro.</span><span class="sxs-lookup"><span data-stu-id="294f9-514">hello node object we call hello log method on, refers tooour current "node" or hello component we're scripting within.</span></span> <span data-ttu-id="294f9-515">Por lo tanto, cada componente tiene Hola capacidad toooutput el registro de datos disponible a través de la ficha de sistema de Hola. En este caso, hemos salida Hola literal de cadena "¡hello world".</span><span class="sxs-lookup"><span data-stu-id="294f9-515">Every component as such has hello ability toooutput logging data, available through hello system tab. In this case, we output hello string literal "hello world".</span></span> <span data-ttu-id="294f9-516">Toounderstand importante aquí es que esto puede resultar toobe una valiosa herramienta de depuración, proporcionando una visión general de la secuencia de comandos de hello realmente está realizando.</span><span class="sxs-lookup"><span data-stu-id="294f9-516">Important toounderstand here is that this can prove toobe an invaluable debugging tool, providing you with insight on what hello script is actually doing.</span></span>

<span data-ttu-id="294f9-517">Desde dentro de nuestro entorno de scripting, también tenemos acceso tooproperties en cuenta otros componentes.</span><span class="sxs-lookup"><span data-stu-id="294f9-517">From within our scripting environment, we also have access tooproperties on other components.</span></span> <span data-ttu-id="294f9-518">Pruebe esto:</span><span class="sxs-lookup"><span data-stu-id="294f9-518">Try this:</span></span>

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

<span data-ttu-id="294f9-519">Nuestra ventana de registro mostrará Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="294f9-519">Our log window will show us hello following:</span></span>

![Salida de registro para obtener acceso a las rutas de acceso del nodo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

<span data-ttu-id="294f9-521">*Salida de registro para obtener acceso a las rutas de acceso del nodo*</span><span class="sxs-lookup"><span data-stu-id="294f9-521">*Log output for accessing node paths*</span></span>

## <span data-ttu-id="294f9-522"><a id="frame_based_trim"></a>Recorte basado en fotogramas de salida MP4 de varias velocidades de bits</span><span class="sxs-lookup"><span data-stu-id="294f9-522"><a id="frame_based_trim"></a>Frame-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="294f9-523">A partir de un flujo de trabajo que genera [una salida de archivos MP4 de una entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), ahora nos encargaremos en vídeo de origen de hello según los recuentos de marco de recorte.</span><span class="sxs-lookup"><span data-stu-id="294f9-523">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on frame counts.</span></span>

### <span data-ttu-id="294f9-524"><a id="frame_based_trim_start"></a>Plano técnico toostart de información general sobre la adición de recorte para</span><span class="sxs-lookup"><span data-stu-id="294f9-524"><a id="frame_based_trim_start"></a>Blueprint overview toostart adding trimming to</span></span>
![Agregar recorte de toostart de flujo de trabajo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

<span data-ttu-id="294f9-526">*Agregar recorte de toostart de flujo de trabajo*</span><span class="sxs-lookup"><span data-stu-id="294f9-526">*Workflow toostart adding trimming to*</span></span>

### <span data-ttu-id="294f9-527"><a id="frame_based_trim_clip_list"></a>Uso de hello XML de la lista de imágenes</span><span class="sxs-lookup"><span data-stu-id="294f9-527"><a id="frame_based_trim_clip_list"></a>Using hello Clip List XML</span></span>
<span data-ttu-id="294f9-528">En todos los tutoriales de flujo de trabajo anterior, hemos usado el componente de entrada de archivo de medios de hello como el origen de entrada de vídeo.</span><span class="sxs-lookup"><span data-stu-id="294f9-528">In all previous workflow tutorials, we used hello Media File Input component as our video input source.</span></span> <span data-ttu-id="294f9-529">Para este escenario concreto, usaremos componente de origen de la lista de Clip de hello en su lugar.</span><span class="sxs-lookup"><span data-stu-id="294f9-529">For this specific scenario though, we'll be using hello Clip List Source component instead.</span></span> <span data-ttu-id="294f9-530">Tenga en cuenta que esto no debería ser Hola preferido forma de trabajar; usar solo hello Clip lista origen cuando hay un toodo verdadera razón de por lo que (al igual que en hello debajo de los casos, donde estamos realizando uso de las capacidades de hello clip lista recorte).</span><span class="sxs-lookup"><span data-stu-id="294f9-530">Note that this should not be hello preferred way of working; only use hello Clip List Source when there's a real reason toodo so (like in hello below case, where we're making use of hello clip list trimming capabilities).</span></span>

<span data-ttu-id="294f9-531">tooswitch de nuestro toohello de entrada de archivo multimedia origen de la lista de Clip, arrastre el componente de origen de la lista de imágenes de hello en la superficie de diseño de Hola y conectarse Hola Clip lista XML pin toohello Clip lista nodo XML del Diseñador de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-531">tooswitch from our Media File Input toohello Clip List Source, drag hello Clip List Source component onto hello design surface and connect hello Clip List XML pin toohello Clip List XML node of hello workflow designer.</span></span> <span data-ttu-id="294f9-532">Esto rellenará Hola Clip lista origen con PIN de salida, según el vídeo de entrada tooour.</span><span class="sxs-lookup"><span data-stu-id="294f9-532">This should populate hello Clip List Source with output pins, according tooour input video.</span></span> <span data-ttu-id="294f9-533">Conectar ahora PIN sin comprimir de Audio y vídeo sin comprimir de Hola de Hola Hola Clip lista origen toohello respectivos AVC codificadores y Interleaver de secuencia de Audio.</span><span class="sxs-lookup"><span data-stu-id="294f9-533">Now connect hello Uncompressed Video and Uncompressed Audio pins from hello hello Clip List Source toohello respective AVC Encoders and Audio Stream Interleaver.</span></span> <span data-ttu-id="294f9-534">Quitar ahora Hola entrada de archivo de medios.</span><span class="sxs-lookup"><span data-stu-id="294f9-534">Now remove hello Media File Input.</span></span>

![Reemplazar Hola entrada de archivo de medios con hello Clip lista origen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

<span data-ttu-id="294f9-536">*Reemplazar Hola entrada de archivo de medios con hello Clip lista origen*</span><span class="sxs-lookup"><span data-stu-id="294f9-536">*Replaced hello Media File Input with hello Clip List Source*</span></span>

<span data-ttu-id="294f9-537">componente de origen de la lista de Clip Hola toma como entrada un "Clip lista XML".</span><span class="sxs-lookup"><span data-stu-id="294f9-537">hello Clip List Source component takes as its input a "Clip List XML".</span></span> <span data-ttu-id="294f9-538">Al seleccionar hello tootest de archivo de origen con localmente, esta lista de clip xml es rellena automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="294f9-538">When selecting hello source file tootest with locally, this clip list xml is auto-populated for you.</span></span>

![Propiedad del XML de la lista de clips rellenado de forma automática](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

<span data-ttu-id="294f9-540">*Propiedad del XML de la lista de clips rellenado de forma automática*</span><span class="sxs-lookup"><span data-stu-id="294f9-540">*Auto-populated Clip List XML property*</span></span>

<span data-ttu-id="294f9-541">Para examinar un poco más de cerca xml toohello, este es su aspecto como:</span><span class="sxs-lookup"><span data-stu-id="294f9-541">Looking a bit closer toohello xml, this is how it looks like:</span></span>

![Cuadro de diálogo Edit clip list (Editar lista de clips)](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

<span data-ttu-id="294f9-543">*Cuadro de diálogo Edit clip list (Editar lista de clips)*</span><span class="sxs-lookup"><span data-stu-id="294f9-543">*Edit clip list dialog*</span></span>

<span data-ttu-id="294f9-544">Esto no obstante no refleja las capacidades de Hola Hola clip lista XML.</span><span class="sxs-lookup"><span data-stu-id="294f9-544">This however does not reflect hello capabilities of hello clip list xml.</span></span> <span data-ttu-id="294f9-545">Una opción que tenemos es tooadd un elemento "Recorte" en vídeo de Hola y origen de audio, similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="294f9-545">One option we have is tooadd a "Trim" element under both hello video and audio source, like this:</span></span>

![Agregar una lista de imágenes de recorte de elemento toohello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

<span data-ttu-id="294f9-547">*Agregar una lista de imágenes de recorte de elemento toohello*</span><span class="sxs-lookup"><span data-stu-id="294f9-547">*Adding a trim element toohello clip list*</span></span>

<span data-ttu-id="294f9-548">Si modifica Hola clip lista xml similar al siguiente por encima y realizar una serie de pruebas local, podrá ver vídeo Hola correctamente sido recortan entre 10 y 20 segundos en vídeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-548">If you modify hello clip list xml like this above and perform a local test run, you'll see hello video correctly been trimmed between 10 and 20 seconds in hello video.</span></span>

<span data-ttu-id="294f9-549">Toowhat contraria se produce cuando se realiza una ejecución local, aunque este mismo xml cliplist no tendría Hola mismo efecto cuando se aplica en un flujo de trabajo que se ejecuta en servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="294f9-549">Contrary toowhat happens when you do a local run though, this very same cliplist xml would not have hello same effect when applied in a workflow that runs in Azure Media Services.</span></span> <span data-ttu-id="294f9-550">Cuando empieza a codificador Premium de Azure, hello cliplist xml se genera cada vez que una vez más, en función de hello codificación de archivo de entrada de Hola se asignó el trabajo.</span><span class="sxs-lookup"><span data-stu-id="294f9-550">When Azure Premium Encoder starts, hello cliplist xml is generated every time again, based on hello input file hello encoding job was given.</span></span> <span data-ttu-id="294f9-551">Esto significa que cualquier cambio que hacemos en xml de hello Lamentablemente se reemplazaría.</span><span class="sxs-lookup"><span data-stu-id="294f9-551">This means that any changes we do on hello xml would unfortunately be overridden.</span></span>

<span data-ttu-id="294f9-552">toocounter hello cliplist xml borrarse cuando se inicia un trabajo de codificación, podemos volver a generar, en marcha Hola justo después del inicio de Hola de nuestro flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="294f9-552">toocounter hello cliplist xml being wiped when an encoding job is started, we can re-generate it on hello fly just after hello start of our workflow.</span></span> <span data-ttu-id="294f9-553">Tales acciones personalizadas se pueden realizar a través de lo que se denomina un "componente generado por script".</span><span class="sxs-lookup"><span data-stu-id="294f9-553">Such custom actions can be taken through what is called a "Scripted Component".</span></span> <span data-ttu-id="294f9-554">Para obtener más información, consulte [Introducing Hola componente incluye en el script](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span><span class="sxs-lookup"><span data-stu-id="294f9-554">For more information, see [Introducing hello Scripted Component](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span></span>

<span data-ttu-id="294f9-555">Arrastre un componente de la secuencia de comandos en la superficie del Diseñador de Hola y cámbiele el nombre demasiado "SetClipListXML".</span><span class="sxs-lookup"><span data-stu-id="294f9-555">Drag a Scripted Component onto hello designer surface and rename it too"SetClipListXML".</span></span>

![Incorporación de un componente generado por script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="294f9-557">*Incorporación de un componente generado por script*</span><span class="sxs-lookup"><span data-stu-id="294f9-557">*Adding a Scripted Component*</span></span>

<span data-ttu-id="294f9-558">Al examinar las propiedades de Hola de Hola componente de la secuencia de comandos, hello se muestran cuatro tipos diferentes de la secuencia de comandos, cada secuencia de comandos distintos de tooa configurable.</span><span class="sxs-lookup"><span data-stu-id="294f9-558">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Propiedades de componente generado por script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="294f9-560">*Propiedades de componente generado por script*</span><span class="sxs-lookup"><span data-stu-id="294f9-560">*Scripted Component properties*</span></span>

### <span data-ttu-id="294f9-561"><a id="frame_based_trim_modify_clip_list"></a>Modificar lista de clip Hola desde un componente de la secuencia de comandos</span><span class="sxs-lookup"><span data-stu-id="294f9-561"><a id="frame_based_trim_modify_clip_list"></a>Modifying hello clip list from a Scripted Component</span></span>
<span data-ttu-id="294f9-562">Antes de volver a podemos escribir hello cliplist xml que se genera durante el inicio del flujo de trabajo, necesitaremos contenido y la propiedad xml de toohave acceso toohello cliplist.</span><span class="sxs-lookup"><span data-stu-id="294f9-562">Before we can re-write hello cliplist xml that is generated during workflow startup, we'll need toohave access toohello cliplist xml property and contents.</span></span> <span data-ttu-id="294f9-563">Para ello podemos hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="294f9-563">We can do so like this:</span></span>

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Lista de clips entrantes que se están registrando](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

<span data-ttu-id="294f9-565">*Lista de clips entrantes que se están registrando*</span><span class="sxs-lookup"><span data-stu-id="294f9-565">*Incoming clip list being logged*</span></span>

<span data-ttu-id="294f9-566">Primero necesitamos una manera toodetermine desde qué momento hasta qué punto queremos tootrim Hola de vídeo.</span><span class="sxs-lookup"><span data-stu-id="294f9-566">First we need a way toodetermine from which point till which point we want tootrim hello video.</span></span> <span data-ttu-id="294f9-567">publicar de este usuario de menos conocimientos técnicos toohello adecuada del flujo de trabajo de hello, toomake raíz de toohello dos propiedades de gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-567">toomake this convenient toohello less-technical user of hello workflow, publish two properties toohello root of hello graph.</span></span> <span data-ttu-id="294f9-568">toodo esto, haga clic en la superficie del Diseñador de Hola y seleccione "Agregar propiedad":</span><span class="sxs-lookup"><span data-stu-id="294f9-568">toodo this, right click hello designer surface and select "Add Property":</span></span>

* <span data-ttu-id="294f9-569">Primera propiedad: "ClippingTimeStart" del tipo: "TIMECODE" (CÓDIGO DE TIEMPO)</span><span class="sxs-lookup"><span data-stu-id="294f9-569">First property: "ClippingTimeStart" of type: "TIMECODE"</span></span>
* <span data-ttu-id="294f9-570">Segunda propiedad: "ClippingTimeEnd" del tipo: "TIMECODE" (CÓDIGO DE TIEMPO)</span><span class="sxs-lookup"><span data-stu-id="294f9-570">Second property: "ClippingTimeEnd" of type: "TIMECODE"</span></span>

![Cuadro de diálogo Add Property (Agregar propiedad) para el tiempo de inicio del recorte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

<span data-ttu-id="294f9-572">*Cuadro de diálogo Add Property (Agregar propiedad) para el tiempo de inicio del recorte*</span><span class="sxs-lookup"><span data-stu-id="294f9-572">*Add Property dialog for clipping start time*</span></span>

![Propiedades del tiempo de recorte publicadas en la raíz del flujo de trabajo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

<span data-ttu-id="294f9-574">*Propiedades del tiempo de recorte publicadas en la raíz del flujo de trabajo*</span><span class="sxs-lookup"><span data-stu-id="294f9-574">*Published clipping time props on workflow root*</span></span>

<span data-ttu-id="294f9-575">Configure ambos valor adecuado de tooa de propiedades:</span><span class="sxs-lookup"><span data-stu-id="294f9-575">Configure both properties tooa suitable value:</span></span>

![Configurar Hola ajustar propiedades de inicio y finalización](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

<span data-ttu-id="294f9-577">*Configurar Hola ajustar propiedades de inicio y finalización*</span><span class="sxs-lookup"><span data-stu-id="294f9-577">*Configure hello clipping start and end properties*</span></span>

<span data-ttu-id="294f9-578">Ahora, desde dentro del script, podemos acceder a ambas propiedades, de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="294f9-578">Now, from within our script, we can access both properties, like this:</span></span>

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Ventana de registro que muestra el inicio y fin del recorte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

<span data-ttu-id="294f9-580">*Ventana de registro que muestra el inicio y fin del recorte*</span><span class="sxs-lookup"><span data-stu-id="294f9-580">*Log window showing start and end of clipping*</span></span>

<span data-ttu-id="294f9-581">Vamos a analizar las cadenas de código de tiempo de hello en un formato más cómodo de toouse, con una expresión regular simple:</span><span class="sxs-lookup"><span data-stu-id="294f9-581">Let's parse hello timecode strings into a more convenient toouse form, using a simple regular expression:</span></span>

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Ventana de registro con salida de código de tiempo redistribuida](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

<span data-ttu-id="294f9-583">*Ventana de registro con salida de código de tiempo redistribuida*</span><span class="sxs-lookup"><span data-stu-id="294f9-583">*Log window with output of parsed timecode*</span></span>

<span data-ttu-id="294f9-584">Con esta información en cuestión, ahora podemos modificamos inicio Hola de hello cliplist xml tooreflect y horas de finalización de hello deseado precisa para el marco de recorte de película Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-584">With this information at hand, we can now modify hello cliplist xml tooreflect hello start and end times for hello desired frame-accurate clipping of hello movie.</span></span>

![Elementos de recorte de tooadd de código de script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

<span data-ttu-id="294f9-586">*Elementos de recorte de tooadd de código de script*</span><span class="sxs-lookup"><span data-stu-id="294f9-586">*Script code tooadd trim elements*</span></span>

<span data-ttu-id="294f9-587">Esto se realizó mediante operaciones de manipulación de cadenas normales.</span><span class="sxs-lookup"><span data-stu-id="294f9-587">This was done through normal string manipulation operations.</span></span> <span data-ttu-id="294f9-588">Hola resultante imagen prediseñada modificada lista xml se escribe volver toohello clipListXML propiedad en la raíz del flujo de trabajo de Hola a través del método de "setProperty" hello.</span><span class="sxs-lookup"><span data-stu-id="294f9-588">hello resulting modified clip list xml is written back toohello clipListXML property on hello workflow root through hello "setProperty" method.</span></span> <span data-ttu-id="294f9-589">ventana de registro de Hello después de ejecutar otra prueba nos mostraría Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="294f9-589">hello log window after another test run would show us hello following:</span></span>

![Registro de lista de clip resultante Hola](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

<span data-ttu-id="294f9-591">*Registro de lista de clip resultante Hola*</span><span class="sxs-lookup"><span data-stu-id="294f9-591">*Logging hello resulting clip list*</span></span>

<span data-ttu-id="294f9-592">Hacer un toosee serie de pruebas, ¿cómo se han recortado secuencias de vídeo y audio de Hola.</span><span class="sxs-lookup"><span data-stu-id="294f9-592">Do a test-run toosee how hello video and audio streams have been clipped.</span></span> <span data-ttu-id="294f9-593">Tal y como se llevará a cabo más de una serie de pruebas con valores diferentes para puntos de recorte de hello, observará que los que no se tendrán en cuenta sin embargo!</span><span class="sxs-lookup"><span data-stu-id="294f9-593">As you'll do more than one test-run with different values for hello trimming points, you'll notice that those will not be taken into account however!</span></span> <span data-ttu-id="294f9-594">motivo Hello es ese diseñador hello, a diferencia de hello Azure en tiempo de ejecución, ocurre no invalidación hello cliplist xml con cada.</span><span class="sxs-lookup"><span data-stu-id="294f9-594">hello reason for this is that hello designer, unlike hello Azure runtime, does NOT override hello cliplist xml every run.</span></span> <span data-ttu-id="294f9-595">Esto significa que solo hello primera vez que se ha establecido Hola de entrada y salida puntos, hará que Hola xml tootransform, todos los otros Hola veces, la cláusula de restricción (si (clipListXML.indexOf ("<trim>") == -1)) impedirá que el flujo de trabajo de hello agregar otro recorte elemento cuando ya hay uno presente.</span><span class="sxs-lookup"><span data-stu-id="294f9-595">This means that only hello very first time you have set hello in and out points, will cause hello xml tootransform, all hello other times, our guard clause (if(clipListXML.indexOf("<trim>") == -1)) will prevent hello workflow from adding another trim element when there's already one present.</span></span>

<span data-ttu-id="294f9-596">toomake nuestro flujo de trabajo adecuada tootest localmente, es mejor agregar un código de mantenimiento de la casa que inspecciona si ya existe un elemento de recorte.</span><span class="sxs-lookup"><span data-stu-id="294f9-596">toomake our workflow convenient tootest locally, we best add some house-keeping code that inspects if a trim element was already present.</span></span> <span data-ttu-id="294f9-597">Si es así, se pueden eliminar antes de continuar modificando Hola xml con los nuevos valores de hello.</span><span class="sxs-lookup"><span data-stu-id="294f9-597">If so, we can remove it before continuing by modifying hello xml with hello new values.</span></span> <span data-ttu-id="294f9-598">En lugar de usar manipulaciones de cadena sin formato, es más seguro probablemente toodo esto a través de objeto xml real del modelo de análisis.</span><span class="sxs-lookup"><span data-stu-id="294f9-598">Rather than using plain string manipulations, it's probably safer toodo this through real xml object model parsing.</span></span>

<span data-ttu-id="294f9-599">Antes de que podemos agregar aunque dicho código, necesitaremos tooadd que un número de instrucciones de importación en hello inicia de nuestro script primero:</span><span class="sxs-lookup"><span data-stu-id="294f9-599">Before we can add such code though, we'll need tooadd a number of import statements at hello start of our script first:</span></span>

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

<span data-ttu-id="294f9-600">Después de esto, podemos agregar Hola requerido código de limpieza:</span><span class="sxs-lookup"><span data-stu-id="294f9-600">After this, we can add hello required cleaning code:</span></span>

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

<span data-ttu-id="294f9-601">Este código entrará justo encima de punto de hello en el que agregamos Hola elementos recorte toohello cliplist xml.</span><span class="sxs-lookup"><span data-stu-id="294f9-601">This code goes just above hello point at which we add hello trim elements toohello cliplist xml.</span></span>

<span data-ttu-id="294f9-602">En este momento, podemos ejecutar y modificar el flujo de trabajo como hora hasta que deseamos ejerciendo cambios Hola aplica alguna vez.</span><span class="sxs-lookup"><span data-stu-id="294f9-602">At this point, we can run and modify our workflow as much as we want while having hello changes applied ever time.</span></span>    

### <span data-ttu-id="294f9-603"><a id="frame_based_trim_clippingenabled_prop"></a>Incorporación de una propiedad de conveniencia ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="294f9-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adding a ClippingEnabled convenience property</span></span>
<span data-ttu-id="294f9-604">Como no siempre puede toohappen de recorte, vamos a concluir el flujo de trabajo mediante la adición de una cómoda marca booleana que indica si desea o no se tooenable recortar / recorte.</span><span class="sxs-lookup"><span data-stu-id="294f9-604">As you might not always want trimming toohappen, let's finish off our workflow by adding a convenient boolean flag that indicates whether or not we want tooenable trimming / clipping.</span></span>

<span data-ttu-id="294f9-605">Al igual que antes, publique una nueva propiedad toohello raíz nuestro flujo de trabajo denominado "ClippingEnabled" de tipo "BOOLEAN".</span><span class="sxs-lookup"><span data-stu-id="294f9-605">Just as before, publish a new property toohello root of our workflow called "ClippingEnabled" of type "BOOLEAN".</span></span>

![Publicación de una propiedad para habilitar el recorte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

<span data-ttu-id="294f9-607">*Publicación de una propiedad para habilitar el recorte*</span><span class="sxs-lookup"><span data-stu-id="294f9-607">*Published a property for enabling clipping*</span></span>

<span data-ttu-id="294f9-608">Con hello por debajo de la cláusula de restricción simple, podemos comprobar si es necesario recorte y decidir si nuestra lista de clip por lo tanto debe toobe modificado o no.</span><span class="sxs-lookup"><span data-stu-id="294f9-608">With hello below simple guard clause, we can check if trimming is required and decide if our clip list as such needs toobe modified or not.</span></span>

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <span data-ttu-id="294f9-609"><a id="code"></a>Código completo</span><span class="sxs-lookup"><span data-stu-id="294f9-609"><a id="code"></a>Complete code</span></span>
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a><span data-ttu-id="294f9-610">Consulte también:</span><span class="sxs-lookup"><span data-stu-id="294f9-610">Also see</span></span>
[<span data-ttu-id="294f9-611">Introducción de la codificación Premium en Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="294f9-611">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[<span data-ttu-id="294f9-612">¿Cómo tooUse Premium de codificación en servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="294f9-612">How tooUse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[<span data-ttu-id="294f9-613">Codificación de contenido a petición con Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="294f9-613">Encoding On-Demand Content with Azure Media Service</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

[<span data-ttu-id="294f9-614">Códecs y formatos de flujo de trabajo del Codificador multimedia Premium</span><span class="sxs-lookup"><span data-stu-id="294f9-614">Media Encoder Premium Workflow Formats and Codecs</span></span>](media-services-premium-workflow-encoder-formats.md)

[<span data-ttu-id="294f9-615">Archivos de flujo de trabajo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="294f9-615">Sample workflow files</span></span>](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[<span data-ttu-id="294f9-616">Explorador de Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="294f9-616">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="294f9-617">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="294f9-617">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="294f9-618">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="294f9-618">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
