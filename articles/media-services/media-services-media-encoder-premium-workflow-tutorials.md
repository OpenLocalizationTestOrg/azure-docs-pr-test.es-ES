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
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a>Tutoriales avanzados sobre el flujo de trabajo premium del codificador multimedia
## <a name="overview"></a>Información general
Este documento contiene tutoriales que muestran cómo los flujos de trabajo de toocustomize con **Workflow Designer**. Puede encontrar archivos de flujo de trabajo real hello [aquí](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).  

## <a name="toc"></a>TABLA DE CONTENIDO
se trata Hola temas siguientes:

* [Codificación de MXF en un MP4 de velocidad de bits única](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [Inicio de un nuevo flujo de trabajo](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [Uso de hello entrada de archivo de medios](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [Inspección de transmisiones multimedia](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [Incorporación de un codificador de vídeo para la generación de archivos .MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [Secuencia de audio de codificación Hola](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [Multiplexación de secuencias de audio y vídeo en un contenedor MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [Escribir el archivo MP4 de Hola](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [Crear un recurso de servicios multimedia de archivo de salida de hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [Hola de prueba terminado localmente el flujo de trabajo](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [Codificación de MXF en archivos MP4 de varias velocidades de bits: empaquetado dinámico habilitado](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [Incorporación de una o más salidas MP4 adicionales](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [Nombres de salida de archivo de configuración Hola](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [Incorporación de una pista de audio independiente](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [Agregar Hola. Archivo SMIL ISM](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [Codificación de MXF en archivos MP4 de varias velocidades de bits: plano mejorado](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [Flujo de trabajo información general sobre tooenhance](#workflow-overview-to-enhance)
  * [Convenciones de nomenclatura de los archivos](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [Propiedades de componente en la raíz del flujo de trabajo de Hola de publicación](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [Se han generado nombres de archivo de salida que se basan en los valores de propiedad publicados](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [Agregar la salida de las miniaturas toomultibitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [Vistas en miniatura de flujo de trabajo información general sobre tooadd a](#workflow-overview-to-add-thumbnails-to)
  * [Incorporación de codificación JPG](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [Relación con la conversión de espacio de colores](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [Miniaturas de Hola de escritura](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [Detección de errores en un flujo de trabajo](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [Flujo de trabajo finalizado](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [Recorte basado en tiempo de salida MP4 de varias velocidades de bits](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [Flujo de trabajo información general sobre toostart Agregar recorte](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [Uso de hello secuencia recortador](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [Flujo de trabajo finalizado](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [Introducción a Hola componente de la secuencia de comandos](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [Scripting en un flujo de trabajo: hola a todos](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [Recorte basado en fotogramas de salida MP4 de varias velocidades de bits](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [Plano técnico toostart de información general sobre la adición de recorte para](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [Uso de hello XML de la lista de imágenes](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [Modificar lista de clip Hola desde un componente de la secuencia de comandos](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [Incorporación de una propiedad de conveniencia ClippingEnabled](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <a id="MXF_to_MP4"></a>Codificación de MXF en un MP4 de velocidad de bits única
En este tutorial crearemos un archivo .MP4 de velocidad de bits única con audio codificado AAC-HE a partir de un archivo de entrada .MXF.

### <a id="MXF_to_MP4_start_new"></a>Inicio de un nuevo flujo de trabajo
Abra el Diseñador de flujo de trabajo y seleccione "File" (Archivo), "New Workspace" (Nueva área de trabajo), "Transcode Blueprint" (Transcodificar plano)

nuevo flujo de trabajo Hola mostrará 3 elementos:

* Primary Source File (Archivo de origen principal)
* Clip List XML (XML de la lista de clips)
* Output File/Asset (Recurso/Archivo de salida)  

![Nuevo flujo de trabajo de codificación](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

*Nuevo flujo de trabajo de codificación*

### <a id="MXF_to_MP4_with_file_input"></a>Uso de hello entrada de archivo de medios
En orden tooaccept nuestro archivo multimedia de entrada, uno se inicia con la adición de un componente de entrada de archivo de medios. tooadd un flujo de trabajo de toohello de componente, busque en el cuadro de búsqueda de repositorio de Hola y arrastre entrada Hola deseado en el panel del diseñador Hola. Hacer esto para entrada de archivo de medios hello y conéctese pin de la entrada de nombre de archivo archivo de código fuente principal componente toohello de Hola desde Hola entrada de archivo de medios.

![Entrada de archivo multimedia conectada](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

*Entrada de archivo multimedia conectada*

Antes de que podemos hacer mucho más, en primer lugar necesitaremos el Diseñador de flujo de trabajo de tooindicate toohello qué archivo de ejemplo nos gustaría toouse toodesign con nuestro flujo de trabajo. toodo por lo tanto, haga clic en fondo del panel del Diseñador de Hola y busque la propiedad de archivo de origen principal de hello en el panel derecho de propiedad de Hola. Haga clic en el icono de carpeta de Hola y Hola seleccione deseado de flujo de trabajo de Hola de tootest archivo con. En cuanto se haga esto, componente de entrada de archivo multimedia de hello inspeccionar el archivo hello y rellenar el archivo de hello tooreflect de PIN de salida que se inspeccionar.

![Entrada de archivo multimedia rellena](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

*Entrada de archivo multimedia rellena*

Mientras que esto se especifica con lo que nos gustaría toowork con de entrada, no indica aún donde debe hacia la salida de hello codificado. Similar hello toohow se ha configurado el archivo de origen principal, ahora configurar Hola propiedad variables de carpeta de salida, justo debajo de él.

![Propiedades de entrada y salida configuradas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

*Propiedades de entrada y salida configuradas*

### <a id="MXF_to_MP4_streams"></a>Inspección de transmisiones multimedia
A menudo se desea tooknow cómo flujo Hola parece probable que fluye a través de flujo de trabajo de Hola. tooinspect una secuencia en cualquier punto en el flujo de trabajo de hello, simplemente haga clic en una salida o entrada pin en cualquiera de los componentes de Hola. En este caso, intente hacer clic en el pin de salida de vídeo sin comprimir Hola a partir de nuestros datos de archivo multimedia. Se abrirá un cuadro de diálogo que permite el vídeo de salida de hello tooinspect.

![Inspeccionar Hola pin de salida de vídeo sin comprimir](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

*Inspeccionar Hola pin de salida de vídeo sin comprimir*

En nuestro caso, nos dice por ejemplo que estamos trabajando con una entrada de 1920 x 1080 a 24 fotogramas por segundo en un muestreo 4:2:2 para ver un vídeo de casi 2 minutos.

### <a id="MXF_to_MP4_file_generation"></a>Incorporación de un codificador de vídeo para la generación de archivos .MP4
Tenga en cuenta que ahora, una clavija de salida de vídeo sin comprimir y varias de audio sin comprimir están disponibles para su utilización en la entrada de archivo multimedia. En orden tooencode Hola vídeo entrante, necesitamos un componente de codificación - en este caso para la generación. Archivos MP4.

tooencode Hola tooH.264 de secuencia de vídeo, agregue la superficie del Diseñador de hello codificador de vídeo AVC componente toohello. Este componente toma una secuencia de vídeo sin comprimir como entrada y entrega una secuencia de vídeo comprimida AVC en su clavija de salida.

![Codificador de AVC no conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

*Codificador de AVC no conectado*

Sus propiedades determinan cómo exactamente Hola codificación ocurre. Echemos un vistazo a algunas de hello configuraciones más importantes:

* Ancho de salida y el alto de salida: estos determinan la resolución de Hola de vídeo de hello codificado. En nuestro caso seleccionaremos 640 x 360
* Velocidad de fotogramas: cuando toopassthrough conjunto será simplemente adopten la velocidad de fotogramas de origen de hello, es posible toooverride aunque este. Tenga en cuenta que esa conversión de velocidad de fotogramas no está compensada por el movimiento.
* Perfil y nivel: determinan perfil Hola AVC y nivel. tooconveniently obtener más información acerca de diferentes niveles de Hola y perfiles, haga clic en el icono de signo de interrogación de hello en el componente de codificador de vídeo AVC hello y página de Ayuda de hello mostrará información más detallada sobre cada uno de los niveles de Hola. Para nuestro ejemplo, vamos a Main Profile en nivel 3.2 (valor predeterminado de hello).
* Velocidad de bits (kbps) y modo de control de velocidad: en nuestro escenario optamos por una salida de velocidad de bits constante (CBR) a 1200 kbps
* Formato de vídeo: este tema trata sobre Hola VUI (información de facilidad de uso de vídeo) que se escriba en la secuencia de hello H.264 (información del lado del que puede ser utilizada por un descodificador tooenhance Hola la visualización pero no es esencial toocorrectly descodificar):
* NTSC (habitual en Estados Unidos o Japón, utiliza 30 fps)
* PAL (típica en Europa, utiliza 25 fps)
* Modo de cambiar el tamaño de GOP: vamos a configurar un tamaño fijo de GOP para nuestros fines con un intervalo de clave de 2 segundos con GOP cerrados. Esto asegura la compatibilidad con hello que proporciona servicios de multimedia de Azure de empaquetado dinámico.

toofeed nuestro codificador AVC, conectarse pin de salida de vídeo sin comprimir de Hola desde Hola medios archivo componente toohello vídeo sin comprimir entrada pin de entrada de codificador de hello AVC.

![Codificador AVC conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

*Codificador principal AVC conectado*

### <a id="MXF_to_MP4_audio"></a>Secuencia de audio de codificación Hola
En este punto, nos hemos codificado vídeo pero secuencia de audio sin comprimir original Hola aún debe toobe comprimido. Para esto decidimos con AAC codificación por hello componente de codificador AAC (Dolby). Agregar flujo de trabajo de toohello.

![Codificador de AVC no conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

*Codificador de AAC no conectado*

Ahora hay una incompatibilidad: hay solo un único sin comprimir audio entrado pin de hello AAC codificador mientras más probable Hola de entrada de archivo de medios tendrán diferentes no lo está disponible de la secuencia de audio: uno para hello dejado canales de audio y otra para Hola Correcto. (Si está trabajando con sonido envolvente, eso suma 6 canales). Por lo que no es posible toodirectly conéctelos audio Hola de origen de datos proporcionados por el archivo multimedia de hello codificador de audio AAC Hola. componente AAC Hello espera una secuencia de audio como los denominados "intercalada": un solo flujo que presente ambos Hola hello e izquierda canales correctos intercalados entre sí. Una vez que sepamos de nuestro archivo de medios de origen las pistas de audio en la posición en el origen de hello, podemos generar esa secuencia de audio intercalada con hello correctamente tienen posiciones de los altavoces para izquierda y derecha.

En primer lugar una desearán toogenerated una secuencia intercalada de canales de audio de origen de hello necesario. componente de Hello Interleaver de secuencia de Audio controlará esto para que podamos. Agregar flujo de trabajo toohello y conéctese salidas de audio de Hola de hello proporcionados por el archivo multimedia en él.

![Entrelazador de secuencias de audio conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

*Entrelazador de secuencias de audio conectado*

Ahora que tenemos una secuencia de audio intercalada, todavía no especificamos donde coloca los altavoces de izquierdo o derecho de hello tooassign a. En orden toospecify esto, podemos aprovechar Hola asignador de posición de altavoces.

![Incorporación de un asignador de posiciones de altavoz](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

*Incorporación de un asignador de posiciones de altavoz*

Configurar Hola asignador de posición de altavoces para su uso con un flujo de entrada estéreo a través de un filtro de valor preestablecido de codificador de "Custom" y Hola canal preestablecido denominado "2.0 (L, R)". (Esto asignará Hola altavoz izquierdo posición toochannel 1 y Hola altavoz derecho posición toochannel 2.)

Conecte la salida de hello de entrada de toohello Hola altavoz posición asignador de hello AAC codificador. A continuación, indicar Hola AAC codificador toowork con un "2.0 (L, R)" predefinidos de canal, para que sepa toodeal con audio estéreo como entrada.

### <a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexación de secuencias de audio y vídeo en un contenedor MP4
Una vez que tenemos nuestra secuencia de vídeo codificado AVC y nuestra secuencia de audio codificada AAC, podemos capturar ambas en un contenedor .MP4. proceso de Hola de mezclar secuencias diferentes en una sola instrucción se denomina "multiplexación" (o "muxing"). En este caso se estamos intercalación audio hello y secuencias de vídeo de hello en una sola coherente. Paquete de MP4. componente de Hola que coordina esto por una. Contenedor de MP4 se denomina hello multiplexor de ISO MPEG-4. Agregue una superficie del diseñador toohello y conecte Hola codificador de vídeo AVC y entradas de hello AAC codificador tooits.

![Multiplexor MPEG4 conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

*Multiplexor MPEG4 conectado*

### <a id="MXF_to_MP4_writing_mp4"></a>Escribir el archivo MP4 de Hola
Al escribir un archivo de salida, se utiliza el componente de archivo de salida de hello. Para que la salida se escriba toodisk se podemos conectar este resultado toohello de hello multiplexor de ISO MPEG-4. toodo, conectar Hola contenedor (MPEG-4) pin toohello escritura entrada conexión de salida del programa Hola a archivo de salida.

![Salida de archivo conectada](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

*Salida de archivo conectada*

Hola filename que se usará viene determinado por hello propiedad de archivo. Mientras que esa propiedad puede ser tooa codificado valor, más probablemente una desearán tooset a través de una expresión en su lugar.

flujo de trabajo de hello toohave determinar automáticamente la salida de hello propiedad de nombre de una expresión de archivo, haga clic en hello botón siguiente toohello nombre de archivo (icono de carpeta de toohello siguiente). De hello menú desplegable, haga clic en "Expression". Se abrirá el editor de expresiones Hola. Borrar contenido de hello del editor de hello en primer lugar.

![Editor de expresiones vacío](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

*Editor de expresiones vacío*

editor de expresiones de Hello permite tooenter cualquier valor literal, combinado con una o más variables. Las variables comienzan con un signo de dólar. Tal y como se presionar la tecla de $ de hello, editor de hello mostrará un cuadro de lista desplegable con una variedad de las variables disponibles. En nuestro caso, vamos a usar una combinación de variables de directorio de salida de hello y variable de nombre de archivo de entrada de base de hello:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Editor de expresiones relleno](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

*Editor de expresiones relleno*

> [!NOTE]
> En orden toosee ver un archivo de salida de su trabajo de codificación en Azure, debe proporcionar un valor en el editor de expresiones Hola.
>
>

Cuando se confirma la expresión de hello presionando Aceptar, ventana de propiedades de hello obtendrá una vista previa toowhat valor Hola archivo propiedad resuelve en este momento.

![La expresión de archivo resuelve el directorio de salida](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

*La expresión de archivo resuelve el directorio de salida*

### <a id="MXF_to_MP4_asset_from_output"></a>Crear un recurso de servicios multimedia de archivo de salida de hello
Mientras lo hemos incluido un archivo de salida MP4, todavía necesitamos tooindicate que pertenece este archivo toohello asset qué servicios de multimedia se generarán como resultado de ejecutar este flujo de trabajo de salida. se utiliza toothis final, nodo de recurso de archivo de salida de hello en el lienzo de flujo de trabajo de Hola. Todos los archivos entrantes en este nodo, formará parte del activo de servicios multimedia de Azure de hello resultante.

Conectar Hola salida del archivo componente toohello recurso de archivo de salida componente toofinish Hola flujo de trabajo.

![Flujo de trabajo finalizado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

*Flujo de trabajo finalizado*

### <a id="MXF_to_MP4_test"></a>Hola de prueba terminado localmente el flujo de trabajo
tootest Hola flujo de trabajo localmente, pulse el botón de reproducción de hello en barra de herramientas de hello en la parte superior de Hola. Cuando finalice la ejecución del flujo de trabajo de hello, inspeccionar el resultado de hello generado en la carpeta de salida de hello configurado. Podrá ver Hola terminado de archivo de salida de MP4 que se codificó de archivo de origen de entrada de hello MXF.

## <a id="MXF_to_MP4_with_dyn_packaging"></a>Codificación de MXF en archivos MP4: empaquetado dinámico de varias velocidades de bits habilitado
En este tutorial crearemos un conjunto de archivos .MP4 de varias velocidades de bits con audio codificado AAC a partir de un archivo de entrada .MXF.

Cuando se desea una salida de activos de velocidades de bits para su uso en combinación con las características de empaquetado dinámico de Hola que ofrece servicios de multimedia de Azure, varios archivos MP4 alineados con GOP de cada una velocidad de bits diferente y resolución deberán toobe generado. por lo tanto, Hola toodo [codificación MXF en una velocidad de bits única MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) tutorial proporciona un buen punto de partida.

![Inicio del flujo de trabajo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

*Inicio del flujo de trabajo*

### <a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Incorporación de una o más salidas MP4 adicionales
Cada archivo MP4 en el recurso resultante de Servicios multimedia de Azure será compatible con una velocidad de bits y resolución diferentes. Vamos a agregar uno o varios MP4 salida archivos toohello flujo de trabajo.

toomake seguro tenemos todos nuestros codificadores de vídeo creados con Hola misma configuración, es más conveniente tooduplicate Hola codificador de vídeo AVC ya existente y configurar otra combinación de resolución y velocidad de bits (vamos a agregar uno de 960 x 540 en 25 fotogramas por segundo en 2,5 Mbps). tooduplicate del codificador existentes hello, copia pegarla en la superficie del Diseñador de Hola.

Conectar la conexión de salida de vídeo sin comprimir de Hola de hello entrada de archivo de medios en nuestro nuevo componente AVC.

![Segundo codificador AVC conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

*Segundo codificador AVC conectado*

Ahora se adaptan configuración Hola para nuestro nuevo toooutput de codificador AVC 960 x 540 a 2,5 Mbps. (Utilice sus propiedades "Output width" (ancho de salida), "Output height" (Altura de salida) y "Bitrate (kbps)" (Velocidad de bits (kbps) para esto).

Dado que deseamos asset resultante de hello toouse junto con el empaquetado dinámico de servicios multimedia de Azure, Hola extremo de streaming debe toobe capaz de generar a partir de estos archivos MP4 de fragmentos de MP4 HLS/fragmentado/DASH que son exactamente alineado tooeach otro de forma que los clientes que al cambian entre distintas velocidades de bits obtienen una sola experiencia sin problemas continua audio y vídeo. toomake que se producen, necesitamos tooensure que, en Propiedades de Hola de codificadores AVC se establece Hola tamaño GOP ("grupo de imágenes") para ambos archivos MP4 too2 segundos, lo que pueden hacer por:

* establecer el tamaño de GOP de tooFixed de modo de tamaño de GOP hello y
* segundos de tootwo de Hello intervalo de fotogramas clave.
* establecer Hola GOP IDR Control tooClosed GOP tooensure se permanente todos los GOP en sus propias sin dependencias

toomake nuestra toounderstand adecuada del flujo de trabajo, cambiar el nombre de codificador de hello primera AVC demasiado "codificador de vídeo AVC 640 x 360 1.200 kbps" y Hola segundo codificador AVC "codificador de vídeo AVC 960 x 540 kbps 2500".

Ahora, agregue un segundo multiplexor ISO MPEG-4 y una segunda salida de archivo. Conecte Hola multiplexor toohello nueva AVC codificador y asegúrese de que se dirige la salida en el archivo de salida de hello. A continuación, conecte también nueva de toohello de salida del codificador de audio de AAC Hola entrada de multiplexor. Hola archivo de salida a su vez, a continuación, puede ser tooadd de nodo de recurso de archivo de salida toohello conectado se toohello activo de servicios multimedia que va a crear.

![Segundo multiplexor y salida de archivo conectados](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

*Segundo multiplexor y salida de archivo conectados*

Por compatibilidad con el empaquetado dinámico de servicios multimedia de Azure, configure tooGOP recuento de hello del multiplexor modo de fragmento o la duración y establezca GOP Hola por fragmento too1. (Esto debe ser Hola predeterminada.)

![Modos de fragmento del multiplexor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

*Modos de fragmento del multiplexor*

Nota: puede que desee toorepeat este proceso para cualquier otro de velocidad de bits y la resolución combinaciones que desee toohave agregan una salida de activos toohello.

### <a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Nombres de salida de archivo de configuración Hola
Contamos con más de un recurso de salida toohello único archivo agregado. Esto proporciona una necesidad toomake seguro hello, nombres de archivo para cada uno de Hola archivos difieren entre sí y quizás incluso aplican una convención de nomenclatura de archivos para lo que usted está tratando con queda claro Hola nombre de archivo de salida.

Nomenclatura de salida de archivos se puede controlar a través de expresiones en el Diseñador de Hola. Abrir Panel de propiedades de Hola para uno de los componentes del archivo de salida de hello y abra el editor de expresiones de Hola para hello propiedad de archivo. Nuestro primer archivo de salida se configura a través de la siguiente expresión de hello (vea tutorial Hola para pasar de [velocidad de bits MXF tooa única salida MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

Esto significa que el nombre de archivo viene determinado por dos variables: Hola output directory toowrite en y hello nombre base del archivo de origen. primero Hola se expone como una propiedad en la raíz del flujo de trabajo de Hola y Hola este último viene determinado por el archivo de entrada de hello. Tenga en cuenta ese directorio de salida de hello es lo que se utiliza para realizar pruebas locales; motor de flujo de trabajo de hello reemplazará esta propiedad cuando se ejecuta el flujo de trabajo de Hola por procesador de multimedia en la nube de hello en los servicios de multimedia de Azure.
toogive ambos archivos de nuestro salida un resultado coherente de nomenclatura, cambio Hola primero archivo nomenclatura expresión para:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

y en segundo lugar Hola para:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

Ejecutar una prueba intermedia ejecutar toomake seguro ambos archivos MP4 de salida se generan correctamente.

### <a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Incorporación de una pista de audio independiente
Como veremos más adelante cuando se genera un toogo de archivo .ism con nuestros archivos MP4 de salida, se también necesitará un archivo MP4 de solo audio como pista de audio de hello para el streaming adaptable. toocreate este archivo, agregue un flujo de trabajo de toohello muxer adicionales (multiplexor de ISO-MPEG-4) y conéctese pin de salida del codificador de hello AAC con su pin de entrada de seguimiento 1.

![Multiplexor de audio agregado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

*Multiplexor de audio agregado*

Cree un tercer flujo de salida de salida del archivo componente toooutput Hola de hello muxer y configure la expresión de asignación de nombres de archivo hello como:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Multiplexor de audio creando una salida de archivo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

*Multiplexor de audio creando una salida de archivo*

### <a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Agregar Hola. Archivo SMIL ISM
Hola empaquetado dinámico toowork en combinación con ambos MP4 en archivos (y Hola solo audio MP4) en el recurso de servicios multimedia, también es necesario un archivo de manifiesto (también denominado archivo de "SMIL": lenguaje de integración Multimedia sincronizada). Este archivo indica los servicios multimedia tooAzure qué archivos MP4 están disponibles para el empaquetado dinámico y cuáles de esos tooconsider para hello audio de transmisión por secuencias. Un archivo de manifiesto típico para un conjunto de archivos MP4 con una única secuencia de audio tiene el siguiente aspecto:

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

archivo .ism de Hello contiene dentro de una instrucción switch, una tooeach de referencia de archivos de vídeo de MP4 individuales hello y además tooan MP4 que solo contiene audio Hola hace referencia a archivo de audio de toothose también una (o más).

Generar archivo de manifiesto de Hola para nuestro conjunto de MP4 puede realizarse a través de un componente denominado Hola "AMS manifiesto Writer". toouse, arrástrelo hasta la superficie de Hola y conecte clavijas de salida "Escritura finalizada" Hola desde Hola tres archivos salida componentes toohello el escritor de manifiesto de AMS de entrada. A continuación, asegúrese de salida de hello tooconnect seguro de hello AMS manifiesto escritor toohello recurso de archivo de salida.

Al igual que con nuestros otros componentes de salida archivo, configurar Hola .ism el nombre de salida de archivo con una expresión:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

El flujo de trabajo terminado es similar a Hola siguiente:

![El flujo de trabajo terminado MXF toomultibitrate MP4](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

*El flujo de trabajo terminado MXF toomultibitrate MP4*

## <a id="MXF_to__multibitrate_MP4"></a>Codificación de MXF en archivos MP4 de varias velocidades de bits: plano mejorado
Hola [tutorial de flujo de trabajo anterior](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) hemos visto cómo se puede convertir un solo activo de entrada de MXF en un recurso de salida con archivos MP4 de varias velocidades de bits, un archivo MP4 de solo audio y un archivo de manifiesto para su uso junto con multimedia de Azure Servicios de empaquetado dinámico.

Este tutorial le mostrará cómo pueden mejorar y algunos de los aspectos de hello pueden realizar más cómodo.

### <a id="MXF_to_multibitrate_MP4_overview"></a>Flujo de trabajo información general sobre tooenhance
![Multibitrate MP4 tooenhance de flujo de trabajo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

*Multibitrate MP4 tooenhance de flujo de trabajo*

### <a id="MXF_to__multibitrate_MP4_file_naming"></a>Convenciones de nomenclatura de los archivos
En el flujo de trabajo anterior Hola se especificó una expresión simple como base de Hola para generar nombres de archivo de salida. Tenemos algunos duplicación aunque: todos los componentes de archivo de salida individual de Hola Hola de dicha expresión especificada.

Por ejemplo, el componente de salida de archivo hello primer archivo de vídeo se configura con esta expresión:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

Mientras que para la segunda salida de hello vídeo, tenemos una expresión como:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

¿No sería más claro, menos propenso a errores y más fácil que pudiéramos eliminar parte de esta duplicación y hacer las cosas más configurables en su lugar? Por suerte podemos: capacidades de expresión del Diseñador de hello en combinación con toocreate de propiedades personalizadas en la raíz del flujo de trabajo para la capacidad Hola nos ofrecen un nivel adicional de comodidad.

Supongamos que se obtendrá de unidades de configuración de nombre de archivo de hello velocidades de bits de archivos MP4 individuales de Hola. Estas velocidades de bits se deberá tratar de conseguir tooconfigure en un centro colocar (en raíz Hola de nuestro gráfico), desde donde podrá ser acceso generación del nombre de archivo tooconfigure y la unidad. toodo, comenzamos mediante la publicación de la propiedad de velocidad de bits de Hola desde ambos raíz AVC codificadores toohello nuestro flujo de trabajo, para que sea accesible desde ambos raíz hello también a partir de los codificadores Hola AVC. (Incluso aunque se muestren en dos lugares diferentes, hay solo un valor subyacente).

### <a id="MXF_to__multibitrate_MP4_publishing"></a>Propiedades de componente en la raíz del flujo de trabajo de Hola de publicación
Abra codificador de hello primera AVC, vaya toohello propiedad de velocidad de bits (kbps) y de lista desplegable de hello elija Publicar.

![Propiedad de velocidad de bits de publicación Hola](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

*Propiedad de velocidad de bits de publicación Hola*

Configurar Hola publicar diálogo toopublish toohello raíz de nuestro gráfico de flujo de trabajo, con un nombre publicado de "video1bitrate" y un nombre para mostrar legible de "Velocidad de bits de vídeo 1". Configure un grupo personalizado denominado "Velocidades de bits de streaming" y haga clic en Publish (Publicar).

![Propiedad de velocidad de bits de publicación Hola](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

*Cuadro de diálogo de publicación para la propiedad de velocidad de bits*

Repita el proceso Hola mismo para la propiedad de velocidad de bits de Hola de hello en segundo lugar codificador AVC y asígnele el nombre "video2bitrate" con un nombre para mostrar de "Velocidad de bits de vídeo 2", en hello misma personalizado de grupo "Velocidades de bits de transmisión por secuencias".

Si ahora se inspeccionar las propiedades de raíz del flujo de trabajo de hello, veremos nuestro grupo personalizado con hello aparecen dos propiedades publicados. Ambos son reflejar el valor de Hola de su respectivo AVC codificador de velocidad de bits.

![Propiedades de velocidad de bits publicadas en la raíz del flujo de trabajo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

Siempre que se desee tooaccess estas propiedades desde el código o desde una expresión, por lo que podemos similar al siguiente:

* desde el código en línea de un componente justo debajo de la raíz de hello: node.getPropertyAsString('.. / video1bitrate', null)
* dentro de una expresión: ${ROOT_video1bitrate}

Vamos a completar grupo de "Velocidades de bits de transmisión por secuencias" hello mediante la publicación de nuestro velocidad pista de audio en él. Dentro de las propiedades de Hola de hello AAC codificador, busque la configuración de velocidad de bits de Hola y seleccione Publicar de hello desplegable siguiente tooit. Publicar toohello raíz del gráfico de hello con nombre "audio1bitrate" y el nombre "Velocidad de bits de Audio 1" dentro de nuestro grupo personalizado "Velocidades de bits de transmisión por secuencias" para mostrar.

![Cuadro de diálogo de publicación para la velocidad de bits de archivos de audio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

*Cuadro de diálogo de publicación para la velocidad de bits de archivos de audio*

![Propiedades resultantes de audio y vídeo en la raíz](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

*Propiedades resultantes de audio y vídeo en la raíz*

Tenga en cuenta que si se cambia cualquiera de los tres valores también vuelve a configurar y cambios Hola valores en los componentes respectivos Hola se vinculan con (y donde publicado desde).

### <a id="MXF_to__multibitrate_MP4_output_files"></a>Se han generado nombres de archivo de salida que se basan en los valores de propiedad publicados
En lugar de codificar nuestros nombres de archivo generado, podemos cambiar ahora la expresión de nombre de archivo en cada uno de los componentes toorely de archivo de salida de hello en las propiedades de la velocidad de bits de Hola que se acaba de publicar en la raíz del gráfico de Hola. A partir de la primera salida de archivo, buscar la propiedad de archivo de Hola y Editar expresión Hola similar al siguiente:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

pueden obtener acceso y escritos cuando se alcanza el signo de dólar Hola teclado Hola mientras esté en la ventana de la expresión de hello distintos parámetros de Hello en esta expresión. Uno de los parámetros disponibles de hello es nuestra propiedad video1bitrate que se publicó con anterioridad.

![Acceso a los parámetros de una expresión](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

*Acceso a los parámetros de una expresión*

Hola mismo para la salida de archivo de Hola para nuestro vídeo segundo:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

y para la salida de archivo de solo audio hello:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

Si ahora cambiamos la velocidad de bits de Hola para cualquiera de los archivos de audio o de vídeo de hello, codificador respectivos Hola se volverá a configurar y convención del nombre de archivo basado en la velocidad de bits Hola respetará todos los automática.

## <a id="thumbnails_to__multibitrate_MP4"></a>Agregar la salida de las miniaturas toomultibitrate MP4
A partir de un flujo de trabajo que genera [una salida de archivos MP4 de una entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), nos encargaremos ahora en Agregar salida toohello de las miniaturas.

### <a id="thumbnails_to__multibitrate_MP4_overview"></a>Vistas en miniatura de flujo de trabajo información general sobre tooadd a
![Multibitrate MP4 toostart de flujo de trabajo de](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

*Multibitrate MP4 toostart de flujo de trabajo de*

### <a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Incorporación de codificación JPG
núcleo de Hello de la generación de miniaturas será componente de codificador JPG hello, toooutput capaz de los archivos JPG.

![Codificador JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

*Codificador JPG*

No podemos directamente sin embargo nos conectamos la secuencia de vídeo sin comprimir de hello entrada de archivo de medios en el codificador de hello JPG. En su lugar, se espera que va a pasar toobe fotogramas individuales. Esto, podemos hacer mediante un componente de puerta de fotograma de vídeo de Hola.

![Conectar un codificador de marco puerta toohello JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

*Conectar un codificador de marco puerta toohello JPG*

puerta de marco de Hello, una vez cada tantas segundos o marcos permite un toopass de fotograma de vídeo. tiempo de Hola y el intervalo de Hello desfase que esto sucede es configurable en las propiedades de Hola.

![Propiedades de puerta de fotogramas de vídeo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

*Propiedades de puerta de fotogramas de vídeo*

Vamos a crear una vista en miniatura de cada minuto estableciendo el modo de hello tooTime (segundos) y Hola too60 de intervalo.

### <a id="thumbnails_to__multibitrate_MP4_color_space"></a>Relación con la conversión de espacio de colores
Aunque podría parecer lógico tanto ahora se pueden conectar los terminales de vídeo sin comprimir de puerta de marco de Hola y Hola entrada de archivo multimedia, se obtendría una advertencia si se debería hacerlo.

![Error de espacio de colores de entrada](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

*Error de espacio de colores de entrada*

Esto es porque la manera de hello en qué color se representa información en nuestro original sin formato sin comprimir secuencia de vídeo, procedentes de nuestro MXF es diferente de qué Hola JPG codificador está esperando. Más específicamente, una denominada "espacio de color" de "RGB" o "Escala de grises" es lo esperado tooflow en. Esto significa la que secuencia de vídeo entrante del que Hola vídeo fotograma puerta deberá toohave una conversión que se aplican en primer lugar con respecto a su espacio de color.

Arrastre Hola de flujo de trabajo de hello convertidor de espacio de Color - Intel y conectar la puerta de marco tooour.

![Conexión con un convertidor de espacio de colores](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

*Conexión con un convertidor de espacio de colores*

En la ventana de propiedades de hello, elija entrada Hola BGR de 24 de hello valor preestablecido de lista.

### <a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Miniaturas de Hola de escritura
A diferencia de nuestro vídeo de MP4, Hola codificador JPG componente dará como resultado más de un archivo. En orden toodeal con esto, se puede usar un componente de sistema de escritura de archivo de escena búsqueda JPG: tomará miniaturas de Hola entrantes JPG y escribirlos, cada nombre de archivo que se va a seguidos de un número diferente. (número de hello normalmente indica el número de Hola de segundos/unidades en flujo de Hola que Hola miniatura se extraen del).

![Introducción a Hola escena búsqueda JPG archivo escritor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

*Introducción a Hola escena búsqueda JPG archivo escritor*

Configurar la propiedad de ruta de acceso de carpeta de salida de hello con expresión hello: ${ROOT_outputWriteDirectory}

y Hola la propiedad con el prefijo de nombre de archivo:

    ${ROOT_sourceFileBaseName}_thumb_

prefijo de Hello determinarán cómo se se denominan archivos de miniaturas de Hola. Se agregará como sufijo con posición de un número que indica Hola general flujo de Hola.

![Propiedades de la escritura de archivos JPG de búsqueda de escenas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

*Propiedades de la escritura de archivos JPG de búsqueda de escenas*

Conecte el nodo de recurso de archivo de salida de hello escena búsqueda JPG archivo escritor toohello.

### <a id="thumbnails_to__multibitrate_MP4_errors"></a>Detección de errores en un flujo de trabajo
Conectar entrada Hola Hola color espacio convertidor toohello sin formato sin comprimir salida de vídeo. Ahora, ejecutar una prueba local para el flujo de trabajo de Hola. Hay un flujo de trabajo de hello muchas posibilidades repentinamente se deje de ejecutarse y se indican con un contorno de color rojo en el componente de Hola que encontró un error:

![Error de convertidor de espacio de colores](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

*Error de convertidor de espacio de colores*

Haga clic en icono de "E" hello poco rojo en hello superior derecho de hello convertidor de espacio de Color componente toosee ¿cuál es el motivo de hello error al tratar de codificación de Hola.

![Cuadro de diálogo de error del convertidor de espacio de colores](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

*Cuadro de diálogo de error del convertidor de espacio de colores*

Esto resulta, como puede ver, que espacio de colores entrante de hello estándar para los convertidores de espacio de color de hello tiene toobe rec601 para la conversión solicitada de YUV tooRGB. Aparentemente, nuestra secuencia no indica que fuera rec601. (Rec 601 es un estándar para codificar señales de vídeo analógicas entrelazadas en formato de vídeo digital. Especifica una región activa que abarcan 720 muestras de luminancia y 360 muestras cromáticas por línea. sistema de codificación de color de Hola se conoce como YCbCr 4:2:2.)

toofix esto, se deberá indicar en los metadatos de Hola de nuestro flujo que estamos trabajando con contenido de rec601. toodo por lo que vamos a usar un componente actualizador de tipo de datos de vídeo, que colocamos entre nuestro raw hello y origen color espacio componente de conversión. Esta actualización del tipo de datos permite la actualización manual de Hola de determinados datos de vídeo propiedades de tipo. Configurar un espacio de Color estándar de "Rec 601" tooindicate. Esto hará que flujo de hello actualizador de tipo de datos de vídeo tootag Hola con espacio de colores de Hola "Rec 601" Si no hay ningún espacio de color definido todavía. (No reemplazará los metadatos existentes, a menos que se activa la casilla de invalidación de Hola.)

![Actualizar espacio de Color estándar en hello actualizador de tipo de datos](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

*Actualizar espacio de Color estándar en hello actualizador de tipo de datos*

### <a id="thumbnails_to__multibitrate_MP4_finish"></a>Flujo de trabajo finalizado
Ahora que nuestro finaliza el flujo de trabajo, realice otra toosee de ejecución de pruebas que pasar.

![Flujo de trabajo terminado para varias salidas MP4 con miniaturas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

*Flujo de trabajo terminado para varias salidas MP4 con miniaturas*

## <a id="time_based_trim"></a>Recorte basado en tiempo de salida MP4 de varias velocidades de bits
A partir de un flujo de trabajo que genera [una salida de archivos MP4 de una entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), ahora nos encargaremos en Recortar el vídeo de origen de hello en función de marcas de tiempo.

### <a id="time_based_trim_start"></a>Flujo de trabajo información general sobre toostart Agregar recorte
![A partir de recorte de tooadd de flujo de trabajo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

*A partir de recorte de tooadd de flujo de trabajo*

### <a id="time_based_trim_use_stream_trimmer"></a>Uso de hello secuencia recortador
componente de flujo recortador Hola permite tootrim Hola principio y al final de un flujo de entrada que se base en información de tiempo (segundos, minutos,...). Recortador Hello no admite basada en el marco de recorte.

![Recortador de transmisiones](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

*Recortador de transmisiones*

En lugar de vincular directamente los codificadores de hello AVC y altavoces posición asignador toohello entrada de archivo multimedia, colocamos entre esos Recortador de flujo de Hola. (Uno para señal de vídeo de hello y otro para hello intercalan la señal de audio.)

![Coloque el recortador de transmisiones entre ellos](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

*Coloque el recortador de transmisiones entre ellos*

Vamos a configurar recortador Hola para que sólo se procesará de vídeo y audio entre 15 y 60 segundos en vídeo de Hola.

Vaya toohello propiedades de hello Recortador de secuencia de vídeo y configure la hora de inicio (15s) y propiedades de la hora de finalización (60 s). toomake seguro tanto nuestro Recortador de audio y vídeo es siempre configurado toohello mismo empezar y terminar valores, se publicará esos raíz toohello de flujo de trabajo de Hola.

![Publique la propiedad de tiempo de inicio del recortador de transmisiones](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

*Publique la propiedad de tiempo de inicio del recortador de transmisiones*

![Cuadro de diálogo de propiedades de publicación para el tiempo de inicio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

*Cuadro de diálogo de propiedades de publicación para el tiempo de inicio*

![Cuadro de diálogo de propiedades de publicación para el tiempo de finalización](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

*Cuadro de diálogo de propiedades de publicación para el tiempo de finalización*

Si ahora se inspecciona raíz Hola nuestro flujo de trabajo, ambas propiedades será claridad mostrada y se puede configurar a partir de ahí.

![Propiedades publicadas disponibles en la raíz](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

*Propiedades publicadas disponibles en la raíz*

Abrir propiedades de recorte de Hola desde recortador audio Hola ahora y configurar horas de inicio y final con una expresión que hace referencia toohello publicado propiedades en la raíz de Hola de nuestro flujo de trabajo.

Para hello recorte audio hora de inicio:

    ${ROOT_TrimmingStartTime}

y para el tiempo de finalización:

    ${ROOT_TrimmingEndTime}

### <a id="time_based_trim_finish"></a>Flujo de trabajo finalizado
![Flujo de trabajo finalizado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

*Flujo de trabajo finalizado*

## <a id="scripting"></a>Introducción a Hola componente de la secuencia de comandos
Componentes de script pueden ejecutar secuencias de comandos arbitrarias durante las fases de ejecución de Hola de nuestro flujo de trabajo. Hay cuatro secuencias de comandos diferentes que se pueden ejecutar, cada uno con su propio contexto de ciclo de vida de flujo de trabajo Hola y de características específicas:

* **commandScript**
* **realizeScript**
* **processInputScript**
* **lifeCycleScript**

documentación de Hola de hello componente incluye en el script va con más detalle para cada uno de hello anterior. En [Hola después de la sección](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** componente scripting es tooconstruct usa un xml cliplist en marcha de hello cuando se inicia el flujo de trabajo de Hola. Este script se llama durante la instalación de componente de hello, lo que sucede solo una vez en su ciclo de vida.

### <a id="scripting_hello_world"></a>Scripting en un flujo de trabajo: hola a todos
Arrastre un componente de la secuencia de comandos en la superficie del Diseñador de Hola y cambie su nombre (por ejemplo, "SetClipListXML").

![Incorporación de un componente generado por script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Incorporación de un componente generado por script*

Al examinar las propiedades de Hola de Hola componente de la secuencia de comandos, hello se muestran cuatro tipos diferentes de la secuencia de comandos, cada secuencia de comandos distintos de tooa configurable.

![Propiedades de componente generado por script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Propiedades de componente generado por script*

Desactive Hola processInputScript y abra el editor de Hola para hello realizeScript. Ahora se está configuradas y listo toostart de scripting.

Las secuencias de comandos se escriben en Groovy, un lenguaje de scripting compilado dinámicamente para la plataforma Java de Hola que conserva la compatibilidad con Java. En realidad, la mayoría del código Java es también código Groovy válido.

Vamos a escribir una secuencia de comandos simple hello world muy bueno en contexto de Hola de nuestra realizeScript. Escriba Hola siguiente en el editor de hello:

    node.log("hello world");

A continuación, ejecute una prueba de forma local. Después de esta ejecución, inspeccionar (a través de la ficha de sistema de hello en Hola componente de la secuencia de comandos) Hola propiedad registros.

![Salida de registro Hola a todos](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

*Salida de registro Hola a todos*

objeto de nodo de Hola se llame al método de registro de hello, hace referencia tooour actual "node" o un componente de hello nos estamos scripting dentro. Por lo tanto, cada componente tiene Hola capacidad toooutput el registro de datos disponible a través de la ficha de sistema de Hola. En este caso, hemos salida Hola literal de cadena "¡hello world". Toounderstand importante aquí es que esto puede resultar toobe una valiosa herramienta de depuración, proporcionando una visión general de la secuencia de comandos de hello realmente está realizando.

Desde dentro de nuestro entorno de scripting, también tenemos acceso tooproperties en cuenta otros componentes. Pruebe esto:

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

Nuestra ventana de registro mostrará Hola siguientes:

![Salida de registro para obtener acceso a las rutas de acceso del nodo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

*Salida de registro para obtener acceso a las rutas de acceso del nodo*

## <a id="frame_based_trim"></a>Recorte basado en fotogramas de salida MP4 de varias velocidades de bits
A partir de un flujo de trabajo que genera [una salida de archivos MP4 de una entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), ahora nos encargaremos en vídeo de origen de hello según los recuentos de marco de recorte.

### <a id="frame_based_trim_start"></a>Plano técnico toostart de información general sobre la adición de recorte para
![Agregar recorte de toostart de flujo de trabajo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

*Agregar recorte de toostart de flujo de trabajo*

### <a id="frame_based_trim_clip_list"></a>Uso de hello XML de la lista de imágenes
En todos los tutoriales de flujo de trabajo anterior, hemos usado el componente de entrada de archivo de medios de hello como el origen de entrada de vídeo. Para este escenario concreto, usaremos componente de origen de la lista de Clip de hello en su lugar. Tenga en cuenta que esto no debería ser Hola preferido forma de trabajar; usar solo hello Clip lista origen cuando hay un toodo verdadera razón de por lo que (al igual que en hello debajo de los casos, donde estamos realizando uso de las capacidades de hello clip lista recorte).

tooswitch de nuestro toohello de entrada de archivo multimedia origen de la lista de Clip, arrastre el componente de origen de la lista de imágenes de hello en la superficie de diseño de Hola y conectarse Hola Clip lista XML pin toohello Clip lista nodo XML del Diseñador de flujo de trabajo de Hola. Esto rellenará Hola Clip lista origen con PIN de salida, según el vídeo de entrada tooour. Conectar ahora PIN sin comprimir de Audio y vídeo sin comprimir de Hola de Hola Hola Clip lista origen toohello respectivos AVC codificadores y Interleaver de secuencia de Audio. Quitar ahora Hola entrada de archivo de medios.

![Reemplazar Hola entrada de archivo de medios con hello Clip lista origen](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

*Reemplazar Hola entrada de archivo de medios con hello Clip lista origen*

componente de origen de la lista de Clip Hola toma como entrada un "Clip lista XML". Al seleccionar hello tootest de archivo de origen con localmente, esta lista de clip xml es rellena automáticamente para usted.

![Propiedad del XML de la lista de clips rellenado de forma automática](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

*Propiedad del XML de la lista de clips rellenado de forma automática*

Para examinar un poco más de cerca xml toohello, este es su aspecto como:

![Cuadro de diálogo Edit clip list (Editar lista de clips)](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

*Cuadro de diálogo Edit clip list (Editar lista de clips)*

Esto no obstante no refleja las capacidades de Hola Hola clip lista XML. Una opción que tenemos es tooadd un elemento "Recorte" en vídeo de Hola y origen de audio, similar al siguiente:

![Agregar una lista de imágenes de recorte de elemento toohello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

*Agregar una lista de imágenes de recorte de elemento toohello*

Si modifica Hola clip lista xml similar al siguiente por encima y realizar una serie de pruebas local, podrá ver vídeo Hola correctamente sido recortan entre 10 y 20 segundos en vídeo de Hola.

Toowhat contraria se produce cuando se realiza una ejecución local, aunque este mismo xml cliplist no tendría Hola mismo efecto cuando se aplica en un flujo de trabajo que se ejecuta en servicios multimedia de Azure. Cuando empieza a codificador Premium de Azure, hello cliplist xml se genera cada vez que una vez más, en función de hello codificación de archivo de entrada de Hola se asignó el trabajo. Esto significa que cualquier cambio que hacemos en xml de hello Lamentablemente se reemplazaría.

toocounter hello cliplist xml borrarse cuando se inicia un trabajo de codificación, podemos volver a generar, en marcha Hola justo después del inicio de Hola de nuestro flujo de trabajo. Tales acciones personalizadas se pueden realizar a través de lo que se denomina un "componente generado por script". Para obtener más información, consulte [Introducing Hola componente incluye en el script](media-services-media-encoder-premium-workflow-tutorials.md#scripting).

Arrastre un componente de la secuencia de comandos en la superficie del Diseñador de Hola y cámbiele el nombre demasiado "SetClipListXML".

![Incorporación de un componente generado por script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Incorporación de un componente generado por script*

Al examinar las propiedades de Hola de Hola componente de la secuencia de comandos, hello se muestran cuatro tipos diferentes de la secuencia de comandos, cada secuencia de comandos distintos de tooa configurable.

![Propiedades de componente generado por script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Propiedades de componente generado por script*

### <a id="frame_based_trim_modify_clip_list"></a>Modificar lista de clip Hola desde un componente de la secuencia de comandos
Antes de volver a podemos escribir hello cliplist xml que se genera durante el inicio del flujo de trabajo, necesitaremos contenido y la propiedad xml de toohave acceso toohello cliplist. Para ello podemos hacer lo siguiente:

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Lista de clips entrantes que se están registrando](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

*Lista de clips entrantes que se están registrando*

Primero necesitamos una manera toodetermine desde qué momento hasta qué punto queremos tootrim Hola de vídeo. publicar de este usuario de menos conocimientos técnicos toohello adecuada del flujo de trabajo de hello, toomake raíz de toohello dos propiedades de gráfico de Hola. toodo esto, haga clic en la superficie del Diseñador de Hola y seleccione "Agregar propiedad":

* Primera propiedad: "ClippingTimeStart" del tipo: "TIMECODE" (CÓDIGO DE TIEMPO)
* Segunda propiedad: "ClippingTimeEnd" del tipo: "TIMECODE" (CÓDIGO DE TIEMPO)

![Cuadro de diálogo Add Property (Agregar propiedad) para el tiempo de inicio del recorte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

*Cuadro de diálogo Add Property (Agregar propiedad) para el tiempo de inicio del recorte*

![Propiedades del tiempo de recorte publicadas en la raíz del flujo de trabajo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

*Propiedades del tiempo de recorte publicadas en la raíz del flujo de trabajo*

Configure ambos valor adecuado de tooa de propiedades:

![Configurar Hola ajustar propiedades de inicio y finalización](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

*Configurar Hola ajustar propiedades de inicio y finalización*

Ahora, desde dentro del script, podemos acceder a ambas propiedades, de la forma siguiente:

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Ventana de registro que muestra el inicio y fin del recorte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

*Ventana de registro que muestra el inicio y fin del recorte*

Vamos a analizar las cadenas de código de tiempo de hello en un formato más cómodo de toouse, con una expresión regular simple:

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

*Ventana de registro con salida de código de tiempo redistribuida*

Con esta información en cuestión, ahora podemos modificamos inicio Hola de hello cliplist xml tooreflect y horas de finalización de hello deseado precisa para el marco de recorte de película Hola.

![Elementos de recorte de tooadd de código de script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

*Elementos de recorte de tooadd de código de script*

Esto se realizó mediante operaciones de manipulación de cadenas normales. Hola resultante imagen prediseñada modificada lista xml se escribe volver toohello clipListXML propiedad en la raíz del flujo de trabajo de Hola a través del método de "setProperty" hello. ventana de registro de Hello después de ejecutar otra prueba nos mostraría Hola siguientes:

![Registro de lista de clip resultante Hola](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

*Registro de lista de clip resultante Hola*

Hacer un toosee serie de pruebas, ¿cómo se han recortado secuencias de vídeo y audio de Hola. Tal y como se llevará a cabo más de una serie de pruebas con valores diferentes para puntos de recorte de hello, observará que los que no se tendrán en cuenta sin embargo! motivo Hello es ese diseñador hello, a diferencia de hello Azure en tiempo de ejecución, ocurre no invalidación hello cliplist xml con cada. Esto significa que solo hello primera vez que se ha establecido Hola de entrada y salida puntos, hará que Hola xml tootransform, todos los otros Hola veces, la cláusula de restricción (si (clipListXML.indexOf ("<trim>") == -1)) impedirá que el flujo de trabajo de hello agregar otro recorte elemento cuando ya hay uno presente.

toomake nuestro flujo de trabajo adecuada tootest localmente, es mejor agregar un código de mantenimiento de la casa que inspecciona si ya existe un elemento de recorte. Si es así, se pueden eliminar antes de continuar modificando Hola xml con los nuevos valores de hello. En lugar de usar manipulaciones de cadena sin formato, es más seguro probablemente toodo esto a través de objeto xml real del modelo de análisis.

Antes de que podemos agregar aunque dicho código, necesitaremos tooadd que un número de instrucciones de importación en hello inicia de nuestro script primero:

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

Después de esto, podemos agregar Hola requerido código de limpieza:

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

Este código entrará justo encima de punto de hello en el que agregamos Hola elementos recorte toohello cliplist xml.

En este momento, podemos ejecutar y modificar el flujo de trabajo como hora hasta que deseamos ejerciendo cambios Hola aplica alguna vez.    

### <a id="frame_based_trim_clippingenabled_prop"></a>Incorporación de una propiedad de conveniencia ClippingEnabled
Como no siempre puede toohappen de recorte, vamos a concluir el flujo de trabajo mediante la adición de una cómoda marca booleana que indica si desea o no se tooenable recortar / recorte.

Al igual que antes, publique una nueva propiedad toohello raíz nuestro flujo de trabajo denominado "ClippingEnabled" de tipo "BOOLEAN".

![Publicación de una propiedad para habilitar el recorte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

*Publicación de una propiedad para habilitar el recorte*

Con hello por debajo de la cláusula de restricción simple, podemos comprobar si es necesario recorte y decidir si nuestra lista de clip por lo tanto debe toobe modificado o no.

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <a id="code"></a>Código completo
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


## <a name="also-see"></a>Consulte también:
[Introducción de la codificación Premium en Servicios multimedia de Azure](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[¿Cómo tooUse Premium de codificación en servicios multimedia de Azure](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[Codificación de contenido a petición con Azure Media Services](media-services-encode-asset.md#media-encoder-premium-workflow)

[Códecs y formatos de flujo de trabajo del Codificador multimedia Premium](media-services-premium-workflow-encoder-formats.md)

[Archivos de flujo de trabajo de ejemplo](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[Explorador de Servicios multimedia de Azure](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
