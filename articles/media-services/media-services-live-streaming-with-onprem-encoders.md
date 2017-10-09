---
title: aaaStream live con codificadores locales que crean secuencias de velocidades de bits - Azure | Documentos de Microsoft
description: "Este tema describe cómo tooset un canal que recibe una velocidad de bits múltiple live secuencia desde un codificador en local. Hello secuencia, a continuación, se puede entregar aplicaciones de reproducción de tooclient a través de uno o más extremos de streaming, mediante uno de los siguientes protocolos de transmisión por secuencias adaptativas de hello: HLS, Smooth Streaming, DASH."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: d9f0912d-39ec-4c9c-817b-e5d9fcf1f7ea
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 04/12/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 00709cecfc3b5b5dcfaa8f1e4b25bcf9d470d50b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-with-on-premises-encoders-that-create-multi-bitrate-streams"></a>Streaming en vivo con codificadores locales que crean transmisiones de velocidad de bits múltiple
## <a name="overview"></a>Información general
En Azure Media Services, un *canal* representa una canalización para procesar contenido de streaming en vivo. Los canales reciben la transmisión de entrada en vivo de dos maneras posibles:

* Un codificador en directo local envía un RTMP de velocidad de multibits o Smooth Streaming (MP4 fragmentado) toohello canal de la secuencia que no está habilitado tooperform codificación con servicios multimedia en directo. Hola ingestión pase de secuencias a través de canales sin más procesamiento. Este método se llama *paso a través*. Puede usar los siguientes codificadores en directo que tienen varias velocidades de bits Smooth Streaming como salida de hello: Excel de medios, Ateme, Imagine las comunicaciones, Envivio, Cisco y Elemental. Hola siguientes codificadores en directo tiene RTMP como salida: Adobe Flash Live el Codificador multimedia, Telestream Wirecast, Haivision, Teradek y TriCaster. Un codificador en directo también puede enviar un canal de tooa de secuencia de velocidad de bits única que no está habilitado para la codificación en directo, pero no se recomienda que. Servicios multimedia transmite hello secuencia toocustomers que lo solicitan.

  > [!NOTE]
  > Con un método paso a través de forma hello más económica toodo streaming en directo.


* Un codificador en directo local envía un canal de toohello de secuencia de velocidad de bits única que es habilitado tooperform live codificar con servicios multimedia en uno de hello siguientes formatos: RTP (MPEG-TS), RTMP o Smooth Streaming (MP4 fragmentado). canal de Hello, a continuación, realiza la codificación en directo de Hola entrantes velocidad de bits única secuencia tooa velocidades de bits (adaptable) secuencia de vídeo. Servicios multimedia transmite hello secuencia toocustomers que lo solicitan.

A partir de la versión 2.10 de servicios multimedia de hello, cuando se crea un canal, puede especificar cómo desea que el flujo de entrada de canal tooreceive Hola. También puede especificar si desea hello tooperform de canal en vivo de codificación de la secuencia. Tiene dos opciones:

* **Pass Through**: especifique este valor si piensa toouse un codificador en directo local que tenga una secuencia de bits múltiple (una secuencia de acceso directo) como salida. En este caso, la secuencia entrante de Hola pasa a través de toohello de salida sin ninguna codificación. Este es el comportamiento de Hola de un canal antes del lanzamiento de hello 2.10. En este tema se proporciona información sobre cómo trabajar con canales de este tipo.
* **Live Encoding**: elija este valor si piensa toouse servicios multimedia tooencode la secuencia de velocidades de bits de tooa de secuencia en directo de velocidad de bits única. Tenga en cuenta que dejar una codificación en vivo del canal en estado **En ejecución** supone cargos de facturación. Se recomienda detener los canales de ejecución inmediatamente después de los eventos de transmisión por secuencias en directo es tooavoid completa cargos adicionales por hora. Servicios multimedia transmite hello secuencia toocustomers que lo solicitan.

> [!NOTE]
> Este tema describen los atributos de canales que no están habilitados tooperform de codificación en directo. Para obtener información sobre cómo trabajar con los canales que son habilitado tooperform de codificación en directo, vea [streaming en vivo al utilizar secuencias de velocidades de bits de servicios multimedia de Azure toocreate](media-services-manage-live-encoder-enabled-channels.md).
>
>

