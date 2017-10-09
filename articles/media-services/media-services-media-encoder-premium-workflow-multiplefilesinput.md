---
title: aaaMultiple de entrada de archivos y propiedades de componente de codificador de Premium - Azure | Documentos de Microsoft
description: "Este tema explica cómo la toouse setRuntimeProperties toouse entrada varios archivos y pasar el procesador de multimedia de flujo de trabajo de Premium de codificación de medios de toohello de datos personalizados."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: 7fb35bdd-9891-4401-a65b-ef3cc8190e8a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: xpouyat;anilmur;juliako
ms.openlocfilehash: e14d10fbf9669e0b88e5ba1c519f1ba5e0bafdd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a><span data-ttu-id="f59f2-103">Uso del codificador Premium con varios archivos de entrada y propiedades de los componentes</span><span class="sxs-lookup"><span data-stu-id="f59f2-103">Using multiple input files and component properties with Premium Encoder</span></span>
## <a name="overview"></a><span data-ttu-id="f59f2-104">Información general</span><span class="sxs-lookup"><span data-stu-id="f59f2-104">Overview</span></span>
<span data-ttu-id="f59f2-105">Hay escenarios en los que puede que tenga propiedades de componente de toocustomize, especifique el contenido del XML de la lista de Clip, o enviar varios archivos de entrada cuando se envía una tarea con hello **flujo de trabajo de Premium de codificación de medios** procesador multimedia.</span><span class="sxs-lookup"><span data-stu-id="f59f2-105">There are scenarios in which you might need toocustomize component properties, specify Clip List XML content, or send multiple input files when you submit a task with hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="f59f2-106">A continuación, se indican algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="f59f2-106">Some examples are:</span></span>

* <span data-ttu-id="f59f2-107">Texto superpuesto en vídeo y establecer el valor de texto hello (por ejemplo, Hola fecha actual) en tiempo de ejecución para cada vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="f59f2-107">Overlaying text on video and setting hello text value (for example, hello current date) at runtime for each input video.</span></span>
* <span data-ttu-id="f59f2-108">Se puede personalizar Hola Clip lista XML (toospecify uno o varios archivos, con o sin recortar, etcetera de origen.).</span><span class="sxs-lookup"><span data-stu-id="f59f2-108">Customizing hello Clip List XML (toospecify one or several source files, with or without trimming, etc.).</span></span>
* <span data-ttu-id="f59f2-109">Superponer una imagen de logotipo en vídeo de entrada de hello mientras Hola vídeo se codifica.</span><span class="sxs-lookup"><span data-stu-id="f59f2-109">Overlaying a logo image on hello input video while hello video is encoded.</span></span>
* <span data-ttu-id="f59f2-110">Codificación de varios idiomas de audio.</span><span class="sxs-lookup"><span data-stu-id="f59f2-110">Multiple audio language encoding.</span></span>

<span data-ttu-id="f59f2-111">Hola toolet **flujo de trabajo de Premium de codificación de medios** sabe que va a cambiar algunas propiedades en el flujo de trabajo de hello al crear la tarea hello o enviar varios archivos de entrada, que tiene una cadena de configuración que contiene toouse  **setRuntimeProperties** o **transcodeSource**.</span><span class="sxs-lookup"><span data-stu-id="f59f2-111">toolet hello **Media Encoder Premium Workflow** know that you are changing some properties in hello workflow when you create hello task or send multiple input files, you have toouse a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span></span> <span data-ttu-id="f59f2-112">Este tema se explica cómo toouse ellos.</span><span class="sxs-lookup"><span data-stu-id="f59f2-112">This topic explains how toouse them.</span></span>

## <a name="configuration-string-syntax"></a><span data-ttu-id="f59f2-113">Sintaxis de la cadena de configuración</span><span class="sxs-lookup"><span data-stu-id="f59f2-113">Configuration string syntax</span></span>
<span data-ttu-id="f59f2-114">tooset de cadena de configuración de Hola Hola codificación tarea usa un documento XML que el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="f59f2-114">hello configuration string tooset in hello encoding task uses an XML document that looks like this:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<transcodeRequest>
  <transcodeSource>
  </transcodeSource>
  <setRuntimeProperties>
    <property propertyPath="Media File Input/filename" value="VideoFileName.mp4" />
  </setRuntimeProperties>
