---
title: aaaDelivering contenido toocustomers | Documentos de Microsoft
description: "Este tema proporciona información general de lo que implica la entrega de contenido con Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 89ede54a-6a9c-4814-9858-dcfbb5f4fed5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 0570bd62d9d42633df0132f9449b357e2abb4086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deliver-content-toocustomers"></a>Entregar contenido toocustomers
Cuando se le entrega su toocustomers contenido de transmisión por secuencias o vídeo bajo demanda, el objetivo es toodeliver toovarious de vídeo de alta calidad dispositivos en condiciones de red diferente.

tooachieve este objetivo, puede:

* Codificar la secuencia de vídeo de secuencia tooa multibits (velocidad de bits adaptable). (esto se encargará de las condiciones de calidad y red).
* Usar servicios de multimedia de Microsoft Azure [empaquetado dinámico](media-services-dynamic-packaging-overview.md) toodynamically volver a empaquetar la secuencia en distintos protocolos. (esto se encargará del streaming en dispositivos diferentes). Servicios multimedia admite la entrega de hello siguiendo las tecnologías de streaming de velocidad de bits adaptativa: HTTP Live Streaming (HLS), Smooth Streaming y MPEG-DASH.

>[!NOTE]
>Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado. 

En este artículo se ofrece información general sobre importantes conceptos de entrega de contenido.

