---
title: "especificación de introducción de aaaAzure Media Services live MP4 fragmentado | Documentos de Microsoft"
description: "Esta especificación describe el protocolo de Hola y el formato fragmentado MP4-based live streaming ingesta de servicios multimedia de Azure. Puede usar eventos en directo de toostream de servicios multimedia de Azure y difundir contenido en tiempo real mediante el uso de Azure como plataforma de nube de Hola. Este documento también describe las prácticas recomendadas para crear mecanismos de ingesta en vivo sólidos y de alta redundancia."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 43fac263-a5ea-44af-8dd5-cc88e423b4de
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 0c191f8d6c5a595621feaba0e571fb984b666f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-fragmented-mp4-live-ingest-specification"></a>Especificación de la introducción en directo de MP4 fragmentado de Azure Media Services
Esta especificación describe el protocolo de Hola y el formato fragmentado MP4-based live streaming ingesta de servicios multimedia de Azure. Servicios multimedia proporciona un servicio de transmisión por secuencias en directo que los clientes pueden usar eventos en directo de toostream y difundir contenido en tiempo real mediante el uso de Azure como plataforma de nube de Hola. Este documento también describe las prácticas recomendadas para crear mecanismos de ingesta en vivo sólidos y de alta redundancia.

## <a name="1-conformance-notation"></a>1. Notación de cumplimiento
Hello palabras clave "debe", "no debe," "Requerido", "Se tendrá que", "no deberá," "Debe", "No debería," "Recomendado", "MAY","y"Opcional"en este documento son toobe lo interpretado como que se describen en RFC 2119.

## <a name="2-service-diagram"></a>2. Diagrama del servicio
Hello siguiente diagrama muestra arquitectura de alto nivel de Hola de hello en vivo de servicio en los servicios multimedia de transmisión por secuencias:

1. Un codificador en directo inserta toochannels fuentes en directo que se crea y se suministra a través de hello SDK de servicios multimedia de Azure.
2. Canales, programas y los extremos de streaming en hello todos live streaming funcionalidades, incluida la introducción, formato, el identificador de servicios multimedia en la nube de DVR, la seguridad, la escalabilidad y la redundancia.
3. Opcionalmente, los clientes pueden elegir toodeploy una capa de red de entrega de contenido de Azure entre Hola punto de conexión y los puntos de conexión de cliente de Hola de transmisión por secuencias.
4. Secuencia de puntos de conexión de cliente de hello extremo de streaming a través de protocolos de transmisión por secuencias adaptativa HTTP. Algunos ejemplos son Microsoft Smooth Streaming, Dynamic Adaptive Streaming sobre HTTP (DASH o MPEG-DASH) y Apple HTTP Live Streaming (HLS).

![flujo de ingestión][image1]

