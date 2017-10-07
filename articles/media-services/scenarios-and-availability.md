---
title: "aaaMicrosoft servicios multimedia de Azure escenarios y la disponibilidad de características en centros de datos | Documentos de Microsoft"
description: "Este tema ofrece información general de los escenarios y la disponibilidad de las características y servicios de Microsoft Azure Media Services en centros de datos."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 3dbab6998ed5da738baf8f1e2fb096dfba336e19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-and-availability-of-media-services-features-across-datacenters"></a>Escenarios y disponibilidad de características de Media Services en centros de datos

Servicios de multimedia de Microsoft Azure (AMS) le permite toosecurely cargar, almacenar, codificar y empaquetar contenido de audio o vídeo a petición y en vivo streaming entrega toovarious para clientes de (por ejemplo, televisión, PC y dispositivos móviles).

AMS funciona en varios centros de datos alrededor de Hola a todos. Estos centros de datos se agrupan en las regiones de toogeographic, lo que le proporciona flexibilidad al elegir dónde toobuild sus aplicaciones. Puede revisar hello [lista de regiones y sus ubicaciones](https://azure.microsoft.com/regions/). 

En este tema se muestran escenarios comunes para la entrega de contenido [en directo](#live_scenarios) o [a petición](#vod_scenarios). tema de Hello también proporciona detalles acerca de la disponibilidad de características multimedia y servicios en centros de datos.

## <a name="overview"></a>Información general

### <a name="prerequisites"></a>Requisitos previos

toostart con servicios multimedia de Azure, como tener Hola siguiente:

* Una cuenta de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com).
* Una cuenta de Azure Media Services. Para obtener más información, consulte [Creación de una cuenta](media-services-portal-create-account.md).
* Hola origen desde el que desea que el contenido de toostream tiene toobe en hello **ejecutando** estado.

    Cuando se crea la cuenta de AMS, un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, extremo de streaming de hello tiene toobe en hello **ejecutando** estado.

### <a name="commonly-used-objects-when-developing-against-hello-ams-odata-model"></a>Objetos utilizados con frecuencia al desarrollar con hello modelo AMS OData

Hello siguiente imagen muestra algunos de los objetos de hello suelen usada al desarrollar con modelo de OData de servicios multimedia de Hola.

Haga clic en tooview de imagen de hello tamaño completo.  

<a href="./media/media-services-overview/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-overview/media-services-overview-object-model-small.png"></a> 

Puede ver todo el modelo de hello [aquí](https://media.windows.net/API/$metadata?api-version=2.15).  

## <a name="protect-content-in-storage-and-deliver-streaming-media-in-hello-clear-non-encrypted"></a>Proteger el contenido en el almacenamiento y entregar contenido multimedia de transmisión por secuencias en hello Borrar (sin cifrar)

![Flujo de trabajo de VoD](./media/scenarios-and-availability/scenarios-and-availability01.png)

1. Cargue un archivo multimedia de alta calidad en un recurso.

    Se recomienda activo tooyour opción de cifrado de almacenamiento de tooapply en orden tooprotect su contenido durante la carga y mientras almacenados en almacenamiento.
2. Codificar tooa conjunto de archivos MP4 de velocidad de bits adaptativa.

    Se recomienda toohello de opción de cifrado de almacenamiento de tooapply de salida de los activos de orden tooprotect su contenido en reposo.
3. Configure la directiva de entrega de recursos(usada por paquetes dinámicos).

    Si el recurso tiene el almacenamiento cifrado, **asegúrese** de configurar la directiva de entrega de recursos.
4. Publicar el recurso de hello mediante la creación de un localizador OnDemand.
5. Trasmita el contenido publicado.

Para obtener información acerca de la disponibilidad en centros de datos, vea hello [disponibilidad](#availability) sección.

## <a name="protect-content-in-storage-deliver-dynamically-encrypted-streaming-media"></a>Protección del contenido en el almacenamiento, entrega de soportes de streaming cifrados dinámicamente

![Protección con PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

1. Cargue un archivo multimedia de alta calidad en un recurso. Aplicar el recurso de toohello de opción de cifrado de almacenamiento.
2. Codificar tooa conjunto de archivos MP4 de velocidad de bits adaptativa. Aplicar el recurso de salida de toohello de opción de cifrado de almacenamiento.
3. Crear clave de cifrado de contenido de los activos de hello que desea toobe cifra dinámicamente durante la reproducción.
4. Configure la directiva de autorización de claves de contenido.
5. Configure la directiva de entrega de recursos (usada por el empaquetado y el cifrado dinámicos).
6. Publicar el recurso de hello mediante la creación de un localizador OnDemand.
7. Trasmita el contenido publicado.

Para obtener información acerca de la disponibilidad en centros de datos, vea hello [disponibilidad](#availability) sección.

## <a name="use-media-analytics-tooderive-actionable-insights-from-your-videos"></a>Use la información procesable de análisis multimedia tooderive de vídeos

Análisis multimedia es una colección de componentes de voz y la visión que resulte más fácil para las organizaciones y empresas información procesable tooderive de sus archivos de vídeo. Para más información, consulte [Información general de análisis de Azure Media Services](media-services-analytics-overview.md).

1. Cargue un archivo multimedia de alta calidad en un recurso.
2. Procesar sus vídeos con uno de los servicios de análisis de medios de hello descritos en hello [información general de análisis de medios](media-services-analytics-overview.md) sección.
3. Los procesadores multimedia de Análisis multimedia generan archivos MP4 o JSON. Si un procesador multimedia genera un archivo MP4, puede descargar progresivamente archivo hello. Si un procesador multimedia genera un archivo JSON, puede descargar el archivo hello de hello almacenamiento de blobs de Azure.

Para obtener información acerca de la disponibilidad en centros de datos, vea hello [disponibilidad](#availability) sección.

## <a name="deliver-progressive-download"></a>Entregar la descarga progresiva

1. Cargue un archivo multimedia de alta calidad en un recurso.
2. Codificar tooa solo el archivo MP4.
3. Publicar el recurso de hello mediante la creación de un localizador OnDemand o SAS.

    Si usa el localizador SAS, se descarga contenido de Hola desde Hola almacenamiento de blobs de Azure. En este caso, no es necesario toohave streaming extremos en estado iniciado.
4. Descargue contenido de forma progresiva.

## <a id="live_scenarios"></a>Entrega de eventos de streaming en vivo 

1. Ingiera contenido en vivo mediante el uso de varios protocolos de streaming en vivo (por ejemplo, RTMP o Smooth Streaming).
2. (Opcionalmente) Codifique la transmisión en un flujo de datos con velocidad de bits adaptable.
3. Obtenga una vista previa del flujo de datos en vivo.
4. Entregar contenido de Hola a través de protocolos de transmisión por secuencias comunes (por ejemplo, MPEG DASH, Smooth, HLS) directamente los clientes de tooyour o tooa red de entrega de contenido (CDN) para su distribución posterior.

    O bien

    Registro y almacén de contenido de hello ingerida en orden toobe transmite más adelante (vídeo bajo demanda).

Cuando se realiza la transmisión por secuencias en directo, puede elegir uno de los siguientes Hola enruta:

### <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>Uso de canales que reciben transmisión por secuencias en directo con velocidad de bits múltiple de codificadores locales (paso a través)

Hello siguiente diagrama muestra hello las partes principales de la plataforma de hello AMS que intervienen en hello **acceso directo** flujo de trabajo.

![Flujo de trabajo activo](./media/scenarios-and-availability/media-services-live-streaming-current.png)

Para más información, consulte [Uso de canales que reciben streaming en vivo con velocidad de bits múltiple de codificadores locales](media-services-live-streaming-with-onprem-encoders.md).

### <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>Trabajar con los canales que son habilitado tooperform live codificar con servicios multimedia de Azure

Hello siguiente diagrama muestra hello principal partes de plataforma de AMS Hola que intervienen en el flujo de trabajo de Streaming en directo donde un canal está habilitado tooperform live codificar con servicios multimedia.

![Flujo de trabajo activo](./media/scenarios-and-availability/media-services-live-streaming-new.png)

Para obtener más información, consulte [trabajar con los canales que es habilitado tooPerform Live codificar con servicios multimedia de Azure](media-services-manage-live-encoder-enabled-channels.md).

Para obtener información acerca de la disponibilidad en centros de datos, vea hello [disponibilidad](#availability) sección.

## <a name="consuming-content"></a>Consumo de contenido

Servicios multimedia de Azure proporciona hello las herramientas necesita toocreate enriquecido, aplicaciones de reproducción de cliente dinámico para la mayoría de las plataformas incluidas: dispositivos con iOS, dispositivos Android, Windows, Windows Phone, Xbox y Set-top cuadros. Hola tema siguiente proporciona vínculos tooSDKs y marcos de Reproductor puede usar toodevelop en sus propias aplicaciones de cliente que puedan consumir contenido multimedia de transmisión por secuencias de servicios multimedia. Para más información, consulte [Desarrollo de aplicaciones para reproductor de vídeo](media-services-develop-video-players.md)

## <a name="enabling-azure-cdn"></a>Habilitación de CDN de Azure

Media Services admite la integración con Azure CDN. Para obtener información acerca de cómo tooenable CDN de Azure, consulte [cómo tooManage los extremos de Streaming en una cuenta de servicios multimedia](media-services-portal-manage-streaming-endpoints.md).

## <a id="scaling"></a>Escalado de una cuenta de Media Services

Los clientes de AMS pueden escalar los puntos de conexión de streaming, el procesamiento multimedia y el almacenamiento en sus cuentas de AMS.

* Los clientes de Media Services pueden elegir un punto de conexión de streaming **estándar** o uno **premium**. Un punto de conexión de streaming **estándar** es adecuado para la mayoría de las cargas de trabajo de streaming. Incluye Hola mismas características como un **Premium** streaming automáticamente los puntos de conexión y las escalas ancho de banda saliente. 

    Los puntos de conexión de streaming **Premium** son adecuados para cargas de trabajo avanzadas y proporcionan una capacidad de ancho de banda dedicada y escalable. Los clientes que tienen un punto de conexión de streaming **Premium**, de forma predeterminada, obtienen una unidad de streaming (SU). Hola extremo de streaming puede ampliarse mediante la adición de SUs. Cada SU proporciona aplicaciones de toohello de capacidad de ancho de banda adicional. Para obtener más información acerca de cómo escalar **Premium** los extremos de streaming, vea hello [ajuste de escala en los extremos de streaming](media-services-portal-scale-streaming-endpoints.md) tema.

* Una cuenta de servicios multimedia está asociada a un tipo de unidad reservada, que determina la velocidad de hello con la que se procesan los medios de las tareas de procesamiento. Puede elegir entre como consecuencia de hello reservado los tipos de unidad: **S1**, **S2**, o **S3**. Por ejemplo, hello mismo trabajo de codificación se ejecuta con mayor rapidez cuando se usa hello **S2** tipo de unidad reservada comparar toohello **S1** tipo.

    Además toospecifying Hola reservado del tipo de unidad, puede especificar su cuenta con tooprovision **unidades reservadas** (RUs). número de Hola de RUs aprovisionados determina número Hola de tareas multimedia que se pueden procesar simultáneamente en una cuenta determinada.

    >[!NOTE]
    >Las unidades reservadas sirven para establecer paralelismos en todo el procesamiento multimedia, incluida la indexación de trabajos mediante Azure Media Indexer. Sin embargo, a diferencia de la codificación, la indexación de los trabajos no se procesará más rápido con unidades reservadas de mayor rapidez.

    Para más información, consulte [Escalado del procesamiento de elementos multimedia mediante Azure Portal](media-services-portal-scale-media-processing.md).
* También puede escalar su cuenta de servicios multimedia mediante la adición de tooit de cuentas de almacenamiento. Cada cuenta de almacenamiento es limitado too500 TB. tooexpand su almacenamiento más allá de limitaciones de hello predeterminadas, puede elegir tooattach varias cuentas tooa único servicios multimedia cuentas de almacenamiento. Para más información, consulte [Administración de recursos de Servicios multimedia entre varias cuentas de almacenamiento](meda-services-managing-multiple-storage-accounts.md).

##<a id="availability"></a>Disponibilidad de características de Media Services en centros de datos

En esta sección se proporcionan detalles acerca de la disponibilidad de las características de Media Services en centros de datos.

### <a name="ams-accounts"></a>Cuentas de AMS

#### <a name="availability"></a>Disponibilidad

Puede crear cuentas de servicios multimedia en hello siguientes regiones: Europa del Norte, Europa occidental, oeste de Estados Unidos, este de EE., sudeste de Asia, este de Asia, oeste de Japón, este de Japón, sur de Brasil, India occidental, sur de India y India Central. 

### <a name="streaming-endpoints"></a>Puntos de conexión de streaming 

Los clientes de Media Services pueden elegir un punto de conexión de streaming **estándar** o uno **premium**. Para obtener más información, vea hello [escalado](#scaling) sección.

#### <a name="availability"></a>Disponibilidad

|Nombre|Estado|Centros de datos
|---|---|---|
|Estándar|GA|Todo|
|Premium|GA|Todo|

### <a name="live-encoding"></a>Live Encoding

#### <a name="availability"></a>Disponibilidad

Disponible en todos los centros de datos excepto: Alemania, Sur de Brasil, India occidental, Sur de India e India central. 

### <a name="encoding-media-processors"></a>Codificación de procesadores de multimedia

AMS ofrece dos codificadores a petición **Media Encoder Standard** y **Flujo de trabajo premium de codificación de medios**. Para más información, consulte [Información general y comparación de los codificadores multimedia a petición de Azure](media-services-encode-asset.md). 

#### <a name="availability"></a>Disponibilidad

|Nombre de procesador de multimedia|Estado|Centros de datos
|---|---|---|
|Media Encoder Estándar|GA|Todo|
|Flujo de trabajo del Codificador multimedia|GA|Todos excepto China|

### <a name="analytics-media-processors"></a>Procesadores de multimedia de Analytics

Análisis multimedia es una colección de componentes de voz y visión que resulta más fácil para las organizaciones y empresas información procesable tooderive de sus archivos de vídeo. Para más información, consulte [Información general de análisis de Azure Media Services](media-services-analytics-overview.md).

#### <a name="availability"></a>Disponibilidad

|Nombre de procesador de multimedia|Estado|Centros de datos
|---|---|---|
|Azure Media Face Detector|Vista previa|Todo|
|Azure Media Hyperlapse|Vista previa|Todo|
|Azure Media Indexer|GA|Todo|
|Azure Media Motion Detector|Vista previa|Todo|
|Azure Media OCR|Vista previa|Todo|
|Azure Media Redactor|Vista previa|Todo|
|Estabilizador de Azure Media|Vista previa|Todo|
|Azure Media Video Thumbnails|Vista previa|Todo|
|Azure Media Indexer 2|Vista previa|Todos excepto China y la región Gobierno Federal|

### <a name="protection"></a>Protección

Servicios de multimedia de Microsoft Azure permite toosecure su media de tiempo de hello sale del equipo a través de almacenamiento, procesamiento y entrega. Para más información, consulte [Protección de contenido de AMS](media-services-content-protection-overview.md).

#### <a name="availability"></a>Disponibilidad

|Cifrado|Estado|Centros de datos|
|---|---|---| 
|Almacenamiento|GA|Todo|
|Claves AES-128|GA|Todo|
|Fairplay|GA|Todo|
|PlayReady|GA|Todo|
|Widevine|GA|Todos, excepto Alemania, el Gobierno Federal y China.

### <a name="reserved-units-rus"></a>Unidades reservadas (RU)

número de Hola de unidades reservadas aprovisionadas determina número Hola de tareas multimedia que se pueden procesar simultáneamente en una cuenta determinada. 

Para obtener más información, vea hello [escalado](#scaling) sección.

#### <a name="availability"></a>Disponibilidad

Está disponible en todos los centros de datos.

### <a name="reserved-unit-ru-type"></a>Tipo de unidad reservada (RU)

Una cuenta de servicios multimedia está asociada a un tipo de unidad reservada, que determina la velocidad de hello con la que se procesan los medios de las tareas de procesamiento. Puede elegir entre como consecuencia de hello reservado los tipos de unidades: S1, S2 o S3.

Para obtener más información, vea hello [escalado](#scaling) sección.

#### <a name="availability"></a>Disponibilidad

|Nombre de tipo de RU|Estado|Centros de datos
|---|---|---|
|S1|GA|Todo|
|S2|GA|Todos, excepto Sur de Brasil e India occidental|
|S3|GA|Todos, excepto India occidental|

## <a name="next-steps"></a>Pasos siguientes

Consulte las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