toocheck errores conocidos, consulte [problemas conocidos](media-services-deliver-content-overview.md#known-issues).

## <a name="dynamic-packaging"></a>Empaquetado dinámico
Con el empaquetado dinámico de Hola que los servicios multimedia ofrecen, que puede entregar el contenido de velocidad de bits adaptativa MP4 o Smooth Streaming codificados en formatos compatibles con los servicios multimedia (MPEG-DASH, HLS, Smooth Streaming) de transmisión sin necesidad de toore-package en estos formatos de streaming. Recomendamos entregar el contenido con empaquetado dinámico.

tootake ventaja del empaquetado dinámico, debe tooencode el archivo mezzanine (origen) en un conjunto de archivos MP4 de velocidad de bits adaptativa o archivos de Smooth Streaming de velocidad de bits adaptativa.

Con el empaquetado dinámico, almacenar y pagar los archivos de hello en formato de almacenamiento único. Servicios multimedia creará y proporcionará la respuesta adecuada Hola según las solicitudes.

Empaquetado dinámico está disponible para puntos de conexión de streaming estándar y premium. 

Para obtener más información, consulte [Empaquetado dinámico](media-services-dynamic-packaging-overview.md).

## <a name="filters-and-dynamic-manifests"></a>Filtros y manifiestos dinámicos
Servicios multimedia permite definir filtros para los recursos. Estos filtros son reglas de servidor que ayudan a los clientes hacer cosas como reproducir una sección concreta de un vídeo o especificar un subconjunto de copias de audio y vídeo que pueden controlar los dispositivos de su cliente (en lugar de todas las copias de Hola que están asociadas a Hola activo ). Este filtrado se logra a través de *manifiestos dinámicos* que se crean cuando el cliente solicita toostream un vídeo basado en uno o más filtros especificados.

Para obtener más información, consulte [Filtros y manifiestos dinámicos](media-services-dynamic-manifest-overview.md).

## <a name="locators"></a>Localizadores
tooprovide el usuario con una dirección URL que se puede toostream usado o descargar el contenido, primero debe toopublish su activo mediante la creación de un localizador. Un localizador proporciona un hello tooaccess de punto de entrada de archivos contenidos en un recurso. Media Services admite dos tipos de localizadores:

* Localizadores OnDemandOrigin. Estos son toostream usa medios (por ejemplo, MPEG-DASH, HLS o Smooth Streaming) o descarga progresiva de archivos.
* Localizadores de direcciones URL de firma de acceso compartido (SAS). Se trata de un equipo local del tooyour de archivos multimedia toodownload usado.

Un *directiva de acceso* es toodefine usa permisos de hello (como lectura, escritura y lista) y la duración para que un cliente tiene acceso para un recurso determinado. Tenga en cuenta que permiso de lista de hello (AccessPermissions.List) no debe utilizarse para crear un localizador OrDemandOrigin.

Los localizadores tienen fecha de expiración. Hola portal de Azure establece que una fecha de expiración en 100 años de hello futura para localizadores.

> [!NOTE]
> Si utiliza los localizadores de hello Azure toocreate portal antes de marzo de 2015, los localizadores se establecieron tooexpire transcurridos dos años.
> 
> 

tooupdate una fecha de caducidad en un localizador, utilice [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) o [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API. Tenga en cuenta que cuando se actualiza la fecha de expiración de Hola de un localizador SAS, dirección URL de hello cambia.

Los localizadores no están diseñados toomanage el control de acceso de cada usuario. Puede dar acceso a diferentes usuarios con derechos tooindividual mediante soluciones de administración de derechos digitales (DRM). Para obtener más información, consulte [Protección de archivos multimedia](http://msdn.microsoft.com/library/azure/dn282272.aspx).

Cuando se crea un localizador, puede haber un retraso de 30 segundos debido a los procesos de almacenamiento y la propagación de toorequired en el almacenamiento de Azure.

## <a name="adaptive-streaming"></a>Streaming adaptativo
Tecnologías de velocidad de bits adaptativa permiten que las aplicaciones de Reproductor de vídeo toodetermine condiciones de red y seleccione en varias velocidades de bits. Cuando se degrada la comunicación de red, cliente hello puede seleccionar velocidades de bits bajas para que reproducción puede continuar con la calidad de vídeo inferior. Mejorar las condiciones de red, el cliente de hello puede cambiar tooa velocidades de bits altas con calidad de vídeo. Servicios multimedia de Azure admite Hola siguiendo las tecnologías de velocidad de bits adaptativa: HTTP Live Streaming (HLS), Smooth Streaming y MPEG-DASH.

tooprovide usuarios con direcciones URL de streaming, primero debe crear un localizador OnDemandOrigin. Creación de hello proporciona localizador Hola activo de toohello de ruta de acceso base que contiene el contenido de Hola desea toostream. Sin embargo, toobe toostream capaz de este contenido, debe toomodify esta ruta de acceso. tooconstruct una dirección URL completa se toohello transmisión por secuencias de archivo de manifiesto, debe concatenar la ruta de acceso del localizador de hello hello y valor de manifiesto (filename.ism) nombre de archivo. A continuación, anexe **/Manifest** y una ruta de acceso del localizador de toohello de formato apropiado (si es necesario).

> [!NOTE]
> También puede transmitir el contenido por una conexión SSL. toodo esto, asegúrese de que la transmisión por secuencias de inicio de las direcciones URL con HTTPS. Tenga en cuenta que, actualmente, AMS no admite SSL con dominios personalizados.  
> 


Solo puede transmitir a través de SSL si Hola origen desde el que entrega el contenido se creó después de 10 de septiembre de 2014. Si sus direcciones URL de streaming se basan en hello streaming creados después del 10 de septiembre de 2014, dirección URL de hello contiene "streaming.mediaservices.windows.net". Direcciones URL de streaming que contienen "origin.mediaservices.windows.net" (formato antiguo de hello) no son compatibles con SSL. Si la dirección URL está en formato antiguo de Hola y desea toobe pueda toostream a través de SSL, cree un nuevo extremo de transmisión por secuencias. Utilice direcciones URL basadas en hello nuevos streaming extremo toostream su contenido a través de SSL.

## <a name="streaming-url-formats"></a>Formatos de la dirección URL de streaming
### <a name="mpeg-dash-format"></a>Formato MPEG-DASH
{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest(formato=mpd-time-csf)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)

### <a name="apple-http-live-streaming-hls-v4-format"></a>Formato Apple HTTP Live Streaming (HLS) V4
{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest(formato=m3u8-aapl)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)

### <a name="apple-http-live-streaming-hls-v3-format"></a>Formato Apple HTTP Live Streaming (HLS) V3
{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest(formato=m3u8-aapl-v3)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)

### <a name="apple-http-live-streaming-hls-format-with-audio-only-filter"></a>Formato Apple HTTP Live Streaming (HLS) con filtro solo de audio
De forma predeterminada, las pistas de audio solo se incluyen en hello que HLS del manifiesto. Esto es necesario para la certificación de la Apple Store para redes celulares. En este caso, si un cliente no tiene suficiente ancho de banda o se conecta a través de una conexión de 2G, reproducción cambia solo tooaudio. Esto ayuda a contenido tookeep sin almacenamiento en búfer de transmisión por secuencias, pero no hay ningún vídeo. En algunos escenarios, es posible que se prefiera el almacenamiento en búfer del reproductor a solo audio. Si desea que el seguimiento de solo audio hello tooremove, agregar **sólo audio = false** toohello URL.

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3,audio-only=false)

Para más información, consulte [Dynamic Manifest Composition support and HLS output additional features](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/)(Compatibilidad con Dynamic Manifest Composition y características adicionales de salida HLS).

### <a name="smooth-streaming-format"></a>Formato Smooth Streaming
{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{filename}.ism/Manifest

Ejemplo:

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest

### <a id="fmp4_v20"></a>Manifiesto Smooth Streaming 2.0 (manifiesto heredado)
De forma predeterminada, formato de manifiesto de Smooth Streaming contiene la etiqueta de repetición de hello (r-tag). Sin embargo, algunos reproductores no admiten Hola r-tag. Los clientes con estos jugadores pueden usar un formato que deshabilita Hola r-tag:

{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest(formato=fmp4-v20)

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=fmp4-v20)

## <a name="progressive-download"></a>Descarga progresiva
La descarga progresiva, podrá iniciar reproducir contenido multimedia antes de que se ha descargado todo el archivo hello. No se puede descargar progresivamente archivos .ism * (ismv, isma, ismt e ismc).

tooprogressively descargar el contenido, use hello OnDemandOrigin tipo de localizador. Hello en el ejemplo siguiente se muestra hello URL que se basa en hello OnDemandOrigin tipo de localizador:

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

Debe descifrar los activos de cifrados de almacenamiento que desea toostream de servicio de origen de hello para la descarga progresiva.

## <a name="download"></a>Descargar
toodownload el dispositivo de cliente tooa contenido, debe crear un localizador SAS. Hola localizador SAS le permite acceso al contenedor de almacenamiento de Azure toohello donde se encuentra el archivo. dirección URL de descarga de toobuild hello, tiene nombre de archivo de hello tooembed entre el host de Hola y la firma SAS.

Hello en el ejemplo siguiente se muestra hello URL que se basa en el localizador SAS de hello:

    https://test001.blob.core.windows.net/asset-ca7a4c3f-9eb5-4fd8-a898-459cb17761bd/BigBuckBunny.mp4?sv=2012-02-12&se=2014-05-03T01%3A23%3A50Z&sr=c&si=7c093e7c-7dab-45b4-beb4-2bfdff764bb5&sig=msEHP90c6JHXEOtTyIWqD7xio91GtVg0UIzjdpFscHk%3D

Hola siguientes consideraciones se aplica:

* Debe descifrar los activos de cifrados de almacenamiento que desea toostream de servicio de origen de hello para la descarga progresiva.
* Se producirá un error en una descarga que no se haya completado en 12 horas.

## <a name="streaming-endpoints"></a>Puntos de conexión de streaming

Un extremo de streaming representa un servicio de streaming que puede entregar contenido directamente tooa cliente Reproductor aplicación o tooa contenido red de entrega (CDN) para obtener más distribución. flujo de salida de Hello de un servicio de transmisión de punto de conexión puede ser una secuencia en directo o un recurso de vídeo bajo demanda en la cuenta de servicios multimedia. Existen dos tipos de puntos de conexión de streaming: **estándar** y **premium**. Para obtener más información, consulte [Streaming endpoints overview](media-services-streaming-endpoints-overview.md) (Información general de puntos de conexión de streaming).

>[!NOTE]
>Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado. 

## <a name="known-issues"></a>Problemas conocidos
### <a name="changes-toosmooth-streaming-manifest-version"></a>Versión del manifiesto de transmisión por secuencias cambios tooSmooth
Se cumple antes de que devuelva Hola versión de servicio de julio de 2016--cuando manifiestos generados por Media Encoder estándar, flujo de trabajo de Premium de codificación de medios u Hola Codificador multimedia de Azure anteriores se transmiten mediante el uso de paquetes dinámicos: Hola Smooth Streaming de activos tooversion 2.0. En la versión 2.0, duraciones de fragmento de hello no utilizan etiquetas de hello denominadas repetir ("r"). Por ejemplo:

<?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" n="0" />
            <c d="2000" />
            <c d="2000" />
            <c d="2000" />
        </StreamIndex>
    </SmoothStreamingMedia>

Hola versión del servicio de julio de 2016, el manifiesto de Smooth Streaming Hola generado cumple tooversion 2.2, con duraciones de fragmento mediante etiquetas de repetición. Por ejemplo:

    <?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="2" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" r="4" />
        </StreamIndex>
    </SmoothStreamingMedia>

Algunos de los clientes heredados de transmisión por secuencias suave de hello pueden no admitir etiquetas de repetición de Hola y se producirá un error de manifiesto de hello tooload. toomitigate este problema, puede usar el parámetro de formato de manifiesto heredado de hello **(formato = v20 fmp4 dinámico)** o actualizar la versión más reciente toohello del cliente, que admite la repetición de etiquetas. Para más información, consulte [Smooth Streaming 2.0](media-services-deliver-content-overview.md#fmp4_v20).

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Temas relacionados
[Actualización de los localizadores de Servicios multimedia después de revertir las claves de almacenamiento](media-services-roll-storage-access-keys.md)

