---
title: aaaOverview de Streaming en directo con servicios multimedia de Azure | Documentos de Microsoft
description: "En este tema se proporciona información general de streaming en vivo con Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: fb63502e-914d-4c1f-853c-4a7831bb08e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: edc49069db6b491902bdcbb808b1974858cc92f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-live-streaming-using-azure-media-services"></a>Información general de streaming en vivo con Azure Media Services
## <a name="overview"></a>Información general
Para entregar contenido en vivo transmisión por secuencias de eventos con servicios multimedia de Azure Hola de los componentes siguientes, suelen intervenir:

* Cámara que es usado toobroadcast un evento.
* Un codificador de vídeo en directo que convierte las señales de hello toostreams de cámara que se envían tooa live streaming de servicio.

    Opcionalmente, varios codificadores sincronizados en directo. Para ciertos eventos críticos en directo que petición muy alta disponibilidad y calidad de la experiencia, se recomienda codificadores redundantes de tooemploy activo / activo con tiempo sincronización tooachieve conmutación por error fluida sin pérdida de datos.
* Un servicio de streaming en vivo que le permite hello toodo siguientes:

  * Recopilar contenido en directo mediante varios protocolos de streaming en vivo (por ejemplo RTMP o Smooth Streaming).
  * (Opcionalmente) Codificar la transmisión en una transmisión con velocidad de bits adaptable.
  * Mostrar una vista previa de la secuencia en vivo.
  * modos de registro y almacén de contenido de hello ingerida en orden toobe más adelante (vídeo bajo demanda)
  * Entregar contenido de Hola a través de protocolos de transmisión por secuencias comunes (por ejemplo, MPEG DASH, Smooth, HLS) directamente los clientes de tooyour o tooa red de entrega de contenido (CDN) para su distribución posterior.

**Servicios de multimedia de Microsoft Azure** (AMS) proporciona Hola tooingest de capacidad, codificar, obtener una vista previa, almacenar y entregar el contenido de transmisión por secuencias en directo.

Cuando se entrega el contenido toocustomers su objetivo es toodeliver un dispositivo de vídeo toovarious de alta calidad en condiciones de red diferente. tooachieve esto, utilice live codificadores tooencode la secuencia de vídeo de secuencia tooa multibits (velocidad de bits adaptable).  tootake atención de transmisión por secuencias en dispositivos diferentes, utilice los servicios multimedia [empaquetado dinámico](media-services-dynamic-packaging-overview.md) toodynamically volver a empaquetar los protocolos de toodifferent de secuencia. Servicios multimedia admite la entrega de hello siguiendo las tecnologías de streaming de velocidad de bits adaptativa: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.

En los servicios de multimedia de Azure, **canales**, **programas**, y **StreamingEndpoints** identificador hello todos live streaming funcionalidades incluidas introducción, el formato, DVR, redundancia, escalabilidad y seguridad.

Un **canal** representa una canalización para procesar contenido de streaming en vivo. Un canal puede recibir activo flujos en hello siguientes formas de entrada:

* Un codificador en directo local envía varias velocidades de bits **RTMP** o **Smooth Streaming** (MP4 fragmentado) toohello canal que está configurado para **acceso directo** entrega. Hola **paso a través** entrega resulta secuencias Hola ingerida atraviesan **canal**s sin ningún procesamiento adicional. Puede usar Hola siguientes codificadores en directo que generan Smooth Streaming de velocidades de bits: MediaExcel, Ateme, Imagine las comunicaciones, Envivio, Cisco y Elemental. Hello siguientes codificadores en directo de salida RTMP: transcodificadores Adobe Flash Media Live codificador (FMLE), Telestream Wirecast, Haivision, Teradek y Tricaster.  Un codificador en directo también puede enviar un canal de tooa de secuencia de velocidad de bits única que no está habilitado para la codificación en directo, pero no se recomienda. Cuando se solicita, servicios multimedia transmite hello secuencia toocustomers.

  > [!NOTE]
  > Con un método paso a través de forma hello más económica toodo streaming en directo cuando realiza varios eventos durante un largo período de tiempo, y ya se ha invertido en codificadores locales. Consulte los detalles en [Precios de Servicios multimedia](https://azure.microsoft.com/pricing/details/media-services/) .
  > 
  > 
* Un codificador en directo local envía una secuencia de velocidad de bits única canal toohello tooperform habilitado live codificar con servicios multimedia en uno de hello siguientes formatos: RTMP o Smooth Streaming (MP4 fragmentado). También se admite RTP (MPEG-TS), siempre que tengan un centro de datos de Azure toohello conexión dedicada. se conocen toowork con canales de este tipo de salida de Hello siguientes codificadores en directo con RTMP: Telestream Wirecast, FMLE. Hola canal, a continuación, realiza la codificación en directo de Hola entrante velocidad de bits única secuencia tooa bits múltiple (adaptable) secuencia de vídeo. Cuando se solicita, servicios multimedia transmite hello secuencia toocustomers.

A partir de la versión 2.10 de servicios multimedia de hello, cuando se crea un canal, puede especificar de qué manera desea para el flujo de entrada de canal tooreceive hello y si desea o no que para hello canal tooperform live codificación de la secuencia. Tiene dos opciones:

* **Ninguno** (paso a través): especifique este valor si piensa toouse un codificador en directo local que dará como resultado el flujo de bits múltiple (una secuencia de acceso directo). En este caso, Hola de secuencia entrante pasa toohello sin ninguna codificación de salida. Este es el comportamiento de Hola de una versión anterior too2.10 de canal.  
* **Estándar** : elija este valor, si tiene previsto toouse servicios multimedia tooencode la secuencia de velocidad de bits toomulti de secuencia en directo de velocidad de bits única. Este método es más económico para la escalación vertical rápida para eventos poco frecuentes. Tenga en cuenta que hay un impacto en la facturación de codificación en directo y debe recordar que salir de un canal de codificación en directo en el estado de "Running" hello supondrán un coste adicional de facturación.  Se recomienda detener los canales de ejecución inmediatamente después de los eventos de transmisión por secuencias en directo es tooavoid completa cargos adicionales por hora.

## <a name="comparison-of-channel-types"></a>Comparación de tipos de canales
La tabla siguiente proporciona a una guía toocomparing Hola dos canales tipos admitidos en los servicios multimedia

| Característica | Canal de paso a través | Canal estándar |
| --- | --- | --- |
| Entrada de velocidad de bits única se codifica en varias velocidades de bits en la nube de Hola |No |Sí |
| Resolución máxima, número de capas |1080p, 8 capas, 60+fps |720p, 6 capas, 30 fps |
| Protocolos de entrada |RTMP, Smooth Streaming |RTMP, Smooth Streaming y RTP |
| Precio |Vea hello [página de precios](https://azure.microsoft.com/pricing/details/media-services/) y haga clic en la ficha "Vídeo en vivo" |Vea hello [página de precios](https://azure.microsoft.com/pricing/details/media-services/) |
| Tiempo de ejecución máximo |24x7 |8 horas |
| Compatibilidad con inserción de tabletas táctiles |No |Sí |
| Compatibilidad con señalización de anuncios |No |Sí |
| Títulos CEA 608/708 de paso a través |Sí |Sí |
| Fuente de toorecover de capacidad de obstrucciones breves de contribución |Sí |No (el canal comenzará a usar la tableta táctil transcurridos más de 6 segundos sin datos de entrada) |
| Compatibilidad con GOP de entrada no uniformes |Sí |No: la entrada debe ser GOP de 2 s fijos |
| Compatibilidad con la entrada de la velocidad de fotogramas variable |Sí |No: la entrada debe ser una velocidad de fotogramas fija.<br/>Se tolerarán pequeñas variaciones, por ejemplo, durante las escenas con grandes movimientos. Pero el codificador no puede quitar too10 fotogramas por segundo. |
| Apagado automático de canales cuando se pierde la fuente de entrada |No |Después de 12 horas, si no hay ningún programa en ejecución |

## <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>Uso de canales que reciben streaming en vivo con velocidad de bits múltiple de codificadores locales (paso a través)
Hello siguiente diagrama muestra hello las partes principales de la plataforma de hello AMS que intervienen en hello **acceso directo** flujo de trabajo.

![Flujo de trabajo activo](./media/media-services-live-streaming-workflow/media-services-live-streaming-current.png)

Para más información, consulte [Uso de canales que reciben streaming en vivo con velocidad de bits múltiple de codificadores locales](media-services-live-streaming-with-onprem-encoders.md).

## <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>Trabajar con los canales que son habilitado tooperform live codificar con servicios multimedia de Azure
Hello siguiente diagrama muestra hello principal partes de plataforma de AMS Hola que intervienen en el flujo de trabajo de Streaming en directo donde un canal está habilitado tooperform live codificar con servicios multimedia.

![Flujo de trabajo activo](./media/media-services-live-streaming-workflow/media-services-live-streaming-new.png)

Para obtener más información, consulte [trabajar con los canales que es habilitado tooPerform Live codificar con servicios multimedia de Azure](media-services-manage-live-encoder-enabled-channels.md).

## <a name="description-of-a-channel-and-its-related-components"></a>Descripción de un canal y sus componentes relacionados
### <a name="channel"></a>canal
En Servicios multimedia, los [canal](https://docs.microsoft.com/rest/api/media/operations/channel)es son los responsables de procesar el contenido de streaming en vivo. Un canal proporciona un extremo de entrada (URL de introducción) que, a continuación, proporcionar transcodificador tooa. canal de Hello recibe las secuencias de entrada en directo de Transcodificador de Hola y pone a disposición de streaming a través de uno o más StreamingEndpoints. Los canales también proporcionan un extremo de vista previa (URL de vista previa) que use toopreview y validar las secuencias antes del procesamiento y entrega.

Puede obtener Hola introducir la dirección URL y la dirección URL de vista previa de hello al crear el canal de Hola. tooget estas direcciones URL, canal de hello no tiene toobe en estado de hello iniciado. Cuando esté listo toostart insertar datos de un transcodificador en vivo en canal de hello, se debe iniciar el canal de Hola. Una vez Hola transcodificador inicia la introducción de datos, puede obtener una vista previa de la secuencia.

Cada cuenta de Servicios multimedia puede contener varios canales, varios programas y varios StreamingEndpoints. Función de necesidades de ancho de banda y seguridad hello, servicios de StreamingEndpoint pueden ser tooone dedicado o más canales. Puede extraer cualquier StreamingEndpoint de cualquier canal.

### <a name="program"></a>Programa
A [programa](https://docs.microsoft.com/rest/api/media/operations/program) permite la publicación de hello toocontrol y el almacenamiento de segmentos en una secuencia en directo. Los canales administran los programas. Hello relación de canales y los programas es un medio muy similar tootraditional donde un canal tiene un flujo constante de contenido y un programa es toosome ámbito ha superado el tiempo de evento en ese canal.
Puede especificar Hola número de horas que quiere tooretain Hola registran contenido de programa Hola, establecer hello **ArchiveWindowLength** propiedad. Este valor puede establecerse entre un mínimo de máximo de tooa de 5 minutos de 25 horas.

ArchiveWindowLength también determina la cantidad máxima de Hola de tiempo que los clientes pueden buscar hacia atrás desde la posición actual en vivo de Hola. Programas pueden ejecutarse durante el período de tiempo especificado de hello, pero se descarta continuamente contenido que queda fuera de la longitud de la ventana de Hola. El valor de esta propiedad también determina cuánto tiempo cliente hello pueden alcanzar los manifiestos.

Cada programa está asociado a un recurso. programa de hello toopublish debe crear un localizador para hello asociado activo. Este localizador permitirá toobuild una URL de streaming puede proporcionar a los clientes de tooyour.

Un canal admite hasta toothree programas en ejecución al mismo tiempo para que pueda crear varios archivos de hello mismo flujo entrante. Esto le permite toopublish y archivar diferentes partes de un evento según sea necesario. Por ejemplo, sus necesidades de negocio es tooarchive 6 horas de un programa, pero toobroadcast solo últimos 10 minutos. tooaccomplish, necesita toocreate dos programas en ejecución simultáneos. Un programa se establece tooarchive 6 horas de evento de hello pero no se publica el programa Hola. Hello otro programa es conjunto tooarchive durante 10 minutos y se publica este programa.

## <a name="billing-implications"></a>Implicaciones de facturación
Un canal comienza tan pronto como su estado cambia de "Running" demasiado a través de la API de Hola de facturación.  

Hello tabla siguiente muestra cómo asignan los Estados del canal toobilling Estados Hola API y portal de Azure. Tenga en cuenta que los Estados de hello son ligeramente diferentes entre Hola API y UX de Portal. Tan pronto como un canal está en estado de "Running" Hola a través de la API de Hola o en estado de "Streaming" en el portal de Azure de Hola u Hola "Listo", se activará de facturación.

Canal de hello toostop de facturación aún más, tiene tooStop Hola canal a través de la API de Hola o en hello portal de Azure.
Usted es responsable de detener los canales cuando haya terminado con canal de Hola. Canal de hello toostop de error se producirá en la facturación continua.

> [!NOTE]
> Cuando se trabaja con los canales estándares, AMS automáticamente interrupción cualquier canal que aún está en estado "Running" 12 horas después de que se pierde la fuente de entrada de hello y no hay ningún programa que se ejecuta. Sin embargo, todavía se facturarán Hola Hola de tiempo que canal estaba en estado "Running".
>
>

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

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Temas relacionados
[Especificación de la introducción en directo de MP4 fragmentado de Servicios multimedia de Azure](media-services-fmp4-live-ingest-overview.md)

[Trabajar con los canales que es habilitado tooPerform Live codificar con servicios multimedia de Azure](media-services-manage-live-encoder-enabled-channels.md)

[Uso de canales que reciben streaming en vivo con velocidad de bits múltiple de codificadores locales](media-services-live-streaming-with-onprem-encoders.md)

[Cuotas y limitaciones](media-services-quotas-and-limitations.md).  

[Conceptos de Servicios multimedia de Azure](media-services-concepts.md)