## <a name="3-bitstream-format--iso-14496-12-fragmented-mp4"></a>3. Formato de secuencia de bits: MP4 fragmentado según ISO 14496-12
Hello formato de transmisión por secuencias en directo de introducción se describe en este documento se basa en [ISO-14496-12]. Consulte [[MS-SSTR]](http://msdn.microsoft.com/library/ff469518.aspx) para una explicación detallada del formato MP4 fragmentado y de las extensiones tanto para archivos de vídeo bajo demanda como para la ingesta de streaming en vivo.

### <a name="live-ingest-format-definitions"></a>Definiciones de formato de introducción en directo
Hello lista siguiente describen las definiciones que se aplican toolive Introducción a servicios multimedia de Azure de formato especiales:

1. Hola **ftyp**, **cuadro del manifiesto de servidor de Live**, y **moov** cuadros deben enviarse con cada solicitud (HTTP POST). Estos cuadros deben enviarse al principio de Hola de secuencia de Hola y cualquier momento codificador Hola debe volver a conectar tooresume flujo de introducción. Para más información, consulte la sección 6 en [1].
2. La sección 3.3.2 en [1] define un cuadro opcional denominado **StreamManifestBox** para la ingestión en vivo. Debido a toohello la lógica de enrutamiento del equilibrador de carga de Azure de hello, mediante este cuadro está en desuso. cuadro de Hello no debe estar presente cuando se recopila en los servicios multimedia. Si el cuadro está presente, Media Services lo omite de modo silencioso.
3. Hola **TrackFragmentExtendedHeaderBox** cuadro definida en 3.2.3.2 en [1] debe estar presente para cada fragmento.
4. Versión 2 de hello **TrackFragmentExtendedHeaderBox** cuadro debe ser toogenerate usa segmentos de medios que tienen direcciones URL idénticas en varios centros de datos. campo de fragmento de índice de Hello es REQUIRED para conmutación por error de entre centros de datos de los formatos de streaming basada en índice como Apple HLS y MPEG-DASH basada en índice. conmutación por error de tooenable entre centros de datos, el índice de fragmento de hello debe sincronizarse a través de varios codificadores y se incrementa en 1 para cada fragmento multimedia sucesivos, incluso en todos los reinicios de codificador o los errores.
5. Sección 3.3.6 en [1] define un cuadro denominado **MovieFragmentRandomAccessBox** (**mfra**) que se pueden enviar al final de Hola de canal de toohello de ingesta en vivo tooindicate final de secuencia (sobrecargas eléctricas). Due toohello introducir lógica de servicios multimedia, utilizando sobrecargas eléctricas está en desuso y Hola **mfra** cuadro para la ingesta en vivo no se enviarán. Si se envía, Media Services lo omite de modo silencioso. estado de hello tooreset de hello introducir punto, se recomienda que use [restablecer el canal](https://docs.microsoft.com/rest/api/media/operations/channel#reset_channels). También se recomienda que use [programa detener](https://msdn.microsoft.com/library/azure/dn783463.aspx#stop_programs) tooend una presentación y la secuencia.
6. duración del fragmento Hola MP4 debe ser una constante, tamaño de hello tooreduce de manifiestos de cliente de Hola. Una duración del fragmento MP4 constante también mejora la heurística de descarga de cliente mediante el uso de Hola de etiquetas de repetición. duración de Hello puede fluctuar toocompensate para velocidades de fotogramas no entero.
7. duración del fragmento Hola MP4 debe estar entre aproximadamente 2 y 6 segundos.
8. Las marcas de tiempo de los fragmentos MP4 y los índices (**TrackFragmentExtendedHeaderBox** `fragment_ absolute_ time` y `fragment_index`) DEBERÍAN llegar en orden ascendente. Aunque los servicios multimedia son fragmentos tooduplicate resistente, tiene limitado fragmentos de tooreorder capacidad según la escala de tiempo de toohello medio.

## <a name="4-protocol-format--http"></a>4. Formato de protocolo: HTTP
En vivo ISO fragmentado la basada en MP4 ingesta de servicios multimedia usa un estándar HTTP POST solicitud tootransmit codificado medios datos de ejecución prolongada que está empaquetados en el servicio de toohello de formato MP4 fragmentado. Cada POST de HTTP envía una completa fragmentado secuencia de bits MP4 ("stream"), desde el principio de hello con cuadros de encabezado (**ftyp**, **cuadro del manifiesto de servidor de Live**, y **moov** cuadros) y continuando con una secuencia de fragmentos (**moof** y **mdat** cuadros). Sintaxis de dirección URL de solicitud HTTP POST de hello, vea la sección 9.2 en [1]. Es un ejemplo de Hola dirección URL de POST: 

    http://customer.channel.mediaservices.windows.net/ingest.isml/streams(720p)

### <a name="requirements"></a>Requisitos
Estos son Hola requisitos detallados:

1. Hello codificador debe iniciarse Hola difundir enviando una solicitud HTTP POST con vacío "cuerpo" (longitud de contenido cero) mediante el uso de Hola la misma dirección URL de recopilación. Esto puede ayudar a codificador Hola detectar rápidamente si el punto de conexión de hello ingesta en vivo es válido y si no hay ninguna autenticación u otras condiciones necesarios. Por el protocolo HTTP, Hola servidor no devolvió una respuesta HTTP hasta hello completa, incluido el cuerpo POST hello, se recibe una solicitud. Dada la naturaleza de ejecución prolongada de Hola de un evento en directo, sin este paso, el codificador de hello podría no ser capaz de toodetect cualquier error hasta que termine de enviar todos los datos de Hola.
2. Codificador de Hello debe controlar los errores o los desafíos de autenticación debido a (1). Si (1) se realiza correctamente con una respuesta 200, continúe.
3. Codificador de Hello debe iniciar una nueva solicitud de HTTP POST con flujo de MP4 de hello fragmentado. carga de Hello debe empezar con los cuadros de encabezado de hello, seguidos de fragmentos. Tenga en cuenta que hello **ftyp**, **cuadro del manifiesto de servidor de Live**, y **moov** cuadros (en este orden) se deben enviar con cada solicitud, incluso si el codificador de hello debe volver a conectarse porque Hola la solicitud anterior finalizó toohello anterior final de secuencia de Hola. 
4. Codificador de Hola debe utilizar la codificación para cargar fragmentada, porque es imposible toopredict Hola todo longitud del contenido de hello activas eventos.
5. Cuando el evento de hello es a través, después de enviar el último fragmento de hello, codificador Hola debe finalizar correctamente Hola fragmentada la secuencia del mensaje (mayoría pilas de cliente HTTP controlen automáticamente) de codificación de transferencia. Codificador de Hello debe esperar para código de hello servicio tooreturn Hola respuesta final y, a continuación, terminan conexión Hola. 
6. Codificador de Hello no debe usar hello `Events()` sustantivo tal como se describe en 9.2 [1] para la ingesta en vivo en los servicios multimedia.
7. Si finaliza la solicitud HTTP POST de Hola u horas con un extremo TCP error toohello anterior del flujo de hello, codificador Hola debe emitir una nueva solicitud POST con una conexión nueva y siga Hola requisitos anteriores. Además, codificador Hola debe reenviar Hola anterior dos fragmentos de MP4 de cada pista en secuencia de Hola y reanudar sin introducir una discontinuidad en la escala de tiempo de hello medio. Volver a enviar Hola últimos dos fragmentos de MP4 de cada pista garantiza que no hay ninguna pérdida de datos. En otras palabras, si una secuencia contiene un sonido y una pista de vídeo y se produce un error en la solicitud POST actual de hello, debe volver a conectar el codificador de Hola y reenvió Hola últimos dos fragmentos de pista de audio de hello, que anteriormente se han enviado correctamente, y Hola dos últimas fragmentos para Hola pista de vídeo, que previamente enviados correctamente, tooensure que no hay ninguna pérdida de datos. Codificador de Hello debe mantener un búfer "forward" de los fragmentos multimedia, que vuelve a enviar cuando se vuelve a conectar.

## <a name="5-timescale"></a>5. Escala de tiempo
[[MS-SSTR] ](https://msdn.microsoft.com/library/ff469518.aspx) describe el uso de Hola de escala de tiempo para **SmoothStreamingMedia** (sección 2.2.2.1), **StreamElement** (sección 2.2.2.3), **StreamFragmentElement**(Sección 2.2.2.6), y **LiveSMIL** (sección 2.2.7.3.1). Si el valor de escala de tiempo de hello no está presente, el valor predeterminado de hello usado es 10.000.000 (10 MHz). Aunque Hola especificación de formato de transmisión por secuencias suave no bloquea el uso de otros valores de escala de tiempo, la mayoría de las implementaciones de codificador usa este valor predeterminado toogenerate valor (10 MHz) Smooth Streaming introducir datos. Due toohello [empaquetado dinámico de Azure Media](media-services-dynamic-packaging-overview.md) característica, se recomienda usar una escala de tiempo de 90 KHz para secuencias de vídeo y 44,1 KHz o 48.1 KHz para secuencias de audio. Si se utilizan valores de escala de tiempo diferente para las secuencias diferentes, se debe enviar la escala temporal del nivel de la secuencia de Hola. Para más información, consulte [[MS-SSTR]](https://msdn.microsoft.com/library/ff469518.aspx).     

## <a name="6-definition-of-stream"></a>6. Definición de "secuencia"
Secuencia es Hola unidad básica de operación de ingesta en vivo para crear presentaciones en directo, control de transmisión por secuencias de conmutación por error y escenarios de redundancia. "Secuencia" se define como una única secuencia de bits MP4 fragmentada que puede contener una sola pista o varias pistas. Una presentación en directo completa puede contener uno o varios flujos, dependiendo de los codificadores en directo de hello configuración de Hola. Hello en los ejemplos siguientes muestra distintas opciones de uso de secuencias toocompose una presentación en directo completa.

**Ejemplo:** 

Un cliente desea toocreate una presentación de transmisión por secuencias en directo que incluye Hola siguientes velocidades de bits de audio/vídeo:

Vídeo: 3000 kbps, 1500 kbps, 750 kbps

Audio: 128 kbps

### <a name="option-1-all-tracks-in-one-stream"></a>Opción 1: todas las pistas de una secuencia
En esta opción, un único codificador genera todas las pistas de audio y vídeo y, a continuación, las agrupa en una secuencia de bits MP4 fragmentada. Hola fragmentado MP4 secuencia de bits, a continuación, se envía a través de una sola conexión de HTTP POST. En este ejemplo, solo hay una secuencia para esta presentación en directo.

![Secuencias: una pista][image2]

### <a name="option-2-each-track-in-a-separate-stream"></a>Opción 2: Cada pista de una secuencia independiente
En esta opción, codificador Hola coloca una pista en cada secuencia de bits de fragmento MP4 y, a continuación, registra todas las secuencias de Hola a través de conexiones HTTP independientes. Esto se puede realizar con un codificador o con varios. ingesta en vivo de Hello ve esta presentación en directo, tal y como se compone de cuatro secuencias.

![Secuencias: pistas independientes][image3]

### <a name="option-3-bundle-audio-track-with-hello-lowest-bitrate-video-track-into-one-stream"></a>Opción 3: Agrupar pista de audio con la pista de vídeo de velocidad de bits más baja hello en una secuencia
En esta opción, el cliente de hello elige pista de audio de Hola de toobundle con pista de vídeo de velocidades de bits bajas de hello en la secuencia de bits de un fragmento MP4 y deje Hola otros dos pistas de vídeo como secuencias independientes. 

![Secuencias: pistas de audio y vídeo][image4]

### <a name="summary"></a>Resumen
Esta no es una lista exhaustiva de todas las opciones de ingestión posibles para este ejemplo. De hecho, cualquier agrupación de pistas en secuencias es compatible con la ingesta en vivo. Los clientes y los proveedores de codificación pueden elegir sus propias implementaciones en función de la complejidad de ingeniería, de la capacidad del codificador, y de las consideraciones de redundancia y conmutación por error. Sin embargo, en la mayoría de los casos, hay sólo una pista de audio para toda la presentación en directo Hola. Por lo tanto, es importante tooensure Hola buen estado del programa Hola a introducir flujo que contiene la pista de audio de Hola. Esta consideración a menudo como resultado poner pista de audio de hello en su propio flujo (como en la opción 2) o unión con la pista de vídeo de velocidades de bits bajas hello (como en la opción 3). Además, para una mejor redundancia y tolerancia a errores, enviar Hola misma pista de audio en dos secuencias diferentes (opción 2 con pistas de audio redundantes) o agrupación pista de audio de hello con al menos dos de pistas de vídeo de velocidades de bits bajas de hello (opción 3 con el audio a secuencias de vídeo de dos menos) es muy recomendable para en vivo en los servicios multimedia de introducción.

## <a name="7-service-failover"></a>7. Conmutación por error del servicio
Dada la naturaleza de Hola de transmisión por secuencias en directo, es fundamental para garantizar la disponibilidad del servicio de Hola Hola compatibilidad con buena conmutación por error. Servicios multimedia es toohandle diseñada diversos tipos de errores, incluidos los errores de red, errores de servidor y problemas de almacenamiento. Cuando se utiliza junto con la lógica adecuada de conmutación por error del lado de codificador en directo de hello, los clientes pueden lograr un servicio de transmisión por secuencias en directo altamente confiable de nube de Hola.

En esta sección, trataremos los escenarios de conmutación por error del servicio. En este caso, error Hola ocurre en algún lugar dentro de servicio de Hola y se manifiesta como un error de red. Estas son algunas recomendaciones para la implementación del codificador Hola para controlar la conmutación por error de servicio:

1. Utilice un tiempo de espera de 10 segundos para establecer la conexión de TCP de Hola. Si una conexión de intento tooestablish Hola tarda más de 10 segundos, anular la operación de Hola y vuelva a intentarlo. 
2. Utilice un tiempo de espera corto para el envío de fragmentos de mensajes de solicitud de hello HTTP. Si la duración del fragmento de MP4 de destino de hello es N segundos, usar un tiempo de espera de envío entre N y 2 N segundos; Por ejemplo, si la duración del fragmento MP4 hello es de 6 segundos, utilice un tiempo de espera de 6 segundos too12. Si se produce un tiempo de espera, restablecer la conexión de hello, abra una conexión nueva y secuencia de reanudación de introducción en las conexiones nuevas Hola. 
3. Mantener un búfer gradual con hello última dos fragmentos de cada pista que se enviaron correctamente y completamente toohello servicio.  Si solicitud HTTP POST de Hola para un flujo de tiempo de espera toohello anterior final de secuencia de Hola o se termina, abrir una nueva conexión y comenzar otra solicitud HTTP POST, enviar encabezados de la secuencia de hello, reenviar Hola última dos fragmentos de cada pista y reanudar el flujo de hello sin Introducción a una discontinuidad en la escala de tiempo de hello medio. Esto reduce la posibilidad de Hola de pérdida de datos.
4. Se recomienda que codificador hello no limitar número de Hola de reintentos tooestablish una conexión o reanudar la transmisión por secuencias cuando se produce un error TCP.
5. Después de un error TCP:
  
    a. se debe cerrar la conexión actual de Hola y debe crearse una nueva conexión para una nueva solicitud HTTP POST.

    b. Hola nueva HTTP POST dirección URL debe ser igual que Hola inicial de dirección URL de POST Hola.
  
    c. Hello nueva HTTP POST debe incluir encabezados de secuencia (**ftyp**, **cuadro del manifiesto de servidor de Live**, y **moov** cuadros) que son encabezados de la secuencia de toohello idénticos en hello inicial POST.
  
    d. deben volver a enviarse dos últimas fragmentos Hola enviados de cada pista y transmisión por secuencias debe reanudar sin introducir una discontinuidad en la escala de tiempo de hello medio. Hola marcas de tiempo de fragmento MP4 debe aumentar de forma continua, incluso a través de solicitudes HTTP POST.
6. Codificador de Hello debe finalizar la solicitud HTTP POST de hello si no se envía datos a una velocidad según la duración del fragmento MP4 Hola.  Una solicitud HTTP POST que no envía datos puede impedir que los servicios multimedia rápidamente desconectando codificador hello en caso de hello de una actualización de servicio. Por esta razón, Hola HTTP POST para dispersas (señal de anuncio) realiza un seguimiento debe ser de corta duración, terminar tan pronto como fragmento disperso Hola se envía.

## <a name="8-encoder-failover"></a>8. Conmutación por error del codificador
Conmutación por error del codificador es el segundo tipo de escenario de conmutación por error que necesita toobe dirigirse para la entrega de transmisión por secuencias en directo-to-end de Hola. En este escenario, condición de error de Hola se produce en el lado del codificador de Hola. 

![conmutación por error del codificador][image5]

Hola siguiendo las expectativas se aplica desde el punto de conexión de hello ingesta en directo cuando se produce la conmutación por error del codificador:

1. Una nueva instancia de codificador debe crearse toocontinue transmisión por secuencias, como se muestra en el diagrama de hello (secuencia de vídeo con línea discontinua de 3000k).
2. DEBE usar Hola misma dirección URL de HTTP POST solicita como Hola de nuevo codificador de Hello error instancia.
3. Hello solicitud POST del nuevo codificador debe incluir Hola mismo fragmentado MP4 cuadros de encabezado como Hola instancia con errores.
4. nuevo codificador de Hello debe sincronizarse correctamente con todos los demás codificadores de ejecución para hello mismo toogenerate de presentación en directo sincronizó muestras de audio/vídeo con los límites del fragmento alineado.
5. nuevo flujo de Hello debe ser semánticamente equivalente con secuencia anterior de hello e intercambiables en los niveles de encabezado y el fragmento de Hola.
6. nuevo codificador de Hello debe intentar toominimize pérdida de datos. Hola `fragment_absolute_time` y `fragment_index` de medios deben aumentar los fragmentos desde punto de Hola donde codificador Hola detuvo la última vez. Hola `fragment_absolute_time` y `fragment_index` debería aumentar de forma continua, pero resulta toointroduce admisible una discontinuidad, si es necesario. Servicios multimedia omite los fragmentos que ya ha recibido y procesado, por lo que es mejor tooerr en lado de Hola de volverlo a enviar fragmentos que toointroduce discontinuidades en la escala de tiempo de hello medio. 

## <a name="9-encoder-redundancy"></a>9. Redundancia del codificador
Para ciertos eventos críticos en directo que petición incluso mayor disponibilidad y calidad de la experiencia, se recomienda usar codificadores redundantes activo-activo tooachieve sin problemas de conmutación por error sin pérdida de datos.

![redundancia del codificador][image6]

Tal y como se muestra en este diagrama, dos grupos de codificadores inserción dos copias de cada secuencia simultáneamente en el servicio de live Hola. Esta configuración se admite porque Media Services puede filtrar fragmentos duplicados según el identificador de secuencia y la marca de tiempo del fragmento. Hola resultante secuencia en directo y de archivo son una sola copia de todas las secuencias de hello es Hola la agregación mejor posible de dos orígenes de Hola. Por ejemplo, en un caso extremo hipotético, siempre que hay un codificador (no tiene toobe Hola uno mismo) ejecutando en un momento dado en el tiempo para cada secuencia, hello resultante de la secuencia en directo desde el servicio de hello es continua sin pérdida de datos. 

requisitos de Hola para este escenario son casi Hola igual como requisitos de hello en caso de "Codificador conmutación por error" ¡hello, con excepción de Hola que se ejecutan segundo conjunto de codificadores de hello en hello mismo tiempo como Hola codificadores principales.

## <a name="10-service-redundancy"></a>10. Redundancia del servicio
Para la distribución global gran redundancia, a veces deben tener desastres regionales toohandle de copia de seguridad entre regiones. Al expandir en la topología de "Redundancia codificador" Hola, los clientes pueden elegir toohave una implementación de servicio redundantes en una región distinta a la que está conectada con el segundo conjunto de Hola de codificadores. Los clientes también pueden trabajar con un toodeploy de proveedor un administrador de tráfico Global delante Hola dos servicio implementaciones tooseamlessly enrutar cliente el tráfico de red de entrega de contenido. requisitos de Hola para los codificadores de hello son idénticos a cómo Hola caso "Redundancia codificador" Hola. Hello solo excepción es que segundo conjunto de Hola de codificadores necesidades toobe que apunta tooa diferentes en vivo extremo de introducción. Hello siguiente diagrama muestra esta configuración:

![redundancia del servicio][image7]

## <a name="11-special-types-of-ingestion-formats"></a>11. Tipos especiales de formatos de ingesta
Esta sección describen los tipos especiales de formatos de ingesta en vivo que están diseñadas toohandle de escenarios concretos.

### <a name="sparse-track"></a>Pista dispersa
Cuando se entrega una presentación de transmisión por secuencias en directo con una experiencia de cliente enriquecido, a menudo es necesario tootransmit sincronizados por tiempo eventos o señala en banda con datos de medios principal de saludo. Un ejemplo de esto es la inserción de anuncios en directo dinámicos. Este tipo de señalización de eventos es diferente del streaming de audio y vídeo regular debido a su naturaleza dispersa. En otras palabras, hello señalización datos normalmente no se producen continuamente, y el intervalo de saludo puede ser difícil toopredict. concepto de Hola de pista dispersa era tooingest diseñada y datos de señalización de difusión en la banda.

Hello pasos siguientes son una implementación recomendada para el consumo de pista dispersa:

1. Cree una secuencia de bits MP4 fragmentada independiente que solo contenga pistas dispersas, sin pistas de audio y vídeo.
2. Hola **cuadro del manifiesto de servidor de Live** tal como se define en la sección 6 en [1], usar hello *parentTrackName* nombre del parámetro toospecify Hola de pista de hello primario. Para más información, consulte la sección 4.2.1.2.1.2 en [1].
3. Hola **cuadro del manifiesto de servidor de Live**, **manifestOutput** debe establecerse demasiado**true**.
4. Dada la naturaleza dispersas de Hola de hello señalar el evento, se recomienda siguiente hello:
   
    a. En principio Hola de evento en vivo de hello, codificador Hola envía cuadros encabezado inicial de hello toohello servicio, lo que permite a pista dispersa de hello servicio tooregister Hola manifiesto de cliente de Hola.
   
    b. codificador Hola debería finalizar la solicitud HTTP POST de hello cuando no están enviando datos. Un HTTP POST de ejecución prolongada que no envía datos pueden impedir que los servicios multimedia rápidamente desconectando codificador hello en caso de hello de un reinicio del servicio update o servidor. En estos casos, el servidor multimedia Hola está bloqueado temporalmente en una operación de recepción en el socket de Hola.
   
    c. Durante el tiempo de hello cuando señalización datos no está disponible, codificador Hola debería cerrar la solicitud HTTP POST de Hola. Mientras está activa la solicitud POST hello, codificador Hola debe enviar los datos.

    d. Al enviar fragmentos dispersos, codificador Hola puede establecer un encabezado content-length explícito, si está disponible.

    e. Al enviar fragmentos dispersas con una nueva conexión, codificador Hola debería empezar a enviar desde los cuadros de encabezado de hello, seguidos de fragmentos de hello nueva. Esto ocurre para los casos en que conmutan por error entre y nueva conexión dispersas Hola se está establecida tooa nuevo servidor que no se ha visto la pista dispersa de hello antes.

    f. fragmento de pista dispersa Hola se vuelve disponible toohello cliente cuando Hola primario pista fragmento correspondiente que tiene un valor de marca de tiempo igual o mayor estará disponible toohello cliente. Por ejemplo, si el fragmento disperso hello tiene una marca de tiempo de t = 1000, se espera que una vez cliente hello ve fragmentar la marca de tiempo 1000 "vídeo" (suponiendo que nombres de pistas de hello primario "vídeo") o versiones posteriores, puede descargar Hola fragmento disperso t = 1000. Tenga en cuenta que Hola señal real podría usarse para una posición diferente en la escala de tiempo de presentación de Hola para su propósito designado. En este ejemplo, del posible que Hola dispersa fragmento de t = 1000 tiene una carga XML, que es para insertar un anuncio en una posición que se unos segundos más tarde.

    g. carga de Hola de fragmentos de pista dispersa puede estar en diferentes formatos (por ejemplo, XML, texto o binario), según el escenario de Hola.

### <a name="redundant-audio-track"></a>Pista de audio redundante
En un HTTP adaptive streaming escenario típico (por ejemplo, Smooth Streaming o guión), a menudo, hay sólo una pista de audio en toda la presentación Hola. A diferencia de las pistas de vídeo, que tienen varios niveles de calidad para hello toochoose de cliente de en condiciones de error, pista de audio de hello puede ser un único punto de error si hello ingesta de secuencia de Hola que contiene la pista de audio de Hola se interrumpe. 

toosolve es compatible con este problema, los servicios multimedia en directo ingesta redundantes de pistas de audio. idea Hello es ese hello misma pista de audio se puede enviar varias veces en diferentes flujos. Aunque hello servicio sólo registra pista de audio de hello una vez en el manifiesto de cliente hello, puede utilizar redundancia pistas de audio como las copias de seguridad para recuperar fragmentos de audio si pista de audio principal hello tiene problemas. tooingest pistas de audio redundantes, codificador Hola debe:

1. Crear Hola pista de audio mismo en varios fragmentos MP4 bitstreams. las pistas de audio redundantes de Hello deben ser semánticamente equivalentes, con hello mismo fragmento de marcas de tiempo y ser intercambiables en el encabezado de Hola y niveles de fragmento.
2. Asegurarse de esa entrada de "audio" Hola Hola Live Server manifiesto (sección 6 en [1]) se hello igual para redundancia todas las pistas de audio.

Hola después de la implementación se recomienda en las pistas de audio redundantes:

1. Envíe cada pista de audio única en una secuencia de manera individual. Además, envíe una secuencia redundante para cada una de estas secuencias de pista de audio, donde segundo flujo de hello solo se diferencia de hello en primer lugar por identificador hello en hello dirección URL de POST de HTTP: {protocolo} :// {dirección del servidor} / {path}/Streams({identifier}) de punto de publicación.
2. Utilice secuencias independientes toosend Hola dos más bajo vídeo velocidades de bits. Cada una de estas secuencias también DEBERÍA contener una copia de cada pista de audio única. Por ejemplo, cuando se admiten varios idiomas, estas secuencias DEBERÍAN contener pistas de audio para cada idioma.
3. Utilizar tooencode de instancias de servidor independiente (codificador) y enviar secuencias de redundancia de hello mencionados en (1) y (2). 

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[image1]: ./media/media-services-fmp4-live-ingest-overview/media-services-image1.png
[image2]: ./media/media-services-fmp4-live-ingest-overview/media-services-image2.png
[image3]: ./media/media-services-fmp4-live-ingest-overview/media-services-image3.png
[image4]: ./media/media-services-fmp4-live-ingest-overview/media-services-image4.png
[image5]: ./media/media-services-fmp4-live-ingest-overview/media-services-image5.png
[image6]: ./media/media-services-fmp4-live-ingest-overview/media-services-image6.png
[image7]: ./media/media-services-fmp4-live-ingest-overview/media-services-image7.png
