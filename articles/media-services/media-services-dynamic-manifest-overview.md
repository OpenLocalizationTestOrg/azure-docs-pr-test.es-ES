---
title: "aaaFilters y manifiestos dinámicos | Documentos de Microsoft"
description: "Este tema describe cómo toocreate filtros para que el cliente pueda usarlas toostream secciones específicas de una secuencia. Servicios multimedia crea manifiestos dinámicos tooarchive este selectivo de transmisión por secuencias."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: ff102765-8cee-4c08-a6da-b603db9e2054
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 9527a011438c11da07a363d701ea736414412ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="filters-and-dynamic-manifests"></a>Filtros y manifiestos dinámicos
A partir de la versión 2.11, servicios multimedia permite toodefine filtros para los activos. Estos filtros son reglas de lado de servidor que permitirán que los clientes toochoose toodo cosas como: reproducción únicamente una sección de un vídeo (en lugar de reproducir Hola completos de vídeo), o especifique solo un subconjunto de copias de audio y vídeo que los dispositivos de su cliente pueden controlar () en lugar de todas las copias de Hola que están asociadas a Hola activo). Dicho filtrado de los activos se archiva a través de **manifiesto dinámica**s que se crean al toostream de solicitud de su cliente un vídeo en función de los filtros especificados.

Estos temas se describen escenarios comunes en los que con filtros sería muy beneficiosos tooyour tootopics de los clientes y los vínculos que muestran cómo se filtra mediante programación toocreate (actualmente, puede crear filtros con las API de REST solo).

## <a name="overview"></a>Información general
Cuando se entrega el contenido toocustomers (transmisión por secuencias de eventos en directo o vídeo bajo demanda) el objetivo es toodeliver un dispositivo de vídeo toovarious de alta calidad en condiciones de red diferente. tooachieve este objetivo Hola siguientes:

* codificar su secuencia toomulti de bits ([velocidad de bits adaptativa](http://en.wikipedia.org/wiki/Adaptive_bitrate_streaming)) secuencia de vídeo (Esto se encargará de condiciones de calidad y la red) y 
* uso de servicios multimedia [empaquetado dinámico](media-services-dynamic-packaging-overview.md) toodynamically volver a empaquetar la secuencia en distintos protocolos (Esto se encargará de transmisión por secuencias en diferentes dispositivos). Servicios multimedia admite la entrega de hello siguiendo las tecnologías de streaming de velocidad de bits adaptativa: HTTP Live Streaming (HLS), Smooth Streaming y MPEG DASH. 

### <a name="manifest-files"></a>Archivos de manifiesto
Al codificar un activo para el streaming de velocidad de bits adaptativa, un **manifiesto** se crea el archivo (lista de reproducción) (archivo hello está basado en texto o XML). Hola **manifiesto** archivo incluye la transmisión por secuencias de metadatos como: realizar un seguimiento de tipo (audio, vídeo o texto), realizar el seguimiento de nombre, hora de inicio y finalización, velocidad de bits (calidades), idiomas de seguimiento, ventana de presentación (una ventana deslizante de duración fija), vídeo códec (FourCC). También indica a fragmento siguiente de hello Reproductor tooretrieve Hola proporcionando información sobre Hola siguiente reproducen fragmentos de vídeo disponibles y su ubicación. Fragmentos (o segmentos) son Hola real "fragmentos" de un contenido de vídeo.

Este es un ejemplo de un archivo de manifiesto: 

    <?xml version="1.0" encoding="UTF-8"?>    
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="330187755" TimeScale="10000000">

    <StreamIndex Chunks="17" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="8">
    <QualityLevel Index="0" Bitrate="5860941" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931300016E360000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="1" Bitrate="4602724" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931100011EDC00002CD29FF8C7076850A45800000000168E9093525" />
    <QualityLevel Index="2" Bitrate="3319311" FourCC="H264" MaxWidth="1280" MaxHeight="720" CodecPrivateData="000000016764001FAC2CA5014016EC054808080A00000300020000030064C0800067C28000103667F8C7076850A4580000000168E9093525" />
    <QualityLevel Index="3" Bitrate="2195119" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C1000044AA0000ABA9FE31C1DA14291600000000168E9093525" />
    <QualityLevel Index="4" Bitrate="1469881" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C04000B71A0000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="5" Bitrate="978815" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C08001E8480004C4B7F8C7076850A45800000000168E9093525" />
    <QualityLevel Index="6" Bitrate="638374" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C080013D60000C65DFE31C1DA1429160000000168E9093525" />
    <QualityLevel Index="7" Bitrate="388851" FourCC="H264" MaxWidth="320" MaxHeight="180" CodecPrivateData="000000016764000DAC2CA505067E7C054830303200000300020000030064C040030D40003D093F8C7076850A45800000000168E9093525" />

    <c t="0" d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="9600000"/>
    </StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_128kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_128kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="125658" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_56kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_56kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="53655" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>

    </SmoothStreamingMedia>

### <a name="dynamic-manifests"></a>Manifiestos dinámicos
Hay [escenarios](media-services-dynamic-manifest-overview.md#scenarios) cuando el cliente necesita más flexibilidad que lo que se describe en el archivo de manifiesto del recurso de Hola de forma predeterminada. Por ejemplo:

* Dispositivo específico: entregar solo Hola especificado o copias especificado pistas de lenguaje que son compatibles con el dispositivo hello tooplayback usado Hola ("copia de filtrado de contenido"). 
* Reducir Hola manifiesto tooshow un clip secundario de un evento en directo ("clip secundario filtrado").
* Inicio de Hola de recorte de un vídeo ("recortar un vídeo").
* Ajustar la ventana de presentación (DVR) en orden tooprovide una longitud limitada de ventana DVR hello en el Reproductor de hello ("ventana de presentación ajustar").

tooachieve esta flexibilidad, ofertas de servicios multimedia **manifiestos dinámicos** basado en predefinidos [filtros](media-services-dynamic-manifest-overview.md#filters).  Una vez que defina los filtros de hello, los clientes podrían utilizar una copia específica de toostream o subcarpetas clips de vídeo. Debería especificar filtros de hello transmisión por secuencias de dirección URL. Filtros pudieron ser la velocidad de bits de tooadaptive aplicado streaming protocolos admitidos por [empaquetado dinámico](media-services-dynamic-packaging-overview.md): HLS, MPEG-DASH y Smooth Streaming. Por ejemplo:

URL de MPEG DASH con filtro

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf,filter=MyLocalFilter)

URL de Smooth Streaming con filtro

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyLocalFilter)


Para obtener más información acerca de cómo toodeliver el contenido y la compilación de transmisión por secuencias de direcciones URL, vea [entregar información general del contenido](media-services-deliver-content-overview.md).

> [!NOTE]
> Tenga en cuenta que manifiestos dinámicos no cambiar activos de Hola y Hola manifiesto predeterminado para ese recurso. El cliente puede elegir toorequest un flujo con o sin filtros. 
> 
> 

### <a id="filters"></a>Filtros
Hay dos tipos de filtros de activos: 

* Filtros globales (puede ser activo tooany aplicados en hello cuenta de servicios multimedia de Azure, tienen una duración de la cuenta de hello) y 
* Filtros locales (pueden ser solo asset tooan aplicada con qué hello filtro se asoció tras su creación, tienen una duración de activos de hello). 

Tipos de filtros globales y locales tienen exactamente hello las mismas propiedades. Hola principal diferencia entre Hola dos es para los escenarios de qué tipo de un sistema de almacenamiento es más adecuado. Filtros globales son suele resultar adecuados para los perfiles de dispositivo (filtrado de copia) donde filtros locales pueden ser utilizado tootrim un activo específico.

## <a id="scenarios"></a>Escenarios comunes
Tal y como se mencionó antes, cuando se entrega el contenido toocustomers (transmisión por secuencias de eventos en directo o vídeo bajo demanda) de su objetivo es toodeliver un vídeo de alta calidad toovarious dispositivos en diferentes las condiciones de red. Además, puede tener otros requisitos que implican el filtrado de los activos y el uso de **manifiestos dinámico**s. Hola las secciones siguientes proporcionan una breve introducción de distintos escenarios de filtrado.

* Especifique solo un subconjunto de copias de audio y vídeo que pueden controlar determinados dispositivos (en lugar de todas las copias de Hola que están asociadas a Hola activo). 
* Reproducir solo una sección de un vídeo (en lugar de reproducir Hola completos de vídeo).
* Ajustar la ventana de presentación de DVR.

## <a name="rendition-filtering"></a>Filtrado de representaciones
Puede elegir tooencode los perfiles de codificación del toomultiple del activo (línea de base de H.264, H.264 alta, AACL, AACH, Dolby Digital Plus) y varias velocidades de bits de calidad. Sin embargo, no todos los dispositivos cliente serán compatibles con todos los perfiles y velocidades de bits de su activo. Por ejemplo, los dispositivos Android más antiguos solo admiten H.264 Baseline+AACL. Enviar superior dispositivo tooa de velocidades de bits que no se puede obtener ventajas de hello, desperdicia cálculo de ancho de banda y el dispositivo. Dispositivo de este tipo debe descodificar todos Hola debido a información, solo tooscale lo hacia abajo para mostrar.

Con manifiestos dinámicos, puede crear perfiles de dispositivos como dispositivos móviles, consola, HD y SD, etc. y se incluyen hello pistas calidades que desee toobe una parte de cada perfil.

![Ejemplo de filtrado de representaciones][renditions2]

En el siguiente ejemplo de Hola, un codificador era tooencode usa un recurso mezzanine en copias de vídeo de ISO MP4s siete (de 180p too1080p). Hello activo codificado puede dinámicamente empaquetarse en cualquiera de hello después de protocolos de transmisión por secuencias: MPEG DASH, HLS y Smooth.  Hola parte superior de diagrama de hello, se muestra hello HLS manifiesto de recurso de hello sin filtros (contiene todas las copias de siete).  En la parte inferior izquierda de hello, se muestra hello que HLS manifiesto toowhich se aplicó un filtro con el nombre "ott". filtro de "ott" Hello especifica tooremove todas las velocidades de bits por debajo de 1 Mbps, lo que provocó Hola inferior dos los niveles de calidad que se separa en respuesta Hola.  En hello parte inferior derecha, Hola HLS toowhich manifiesto se aplicó un filtro con el nombre "móvil" se muestra. filtro "móvil" Hello especifica copias tooremove donde hello resolución es mayor que 720p, lo que produce dos copias de 1080p Hola perdiendo.

![Filtrado de representaciones][renditions1]

## <a name="removing-language-tracks"></a>Quitar pistas de idioma
Los activos pueden incluir varios idiomas de audio como inglés, español, francés, etc. Por lo general, realiza un seguimiento de audio disponible por selección de usuarios y administradores de SDK del Reproductor de hello predeterminadas selección de pista de audio. Resulta difícil toodevelop estos SDK de Reproductor, requiere que las implementaciones diferentes a través de los marcos de Reproductor específico del dispositivo. Además, en algunas plataformas, las API del Reproductor están limitadas y no incluyen la característica de selección de audio donde los usuarios no se pueden seleccionar o cambiar la pista de audio predeterminada de Hola. Con los filtros de recurso, puede controlar el comportamiento de hello mediante la creación de filtros que incluyan solo los idiomas de audio deseados.

![Filtrado de pistas de idioma][language_filter]

## <a name="trimming-start-of-an-asset"></a>Recorte del inicio de un activo
En la mayoría los eventos de transmisión por secuencias en directo, operadores ejecutan algunas pruebas antes del evento real Hola. Por ejemplo, puede que incluyan una pizarra así antes del inicio de Hola de evento de hello: "Programa comenzará en breve". Si archiva programa Hola, prueba hello y tableta táctil datos también se almacenan y se incluirá en la presentación de Hola. Sin embargo, esta información no se debería mostrar a clientes toohello. Con manifiestos dinámicos, puede crear un filtro de tiempo de inicio y quitar datos de hello no deseado de manifiesto de Hola.

![Inicio de recorte][trim_filter]

## <a name="creating-sub-clips-views-from-a-live-archive"></a>Crear clips secundarios (vistas) desde un archivo en directo
Muchos eventos en directo son de larga ejecución y el archivo en directo puede incluir varios eventos. Después de que los emisores de extremos de evento en directo de hello pueden querer toobreak seguridad Hola live archivo en el inicio del programa lógico y detener las secuencias. A continuación, publicar estos programas virtuales por separado sin post procesar archivos activos de hello y no crear activos independientes (que no obtendrá las ventajas de fragmentos en caché existente de hello en CDN Hola). Ejemplos de estos programas virtuales (subcarpetas clips) son trimestres Hola de fútbol o partido de baloncesto, entradas de hello en béisbol o eventos individuales de una tarde de programa Olimpiadas.

Con manifiestos dinámicos, puede crear filtros de uso de tiempos de inicio y fin y crear vistas virtuales encima de Hola de su archivo dinámico. 

![Filtro de clips secundarios][subclip_filter]

Activo filtrado:

![Esquí][skiing]

## <a name="adjusting-presentation-window-dvr"></a>Ajustar la ventana de presentación (DVR)
Actualmente, los servicios multimedia de Azure ofrece circular archivo donde se puede configurar la duración de hello entre 5 minutos: 25 horas. Filtrado de manifiesto puede ser toocreate usa una ventana DVR gradual encima Hola archivo hello, sin eliminar los medios. Hay muchos escenarios donde los emisores desea tooprovide una ventana DVR limitada que se mueve con hello live borde y en hello mismo tiempo mantener una ventana de archivo más grande. Un emisor puede toouse Hola datos fuera de clips de toohighlight de ventana DVR hello, o he\she tooprovide varias ventanas DVR para diferentes dispositivos. Por ejemplo, la mayoría de los dispositivos móviles de hello no encarga de ventanas DVR grandes (puede tener una ventana DVR de 2 minutos para dispositivos móviles y 1 hora para clientes de escritorio).

![Ventana de DVR][dvr_filter]

## <a name="adjusting-livebackoff-live-position"></a>Ajustar LiveBackoff (posición en directo)
Filtrado de manifiesto puede ser usado tooremove varios segundos del borde en vivo de Hola de un programa en vivo. Esto permite que los emisores toowatch presentación de hello en la publicación de la vista previa de hello punto y crear puntos de inserción de anuncios antes de que los visores de Hola reciban flujo hello (normalmente copia-off durante 30 segundos). Los emisores, a continuación, incorporar estos marcos de trabajo de cliente de tootheir de anuncios en el tiempo para ellos tooreceived y proceso Hola información antes de oportunidad de anuncio Hola.

Además admite toohello anuncio, LiveBackoff se puede utilizar para ajustar la posición de la descarga en vivo de cliente para que cuando los clientes desfase y alcanza el límite de hello en directo todavía pueden obtener fragmentos de servidor en lugar de ver los errores HTTP 404 o 412.

![livebackoff_filter][livebackoff_filter]

## <a name="combining-multiple-rules-in-a-single-filter"></a>Combinación de varias reglas en un filtro único
Puede combinar varias reglas de filtrado en un filtro único. Por ejemplo puede definir una pizarra de tooremove de regla de intervalo de archivo en vivo y también filtrar velocidades de bits disponibles. Para varios final de hello reglas filtrado resultado es una composición de hello (solo intersección) de estas reglas.

![varias reglas][multiple-rules]

## <a name="create-filters-programmatically"></a>Crear filtros mediante programación
Hola tema siguiente describe las entidades de servicios multimedia son toofilters relacionados. tema de Hello también muestra cómo tooprogrammatically crear filtros.  

[Crear filtros con las API de REST](media-services-rest-dynamic-manifest.md).

## <a name="combining-multiple-filters-filter-composition"></a>Combinar múltiples filtros (composición de filtros)
También puede combinar varios filtros en una sola dirección URL. 

Hello escenario siguiente muestra que puede interesarle toocombine filtros:

1. Deberá toofilter la calidad de vídeo para dispositivos móviles, como Android o iPAD (en calidad de vídeo de toolimit de orden). tooremove Hola calidades no deseados, debe crear un filtro global que es adecuado para los perfiles de dispositivo. Tal y como se mencionó anteriormente, los filtros globales pueden utilizarse para todos sus activos en hello cuenta sin ninguna otra asociación de servicios multimedia mismo. 
2. También desea tootrim inicio de Hola y hora de un recurso de finalización. tooachieve esto, podría crear un filtro local y establecer la hora de inicio/fin de Hola. 
3. Desea toocombine de estos filtros (sin combinación deberá tooadd calidad filtrado toohello recorte filtro que dificultan el uso de filtros).

filtros de toocombine, necesita tooset Hola filtro nombres toohello manifiesto/lista de reproducción dirección URL con punto y coma delimitada. Supongamos que tiene un filtro denominado *MyMobileDevice* que filtra calidades y tiene otro denominado *MyStartTime* tooset una determinada hora de inicio. Puede combinarlos así:

    http://teststreaming.streaming.mediaservices.windows.net/3d56a4d-b71d-489b-854f-1d67c0596966/64ff1f89-b430-43f8-87dd-56c87b7bd9e2.ism/Manifest(filter=MyMobileDevice;MyStartTime)

Puede combinar los filtros de too3. 

Para más información, vea [este blog](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) .

## <a name="know-issues-and-limitations"></a>Problemas conocidos y limitaciones
* El manifiesto dinámico funciona en los límites GOP (fotogramas clave), por lo que el recorte tiene precisión GOP. 
* Puede usar el mismo nombre de filtro para los filtros globales y locales. Tenga en cuenta que el filtro local tienen una mayor prioridad e invalidará los filtros globales.
* Si actualiza un filtro, puede tardar minutos too2 para reglas de hello toorefresh de extremo de transmisión por secuencias. Si el contenido de Hola se sirvió usando algunos filtros (y almacena en caché en los servidores proxy y CDN memorias caché), actualizar estos filtros puede producir errores en el Reproductor. Es recomendable caché de hello tooclear después de actualizar el filtro de Hola. Si esta opción no es posible, piense en usar un filtro diferente.

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Otras referencias
[Entrega de contenido tooCustomers información general](media-services-deliver-content-overview.md)

[renditions1]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter.png
[renditions2]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter2.png

[rendered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[timeline_trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[timeline_trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png

[multiple-rules]:./media/media-services-dynamic-manifest-overview/media-services-multiple-rules-filters.png

[subclip_filter]: ./media/media-services-dynamic-manifest-overview/media-services-subclips-filter.png
[trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png
[trim_filter]: ./media/media-services-dynamic-manifest-overview/media-services-trim-filter.png
[redered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[livebackoff_filter]: ./media/media-services-dynamic-manifest-overview/media-services-livebackoff-filter.png
[language_filter]: ./media/media-services-dynamic-manifest-overview/media-services-language-filter.png
[dvr_filter]: ./media/media-services-dynamic-manifest-overview/media-services-dvr-filter.png
[skiing]: ./media/media-services-dynamic-manifest-overview/media-services-skiing.png
