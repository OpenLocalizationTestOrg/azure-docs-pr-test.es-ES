---
title: "aaaLive transmisión por secuencias al utilizar secuencias de velocidades de bits de toocreate de servicios multimedia de Azure | Documentos de Microsoft"
description: "Este tema describe cómo tooset un canal que recibe una velocidad de bits única secuencia de un codificador local en directo y, a continuación, realiza la secuencia de velocidad de bits tooadaptive codificación en directo con servicios multimedia. Hello secuencia puede, a continuación, obtener aplicaciones de reproducción de tooclient a través de uno o más extremos de transmisión por secuencias, mediante uno de los siguientes protocolos de transmisión por secuencias adaptativas de hello: HLS, Smooth Streaming, MPEG DASH."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 30ce6556-b0ff-46d8-a15d-5f10e4c360e2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: a8bbdd1570cc9a11bfc2de7bb4ceb9006cc25534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams"></a>Live streaming con secuencias de velocidades de bits de toocreate de servicios multimedia de Azure
## <a name="overview"></a>Información general
En Servicios multimedia de Azure (AMS), un **canal** representa una canalización para procesar contenido de streaming en vivo. Los **canales** reciben el flujo de entrada en directo de dos maneras posibles:

* Un codificador en directo local envía una secuencia de velocidad de bits única canal toohello tooperform habilitado live codificar con servicios multimedia en uno de hello siguientes formatos: RTP (MPEG-TS), RTMP o Smooth Streaming (MP4 fragmentado). Hola canal, a continuación, realiza la codificación en directo de Hola entrante velocidad de bits única secuencia tooa bits múltiple (adaptable) secuencia de vídeo. Cuando se solicita, servicios multimedia transmite hello secuencia toocustomers.
* Un codificador en directo local envía una velocidad de bits múltiple **RTMP** o **Smooth Streaming** (MP4 fragmentado) toohello canal que no está habilitado tooperform en vivo de codificación con AMS. secuencias de Hello ingerida pasan a través de **canal**s sin ningún procesamiento adicional. Este método se llama **paso a través**. Puede usar Hola siguientes codificadores en directo que generan Smooth Streaming de velocidades de bits: MediaExcel, Ateme, Imagine las comunicaciones, Envivio, Cisco y Elemental. Hello siguientes codificadores en directo de salida RTMP: codificadores Adobe Flash Media Live codificador (FMLE), Telestream Wirecast, Haivision, Teradek y Tricaster.  Un codificador en directo también puede enviar un canal de tooa de secuencia de velocidad de bits única que no está habilitado para la codificación en directo, pero no se recomienda. Cuando se solicita, servicios multimedia transmite hello secuencia toocustomers.
  
  > [!NOTE]
  > Con un método paso a través de forma hello más económica toodo streaming en directo.
  > 
  > 

A partir de la versión 2.10 de servicios multimedia de hello, cuando se crea un canal, puede especificar de qué manera desea para el flujo de entrada de canal tooreceive hello y si desea o no que para hello canal tooperform live codificación de la secuencia. Tiene dos opciones:

* **Ninguno** : especifique este valor si piensa toouse un codificador en directo local que dará como resultado el flujo de bits múltiple (una secuencia de acceso directo). En este caso, Hola de secuencia entrante pasa toohello sin ninguna codificación de salida. Este es el comportamiento de Hola de una versión anterior too2.10 de canal.  Para más información sobre cómo trabajar con los canales de este tipo, consulte [Transmisión en vivo con codificadores locales que crean transmisiones de velocidad de bits múltiple](media-services-live-streaming-with-onprem-encoders.md).
* **Estándar** : elija este valor, si tiene previsto toouse servicios multimedia tooencode la secuencia de velocidad de bits toomulti de secuencia en directo de velocidad de bits única. Tenga en cuenta que hay un impacto en la facturación de codificación en directo y debe recordar que salir de un canal de codificación en directo en el estado de "Running" hello supondrán un coste adicional de facturación.  Se recomienda detener los canales de ejecución inmediatamente después de los eventos de transmisión por secuencias en directo es tooavoid completa cargos adicionales por hora.