</transcodeRequest>
```

<span data-ttu-id="f59f2-115">Hola siguiente es código de hello C# que lee la configuración de XML de Hola desde un archivo, actualícelo con Hola filename vídeo adecuada y la pasa toohello tarea en un trabajo:</span><span class="sxs-lookup"><span data-stu-id="f59f2-115">hello following is hello C# code that reads hello XML configuration from a file, update it with hello right video filename and passes it toohello task in a job:</span></span>

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass tooit hello name of hello 
// processor toouse for hello specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with hello encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify hello input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset toocontain hello results of hello job. 
// This output is specified as AssetCreationOptions.None, which 
// means hello output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a><span data-ttu-id="f59f2-116">Personalización de las propiedades de los componentes</span><span class="sxs-lookup"><span data-stu-id="f59f2-116">Customizing component properties</span></span>
### <a name="property-with-a-simple-value"></a><span data-ttu-id="f59f2-117">Propiedad con un valor simple</span><span class="sxs-lookup"><span data-stu-id="f59f2-117">Property with a simple value</span></span>
<span data-ttu-id="f59f2-118">En algunos casos, resulta útil toocustomize una propiedad del componente junto con el archivo de flujo de trabajo de Hola que se va toobe ejecutado por el flujo de trabajo de Premium de codificación de medios.</span><span class="sxs-lookup"><span data-stu-id="f59f2-118">In some cases, it is useful toocustomize a component property together with hello workflow file that is going toobe executed by Media Encoder Premium Workflow.</span></span>

<span data-ttu-id="f59f2-119">Supongamos que ha diseñado un flujo de trabajo que el texto se superpone en los vídeos y texto hello (por ejemplo, Hola fecha actual) se supone que el conjunto de toobe en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="f59f2-119">Suppose you designed a workflow that overlays text on your videos, and hello text (for example, hello current date) is supposed toobe set at runtime.</span></span> <span data-ttu-id="f59f2-120">Puede hacerlo mediante el envío de hello texto toobe establecer como nuevo valor para la propiedad de texto hello del componente de superposición de Hola de Hola de hello tarea de codificación.</span><span class="sxs-lookup"><span data-stu-id="f59f2-120">You can do this by sending hello text toobe set as hello new value for hello text property of hello overlay component from hello encoding task.</span></span> <span data-ttu-id="f59f2-121">Puede utilizar este mecanismo toochange otras propiedades de un componente de flujo de trabajo de hello (por ejemplo, la posición de Hola o color de superposición de hello, velocidad de bits de Hola de codificador de hello AVC, etcetera.).</span><span class="sxs-lookup"><span data-stu-id="f59f2-121">You can use this mechanism toochange other properties of a component in hello workflow (such as hello position or color of hello overlay, hello bitrate of hello AVC encoder, etc.).</span></span>

<span data-ttu-id="f59f2-122">**setRuntimeProperties** es toooverride usa una propiedad en componentes de Hola de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-122">**setRuntimeProperties** is used toooverride a property in hello components of hello workflow.</span></span>

<span data-ttu-id="f59f2-123">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f59f2-123">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text tooImage Converter/text" value="Today is Friday hello 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a><span data-ttu-id="f59f2-124">Propiedad con un valor XML</span><span class="sxs-lookup"><span data-stu-id="f59f2-124">Property with an XML value</span></span>
<span data-ttu-id="f59f2-125">encapsular tooset una propiedad que espera un valor XML, mediante el uso de `<![CDATA[ and ]]>`.</span><span class="sxs-lookup"><span data-stu-id="f59f2-125">tooset a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span></span>

<span data-ttu-id="f59f2-126">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f59f2-126">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

> [!NOTE]
> <span data-ttu-id="f59f2-127">Asegúrese de que no tooput un carro devolver justo después `<![CDATA[`.</span><span class="sxs-lookup"><span data-stu-id="f59f2-127">Make sure not tooput a carriage return just after `<![CDATA[`.</span></span>

### <a name="propertypath-value"></a><span data-ttu-id="f59f2-128">Valor de propertyPath</span><span class="sxs-lookup"><span data-stu-id="f59f2-128">propertyPath value</span></span>
<span data-ttu-id="f59f2-129">En los ejemplos anteriores de hello, era Hola propertyPath "archivos de medios / / nombre de archivo de entrada" o "/ inactiveTimeout" o "clipListXml".</span><span class="sxs-lookup"><span data-stu-id="f59f2-129">In hello previous examples, hello propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span></span>
<span data-ttu-id="f59f2-130">Esto es, por lo general, nombre hello del componente de hello y, a continuación, nombre de Hola de propiedad de Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-130">This is, in general, hello name of hello component, then hello name of hello property.</span></span> <span data-ttu-id="f59f2-131">Hello ruta de acceso puede tener más o menos niveles, al igual que "/ primarySourceFile" (porque es propiedad hello en raíz de Hola de flujo de trabajo de hello) o "/ vídeo procesamiento/gráfico superposición/opacidad" (porque Hola superposición está en un grupo).</span><span class="sxs-lookup"><span data-stu-id="f59f2-131">hello path can have more or fewer levels, like "/primarySourceFile" (because hello property is at hello root of hello workflow) or "/Video Processing/Graphic Overlay/Opacity" (because hello Overlay is in a group).</span></span>    

<span data-ttu-id="f59f2-132">toocheck Hola ruta de acceso y nombre de propiedad, botón de acción de Hola de uso que se encuentre inmediatamente al lado de cada propiedad.</span><span class="sxs-lookup"><span data-stu-id="f59f2-132">toocheck hello path and property name, use hello action button that is immediately beside each property.</span></span> <span data-ttu-id="f59f2-133">Puede hacer clic en este botón de acción y seleccione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="f59f2-133">You can click this action button and select **Edit**.</span></span> <span data-ttu-id="f59f2-134">Esto mostrará que Hola real el nombre de propiedad de Hola e inmediatamente por encima de él, Hola espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="f59f2-134">This will show you hello actual name of hello property, and immediately above it, hello namespace.</span></span>

![Acción o edición](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Propiedad](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a><span data-ttu-id="f59f2-137">Varios archivos de entrada</span><span class="sxs-lookup"><span data-stu-id="f59f2-137">Multiple input files</span></span>
<span data-ttu-id="f59f2-138">Cada tarea que se envía toohello **flujo de trabajo de Premium de codificación de medios** requiere dos recursos:</span><span class="sxs-lookup"><span data-stu-id="f59f2-138">Each task that you submit toohello **Media Encoder Premium Workflow** requires two assets:</span></span>

* <span data-ttu-id="f59f2-139">Hello primero uno es un *activos de flujo de trabajo* que contiene un archivo de flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f59f2-139">hello first one is a *Workflow Asset* that contains a workflow file.</span></span> <span data-ttu-id="f59f2-140">Puede diseñar archivos de flujo de trabajo mediante el uso de hello [Workflow Designer](media-services-workflow-designer.md).</span><span class="sxs-lookup"><span data-stu-id="f59f2-140">You can design workflow files by using hello [Workflow Designer](media-services-workflow-designer.md).</span></span>
* <span data-ttu-id="f59f2-141">Hello segunda es un *activo multimedia* que contiene los archivos de medios de Hola que desea tooencode.</span><span class="sxs-lookup"><span data-stu-id="f59f2-141">hello second one is a *Media Asset* that contains hello media file(s) that you want tooencode.</span></span>

<span data-ttu-id="f59f2-142">Si va a enviar varios medios archivos toohello **flujo de trabajo de Premium de codificación de medios** codificador, Hola siguiendo las restricciones se aplica:</span><span class="sxs-lookup"><span data-stu-id="f59f2-142">When you're sending multiple media files toohello **Media Encoder Premium Workflow** encoder, hello following constraints apply:</span></span>

* <span data-ttu-id="f59f2-143">Hola a todos los medios de hello archivos deben estar en mismo *activo multimedia*.</span><span class="sxs-lookup"><span data-stu-id="f59f2-143">All hello media files must be in hello same *Media Asset*.</span></span> <span data-ttu-id="f59f2-144">No se admite el uso de varios recursos multimedia.</span><span class="sxs-lookup"><span data-stu-id="f59f2-144">Using multiple Media Assets is not supported.</span></span>
* <span data-ttu-id="f59f2-145">Debe establecer el archivo principal de hello en este recurso multimedia (idealmente, se trata de hello principal archivo de vídeo que Hola codificador se pregunta a tooprocess).</span><span class="sxs-lookup"><span data-stu-id="f59f2-145">You must set hello primary file in this Media Asset (ideally, this is hello main video file that hello encoder is asked tooprocess).</span></span>
* <span data-ttu-id="f59f2-146">Se trata de datos de configuración toopass es necesario que incluya hello **setRuntimeProperties** o **transcodeSource** procesador toohello de elemento.</span><span class="sxs-lookup"><span data-stu-id="f59f2-146">It is necessary toopass configuration data that includes hello **setRuntimeProperties** and/or **transcodeSource** element toohello processor.</span></span>
  * <span data-ttu-id="f59f2-147">**setRuntimeProperties** es propiedad de nombre de archivo usado toooverride Hola u otra propiedad en componentes de Hola de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-147">**setRuntimeProperties** is used toooverride hello filename property or another property in hello components of hello workflow.</span></span>
  * <span data-ttu-id="f59f2-148">**transcodeSource** es toospecify usado hello contenido XML de la lista de imágenes.</span><span class="sxs-lookup"><span data-stu-id="f59f2-148">**transcodeSource** is used toospecify hello Clip List XML content.</span></span>

<span data-ttu-id="f59f2-149">Conexiones en el flujo de trabajo de hello:</span><span class="sxs-lookup"><span data-stu-id="f59f2-149">Connections in hello workflow:</span></span>

* <span data-ttu-id="f59f2-150">Si utiliza uno o varios componentes de entrada de archivo multimedia y planear toouse **setRuntimeProperties** toospecify Hola nombre de archivo, a continuación, no se conectan Hola archivo principal componente pin toothem.</span><span class="sxs-lookup"><span data-stu-id="f59f2-150">If you use one or several Media File Input components and plan toouse **setRuntimeProperties** toospecify hello file name, then do not connect hello primary file component pin toothem.</span></span> <span data-ttu-id="f59f2-151">Asegúrese de que no hay ninguna conexión entre el objeto de archivo principal de Hola y Hola las entradas del archivo de medios.</span><span class="sxs-lookup"><span data-stu-id="f59f2-151">Make sure that there is no connection between hello primary file object and hello Media File Input(s).</span></span>
* <span data-ttu-id="f59f2-152">Si prefiere toouse Clip lista XML y un componente de origen de los medios, a continuación, puede conectar ambos juntos.</span><span class="sxs-lookup"><span data-stu-id="f59f2-152">If you prefer toouse Clip List XML and one Media Source component, then you can connect both together.</span></span>

![Ninguna conexión desde el archivo de código fuente principal tooMedia proporcionados por el archivo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

<span data-ttu-id="f59f2-154">*No hay ninguna conexión desde el archivo principal de hello tooMedia componentes proporcionados por el archivo si utiliza la propiedad de nombre de archivo de setRuntimeProperties tooset Hola.*</span><span class="sxs-lookup"><span data-stu-id="f59f2-154">*There is no connection from hello primary file tooMedia File Input component(s) if you use setRuntimeProperties tooset hello filename property.*</span></span>

![Conexión de XML de la lista de Clip tooClip origen de la lista](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

<span data-ttu-id="f59f2-156">*Puede conectarse tooMedia origen de XML de la lista de imágenes y usar transcodeSource.*</span><span class="sxs-lookup"><span data-stu-id="f59f2-156">*You can connect Clip List XML tooMedia Source and use transcodeSource.*</span></span>

### <a name="clip-list-xml-customization"></a><span data-ttu-id="f59f2-157">Personalización del XML de lista de clips</span><span class="sxs-lookup"><span data-stu-id="f59f2-157">Clip List XML customization</span></span>
<span data-ttu-id="f59f2-158">Puede especificar Hola Clip lista XML en el flujo de trabajo de hello en tiempo de ejecución mediante **transcodeSource** en la configuración de Hola de cadena XML.</span><span class="sxs-lookup"><span data-stu-id="f59f2-158">You can specify hello Clip List XML in hello workflow at runtime by using **transcodeSource** in hello configuration string XML.</span></span> <span data-ttu-id="f59f2-159">Esto requiere Hola Clip lista XML pin toobe conectado toohello origen multimedia componente de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-159">This requires hello Clip List XML pin toobe connected toohello Media Source component in hello workflow.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <transcodeSource>
      <clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
      </clipList>
    </transcodeSource>
    <setRuntimeProperties>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="f59f2-160">Si desea toospecify /primarySourceFile toouse esta salida de hello de propiedad tooname archivos mediante 'Expresiones', se recomienda pasar Hola Clip lista XML como una propiedad *después* propiedad /primarySourceFile de hello, tooavoid tener Hola Clip lista reemplazarse por valor de /primarySourceFile Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-160">If you want toospecify /primarySourceFile toouse this property tooname hello output files by using 'Expressions', then we recommend passing hello Clip List XML as a property *after* hello /primarySourceFile property, tooavoid having hello Clip List be overridden by hello /primarySourceFile setting.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="c:\temp\start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="f59f2-161">Con un recorte preciso de marco adicional:</span><span class="sxs-lookup"><span data-stu-id="f59f2-161">With additional frame-accurate trimming:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a><span data-ttu-id="f59f2-162">Ejemplo 1: Superposición de una imagen en la parte superior Hola vídeo</span><span class="sxs-lookup"><span data-stu-id="f59f2-162">Example 1 : Overlay an image on top of hello video</span></span>

### <a name="presentation"></a><span data-ttu-id="f59f2-163">Presentación</span><span class="sxs-lookup"><span data-stu-id="f59f2-163">Presentation</span></span>
<span data-ttu-id="f59f2-164">Tenga en cuenta un ejemplo en el que desea toooverlay una imagen de logotipo en vídeo de entrada de hello mientras Hola vídeo se codifica.</span><span class="sxs-lookup"><span data-stu-id="f59f2-164">Consider an example in which you want toooverlay a logo image on hello input video while hello video is encoded.</span></span> <span data-ttu-id="f59f2-165">En este ejemplo, vídeo de entrada de Hola se denomina "Microsoft_HoloLens_Possibilities_816p24.mp4" y el logotipo de Hola se denomina "logo.png".</span><span class="sxs-lookup"><span data-stu-id="f59f2-165">In this example, hello input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and hello logo is named "logo.png".</span></span> <span data-ttu-id="f59f2-166">Debe realizar pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="f59f2-166">You should perform hello following steps:</span></span>

* <span data-ttu-id="f59f2-167">Crear un recurso de flujo de trabajo con el archivo de flujo de trabajo de hello (vea el siguiente ejemplo de Hola).</span><span class="sxs-lookup"><span data-stu-id="f59f2-167">Create a Workflow Asset with hello workflow file (see hello following example).</span></span>
* <span data-ttu-id="f59f2-168">Crear un recurso multimedia, que contiene dos archivos: MyInputVideo.mp4 como Hola archivo principal y MyLogo.png.</span><span class="sxs-lookup"><span data-stu-id="f59f2-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as hello primary file and MyLogo.png.</span></span>
* <span data-ttu-id="f59f2-169">Enviar un medio de flujo de trabajo de Premium de codificación de medios de tarea toohello activos de procesador con hello anterior de entrada y especifique Hola después de la cadena de configuración.</span><span class="sxs-lookup"><span data-stu-id="f59f2-169">Send a task toohello Media Encoder Premium Workflow media processor with hello above input assets and specify hello following configuration string.</span></span>

<span data-ttu-id="f59f2-170">Configuración:</span><span class="sxs-lookup"><span data-stu-id="f59f2-170">Configuration:</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="f59f2-171">En el ejemplo de Hola anterior, el nombre de Hola Hola del archivo de vídeo se envía toohello propiedad de entrada de archivo multimedia hello y componente primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="f59f2-171">In hello example above, hello name of hello video file is sent toohello Media File Input component and hello primarySourceFile property.</span></span> <span data-ttu-id="f59f2-172">nombre de Hello del archivo de logotipo de Hola se envía tooanother entrada de archivo multimedia que está conectado toohello superposición gráfica componente.</span><span class="sxs-lookup"><span data-stu-id="f59f2-172">hello name of hello logo file is sent tooanother Media File Input that is connected toohello graphic overlay component.</span></span>

> [!NOTE]
> <span data-ttu-id="f59f2-173">nombre de archivo de vídeo de Hola se envía toohello primarySourceFile propiedad.</span><span class="sxs-lookup"><span data-stu-id="f59f2-173">hello video file name is sent toohello primarySourceFile property.</span></span> <span data-ttu-id="f59f2-174">Hola razón para esto es toouse esta propiedad en el flujo de trabajo de Hola para generar un nombre de archivo de salida correcta de hello usando expresiones, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f59f2-174">hello reason for this is toouse this property in hello workflow for building hello correct output file name using Expressions, for example.</span></span>

### <a name="step-by-step-workflow-creation"></a><span data-ttu-id="f59f2-175">Creación paso a paso de un flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="f59f2-175">Step-by-step workflow creation</span></span>
<span data-ttu-id="f59f2-176">Presentamos Hola pasos toocreate un flujo de trabajo que se toma como entrada dos archivos: un vídeo y una imagen.</span><span class="sxs-lookup"><span data-stu-id="f59f2-176">Here are hello steps toocreate a workflow that takes two files as input: a video and an image.</span></span> <span data-ttu-id="f59f2-177">Se superpondrán imagen de hello encima Hola vídeo.</span><span class="sxs-lookup"><span data-stu-id="f59f2-177">It will overlay hello image on top of hello video.</span></span>

<span data-ttu-id="f59f2-178">Abra el **Diseñador de flujo de trabajo** y seleccione **File** > **New Workspace** > **Transcode Blueprint** (Archivo > Nueva área de trabajo > Transcodificar plano).</span><span class="sxs-lookup"><span data-stu-id="f59f2-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span></span>

<span data-ttu-id="f59f2-179">nuevo flujo de trabajo de Hello muestra tres elementos:</span><span class="sxs-lookup"><span data-stu-id="f59f2-179">hello new workflow shows three elements:</span></span>

* <span data-ttu-id="f59f2-180">Primary Source File (Archivo de origen principal)</span><span class="sxs-lookup"><span data-stu-id="f59f2-180">Primary Source File</span></span>
* <span data-ttu-id="f59f2-181">Clip List XML (XML de la lista de clips)</span><span class="sxs-lookup"><span data-stu-id="f59f2-181">Clip List XML</span></span>
* <span data-ttu-id="f59f2-182">Output File/Asset (Recurso/Archivo de salida)</span><span class="sxs-lookup"><span data-stu-id="f59f2-182">Output File/Asset</span></span>  

![Nuevo flujo de trabajo de codificación](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

<span data-ttu-id="f59f2-184">*Nuevo flujo de trabajo de codificación*</span><span class="sxs-lookup"><span data-stu-id="f59f2-184">*New Encoding Workflow*</span></span>

<span data-ttu-id="f59f2-185">En el archivo multimedia de entrada de pedido tooaccept hello, comience por agregar un componente de entrada de archivo de medios.</span><span class="sxs-lookup"><span data-stu-id="f59f2-185">In order tooaccept hello input media file, start with adding a Media File Input component.</span></span> <span data-ttu-id="f59f2-186">tooadd un flujo de trabajo de toohello de componente, busque en el cuadro de búsqueda de repositorio de Hola y arrastre entrada Hola deseado en el panel del diseñador Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-186">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span>

<span data-ttu-id="f59f2-187">A continuación, agregue hello toobe de archivo de vídeo utilizado para diseñar el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f59f2-187">Next, add hello video file toobe used for designing your workflow.</span></span> <span data-ttu-id="f59f2-188">toodo por lo tanto, haga clic en panel de fondo de hello en el Diseñador de flujo de trabajo y busque la propiedad de archivo de origen principal de hello en el panel derecho de propiedad de Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-188">toodo so, click hello background pane in Workflow Designer and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="f59f2-189">Haga clic en el icono de carpeta de Hola y seleccione el archivo de vídeo adecuado Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-189">Click hello folder icon and select hello appropriate video file.</span></span>

![Primary Source File (Archivo de origen principal)](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

<span data-ttu-id="f59f2-191">*Primary Source File (Archivo de origen principal)*</span><span class="sxs-lookup"><span data-stu-id="f59f2-191">*Primary File Source*</span></span>

<span data-ttu-id="f59f2-192">A continuación, especificar archivo de vídeo de hello en el componente de entrada de archivo multimedia de Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-192">Next, specify hello video file in hello Media File Input component.</span></span>   

![Origen de entrada de archivo multimedia](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

<span data-ttu-id="f59f2-194">*Origen de entrada de archivo multimedia*</span><span class="sxs-lookup"><span data-stu-id="f59f2-194">*Media File Input Source*</span></span>

<span data-ttu-id="f59f2-195">En cuanto se haga esto, componente de entrada de archivo multimedia de hello inspeccionar el archivo hello y rellenar el archivo de hello PIN tooreflect de salida se inspecciona.</span><span class="sxs-lookup"><span data-stu-id="f59f2-195">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file that it inspected.</span></span>

<span data-ttu-id="f59f2-196">Hola siguiente paso es tooadd un tooRec.709 de espacio de color de "Actualizador de tipo de datos de vídeo" toospecify Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-196">hello next step is tooadd a "Video Data Type Updater" toospecify hello color space tooRec.709.</span></span> <span data-ttu-id="f59f2-197">Para agregar un "convertidor de formato de vídeo" que se establece el tipo de diseño/diseño tooData = Configurable Planar.</span><span class="sxs-lookup"><span data-stu-id="f59f2-197">Add a "Video Format Converter" that is set tooData Layout/Layout type = Configurable Planar.</span></span> <span data-ttu-id="f59f2-198">Esto convertirá a formato tooa de hello secuencia de vídeo que puede considerarse como un origen de componente de superposición de Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-198">This will convert hello video stream tooa format that can be taken as a source of hello overlay component.</span></span>

![Actualizador de tipo de datos de vídeo y convertidor de formato](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

<span data-ttu-id="f59f2-200">*Actualizador de tipo de datos de vídeo y convertidor de formato*</span><span class="sxs-lookup"><span data-stu-id="f59f2-200">*Video Data Type Updater and Format Converter*</span></span>

![Layout type = Configurable Planar (Tipo de diseño = Planar configurable)](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<span data-ttu-id="f59f2-202">*El valor de Layout type es Configurable Planar (Planar configurable)*</span><span class="sxs-lookup"><span data-stu-id="f59f2-202">*Layout type is Configurable Planar*</span></span>

<span data-ttu-id="f59f2-203">A continuación, agregue un componente de superposición de vídeo y conecte Hola pin de vídeo (sin comprimir) toohello (sin comprimir) vídeo pin de entrada de archivo de medios de Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-203">Next, add a Video Overlay component and connect hello (uncompressed) video pin toohello (uncompressed) video pin of hello media file input.</span></span>

<span data-ttu-id="f59f2-204">Agregar otra entrada de archivo de medios (archivo de logotipo de hello tooload), haga clic en este componente y cámbiele el nombre demasiado "Logotipo de entrada de archivo multimedia" y seleccione una imagen (un archivo .png por ejemplo) en la propiedad de archivo Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-204">Add another Media File Input (tooload hello logo file), click on this component and rename it too"Media File Input Logo", and select an image (a .png file for example) in hello file property.</span></span> <span data-ttu-id="f59f2-205">Conectar pin Hola imagen sin comprimir pin toohello imagen sin comprimir de superposición de Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-205">Connect hello Uncompressed image pin toohello Uncompressed image pin of hello overlay.</span></span>

![Componente de superposición y origen del archivo de imagen](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

<span data-ttu-id="f59f2-207">*Componente de superposición y origen del archivo de imagen*</span><span class="sxs-lookup"><span data-stu-id="f59f2-207">*Overlay component and image file source*</span></span>

<span data-ttu-id="f59f2-208">Si desea que la posición de hello toomodify logotipo de hello en vídeo de hello (por ejemplo, puede querer tooposition en 10 por ciento en la parte superior de hello esquina izquierda del vídeo de hello), desactive casilla de verificación de Hola "Entrada Manual".</span><span class="sxs-lookup"><span data-stu-id="f59f2-208">If you want toomodify hello position of hello logo on hello video (for example, you might want tooposition it at 10 percent off of hello top left corner of hello video), clear hello "Manual Input" check box.</span></span> <span data-ttu-id="f59f2-209">Puede hacerlo porque está usando un componente de superposición del logotipo archivo toohello de entrada de archivo multimedia tooprovide Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-209">You can do this because you are using a Media File Input tooprovide hello logo file toohello overlay component.</span></span>

![Posición de superposición](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

<span data-ttu-id="f59f2-211">*Posición de superposición*</span><span class="sxs-lookup"><span data-stu-id="f59f2-211">*Overlay position*</span></span>

<span data-ttu-id="f59f2-212">tooencode Hola tooH.264 de secuencia de vídeo, agregue hello codificador de vídeo AVC y la superficie del Diseñador de AAC codificador componentes toohello.</span><span class="sxs-lookup"><span data-stu-id="f59f2-212">tooencode hello video stream tooH.264, add hello AVC Video Encoder and AAC encoder components toohello designer surface.</span></span> <span data-ttu-id="f59f2-213">Conectar los PIN de Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-213">Connect hello pins.</span></span>
<span data-ttu-id="f59f2-214">Configurar el codificador AAC hello y seleccione la conversión de formato de Audio/valor preestablecido: 2.0 (L, R).</span><span class="sxs-lookup"><span data-stu-id="f59f2-214">Set up hello AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span></span>

![Codificadores de audio y vídeo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

<span data-ttu-id="f59f2-216">*Codificadores de audio y vídeo*</span><span class="sxs-lookup"><span data-stu-id="f59f2-216">*Audio and Video Encoders*</span></span>

<span data-ttu-id="f59f2-217">Ahora agregue hello **ISO Mpeg-4 multiplexor** y **salida del archivo** componentes y conecte los PIN de hello como se muestra.</span><span class="sxs-lookup"><span data-stu-id="f59f2-217">Now add hello **ISO Mpeg-4 Multiplexer** and **File Output** components and connect hello pins as shown.</span></span>

![Multiplexor MP4 y salida de archivo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

<span data-ttu-id="f59f2-219">*Multiplexor MP4 y salida de archivo*</span><span class="sxs-lookup"><span data-stu-id="f59f2-219">*MP4 multiplexer and file output*</span></span>

<span data-ttu-id="f59f2-220">Necesita tooset Hola nombre de archivo de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="f59f2-220">You need tooset hello name for hello output file.</span></span> <span data-ttu-id="f59f2-221">Haga clic en hello **archivo salida** componente y editar una expresión de hello para el archivo hello:</span><span class="sxs-lookup"><span data-stu-id="f59f2-221">Click hello **File Output** component and edit hello expression for hello file:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Nombre de salida de archivo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

<span data-ttu-id="f59f2-223">*Nombre de salida de archivo*</span><span class="sxs-lookup"><span data-stu-id="f59f2-223">*File output name*</span></span>

<span data-ttu-id="f59f2-224">Puede ejecutar el flujo de trabajo de hello localmente toocheck que se está ejecutando correctamente.</span><span class="sxs-lookup"><span data-stu-id="f59f2-224">You can run hello workflow locally toocheck that it is running correctly.</span></span>

<span data-ttu-id="f59f2-225">Al finalizar, puede ejecutarlo en Servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="f59f2-225">After it finishes, you can run it in Azure Media Services.</span></span>

<span data-ttu-id="f59f2-226">En primer lugar, prepare un activo de servicios multimedia de Azure con dos archivos: archivos de vídeo de Hola y el logotipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-226">First, prepare an asset in Azure Media Services with two files in it: hello video file and hello logo.</span></span> <span data-ttu-id="f59f2-227">Puede hacerlo mediante el uso de .NET de Hola o la API de REST.</span><span class="sxs-lookup"><span data-stu-id="f59f2-227">You can do this by using hello .NET or REST API.</span></span> <span data-ttu-id="f59f2-228">También puede hacerlo mediante el uso de hello portal de Azure o [Explorador de servicios multimedia de Azure](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span><span class="sxs-lookup"><span data-stu-id="f59f2-228">You can also do this by using hello Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span></span>

<span data-ttu-id="f59f2-229">Este tutorial muestra cómo toomanage activos con AMSE.</span><span class="sxs-lookup"><span data-stu-id="f59f2-229">This tutorial shows you how toomanage assets with AMSE.</span></span> <span data-ttu-id="f59f2-230">Hay dos de los activos de tooan maneras tooadd archivos:</span><span class="sxs-lookup"><span data-stu-id="f59f2-230">There are two ways tooadd files tooan asset:</span></span>

* <span data-ttu-id="f59f2-231">Cree una carpeta local, copie los archivos de hello dos en él y arrastre y coloque Hola carpeta toohello **Asset** ficha.</span><span class="sxs-lookup"><span data-stu-id="f59f2-231">Create a local folder, copy hello two files in it, and drag and drop hello folder toohello **Asset** tab.</span></span>
* <span data-ttu-id="f59f2-232">Cargar archivo de vídeo de Hola como un recurso, mostrar información de activos de hello, vaya toohello archivos (ficha) y cargar un archivo adicional (logotipo).</span><span class="sxs-lookup"><span data-stu-id="f59f2-232">Upload hello video file as an asset, display hello asset information, go toohello files tab, and upload an additional file (logo).</span></span>

> [!NOTE]
> <span data-ttu-id="f59f2-233">Asegúrese de tooset seguro de un archivo principal en activos de hello (archivo vídeo principal de hello).</span><span class="sxs-lookup"><span data-stu-id="f59f2-233">Make sure tooset a primary file in hello asset (hello main video file).</span></span>

![Archivos de recursos en AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

<span data-ttu-id="f59f2-235">*Archivos de recursos en AMSE*</span><span class="sxs-lookup"><span data-stu-id="f59f2-235">*Asset files in AMSE*</span></span>

<span data-ttu-id="f59f2-236">Seleccione Hola activo y elija tooencode con codificador Premium.</span><span class="sxs-lookup"><span data-stu-id="f59f2-236">Select hello asset and choose tooencode it with Premium Encoder.</span></span> <span data-ttu-id="f59f2-237">Cargar el flujo de trabajo de Hola y selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="f59f2-237">Upload hello workflow and select it.</span></span>

<span data-ttu-id="f59f2-238">Haga clic en procesador de hello botón toopass datos toohello y agregue Hola XML tooset hello en tiempo de ejecución propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="f59f2-238">Click hello button toopass data toohello processor, and add hello following XML tooset hello runtime properties:</span></span>

![Codificador Premium en AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

<span data-ttu-id="f59f2-240">*Codificador Premium en AMSE*</span><span class="sxs-lookup"><span data-stu-id="f59f2-240">*Premium Encoder in AMSE*</span></span>

<span data-ttu-id="f59f2-241">A continuación, pegue Hola después de los datos XML.</span><span class="sxs-lookup"><span data-stu-id="f59f2-241">Then, paste hello following XML data.</span></span> <span data-ttu-id="f59f2-242">Necesita toospecify Hola nombre de archivo de vídeo de Hola Hola proporcionados por el archivo multimedia y primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="f59f2-242">You need toospecify hello name of hello video file for both hello Media File Input and primarySourceFile.</span></span> <span data-ttu-id="f59f2-243">Especificar nombre de Hola de nombre de archivo de hello para el logotipo de hello demasiado.</span><span class="sxs-lookup"><span data-stu-id="f59f2-243">Specify hello name of hello file name for hello logo too.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

![setRuntimeProperties](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture20_amsexmldata.png)

<span data-ttu-id="f59f2-245">*setRuntimeProperties*</span><span class="sxs-lookup"><span data-stu-id="f59f2-245">*setRuntimeProperties*</span></span>

<span data-ttu-id="f59f2-246">Si usa toocreate del SDK de .NET de Hola y ejecutar la tarea hello, estos datos XML tienen toobe pasa como cadena de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-246">If you use hello .NET SDK toocreate and run hello task, this XML data has toobe passed as hello configuration string.</span></span>

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

<span data-ttu-id="f59f2-247">Una vez completado el trabajo de hello, archivo MP4 Hola Hola salida asset muestra superposición de Hola!</span><span class="sxs-lookup"><span data-stu-id="f59f2-247">After hello job is complete, hello MP4 file in hello output asset displays hello overlay!</span></span>

![Superposición de vídeo Hola](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

<span data-ttu-id="f59f2-249">*Superposición de vídeo Hola*</span><span class="sxs-lookup"><span data-stu-id="f59f2-249">*Overlay on hello video*</span></span>

<span data-ttu-id="f59f2-250">Puede descargar el flujo de trabajo de ejemplo de Hola desde [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span><span class="sxs-lookup"><span data-stu-id="f59f2-250">You can download hello sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span></span>

## <a name="example-2--multiple-audio-language-encoding"></a><span data-ttu-id="f59f2-251">Ejemplo 2: Codificación de varios idiomas de audio</span><span class="sxs-lookup"><span data-stu-id="f59f2-251">Example 2 : Multiple audio language encoding</span></span>

<span data-ttu-id="f59f2-252">En [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding), hay un ejemplo de un flujo de trabajo para la codificación de varios idiomas de audio.</span><span class="sxs-lookup"><span data-stu-id="f59f2-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span></span>

<span data-ttu-id="f59f2-253">Esta carpeta contiene un flujo de trabajo de ejemplo que puede ser tooencode usa un recurso de archivos MXF archivo tooa múltiples MP4 con varias pistas de audio.</span><span class="sxs-lookup"><span data-stu-id="f59f2-253">This folder contains a sample workflow which can be used tooencode a MXF file tooa multi MP4 files asset with multiple audio tracks.</span></span>

<span data-ttu-id="f59f2-254">Este flujo de trabajo, se da por supuesto que MXF Hola el archivo contiene una pista de audio; pistas de audio de Hello adicionales deben pasarse como archivos de audio independientes (WAV o MP4...).</span><span class="sxs-lookup"><span data-stu-id="f59f2-254">This workflow assumes that hello MXF file contains one audio track ; hello additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span></span>

<span data-ttu-id="f59f2-255">tooencode, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f59f2-255">tooencode, please follow these steps:</span></span>

* <span data-ttu-id="f59f2-256">Crear un recurso de servicios multimedia con hello y archivo MXF de hello archivos de Audio (0 too18 archivos de audio).</span><span class="sxs-lookup"><span data-stu-id="f59f2-256">Create a Media Services asset with hello MXF file and hello Audio files (0 too18 audio files).</span></span>
* <span data-ttu-id="f59f2-257">Asegúrese de que ese archivo MXF Hola se establece como un archivo principal.</span><span class="sxs-lookup"><span data-stu-id="f59f2-257">Make sure that hello MXF file is set as a primary file.</span></span>
* <span data-ttu-id="f59f2-258">Crear un trabajo y una tarea que usa el procesador de codificador de flujo de trabajo Premium de Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-258">Create a job and a task using hello Premium Workflow Encoder processor.</span></span> <span data-ttu-id="f59f2-259">Usar el flujo de trabajo de hello proporcionado (MultiMP4 1080p-19audio v1.workflow).</span><span class="sxs-lookup"><span data-stu-id="f59f2-259">Use hello workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span></span>
* <span data-ttu-id="f59f2-260">Pasar la tarea de hello setruntime.xml datos toohello (si se utiliza el Explorador de servicios multimedia de Azure, usar el botón "pasar el flujo de trabajo de xml data toohello" hello).</span><span class="sxs-lookup"><span data-stu-id="f59f2-260">Pass hello setruntime.xml data toohello task (if you use Azure Media Services Explorer, use hello “pass xml data toohello workflow” button).</span></span>
  * <span data-ttu-id="f59f2-261">Actualice Hola datos toospecify Hola archivo correcto idiomas y los nombres de etiquetas XML.</span><span class="sxs-lookup"><span data-stu-id="f59f2-261">Please update hello XML data toospecify hello correct file names and languages tags.</span></span>
  * <span data-ttu-id="f59f2-262">flujo de trabajo de Hello tiene componentes audio denominados 1 Audio tooAudio 18.</span><span class="sxs-lookup"><span data-stu-id="f59f2-262">hello workflow has audio components named Audio 1 tooAudio 18.</span></span>
  * <span data-ttu-id="f59f2-263">RFC5646 es compatible con la etiqueta de idioma de Hola.</span><span class="sxs-lookup"><span data-stu-id="f59f2-263">RFC5646 is supported for hello language tag.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
<transcodeRequest>
  <setRuntimeProperties>
    <property propertyPath="Media File Input Video/filename" value="MainVideo.mxf" />
    <property propertyPath="Language/language_code" value="en" />
    <property propertyPath="/primarySourceFile" value="MainVideo.mxf" />
    <property propertyPath="Audio 1/Media File Input/filename" value="french-audio.wav" />
    <property propertyPath="Audio 1/Language/language_code" value="fr" />
    <property propertyPath="Audio 2/Media File Input/filename" value="german-audio.wav" />
    <property propertyPath="Audio 2/Language/language_code" value="de" />
    <property propertyPath="Audio 3/Media File Input/filename" value="japanese-audio.wav" />
    <property propertyPath="Audio 3/Language/language_code" value="ja" />
  </setRuntimeProperties>
</transcodeRequest>
```

* <span data-ttu-id="f59f2-264">activos de Hello codificado contendrá varias pistas de audio de lenguaje y realiza un seguimiento de estos debe ser seleccionable en el Reproductor de Media de Azure.</span><span class="sxs-lookup"><span data-stu-id="f59f2-264">hello encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span></span>

## <a name="see-also"></a><span data-ttu-id="f59f2-265">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="f59f2-265">See also</span></span>
* [<span data-ttu-id="f59f2-266">Introducción de la codificación Premium en Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="f59f2-266">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="f59f2-267">¿Cómo toouse Premium de codificación en servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="f59f2-267">How toouse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="f59f2-268">Codificación de contenido a petición con Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="f59f2-268">Encoding on-demand content with Azure Media Services</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)
* [<span data-ttu-id="f59f2-269">Códecs y formatos de flujo de trabajo del Codificador multimedia Premium</span><span class="sxs-lookup"><span data-stu-id="f59f2-269">Media Encoder Premium Workflow formats and codecs</span></span>](media-services-premium-workflow-encoder-formats.md)
* [<span data-ttu-id="f59f2-270">Archivos de flujo de trabajo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f59f2-270">Sample workflow files</span></span>](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [<span data-ttu-id="f59f2-271">Explorador de Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="f59f2-271">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="f59f2-272">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="f59f2-272">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f59f2-273">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="f59f2-273">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