Hola siguiente diagrama representa un flujo de trabajo transmisión por secuencias en directo que utiliza una secuencias de local codificador en directo toohave velocidades de bits RTMP o MP4 fragmentado (Smooth Streaming) como salida.

![Flujo de trabajo activo][live-overview]

## <a id="scenario"></a>Escenario típico de streaming en vivo
Hello pasos siguientes describen las tareas implicadas en la creación de aplicaciones de transmisión por secuencias en directo común.

1. Conectar un equipo de tooa de cámara de vídeo. Inicie y configure un codificador en vivo local que genera una transmisión de RTMP o MP4 fragmentado de velocidad de bits múltiple (Smooth Streaming) de salida. Para obtener más información, consulte [Compatibilidad con RTMP de Servicios multimedia de Azure y codificadores en directo](http://go.microsoft.com/fwlink/?LinkId=532824).

    También puede realizar este paso después de crear el canal.
2. Cree e inicie un canal.

3. Dirección URL de introducción del canal de Hola de recuperar.

    Hola Hola de usos de codificador en directo introducir canal toohello de la secuencia de hello toosend de dirección URL.
4. Recuperar la dirección URL de vista previa de canal de Hola.

    Utilice este tooverify de dirección URL que el canal está recibiendo correctamente la secuencia en directo de Hola.
5. Cree un programa.

    Cuando usas Hola portal de Azure, crear un programa crea también un activo.

    Cuando usas Hola SDK de .NET o REST, es necesario toocreate un activo y especifique toouse este recurso al crear un programa.
6. Publicar el recurso de Hola que esté asociada con el programa Hola.   

    >[!NOTE]
    >Cuando se crea la cuenta de servicios multimedia de Azure, un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. Hola origen desde el que desea que el contenido de toostream tiene toobe en hello **ejecutando** estado.

7. Inicie el programa de hello cuando estés listo toostart streaming y archivado.

8. Si lo desea, codificador en directo de hello puede ser señalado toostart un anuncio. anuncio de Hola se inserta en el flujo de salida de hello.

9. Detener el programa de hello siempre que lo desee toostop transmisión por secuencias y archivar eventos Hola.

10. Eliminar el programa Hola (y opcionalmente eliminar recurso de hello).     

## <a id="channel"></a>Descripción de un canal y sus componentes relacionados
### <a id="channel_input"></a>Configuraciones de entrada de canal (introducción)
#### <a id="ingest_protocols"></a>Protocolo de streaming de ingesta
Media Services admite la ingesta de fuentes en vivo mediante MP4 fragmentado y RTMP de velocidad de bits múltiple como protocolos de streaming. Al introducir Hola RTMP protocolo de transmisión está seleccionada, dos puntos de conexión (entradas) de introducción se crean para el canal de hello:

* **Dirección URL principal**: especifica Hola extremo de introducción de la dirección URL completa del RTMP principal del canal de Hola.
* **Dirección URL secundaria** (opcional): especifica Hola extremo de introducción de la dirección URL completa del RTMP secundario del canal de Hola.

Utilice URL secundaria Hola si desea tooimprove Hola durabilidad y tolerancia a errores de la ingesta flujo (así como codificador conmutación por error y tolerancia a errores), especialmente para hello los escenarios siguientes:

- Direcciones URL principal y secundaria tooboth e inserta el doble de codificador único:

    Hola propósito principal de este escenario es tooprovide más las fluctuaciones de toonetwork de resistencia y compiladores JIT. Algunos codificadores RTMP no controlan bien las desconexiones de red. Cuando se produce una desconexión de red, un codificador puede detener la codificación y, a continuación, no enviar datos de hello almacenado en búfer cuando se produce una reconexión. Esto provoca discontinuidades y pérdida de datos. Desconexión de la red puede suceder debido a una red incorrecta o el mantenimiento en hello parte de Azure. Direcciones URL principal/secundario reducen los problemas de red de Hola y proporcionan un proceso de actualización controlado. Cada vez que se produce una desconexión programada de redes, servicios multimedia administra Hola principal y secundaria se desconecta y proporciona un diferida desconectar entre Hola dos. Codificadores, a continuación, tienen tookeep tiempo envío de datos y volver a conectarse de nuevo. desconecta el orden de Hola de hello puede ser aleatorio, pero siempre habrá un retraso entre las direcciones URL principal y secundario o principal secundario. En este escenario, el codificador de hello sigue siendo punto de error único Hola.

- Varios codificadores, con cada codificador insertar tooa dedicado punto:

    Este escenario proporciona redundancia tanto para el codificador como para la entrada. En este escenario, encoder1 inserta la dirección URL principal de toohello y encoder2 inserta URL secundaria toohello. Cuando se produce un error en un codificador, hello otro codificador puede mantener enviar datos. Se puede mantener la redundancia de datos porque los servicios multimedia no desconecta direcciones URL primarios y secundarias en hello mismo tiempo. Este escenario se supone que los codificadores son de tiempo que se sincronizan y proporcionan exactamente Hola los mismos datos.  

- Varios codificadores tooboth direcciones URL principal y secundaria de inserción de doble:

    En este escenario, los codificadores inserción datos tooboth principal y secundaria las direcciones URL. Esto proporciona confiabilidad mejor hello y tolerancia a errores, así como redundancia de datos. Este escenario puede tolerar errores y desconexiones en ambos codificadores, aunque un codificador deje de funcionar. Se supone que los codificadores son de tiempo que se sincronizan y proporcionan exactamente Hola los mismos datos.  

Para obtener información sobre los codificadores en directo de RTMP, consulte [Compatibilidad con RTMP de Servicios multimedia de Azure y codificadores en directo](http://go.microsoft.com/fwlink/?LinkId=532824).

#### <a name="ingest-urls-endpoints"></a>Direcciones URL de ingesta (extremos)
Un canal proporciona un extremo de entrada (URL de introducción) que especifique en el codificador en directo de hello, por lo que puede insertar codificador hello tooyour canales se transmita por secuencias.   

Puede obtener Hola direcciones URL de entrada cuando se crea el canal de Hola. Para tooget estas direcciones URL, canal de hello no tiene toobe en hello **ejecutando** estado. Cuando esté listo toostart insertar canal toohello de datos, canal de hello debe encontrarse en hello **ejecutando** estado. Después de canal de hello inicia la introducción de datos, puede obtener una vista previa de la secuencia a través de la dirección URL de vista previa de Hola.

Tiene la opción de ingerir una transmisión en vivo de MP4 fragmentado (Smooth Streaming) a través de una conexión SSL. tooingest a través de SSL, que seguro Hola de tooupdate tooHTTPS de dirección URL de introducción. Actualmente, no se puede consumir RTMP a través de SSL.

#### <a id="keyframe_interval"></a>Intervalo de fotogramas clave
Cuando se usa una secuencia de varias velocidades de bits de toogenerate de codificador en directo local, intervalo de fotogramas clave Hola especifica la duración de hello del grupo de Hola de imágenes (GOP) como se utiliza ese codificador externo. Después de canal de hello recibe esta secuencia entrante, puede entregar la secuencia en directo tooclient las aplicaciones de reproducción en cualquiera de hello siguientes formatos: Smooth Streaming, Streaming adaptable dinámico a través de HTTP (DASH) y HTTP Live Streaming (HLS). Cuando se realiza el streaming en vivo, HLS siempre se empaqueta dinámicamente. De forma predeterminada, los servicios multimedia calcula automáticamente Hola empaquetado proporción de segmento HLS (fragmentos por segmento) basado en intervalo de fotogramas clave de Hola que se recibe de codificador en directo de Hola.

Hello en la tabla siguiente muestra cómo se calcula la duración del segmento hello:

| Intervalo de fotogramas clave | Relación de empaquetado por segmento HLS (fragmento por segmento) | Ejemplo |
| --- | --- | --- |
| Menor que o igual a too3 segundos |3:1 |Si el KeyFrameInterval (o GOP) es de 2 segundos, proporción de empaquetado de segmento HLS de hello predeterminada es too1 3. Esto crea un segmento HLS de 6 segundos. |
| too5 3 segundos |2:1 |Si el KeyFrameInterval (o GOP) tiene 4 segundos, proporción de empaquetado de segmento HLS de hello predeterminada es too1 2. Esto crea un segmento HLS de 8 segundos. |
| Mayor que 5 segundos |1:1 |Si el KeyFrameInterval (o GOP) es de 6 segundos, proporción de empaquetado de segmento HLS de hello predeterminada es 1 too1. Esto crea un segmento HLS de 6 segundos. |

Puede cambiar la proporción de fragmentos por segmento de hello, salida y configure FragmentsPerSegment en ChannelOutputHls de configurar canal Hola.

También puede cambiar el valor de intervalo de fotogramas clave de Hola estableciendo la propiedad de hello KeyFrameInterval en ChanneInput. Si se establece explícitamente KeyFrameInterval, Hola proporción de empaquetado del segmento HLS que fragmentspersegment se calcula a través de las reglas de Hola que se ha descrito anteriormente.  

Si se establece explícitamente KeyFrameInterval y FragmentsPerSegment, servicios multimedia utilizará valores de hello que establezca.

#### <a name="allowed-ip-addresses"></a>Direcciones IP permitidas
Puede definir direcciones IP de Hola que se permiten toopublish toothis vídeo canal. Puede especificarse una dirección IP permitida como uno de hello siguientes:

* Una única dirección IP, por ejemplo, 10.0.0.1.
* Un intervalo de direcciones IP que use una dirección IP y una máscara de subred CIDR, por ejemplo, 10.0.0.1/22.
* Un intervalo de direcciones IP que use una dirección IP y una máscara de subred decimal con puntos, por ejemplo, 10.0.0.1(255.255.252.0).

Si no se especifica ninguna dirección IP y no hay ninguna definición de regla, no se permitirá ninguna dirección IP. tooallow todas las direcciones IP, cree una regla y establezca 0.0.0.0/0.

### <a name="channel-preview"></a>Vista previa de canal
#### <a name="preview-urls"></a>Direcciones URL de vista previa
Los canales proporcionan un extremo de vista previa (URL de vista previa) que use toopreview y validar las secuencias antes del procesamiento y entrega.

Puede obtener la URL de vista previa de hello al crear el canal de Hola. Se tooget hello como dirección URL, canal de hello no tiene toobe en hello **ejecutando** estado. Después de canal de hello inicia la introducción de datos, puede obtener una vista previa de la secuencia.

Actualmente, se puede entregar la secuencia de vista previa de hello solo en MP4 fragmentado (Smooth Streaming) formato, independientemente de hello especifica el tipo de entrada. Puede usar hello [Monitor de estado de transmisión por secuencias suave](http://smf.cloudapp.net/healthmonitor) Reproductor tootest Hola transmisión por secuencias suave. También puede utilizar un reproductor que se hospeda en hello Azure tooview portal la secuencia.

#### <a name="allowed-ip-addresses"></a>Direcciones IP permitidas
Puede definir direcciones IP de Hola que se permiten el extremo de vista previa de tooconnect toohello. Si no se especifican direcciones IP, se permitirá cualquiera. Puede especificarse una dirección IP permitida como uno de hello siguientes:

* Una única dirección IP, por ejemplo, 10.0.0.1.
* Un intervalo de direcciones IP que use una dirección IP y una máscara de subred CIDR, por ejemplo, 10.0.0.1/22.
* Un intervalo de direcciones IP que use una dirección IP y una máscara de subred decimal con puntos, por ejemplo, 10.0.0.1(255.255.252.0).

### <a name="channel-output"></a>Salida del canal
Para obtener información acerca de la salida del canal, vea hello [intervalo de fotogramas clave](#keyframe_interval) sección.

### <a name="channel-managed-programs"></a>Programas administrados por canal
Un canal está asociado con programas que puede utilizar la publicación de hello toocontrol y el almacenamiento de segmentos en una secuencia en directo. Los canales administran los programas. Hello relación de canales y los programas es un medio tootraditional muy similar, donde un canal tiene un flujo constante de contenido y un programa es toosome ámbito ha superado el tiempo de evento en ese canal.

Puede especificar Hola número de horas que quiere tooretain Hola registran contenido de programa Hola, establecer hello **ventana de archivo** longitud. Este valor puede establecerse entre un mínimo de máximo de tooa de 5 minutos de 25 horas. Duración de la ventana de archivo también establece la cantidad máxima de Hola de tiempo que los clientes pueden buscar hacia atrás desde la posición actual en vivo de Hola. Programas pueden ejecutarse durante el período de tiempo especificado de hello, pero se descarta continuamente contenido que queda fuera de la longitud de la ventana de Hola. El valor de esta propiedad también determina cuánto tiempo cliente hello pueden alcanzar los manifiestos.

Cada programa está asociado a un recurso que almacena el contenido de hello transmite por secuencias. Un activo es el contenedor de blob de bloque de tooa asignada en la cuenta de almacenamiento de Azure de Hola y archivos de hello en activos de Hola se almacenan como blobs del contenedor. programa de hello toopublish para que los clientes puedan ver la secuencia de hello, debe crear un localizador OnDemand para activo Hola asociado. Puede usar este toobuild localizador una URL de streaming puede proporcionar a los clientes de tooyour.

Un canal admite hasta toothree simultáneamente ejecutar programas, por lo que puede crear varios archivos de hello mismo flujo entrante. Puede publicar y archivar distintas partes de un evento, según sea necesario. Por ejemplo, imagine que sus necesidades de negocio es tooarchive 6 horas de un programa, pero toobroadcast solo Hola últimos 10 minutos. tooaccomplish, necesita toocreate dos programas en ejecución simultáneos. Un programa se establece tooarchive 6 horas de evento de Hola, pero no se publica el programa Hola. Hello otro programa es conjunto tooarchive durante 10 minutos, y este programa se publica.

No debe volver a usar programas existentes para eventos nuevos. En su lugar, cree un programa nuevo para cada evento. Inicie el programa de hello cuando estés listo toostart streaming y archivado. Detener el programa de hello siempre que lo desee toostop transmisión por secuencias y archivar eventos Hola.

contenido toodelete archivado, detener y eliminar el programa hello y, a continuación, eliminar recurso asociado Hola. No se puede eliminar un recurso si un programa lo está usando. programa Hello debe eliminarse en primer lugar.

Incluso después de detener y eliminar el programa hello, los usuarios pueden transmitir el contenido archivado como un vídeo bajo demanda, hasta que se eliminan los activos de Hola. Si se desea tooretain Hola archiva contenido pero no que esté disponible para la transmisión por secuencias, eliminar Hola localizador de streaming.

## <a id="states"></a>Estados de los canales y facturación
Los valores posibles para el estado actual de Hola de un canal de incluyen:

* **Detenido**: se trata de estado inicial de Hola de canal de hello después de su creación. En este estado, se pueden actualizar las propiedades del canal Hola pero no se permite la transmisión por secuencias.
* **A partir de**: Hola canal se está iniciando. No se permiten actualizaciones ni streaming durante este estado. Si se produce un error, canal de hello devuelve toohello **detenido** estado.
* **Ejecuta**: canal de hello puede procesar secuencias en directo.
* **Detener**: Hola canal está deteniéndose. No se permiten actualizaciones ni streaming durante este estado.
* **Eliminar**: Hola canal está eliminándose. No se permiten actualizaciones ni streaming durante este estado.

Hello tabla siguiente muestra cómo canal indica el modo de facturación toohello mapa.

| Estado del canal | Indicadores de la IU del portal | ¿Facturado? |
| --- | --- | --- | --- |
| **Starting** (iniciándose) |**Starting** (iniciándose) |No (estado transitorio) |
| **Ejecución** |**Ready** (Listo) (sin programas en ejecución)<p><p>o<p>**Streaming** (al menos un programa en ejecución) |Sí |
| **Stopping** (Deteniéndose) |**Stopping** (Deteniéndose) |No (estado transitorio) |
| **Stopped** |**Stopped** |No |

## <a id="cc_and_ads"></a>Subtítulos e inserción de anuncios
Hello en la tabla siguiente muestra los estándares compatibles para subtítulos e inserción de anuncios.

| Estándar | Notas |
| --- | --- |
| CEA-708 y EIA-608 (708/608) |CEA-708 y EIA-608 son subtítulos estándares de Estados Unidos de Hola y Canadá.<p><p>Actualmente, subtítulos (CC) se admite sólo si se incluyen en la secuencia de entrada codificada Hola. Deberá toouse un Codificador multimedia en directo que pueda insertar subtítulos de 608 o 708 en hello secuencia codificada que ha enviado tooMedia servicios. Servicios multimedia ofrece el contenido de hello visores de tooyour títulos insertado. |
| TTML dentro de .ismt (pistas de texto Smooth Streaming) |Empaquetado dinámico de servicios multimedia permite que el contenido de toostream de clientes en cualquiera de hello siguientes formatos: DASH, HLS o Smooth Streaming. Sin embargo, si se introduce MP4 fragmentado (Smooth Streaming) con subtítulos en .ismt (pistas de texto de Smooth Streaming), puede entregar hello secuencia tooonly clientes de transmisión por secuencias suave. |
| SCTE-35 |SCTE-35 es un sistema de señalización digital que ha usado la inserción de publicidad toocue. Receptores de nivel inferior usar anuncios de Hola señal toosplice en secuencia de Hola para hello asignada tiempo. SCTE-35 debe enviarse como una pista dispersa en el flujo de entrada de Hola.<p><p>Actualmente, está fragmentado formato de flujo de entrada de hello solo admitido que transporta señales de publicidad MP4 (Smooth Streaming). formato de salida de Hello solo admitido también es Smooth Streaming. |

## <a id="considerations"></a>Consideraciones
Cuando se usa un toosend de codificador en directo local un canal de tooa de flujo de bits múltiple, se aplica Hola siguientes restricciones:

* Asegúrese de que tiene suficiente libre Internet conectividad toosend datos toohello introducir puntos.
* El uso de una dirección URL de ingesta secundaria requiere más ancho de banda.
* secuencia de varias velocidades de bits de Hola entrantes puede tener un máximo de 10 niveles de calidad de vídeo (capas) y un máximo de 5 pistas de audio.
* Hola mayor velocidad de bits Media para cualquiera de los niveles de calidad de vídeo de hello debe ser inferior a 10 Mbps.
* Hello debe ser agregado de hello velocidades de bits Media de todas las secuencias de audio y vídeo de hello inferior a 25 Mbps.
* No puede cambiar el protocolo de entrada de hello al canal de Hola o sus programas asociados están en ejecución. Si necesita diferentes protocolos, debe crear canales independientes para cada protocolo de entrada.
* Puede ingerir una velocidad de bits única en el canal. Pero porque canal hello no procesar el flujo de hello, las aplicaciones de cliente de hello también recibirá una secuencia de velocidad de bits única. (Esta opción no se recomienda).

Estas son otra tooworking de consideraciones relacionadas con los canales y los componentes relacionados:

* Cada vez que vuelve a configurar de codificador en directo de hello, llame a hello **restablecer** método en el canal de Hola. Antes de restablecer el canal de hello, tendrá programa Hola de toostop. Después de restablecer el canal de hello, reinicie el programa Hola.
* Se puede detener un canal únicamente cuando se encuentra en hello **ejecutando** estado y todos los programas en el canal de Hola se han detenido.
* De forma predeterminada, puede agregar la cuenta de servicios multimedia de tooyour solo 5 canales. Para más información, consulte [Cuotas y limitaciones](media-services-quotas-and-limitations.md).
* Se le facturará solo cuando el canal esté en hello **ejecutando** estado. Para obtener más información, consulte toohello [Channel Estados y facturación](media-services-live-streaming-with-onprem-encoders.md#states) sección.

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="feedback"></a>Comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Temas relacionados
[Especificación de la introducción en directo de MP4 fragmentado de Azure Media Services](media-services-fmp4-live-ingest-overview.md)

[Información general y escenarios comunes de Azure Media Services](media-services-overview.md)

[Conceptos de Azure Media Services](media-services-concepts.md)

[live-overview]: ./media/media-services-manage-channels-overview/media-services-live-streaming-current.png