> [!NOTE]
> Este tema describen los atributos de canales que se habilitan la codificación en directo de tooperform (**estándar** tipo de codificación). Para obtener información sobre cómo trabajar con los canales que no están habilitado tooperform de codificación en directo, vea [de transmisión por secuencias en directo con codificadores locales que crean secuencias de velocidades de bits](media-services-live-streaming-with-onprem-encoders.md).
> 
> Realizar seguro hello tooreview [consideraciones](media-services-manage-live-encoder-enabled-channels.md#Considerations) sección.
> 
> 

## <a name="billing-implications"></a>Implicaciones de facturación
Un canal de codificación en directo comienza tan pronto como su estado cambia de "Running" demasiado a través de la API de Hola de facturación.   También puede ver el estado de hello en hello portal de Azure, o en la herramienta de explorador de servicios multimedia de Azure de hello (http://aka.ms/amse).

Hello tabla siguiente muestra cómo asignan los Estados del canal toobilling Estados Hola API y portal de Azure. Tenga en cuenta que los Estados de hello son ligeramente diferentes entre Hola API y UX de Portal. Tan pronto como un canal está en estado de "Running" Hola a través de la API de Hola o en estado de "Streaming" en el portal de Azure de Hola u Hola "Listo", se activará de facturación.
Canal de hello toostop de facturación aún más, tiene tooStop Hola canal a través de la API de Hola o en hello portal de Azure.
Usted es responsable de detener los canales cuando haya terminado con canal de codificación en directo de Hola.  Error toostop un canal de codificación dará como resultado en la facturación continua.

### <a id="states"></a>Los Estados del canal y cómo se asignan toohello modo de facturación
estado actual de Hola de un canal. Los valores posibles son:

* **Detenido**. Se trata de estado inicial de Hola de hello canal después de su creación (a menos que el inicio automático se seleccionó en el portal de Hola.) No se produce ninguna facturación en este estado. En este estado, se pueden actualizar las propiedades del canal Hola pero no se permite la transmisión por secuencias.
* **Iniciando**. Canal de saludo se está iniciando. No se produce ninguna facturación en este estado. No se permiten actualizaciones ni streaming durante este estado. Si se produce un error, Hola canal devuelve toohello estado detenido.
* **En ejecución**. Hola canal es capaz de procesar secuencias en directo. Está ahora el uso de facturación. Debe detener Hola canal tooprevent aún más la facturación. 
* **Deteniéndose**. Canal de saludo se está deteniendo. No se produce facturación en este estado transitorio. No se permiten actualizaciones ni streaming durante este estado.
* **Eliminando**. Canal de saludo se está eliminando. No se produce facturación en este estado transitorio. No se permiten actualizaciones ni streaming durante este estado.

Hello tabla siguiente muestra cómo canal indica el modo de facturación toohello mapa. 

| Estado del canal | Indicadores IU del portal | ¿Es la facturación? |
| --- | --- | --- |
| Iniciando |Iniciando |No (estado transitorio) |
| En ejecución |Listo (no hay programas en ejecución)<br/>o<br/>Streaming (al menos un programa en ejecución) |SÍ |
| Deteniéndose |Deteniéndose |No (estado transitorio) |
| Detenido |Detenido |No |

### <a name="automatic-shut-off-for-unused-channels"></a>Cierre automático para canales no utilizados
A partir del 25 de enero de 2016, Servicios multimedia implementó una actualización que detiene automáticamente un canal (con codificación en directo habilitada), después de haber estado ejecutándose en un estado no usado durante un largo período. Esto aplica tooChannels que no tienen ningún programa activo, y que no han recibido una contribución entrada fuente durante un largo período de tiempo.

umbral de Hola durante un período sin usar intervalo nominal es de 12 horas, pero es toochange de asunto.

## <a name="live-encoding-workflow"></a>Flujo de trabajo de la codificación en directo
Hello siguiente diagrama representa un flujo de trabajo transmisión por secuencias en directo donde un canal recibe una secuencia de velocidad de bits única en uno de hello siguientes protocolos: RTMP, Smooth Streaming o RTP (MPEG-TS); a continuación, se codifica flujo de hello secuencia tooa velocidades de bits. 

![Flujo de trabajo activo][live-overview]

## <a id="scenario"></a>Escenario común de streaming en vivo
Hola siguientes pasos son generales implicadas en la creación de aplicaciones de transmisión por secuencias en directo común.

> [!NOTE]
> Actualmente, Hola máximo recomendado de duración de un evento en directo es 8 horas. Póngase en contacto con amslived Microsoft.com si necesitas toorun un canal para períodos más largos de tiempo. Tenga en cuenta que hay un impacto en la facturación de codificación en directo y debe recordar que salir de un canal de codificación en directo en el estado de "Running" hello supondrán un coste adicional de facturación por hora.  Se recomienda detener los canales de ejecución inmediatamente después de los eventos de transmisión por secuencias en directo es tooavoid completa cargos adicionales por hora. 
> 
> 

1. Conectar un equipo de tooa de cámara de vídeo. Iniciar y configurar un codificador en directo local que pueda dar como resultado un **único** secuencia de velocidad de bits de hello siguientes protocolos: RTP (MPEG-TS), Smooth Streaming o RTMP. 
   
    Este paso también puede realizarse después de crear el canal.
2. Cree e inicie un canal. 
3. URL de introducción de hello recuperar canales. 
   
    URL de introducción de Hola Hola codificador en directo toosend hello secuencia toohello canal utiliza.
4. Recuperar la dirección URL de vista previa de canal de Hola. 
   
    Utilice este tooverify de dirección URL que el canal está recibiendo correctamente la secuencia en directo de Hola.
5. Cree un programa. 
   
    Al usar hello portal de Azure, también crear un programa crea un activo. 
   
    Cuando se usa el SDK de .NET o REST necesario toocreate un activo y especifique toouse este recurso al crear un programa. 
6. Publicar asset Hola asociado programa Hola.   
   
    >[!NOTE]
    >Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. Hola origen desde el que desea que el contenido de toostream tiene toobe en hello **ejecutando** estado. 
    
7. Inicie el programa de hello cuando esté listo toostart streaming y archivado.
8. Si lo desea, codificador en directo de hello puede ser señalado toostart un anuncio. anuncio de Hola se inserta en el flujo de salida de hello.
9. Detener el programa de hello siempre que lo desee toostop transmisión por secuencias y archivar eventos Hola.
10. Eliminar programa Hola (y opcionalmente eliminar recurso de hello).   

> [!NOTE]
> Es muy importante no tooforget tooStop un canal de codificación en directo. Tenga en cuenta que hay una hora impacto para la codificación en directo de facturación y debe recordar que salir de un canal de codificación en directo en el estado de "Running" hello supondrán un coste adicional de facturación.  Se recomienda detener los canales de ejecución inmediatamente después de los eventos de transmisión por secuencias en directo es tooavoid completa cargos adicionales por hora. 
> 
> 

## <a id="channel"></a>Configuraciones de entrada de canal (ingesta)
### <a id="Ingest_Protocols"></a>Protocolo de streaming de ingesta
Si hello **tipo de codificador** se establece demasiado**estándar**, las opciones válidas son:

* **RTP** (MPEG-TS): secuencia de transporte MPEG-2 a través de RTP.  
* **RTMP**
* **MP4 fragmentado** de una sola velocidad de bits (Smooth Streaming)

#### <a name="rtp-mpeg-ts---mpeg-2-transport-stream-over-rtp"></a>RTP (MPEG-TS): secuencia de transporte MPEG-2 a través de RTP.
Caso de uso típico: 

Los emisores profesionales normalmente es necesario trabajar con codificadores en directo de tecnología avanzada de local de proveedores como tecnologías Elemental, Ericsson, Ateme, Imagine o Envivio toosend una secuencia. Estos suelen usarse conjuntamente con un departamento de TI y redes privadas.

Consideraciones:

* se recomienda el uso de Hola de una secuencia de transporte de programa único (SPTS) de entrada. 
* Puede introducir los flujos de audio too8 con MPEG-2 TS a través de RTP. 
* secuencia de vídeo de Hello debe tener una velocidad de bits Media inferior a 15 Mbps
* Hola agregado velocidad de bits Media de secuencias de audio de hello debe ser inferior a 1 Mbps
* A continuación se Hola códecs admitidos:
  
  * MPEG-2/H.262 Video 
    
    * Perfil Principal (4:2:0)
    * Perfil Alta (4:2:0, 4:2:2)
    * Perfil 422 (4:2:0, 4:2:2)
  * MPEG-4 AVC/H.264 Video  
    
    * Perfil Línea de base, Principal, Alta (4:2:0 de 8 bits)
    * Perfil Alta 10 (4:2:0 de 10 bits)
    * Perfil Alta 422 (4:2:2 de 10 bits)
  * MPEG-2 AAC-LC Audio 
    
    * Mono, estéreo, Surround (5.1, 7.1)
    * Empaquetado ADTS estilo MPEG-2
  * Audio Dolby Digital (AC-3) 
    
    * Mono, estéreo, Surround (5.1, 7.1)
  * Audio MPEG (nivel II y III) 
    
    * Mono, estéreo
* Entre los codificadores de difusión recomendados se incluyen:
  
  * Imagine Communications Selenio ENC 1
  * Imagine Communications Selenio ENC 2
  * Elemental Live

#### <a id="single_bitrate_RTMP"></a>RTMP de una sola velocidad de bits
Consideraciones:

* flujo de entrada de Hello no puede contener vídeo de varias velocidades de bits
* secuencia de vídeo de Hello debe tener una velocidad de bits Media inferior a 15 Mbps
* secuencia de audio de Hello debe tener una velocidad de bits Media por debajo de 1 Mbps
* A continuación se Hola códecs admitidos:
* MPEG-4 AVC/H.264 Video
* Perfil Línea de base, Principal, Alta (4:2:0 de 8 bits)
* Perfil Alta 10 (4:2:0 de 10 bits)
* Perfil Alta 422 (4:2:2 de 10 bits)
* MPEG-2 AAC-LC Audio
* Mono, estéreo, Surround (5.1, 7.1)
* Velocidad de muestreo 44,1 kHz
* Empaquetado ADTS estilo MPEG-2
* Entre los codificadores recomendados se incluyen:
* Telestream Wirecast
* Flash Media Live Encoder

#### <a name="single-bitrate-fragmented-mp4-smooth-streaming"></a>MP4 fragmentado de una sola velocidad de bits (Smooth Streaming)
Caso de uso típico:

Usar codificadores en directo de proveedores como tecnologías Elemental, Ericsson, Ateme, flujo de entrada Hola de Envivio toosend sobre Hola abra internet tooa cerca del centro de datos de Azure en local.

Consideraciones:

Las mismas aplicables al apartado [RTMP de una sola velocidad de bits](media-services-manage-live-encoder-enabled-channels.md#single_bitrate_RTMP).

#### <a name="other-considerations"></a>Otras consideraciones
* No puede cambiar el protocolo de entrada de hello al canal de Hola o sus programas asociados están en ejecución. Si necesita diferentes protocolos, debe crear canales independientes para cada protocolo de entrada.
* Resolución máxima de la secuencia de vídeo entrante hello es 1920 x 1080 y al menos 60 campos por segundo si entrelazado o 30 fotogramas por segundo si progresiva.

### <a name="ingest-urls-endpoints"></a>Direcciones URL de ingesta (extremos)
Un canal proporciona un extremo de entrada (URL de introducción) que especifique en el codificador en directo de hello, por lo que puede insertar codificador hello tooyour canales se transmita por secuencias.

Puede obtener Hola direcciones URL de entrada una vez que se crea un canal. tooget estas direcciones URL, Hola canal no tiene toobe en hello **ejecutando** estado. Cuando esté listo toostart insertar datos en hello canal, debe estar en hello **ejecutando** estado. Una vez que el canal de hello inicia la introducción de datos, puede obtener una vista previa de la secuencia a través de la dirección URL de vista previa de Hola.

Tiene la opción de consumir una secuencia en directo de MP4 fragmentado (Smooth Streaming) a través de una conexión SSL. tooingest a través de SSL, que seguro Hola de tooupdate tooHTTPS de dirección URL de introducción. Tenga en cuenta que, actualmente, AMS no admite SSL con dominios personalizados.  

### <a name="allowed-ip-addresses"></a>Direcciones IP permitidas
Puede definir direcciones IP de Hola que se permiten toopublish toothis vídeo canal. Dichas direcciones se pueden especificar como dirección IP individual (por ejemplo, ‘10.0.0.1’), un intervalo de direcciones IP mediante una dirección IP y una máscara de subred CIDR (por ejemplo, ‘10.0.0.1/22’) o un intervalo de direcciones IP mediante una dirección IP y una máscara de subred decimal con puntos (por ejemplo, '10.0.0.1(255.255.252.0)').

Si no se especifican direcciones IP y no hay ninguna definición de regla, no se permitirá ninguna dirección IP. tooallow todas las direcciones IP, cree una regla y establezca 0.0.0.0/0.

## <a name="channel-preview"></a>Vista previa de canal
### <a name="preview-urls"></a>Direcciones URL de vista previa
Los canales proporcionan un extremo de vista previa (URL de vista previa) que use toopreview y validar las secuencias antes del procesamiento y entrega.

Puede obtener la URL de vista previa de hello al crear el canal de Hola. dirección URL de hello tooget, canal de Hola no tiene toobe en hello **ejecutando** estado.

Una vez que el canal de hello inicia la introducción de datos, puede obtener una vista previa de la secuencia.

> [!NOTE]
> Actualmente flujo de vista previa de hello solo se puede entregar en MP4 fragmentado (Smooth Streaming) formato independientemente Hola especifica el tipo de entrada. Puede usar hello [http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor) Reproductor tootest Hola transmisión por secuencias suave. También puede utilizar un reproductor hospedado en hello Azure tooview portal la secuencia.
> 
> 

### <a name="allowed-ip-addresses"></a>Direcciones IP permitidas
Puede definir direcciones IP de Hola que se permiten el extremo de vista previa de tooconnect toohello. Si no se especifica ninguna dirección IP, se permitirá cualquier dirección IP. Dichas direcciones se pueden especificar como dirección IP individual (por ejemplo, ‘10.0.0.1’), un intervalo de direcciones IP mediante una dirección IP y una máscara de subred CIDR (por ejemplo, ‘10.0.0.1/22’) o un intervalo de direcciones IP mediante una dirección IP y una máscara de subred decimal con puntos (por ejemplo, ‘10.0.0.1(255.255.252.0)’).

## <a name="live-encoding-settings"></a>Configuración de la codificación en directo
Esta sección describe cómo la configuración de hello para el codificador en directo de hello en hello canal puede ser ajustado, Hola cuando **tipo de codificación** de un canal se establece demasiado**estándar**.

> [!NOTE]
> Al introducir varias pistas de idioma y realizar codificación en directo con Azure, solo se admite RTP como entrada de varios idiomas. Puede definir los flujos de audio too8 con MPEG-2 TS a través de RTP. Actualmente no se admite la introducción de varias pistas de audio con Smooth Streaming ni RTMP. Al realizar la codificación en directo con [live local codifica](media-services-live-streaming-with-onprem-encoders.md), no hay ninguna limitación de este tipo porque lo que se envía tooAMS pasa a través de un canal sin ningún procesamiento adicional.
> 
> 

### <a name="ad-marker-source"></a>Origen de marcador de anuncio
Puede especificar el origen de hello señales de marcadores publicitarios. Valor predeterminado es **Api**, lo que indica que codificador en directo de hello en hello canal debe escuchar tooan asincrónica **Ad marcador API**.

Hola otra opción válida es **Scte35** (permitido solo si la ingesta de hello protocolo de transmisión se establece tooRTP (MPEG-TS). Cuando se especifica Scte35, codificador en directo de hello analizará las señales de SCTE-35 Hola flujo de entrada RTP (MPEG-TS).

### <a name="cea-708-closed-captions"></a>Subtítulos CEA 708
Un marcador opcional que indica tooignore de codificador en directo de hello ningún dato de subtítulos CEA 708 incrustado en el vídeo entrante Hola. Cuando se establece marca de hello toofalse (valor predeterminado), el codificador de hello detectará y volver a insertar datos CEA 708 en secuencias de vídeo de salida de hello.

### <a name="video-stream"></a>Secuencia de vídeo
Opcional. Describe la secuencia de vídeo de entrada de Hola. Si no se especifica este campo, se utiliza el valor predeterminado de Hola. Esta configuración solo se permite si el protocolo de transmisión por secuencias se establece tooRTP (MPEG-TS) de entrada de Hola.

#### <a name="index"></a>Índice
Índice de base cero que especifica qué secuencia de vídeo de entrada debe ser procesado por el codificador en directo de hello en hello canal. Esta configuración solo se aplica si el protocolo de streaming de ingesta es RTP (MPEG-TS).

El valor predeterminado es cero. Se recomienda toosend en una secuencia de transporte de programa único (SPTS). Si el flujo de entrada de hello contiene varios programas, codificador en directo de hello analiza Hola tabla de asignación de programa (PMT) en la entrada de hello, identifica las entradas de Hola que tengan un nombre de tipo de secuencia de MPEG-2 Video o H.264 y los organiza en orden de hello especificado en hello Pmt. a continuación, se utiliza el índice de base cero de Hello toopick entrada de n-ésimo de hello en esta organización.

### <a name="audio-stream"></a>Secuencia de audio
Opcional. Describe las secuencias de audio de entrada de Hola. Si no se especifica este campo, se aplican valores predeterminados de hello especificados. Esta configuración solo se permite si el protocolo de transmisión por secuencias se establece tooRTP (MPEG-TS) de entrada de Hola.

#### <a name="index"></a>Índice
Se recomienda toosend en una secuencia de transporte de programa único (SPTS). Si el flujo de entrada de hello contiene varios programas, hello codificador en directo dentro Hola canal analiza Hola tabla de asignación de programa (PMT) en la entrada de hello, identifica las entradas de Hola que tengan un nombre de tipo de secuencia de MPEG-2 AAC ADTS o AC-3 System-A o AC-3 System-B o privada de MPEG-2 PES o MPEG-1 Audio o Audio MPEG-2 y los organiza en orden de hello especificado en hello Pmt. a continuación, se utiliza el índice de base cero de Hello toopick entrada de n-ésimo de hello en esta organización.

#### <a name="language"></a>language
Hola identificador de idioma de la secuencia de audio hello, que cumple las especificaciones tooISO 639-2, por ejemplo, ENG. Si no está presente, valor predeterminado de hello es UND (no definido).

Puede haber una secuencia de audio de too8 conjuntos especificados si Hola entrada toohello canal es MPEG-2 TS a través de RTP. Sin embargo, puede haber ningún dos entradas con hello mismo valor de índice.

### <a id="preset"></a>Valor preestablecido del sistema
Especifica Hola preestablecido toobe usado Hola codificador en vivo dentro de este canal. Hola actualmente, solo se permite el valor es **Default720p** (valor predeterminado).

Tenga en cuenta que, si necesita valores preestablecidos personalizados, debe ponerse en contacto con amslived en Microsoft.com.

**Default720p** codificará vídeo hello en hello después de 7 capas.

#### <a name="output-video-stream"></a>Secuencia de vídeo de salida
| Velocidad de bits | Ancho | Alto | Fotogramas/seg. máx. | Perfil | Nombre secuencia salida |
| --- | --- | --- | --- | --- | --- |
| 3500 |1280 |720 |30 |Alto |Video_1280x720_3500kbps |
| 2200 |960 |540 |30 |Principal |Video_960x540_2200kbps |
| 1350 |704 |396 |30 |Principal |Video_704x396_1350kbps |
| 850 |512 |288 |30 |Principal |Video_512x288_850kbps |
| 550 |384 |216 |30 |Principal |Video_384x216_550kbps |
| 350 |340 |192 |30 |Línea base |Video_340x192_350kbps |
| 200 |340 |192 |30 |Línea base |Video_340x192_200kbps |

#### <a name="output-audio-stream"></a>Secuencia de audio de salida
Audio está codificado toostereo AAC-LC a 64 kbps, frecuencia de muestreo de 44,1 kHz.

## <a name="signaling-advertisements"></a>Señalización de anuncios
Si el canal tiene habilitada la codificación en directo, dispone de un componente en la canalización de procesamiento de vídeo y puede manipularlo. Puede señalar para hello canal tooinsert pizarras o anuncios en la secuencia de velocidad de bits adaptativa salientes Hola. Pizarras siguen siendo imágenes que puede usar toocover una fuente directa de entrada de hello en algunos casos (por ejemplo, durante una pausa comercial). Anuncio de señales, están sincronizados señales que incrustar en hello saliente flujo tootell Hola Reproductor de vídeo tootake ninguna acción especial, como anuncios de tooan tooswitch en el momento adecuado de Hola. Consulte esta [blog](https://codesequoia.wordpress.com/2014/02/24/understanding-scte-35/) para obtener información general del mecanismo de señalización hello SCTE-35 utilizado para este propósito. A continuación se muestra un escenario típico que puede implementar en el evento en directo.

1. Tener los usuarios obtener una imagen de evento previo antes de que comience el evento de Hola.
2. Tener los usuarios obtener una imagen de evento posterior a la de una vez finalizado el evento Hola.
3. Tener los usuarios obtener una imagen de evento de ERROR si hay un problema durante el evento de hello (por ejemplo, error de alimentación en estadio hello).
4. Enviar un evento para el saludo en vivo de pausa Publicitaria imagen toohide fuente durante una pausa comercial.

siguiente Hola es propiedades de hello que puede establecer cuando los anuncios de señalización. 

### <a name="duration"></a>Duration
duración de Hello, en segundos, de la pausa comercial Hola. Esto tiene toobe un valor positivo distinto de cero en pausa comercial de orden toostart Hola. Cuando una pausa comercial está en curso y la duración de hello conjunto toozero con hello CueId coincidentes pausa comercial en curso de hello, a continuación, se cancela la instrucción break.

### <a name="cueid"></a>Identificador de pila
Un identificador único para la pausa comercial de hello, toobe utilizado por la aplicación de bajada tootake las acciones oportunas. Debe toobe un número entero positivo. Puede establecer este valor tooany aleatorio enteros o usar un hello de tootrack identificadores de indicación de sistema de nivel superior. Realizar determinada toonormalize los enteros de toopositive identificadores antes de enviar a través de la API de Hola.

### <a name="show-slate"></a>Mostrar pizarra
Opcional. Señala Hola codificador en directo tooswitch toohello [predeterminado Pizarra](media-services-manage-live-encoder-enabled-channels.md#default_slate) imagen durante una pausa comercial y ocultar la señal de vídeo entrante Hola. El audio también está desactivado durante el uso de la pizarra. El valor predeterminado es **false**. 

imagen de Hello utilizada será Hola especificada a través de activo de tableta táctil predeterminada Hola propiedad Id en tiempo de Hola de creación del canal Hola. Pizarra Hola será ajusta el tamaño de la imagen de pantalla de toofit Hola. 

## <a name="insert-slate--images"></a>Insertar imágenes de pizarra
codificador en directo de Hello en hello canal puede ser imagen de tableta táctil tooa tooswitch señalado. También puede ser señalado tooend una careta en curso. 

codificador en directo de Hello puede ser imagen de tableta táctil tooa tooswitch configurado y ocultar Hola señal de vídeo entrante en determinadas situaciones, por ejemplo, durante una pausa publicitaria. Si no se ha configurado ninguna pizarra de este tipo, el vídeo de entrada no se enmascara durante esa pausa.

### <a name="duration"></a>Duration
duración de Hola de tableta táctil hello en segundos. Esto tiene toobe un valor positivo distinto de cero en Pizarra de orden toostart Hola. Si hay una pizarra en curso y se especifica una duración de cero, dicha pizarra se terminará.

### <a name="insert-slate-on-ad-marker"></a>Insertar pizarra en marcador de anuncio
Cuando set tootrue, esta opción configura tooinsert de codificador en directo de hello una careta durante una pausa publicitaria. valor predeterminado de Hello es true. 

### <a id="default_slate"></a>Identificador de activo de activo de tableta táctil predeterminado

Opcional. Especifica el identificador de recurso del activo de servicios multimedia que contiene la imagen de tableta táctil Hola Hola Hola. El valor predeterminado es null. 


>[!NOTE] 
>Antes de crear el canal de hello, hello careta con hello siguiendo las restricciones se debe cargar como un recurso dedicado (ningún otro archivo debe estar en este recurso). Esta imagen se utiliza únicamente cuando consiste en Insertar una pizarra debido pausa publicitaria de tooan codificador en directo de Hola o ha sido explícitamente había señalado tooinsert una pizarra. codificador en directo de Hello también puede entrar en un modo de tableta táctil durante determinadas condiciones de error: por ejemplo si la señal de entrada de Hola se pierde. No hay actualmente ninguna toouse opción una imagen personalizada al codificador en directo de hello entra en este tipo estado 'pérdida de señal de entrada'. Puede votar por esta característica [aquí](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/10190457-define-custom-slate-image-on-a-live-encoder-channel).


* Máximo 1920x1080 de resolución.
* Al menos 3 MB de tamaño.
* nombre de archivo de Hello debe tener una extensión *.jpg.
* imagen de Hola se debe cargar en un recurso como hello que assetfile solo en ese recurso y este AssetFile deben marcarse como archivo principal de Hola. Hola activo no puede ser el almacenamiento de cifrado.

Si hello **predeterminado Pizarra identificador de recurso** no se especifica, y **insertar tableta táctil en marcador publicitario** se establece demasiado**true**, una imagen de servicios multimedia de Azure predeterminada será hello toohide usado de entrada secuencia de vídeo. El audio también está desactivado durante el uso de la pizarra. 

## <a name="channels-programs"></a>Programas del canal
Un canal está asociado con los programas que permiten la publicación de hello toocontrol y el almacenamiento de segmentos en una secuencia en directo. Los canales administran los programas. Hello relación de canales y los programas es un medio muy similar tootraditional donde un canal tiene un flujo constante de contenido y un programa es toosome ámbito ha superado el tiempo de evento en ese canal.

Puede especificar Hola número de horas que quiere tooretain Hola registran contenido de programa Hola, establecer hello **ventana de archivo** longitud. Este valor puede establecerse entre un mínimo de máximo de tooa de 5 minutos de 25 horas. Duración de la ventana de archivo también establece la cantidad máxima de Hola de tiempo que los clientes pueden buscar hacia atrás desde la posición actual en vivo de Hola. Programas pueden ejecutarse durante el período de tiempo especificado de hello, pero se descarta continuamente contenido que queda fuera de la longitud de la ventana de Hola. El valor de esta propiedad también determina cuánto tiempo cliente hello pueden alcanzar los manifiestos.

Cada programa está asociado a un recurso que almacena el contenido de hello transmite por secuencias. Un recurso es el contenedor de blob de bloque de tooa asignada en la cuenta de almacenamiento de Azure de Hola y archivos de hello en activos de Hola se almacenan como blobs en ese contenedor. programa hello de toopublish para que los clientes puedan ver flujo Hola debe crear un localizador OnDemand para hello asociado activo. Este localizador permitirá toobuild una URL de streaming puede proporcionar a los clientes de tooyour.

Un canal admite hasta toothree programas en ejecución al mismo tiempo para que pueda crear varios archivos de hello mismo flujo entrante. Esto le permite toopublish y archivar diferentes partes de un evento según sea necesario. Por ejemplo, sus necesidades de negocio es tooarchive 6 horas de un programa, pero toobroadcast solo últimos 10 minutos. tooaccomplish, necesita toocreate dos programas en ejecución simultáneos. Un programa se establece tooarchive 6 horas de evento de hello pero no se publica el programa Hola. Hello otro programa es conjunto tooarchive durante 10 minutos y se publica este programa.

No debe volver a usar programas existentes para eventos nuevos. En su lugar, cree e inicie un nuevo programa para cada evento como se describe en la sección de programar aplicaciones de transmisión por secuencias en directo de Hola.

Inicie el programa de hello cuando esté listo toostart streaming y archivado. Detener el programa de hello siempre que lo desee toostop transmisión por secuencias y archivar eventos Hola. 

contenido toodelete archivado, detener y eliminar programa hello y, a continuación, eliminar recurso asociado Hola. No se puede eliminar un recurso si lo está usando un programa; programa Hello debe eliminarse en primer lugar. 

Incluso después de detener y eliminar el programa hello, Hola usuarios sería capaz de toostream el contenido archivado como un vídeo bajo demanda, siempre y cuando no se elimine de recurso de Hola.

Si desea hello tooretain archivado de contenido, pero no la tiene disponible para la transmisión por secuencias, eliminar Hola localizador de streaming.

## <a name="getting-a-thumbnail-preview-of-a-live-feed"></a>Obtención de una vista previa en miniatura de una fuente directa
Cuando se habilita la codificación en directo, ahora puede obtener una vista previa de fuente directa de hello alcanzar Hola canal. Esto puede ser una valiosa herramienta toocheck si su entrada en vivo llega Hola canal. 

## <a id="states"></a>Los Estados del canal y cómo asignan los Estados toohello modo de facturación
estado actual de Hola de un canal. Los valores posibles son:

* **Detenido**. Esto es estado inicial de Hola de hello canal después de su creación. En este estado, se pueden actualizar las propiedades del canal Hola pero no se permite la transmisión por secuencias.
* **Iniciando**. Canal de saludo se está iniciando. No se permiten actualizaciones ni streaming durante este estado. Si se produce un error, Hola canal devuelve toohello estado detenido.
* **En ejecución**. Hola canal es capaz de procesar secuencias en directo.
* **Deteniéndose**. Canal de saludo se está deteniendo. No se permiten actualizaciones ni streaming durante este estado.
* **Eliminando**. Canal de saludo se está eliminando. No se permiten actualizaciones ni streaming durante este estado.

Hello tabla siguiente muestra cómo canal indica el modo de facturación toohello mapa. 

| Estado del canal | Indicadores IU del portal | ¿Facturado? |
| --- | --- | --- |
| Iniciando |Iniciando |No (estado transitorio) |
| En ejecución |Listo (no hay programas en ejecución)<br/>o<br/>Streaming (al menos un programa en ejecución) |SÍ |
| Deteniéndose |Deteniéndose |No (estado transitorio) |
| Detenido |Detenido |No |

> [!NOTE]
> Actualmente, promedio de inicio de canal de hello es de aproximadamente 2 minutos, pero a veces puede llevar too20 + minutos. Restablece de canal puede tardar hasta too5 minutos.
> 
> 

## <a id="Considerations"></a>Consideraciones
* Cuando un canal de **estándar** tipo de codificación produce una pérdida de fuente de entrada de origen/contribución, compensa para ella mediante la sustitución de audio/vídeo de origen de hello con una pizarra de error y la latencia. Hola canal continuará tooemit una pizarra hasta que Hola entrada/contribución fuente se reanuda. Se recomienda no dejar un canal en directo en este estado durante más de dos horas. Después de ese punto, comportamiento de Hola de hello canal en la reconexión de entrada no está garantizado, ninguno es su comportamiento en respuesta tooa comando de restablecimiento. Tendrá toostop Hola canal, elimínelo y cree uno nuevo.
* No puede cambiar el protocolo de entrada de hello al canal de Hola o sus programas asociados están en ejecución. Si necesita diferentes protocolos, debe crear canales independientes para cada protocolo de entrada.
* Cada vez que vuelve a configurar de codificador en directo de hello, llame a hello **restablecer** método en el canal de Hola. Antes de restablecer el canal de hello, tendrá programa Hola de toostop. Después de restablecer el canal de hello, reinicie el programa Hola.
* Un canal se puede detener solo cuando se encuentra en estado de ejecución de Hola y todos los programas en el canal de Hola se han detenido.
* De forma predeterminada sólo se puede agregar 5 canales tooyour cuenta de servicios multimedia. Esta es una cuota de advertencia a todas las cuentas nuevas. Para obtener más información, consulte [Cuotas y limitaciones](media-services-quotas-and-limitations.md).
* No puede cambiar el protocolo de entrada de hello al canal de Hola o sus programas asociados están en ejecución. Si necesita diferentes protocolos, debe crear canales independientes para cada protocolo de entrada.
* Solo se le facturará cuando el canal esté en hello **ejecutando** estado. Para obtener más información, consulte demasiado[esto](media-services-manage-live-encoder-enabled-channels.md#states) sección.
* Actualmente, Hola máximo recomendado de duración de un evento en directo es 8 horas. Póngase en contacto con amslived Microsoft.com si necesitas toorun un canal para períodos más largos de tiempo.
* Asegúrese de que toohave Hola extremo de streaming desde el que desea que el contenido de toostream Hola **ejecutando** estado.
* Al introducir varias pistas de idioma y realizar codificación en directo con Azure, solo se admite RTP como entrada de varios idiomas. Puede definir los flujos de audio too8 con MPEG-2 TS a través de RTP. Actualmente no se admite la introducción de varias pistas de audio con Smooth Streaming ni RTMP. Al realizar la codificación en directo con [live local codifica](media-services-live-streaming-with-onprem-encoders.md), no hay ninguna limitación de este tipo porque lo que se envía tooAMS pasa a través de un canal sin ningún procesamiento adicional.
* utiliza valores preestablecidos de codificación de Hola Hola noción de "velocidad de fotogramas max" de 30 fps. Por lo que si hello entrada es 60fps / 59.97i, cuadros de entrada de hello son quita/desinstalación-interlaced too30/29,97 fps. Si la entrada de hello es 50fps/50i, cuadros de entrada de hello son quita/desinstalación-interlaced too25 fps. Si la entrada de hello es 25 fps, salida sigue siendo 25 fps.
* No olvide tooSTOP YOUR canales cuando haya finalizado. Si no lo hace, la facturación continuará.

## <a name="known-issues"></a>Problemas conocidos
* Se ha mejorado el tiempo de inicio canal tooan promedio de 2 minutos, pero a veces mayor demanda aún puede tardar minutos too20 +.
* La compatibilidad con RTP está dirigida a los operadores de radiodifusión profesionales. Revise las notas de hello en RTP en [esto](https://azure.microsoft.com/blog/2015/04/13/an-introduction-to-live-encoding-with-azure-media-services/) blog.
* Imágenes de tableta deben cumplir toorestrictions descritos [aquí](media-services-manage-live-encoder-enabled-channels.md#default_slate). Si intenta crear un canal con un error de tableta táctil predeterminada que es mayor que 1920 x 1080, hello solicitud finalmente le espera.
* Una vez más... no olvide tooSTOP YOUR canales cuando haya terminado de transmisión por secuencias. Si no lo hace, la facturación continuará.

## <a name="next-step"></a>Paso siguiente
Consulte las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Temas relacionados
[Entrega de eventos de streaming en vivo con Servicios multimedia de Azure](media-services-overview.md)

[Crear los canales que llevan a cabo la codificación en directo desde una secuencia de velocidad de bits de tooadaptive de velocidad de bits único con el Portal](media-services-portal-creating-live-encoder-enabled-channel.md)

[Crear los canales que llevan a cabo la codificación en directo desde una secuencia de velocidad de bits única tooadaptive de velocidad de bits con el SDK de .NET](media-services-dotnet-creating-live-encoder-enabled-channel.md)

[Administración de canales con la API de REST](https://docs.microsoft.com/rest/api/media/operations/channel)
 
[Conceptos de Servicios multimedia de Azure](media-services-concepts.md)

[Especificación de la introducción en directo de MP4 fragmentado de Servicios multimedia de Azure](media-services-fmp4-live-ingest-overview.md)

[live-overview]: ./media/media-services-manage-live-encoder-enabled-channels/media-services-live-streaming-new.png

