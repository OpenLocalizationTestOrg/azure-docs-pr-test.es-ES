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
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a>Uso del codificador Premium con varios archivos de entrada y propiedades de los componentes
## <a name="overview"></a>Información general
Hay escenarios en los que puede que tenga propiedades de componente de toocustomize, especifique el contenido del XML de la lista de Clip, o enviar varios archivos de entrada cuando se envía una tarea con hello **flujo de trabajo de Premium de codificación de medios** procesador multimedia. A continuación, se indican algunos ejemplos:

* Texto superpuesto en vídeo y establecer el valor de texto hello (por ejemplo, Hola fecha actual) en tiempo de ejecución para cada vídeo de entrada.
* Se puede personalizar Hola Clip lista XML (toospecify uno o varios archivos, con o sin recortar, etcetera de origen.).
* Superponer una imagen de logotipo en vídeo de entrada de hello mientras Hola vídeo se codifica.
* Codificación de varios idiomas de audio.

Hola toolet **flujo de trabajo de Premium de codificación de medios** sabe que va a cambiar algunas propiedades en el flujo de trabajo de hello al crear la tarea hello o enviar varios archivos de entrada, que tiene una cadena de configuración que contiene toouse  **setRuntimeProperties** o **transcodeSource**. Este tema se explica cómo toouse ellos.

## <a name="configuration-string-syntax"></a>Sintaxis de la cadena de configuración
tooset de cadena de configuración de Hola Hola codificación tarea usa un documento XML que el siguiente aspecto:

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

Hola siguiente es código de hello C# que lee la configuración de XML de Hola desde un archivo, actualícelo con Hola filename vídeo adecuada y la pasa toohello tarea en un trabajo:

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

## <a name="customizing-component-properties"></a>Personalización de las propiedades de los componentes
### <a name="property-with-a-simple-value"></a>Propiedad con un valor simple
En algunos casos, resulta útil toocustomize una propiedad del componente junto con el archivo de flujo de trabajo de Hola que se va toobe ejecutado por el flujo de trabajo de Premium de codificación de medios.

Supongamos que ha diseñado un flujo de trabajo que el texto se superpone en los vídeos y texto hello (por ejemplo, Hola fecha actual) se supone que el conjunto de toobe en tiempo de ejecución. Puede hacerlo mediante el envío de hello texto toobe establecer como nuevo valor para la propiedad de texto hello del componente de superposición de Hola de Hola de hello tarea de codificación. Puede utilizar este mecanismo toochange otras propiedades de un componente de flujo de trabajo de hello (por ejemplo, la posición de Hola o color de superposición de hello, velocidad de bits de Hola de codificador de hello AVC, etcetera.).

**setRuntimeProperties** es toooverride usa una propiedad en componentes de Hola de flujo de trabajo de Hola.

Ejemplo:

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

### <a name="property-with-an-xml-value"></a>Propiedad con un valor XML
encapsular tooset una propiedad que espera un valor XML, mediante el uso de `<![CDATA[ and ]]>`.

Ejemplo:

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
> Asegúrese de que no tooput un carro devolver justo después `<![CDATA[`.

### <a name="propertypath-value"></a>Valor de propertyPath
En los ejemplos anteriores de hello, era Hola propertyPath "archivos de medios / / nombre de archivo de entrada" o "/ inactiveTimeout" o "clipListXml".
Esto es, por lo general, nombre hello del componente de hello y, a continuación, nombre de Hola de propiedad de Hola. Hello ruta de acceso puede tener más o menos niveles, al igual que "/ primarySourceFile" (porque es propiedad hello en raíz de Hola de flujo de trabajo de hello) o "/ vídeo procesamiento/gráfico superposición/opacidad" (porque Hola superposición está en un grupo).    

toocheck Hola ruta de acceso y nombre de propiedad, botón de acción de Hola de uso que se encuentre inmediatamente al lado de cada propiedad. Puede hacer clic en este botón de acción y seleccione **Editar**. Esto mostrará que Hola real el nombre de propiedad de Hola e inmediatamente por encima de él, Hola espacio de nombres.

![Acción o edición](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Propiedad](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a>Varios archivos de entrada
Cada tarea que se envía toohello **flujo de trabajo de Premium de codificación de medios** requiere dos recursos:

* Hello primero uno es un *activos de flujo de trabajo* que contiene un archivo de flujo de trabajo. Puede diseñar archivos de flujo de trabajo mediante el uso de hello [Workflow Designer](media-services-workflow-designer.md).
* Hello segunda es un *activo multimedia* que contiene los archivos de medios de Hola que desea tooencode.

Si va a enviar varios medios archivos toohello **flujo de trabajo de Premium de codificación de medios** codificador, Hola siguiendo las restricciones se aplica:

* Hola a todos los medios de hello archivos deben estar en mismo *activo multimedia*. No se admite el uso de varios recursos multimedia.
* Debe establecer el archivo principal de hello en este recurso multimedia (idealmente, se trata de hello principal archivo de vídeo que Hola codificador se pregunta a tooprocess).
* Se trata de datos de configuración toopass es necesario que incluya hello **setRuntimeProperties** o **transcodeSource** procesador toohello de elemento.
  * **setRuntimeProperties** es propiedad de nombre de archivo usado toooverride Hola u otra propiedad en componentes de Hola de flujo de trabajo de Hola.
  * **transcodeSource** es toospecify usado hello contenido XML de la lista de imágenes.

Conexiones en el flujo de trabajo de hello:

* Si utiliza uno o varios componentes de entrada de archivo multimedia y planear toouse **setRuntimeProperties** toospecify Hola nombre de archivo, a continuación, no se conectan Hola archivo principal componente pin toothem. Asegúrese de que no hay ninguna conexión entre el objeto de archivo principal de Hola y Hola las entradas del archivo de medios.
* Si prefiere toouse Clip lista XML y un componente de origen de los medios, a continuación, puede conectar ambos juntos.

![Ninguna conexión desde el archivo de código fuente principal tooMedia proporcionados por el archivo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

*No hay ninguna conexión desde el archivo principal de hello tooMedia componentes proporcionados por el archivo si utiliza la propiedad de nombre de archivo de setRuntimeProperties tooset Hola.*

![Conexión de XML de la lista de Clip tooClip origen de la lista](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

*Puede conectarse tooMedia origen de XML de la lista de imágenes y usar transcodeSource.*

### <a name="clip-list-xml-customization"></a>Personalización del XML de lista de clips
Puede especificar Hola Clip lista XML en el flujo de trabajo de hello en tiempo de ejecución mediante **transcodeSource** en la configuración de Hola de cadena XML. Esto requiere Hola Clip lista XML pin toobe conectado toohello origen multimedia componente de flujo de trabajo de Hola.

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

Si desea toospecify /primarySourceFile toouse esta salida de hello de propiedad tooname archivos mediante 'Expresiones', se recomienda pasar Hola Clip lista XML como una propiedad *después* propiedad /primarySourceFile de hello, tooavoid tener Hola Clip lista reemplazarse por valor de /primarySourceFile Hola.

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

Con un recorte preciso de marco adicional:

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

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a>Ejemplo 1: Superposición de una imagen en la parte superior Hola vídeo

### <a name="presentation"></a>Presentación
Tenga en cuenta un ejemplo en el que desea toooverlay una imagen de logotipo en vídeo de entrada de hello mientras Hola vídeo se codifica. En este ejemplo, vídeo de entrada de Hola se denomina "Microsoft_HoloLens_Possibilities_816p24.mp4" y el logotipo de Hola se denomina "logo.png". Debe realizar pasos de hello:

* Crear un recurso de flujo de trabajo con el archivo de flujo de trabajo de hello (vea el siguiente ejemplo de Hola).
* Crear un recurso multimedia, que contiene dos archivos: MyInputVideo.mp4 como Hola archivo principal y MyLogo.png.
* Enviar un medio de flujo de trabajo de Premium de codificación de medios de tarea toohello activos de procesador con hello anterior de entrada y especifique Hola después de la cadena de configuración.

Configuración:

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

En el ejemplo de Hola anterior, el nombre de Hola Hola del archivo de vídeo se envía toohello propiedad de entrada de archivo multimedia hello y componente primarySourceFile. nombre de Hello del archivo de logotipo de Hola se envía tooanother entrada de archivo multimedia que está conectado toohello superposición gráfica componente.

> [!NOTE]
> nombre de archivo de vídeo de Hola se envía toohello primarySourceFile propiedad. Hola razón para esto es toouse esta propiedad en el flujo de trabajo de Hola para generar un nombre de archivo de salida correcta de hello usando expresiones, por ejemplo.

### <a name="step-by-step-workflow-creation"></a>Creación paso a paso de un flujo de trabajo
Presentamos Hola pasos toocreate un flujo de trabajo que se toma como entrada dos archivos: un vídeo y una imagen. Se superpondrán imagen de hello encima Hola vídeo.

Abra el **Diseñador de flujo de trabajo** y seleccione **File** > **New Workspace** > **Transcode Blueprint** (Archivo > Nueva área de trabajo > Transcodificar plano).

nuevo flujo de trabajo de Hello muestra tres elementos:

* Primary Source File (Archivo de origen principal)
* Clip List XML (XML de la lista de clips)
* Output File/Asset (Recurso/Archivo de salida)  

![Nuevo flujo de trabajo de codificación](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

*Nuevo flujo de trabajo de codificación*

En el archivo multimedia de entrada de pedido tooaccept hello, comience por agregar un componente de entrada de archivo de medios. tooadd un flujo de trabajo de toohello de componente, busque en el cuadro de búsqueda de repositorio de Hola y arrastre entrada Hola deseado en el panel del diseñador Hola.

A continuación, agregue hello toobe de archivo de vídeo utilizado para diseñar el flujo de trabajo. toodo por lo tanto, haga clic en panel de fondo de hello en el Diseñador de flujo de trabajo y busque la propiedad de archivo de origen principal de hello en el panel derecho de propiedad de Hola. Haga clic en el icono de carpeta de Hola y seleccione el archivo de vídeo adecuado Hola.

![Primary Source File (Archivo de origen principal)](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

*Primary Source File (Archivo de origen principal)*

A continuación, especificar archivo de vídeo de hello en el componente de entrada de archivo multimedia de Hola.   

![Origen de entrada de archivo multimedia](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

*Origen de entrada de archivo multimedia*

En cuanto se haga esto, componente de entrada de archivo multimedia de hello inspeccionar el archivo hello y rellenar el archivo de hello PIN tooreflect de salida se inspecciona.

Hola siguiente paso es tooadd un tooRec.709 de espacio de color de "Actualizador de tipo de datos de vídeo" toospecify Hola. Para agregar un "convertidor de formato de vídeo" que se establece el tipo de diseño/diseño tooData = Configurable Planar. Esto convertirá a formato tooa de hello secuencia de vídeo que puede considerarse como un origen de componente de superposición de Hola.

![Actualizador de tipo de datos de vídeo y convertidor de formato](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

*Actualizador de tipo de datos de vídeo y convertidor de formato*

![Layout type = Configurable Planar (Tipo de diseño = Planar configurable)](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

*El valor de Layout type es Configurable Planar (Planar configurable)*

A continuación, agregue un componente de superposición de vídeo y conecte Hola pin de vídeo (sin comprimir) toohello (sin comprimir) vídeo pin de entrada de archivo de medios de Hola.

Agregar otra entrada de archivo de medios (archivo de logotipo de hello tooload), haga clic en este componente y cámbiele el nombre demasiado "Logotipo de entrada de archivo multimedia" y seleccione una imagen (un archivo .png por ejemplo) en la propiedad de archivo Hola. Conectar pin Hola imagen sin comprimir pin toohello imagen sin comprimir de superposición de Hola.

![Componente de superposición y origen del archivo de imagen](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

*Componente de superposición y origen del archivo de imagen*

Si desea que la posición de hello toomodify logotipo de hello en vídeo de hello (por ejemplo, puede querer tooposition en 10 por ciento en la parte superior de hello esquina izquierda del vídeo de hello), desactive casilla de verificación de Hola "Entrada Manual". Puede hacerlo porque está usando un componente de superposición del logotipo archivo toohello de entrada de archivo multimedia tooprovide Hola.

![Posición de superposición](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

*Posición de superposición*

tooencode Hola tooH.264 de secuencia de vídeo, agregue hello codificador de vídeo AVC y la superficie del Diseñador de AAC codificador componentes toohello. Conectar los PIN de Hola.
Configurar el codificador AAC hello y seleccione la conversión de formato de Audio/valor preestablecido: 2.0 (L, R).

![Codificadores de audio y vídeo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

*Codificadores de audio y vídeo*

Ahora agregue hello **ISO Mpeg-4 multiplexor** y **salida del archivo** componentes y conecte los PIN de hello como se muestra.

![Multiplexor MP4 y salida de archivo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

*Multiplexor MP4 y salida de archivo*

Necesita tooset Hola nombre de archivo de salida de hello. Haga clic en hello **archivo salida** componente y editar una expresión de hello para el archivo hello:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Nombre de salida de archivo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

*Nombre de salida de archivo*

Puede ejecutar el flujo de trabajo de hello localmente toocheck que se está ejecutando correctamente.

Al finalizar, puede ejecutarlo en Servicios multimedia de Azure.

En primer lugar, prepare un activo de servicios multimedia de Azure con dos archivos: archivos de vídeo de Hola y el logotipo de Hola. Puede hacerlo mediante el uso de .NET de Hola o la API de REST. También puede hacerlo mediante el uso de hello portal de Azure o [Explorador de servicios multimedia de Azure](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).

Este tutorial muestra cómo toomanage activos con AMSE. Hay dos de los activos de tooan maneras tooadd archivos:

* Cree una carpeta local, copie los archivos de hello dos en él y arrastre y coloque Hola carpeta toohello **Asset** ficha.
* Cargar archivo de vídeo de Hola como un recurso, mostrar información de activos de hello, vaya toohello archivos (ficha) y cargar un archivo adicional (logotipo).

> [!NOTE]
> Asegúrese de tooset seguro de un archivo principal en activos de hello (archivo vídeo principal de hello).

![Archivos de recursos en AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

*Archivos de recursos en AMSE*

Seleccione Hola activo y elija tooencode con codificador Premium. Cargar el flujo de trabajo de Hola y selecciónelo.

Haga clic en procesador de hello botón toopass datos toohello y agregue Hola XML tooset hello en tiempo de ejecución propiedades siguientes:

![Codificador Premium en AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

*Codificador Premium en AMSE*

A continuación, pegue Hola después de los datos XML. Necesita toospecify Hola nombre de archivo de vídeo de Hola Hola proporcionados por el archivo multimedia y primarySourceFile. Especificar nombre de Hola de nombre de archivo de hello para el logotipo de hello demasiado.

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

*setRuntimeProperties*

Si usa toocreate del SDK de .NET de Hola y ejecutar la tarea hello, estos datos XML tienen toobe pasa como cadena de configuración de Hola.

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

Una vez completado el trabajo de hello, archivo MP4 Hola Hola salida asset muestra superposición de Hola!

![Superposición de vídeo Hola](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

*Superposición de vídeo Hola*

Puede descargar el flujo de trabajo de ejemplo de Hola desde [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).

## <a name="example-2--multiple-audio-language-encoding"></a>Ejemplo 2: Codificación de varios idiomas de audio

En [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding), hay un ejemplo de un flujo de trabajo para la codificación de varios idiomas de audio.

Esta carpeta contiene un flujo de trabajo de ejemplo que puede ser tooencode usa un recurso de archivos MXF archivo tooa múltiples MP4 con varias pistas de audio.

Este flujo de trabajo, se da por supuesto que MXF Hola el archivo contiene una pista de audio; pistas de audio de Hello adicionales deben pasarse como archivos de audio independientes (WAV o MP4...).

tooencode, siga estos pasos:

* Crear un recurso de servicios multimedia con hello y archivo MXF de hello archivos de Audio (0 too18 archivos de audio).
* Asegúrese de que ese archivo MXF Hola se establece como un archivo principal.
* Crear un trabajo y una tarea que usa el procesador de codificador de flujo de trabajo Premium de Hola. Usar el flujo de trabajo de hello proporcionado (MultiMP4 1080p-19audio v1.workflow).
* Pasar la tarea de hello setruntime.xml datos toohello (si se utiliza el Explorador de servicios multimedia de Azure, usar el botón "pasar el flujo de trabajo de xml data toohello" hello).
  * Actualice Hola datos toospecify Hola archivo correcto idiomas y los nombres de etiquetas XML.
  * flujo de trabajo de Hello tiene componentes audio denominados 1 Audio tooAudio 18.
  * RFC5646 es compatible con la etiqueta de idioma de Hola.

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

* activos de Hello codificado contendrá varias pistas de audio de lenguaje y realiza un seguimiento de estos debe ser seleccionable en el Reproductor de Media de Azure.

## <a name="see-also"></a>Otras referencias
* [Introducción de la codificación Premium en Servicios multimedia de Azure](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [¿Cómo toouse Premium de codificación en servicios multimedia de Azure](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [Codificación de contenido a petición con Servicios multimedia de Azure](media-services-encode-asset.md#media-encoder-premium-workflow)
* [Códecs y formatos de flujo de trabajo del Codificador multimedia Premium](media-services-premium-workflow-encoder-formats.md)
* [Archivos de flujo de trabajo de ejemplo](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [Explorador de Servicios multimedia de Azure](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
