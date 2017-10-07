---
title: "aaaAzure Media Services telemetría | Documentos de Microsoft"
description: "Este artículo proporciona información general de la telemetría de Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 95c20ec4-c782-4063-8042-b79f95741d28
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 659e1c947a77aad0e4acacb541d95714da4775ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-telemetry"></a>Sistema de telemetría de Azure Media Services

Servicios de multimedia de Azure (AMS) le permite tooaccess los datos de telemetría y las métricas para sus servicios. versión actual de Hola de AMS le permite recopilar datos de telemetría de live **canal**, **StreamingEndpoint**y en directo **archivo** entidades. 

Telemetría se escribe tooa tabla de almacenamiento en una cuenta de almacenamiento de Azure que especifique (normalmente, usaría cuenta de almacenamiento de hello asociada con su cuenta de AMS). 

sistema de telemetría de Hello no administra la retención de datos. Puede quitar los datos de telemetría antiguos hello mediante la eliminación de tablas de almacenamiento de Hola.

Este tema se describe cómo tooconfigure y consumir telemetría Hola AMS.

## <a name="configuring-telemetry"></a>Configuración del sistema de telemetría

Puede configurar la telemetría en la granularidad de nivel de componente. Hay dos niveles de detalle "Normal" y "Detallado". Actualmente, los niveles de devuelven Hola misma información. Se recomienda toouse "Normal. 

Hola después cómo mostrar temas tooenable telemetría:

[Habilitación del sistema de telemetría con .NET](media-services-dotnet-telemetry.md) 

[Habilitación del sistema de telemetría con REST](media-services-rest-telemetry.md)

## <a name="consuming-telemetry-information"></a>uso de información de telemetría

Telemetría se escribe tooan tabla de almacenamiento de Azure en la cuenta de almacenamiento de Hola que especificó al configurar la telemetría para hello cuenta de servicios multimedia. Esta sección describen las tablas de almacenamiento de Hola para las métricas de Hola.

Puede consumir datos de telemetría en uno de hello siguientes maneras:

- Leer datos directamente desde el almacenamiento de tabla de Azure (por ejemplo, mediante Hola SDK de almacenamiento). Para descripción de Hola de tablas de almacenamiento de información de telemetría, vea hello **consumir información de telemetría** en [esto](https://msdn.microsoft.com/library/mt742089.aspx) tema.

O

- Usar compatibilidad de Hola de hello SDK de .NET de servicios multimedia para leer los datos de almacenamiento, como se describe en [esto](media-services-dotnet-telemetry.md) tema. 


esquema de telemetría de Hola que se describe a continuación es toogive diseñado un buen rendimiento dentro de los límites de hello tabla de almacenamiento de Azure:

- Datos se dividen por cuenta de identificador y el identificador de servicio tooallow telemetría de cada toobe servicio consultado de forma independiente.
- Particiones contienen Hola fecha toogive un límite superior razonable en el tamaño de la partición de Hola.
- En el tiempo invertido orden tooallow hello más reciente telemetría elementos toobe las claves de fila se consultan para un servicio determinado.

Esto permitiría muchas toobe consultas comunes de Hola eficaz:

- Descarga paralelas e independientes de datos de servicios específicos
- Recuperación de todos los datos de un servicio determinado en un intervalo de fechas
- Recuperación de datos más recientes de Hola para un servicio.

### <a name="telemetry-table-storage-output-schema"></a>Esquema de salida de almacenamiento de tablas de telemetría

Los datos de telemetría se almacenan en el agregado de una tabla, "TelemetryMetrics20160321" donde "20160321" es la fecha de la tabla de hello creado. El sistema de telemetría creará una tabla independiente para cada día nuevo con el formato de hora 00:00 UTC. se utiliza la tabla de Hello toostore periódica valores como introducción dentro de una determinada ventana de tiempo, bytes enviados, etcetera de velocidad de bits. 

Propiedad|Valor|Ejemplos y notas
---|---|---
PartitionKey|{IDdeCuenta}_{IDdeEntidad}|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66<br/<br/>Hola cuenta identificador se incluye en hello partición toosimplify clave los flujos de trabajo donde varias cuentas de servicios multimedia están escribiendo toohello misma cuenta de almacenamiento.
RowKey|{toomidnight segundos} _ {valor aleatorio}|01688_00199<br/><br/>clave de fila de Hello empieza por número de Hola de consultas de segundos toomidnight tooallow estilo n superior dentro de una partición. Para obtener más información, consulte [este](../cosmos-db/table-storage-design-guide.md#log-tail-pattern) artículo. 
Timestamp|Fecha y hora|Auto marca de tiempo de hello Azure tabla 2016-09-09T22:43:42.241Z
Tipo|tipo de Hola de entidad de Hola que proporciona los datos de telemetría|Channel, StreamingEndpoint y Archive<br/><br/>El tipo de evento es un valor de cadena.
Nombre|nombre de Hola de evento de telemetría de Hola|ChannelHeartbeat y StreamingEndpointRequestLog
ObservedTime|evento de telemetría de Hola Hola tiempo produjo (UTC)|2016-09-09T22:42:36.924Z<br/><br/>Hola observados telemetría Hola envío Hola entidad (por ejemplo, un canal) proporcionan el tiempo. Puede haber problemas de sincronización en los componentes, así que este valor es aproximado.
ServiceID|{IDdeServicio}|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
Propiedades específicas de la entidad|Tal como se define por evento de Hola|StreamName: stream1, Bitrate 10123, etc.<br/><br/>propiedades de Hello restantes se definen para hello proporcionado el tipo de evento. El contenido de la tabla de Azure son pares clave-valor  (es decir, diferentes filas de tabla de hello tengan conjuntos diferentes de propiedades).

### <a name="entity-specific-schema"></a>Esquema específico de la entidad

Hay tres tipos de entradas de datos telemetric específicos de la entidad de que cada uno se inserta con hello después de frecuencia:

- Puntos de conexión de streaming: cada 30 segundos
- Canales activos: cada minuto
- Archivo activo: cada minuto

**Punto de conexión de streaming**

Propiedad|Valor|Ejemplos
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Marca de tiempo creada automáticamente en la tabla de Azure: 2016-09-09T22:43:42.241Z.
Tipo|Tipo|StreamingEndpoint
Nombre|Nombre|StreamingEndpointRequestLog
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|Identificador de servicio|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
HostName|Nombre de host del punto de conexión de Hola|builddemoserver.origin.mediaservices.windows.net
StatusCode|Estado HTTP de los registros|200
ResultCode|Detalles del código de resultado|S_OK
RequestCount|Número total de peticiones de agregación de Hola|3
BytesSent|Bytes agregados enviados|2987358
ServerLatency|Latencia media del servidor (incluido el almacenamiento)|129
E2ELatency|Latencia media de extremo a extremo|250

**Canal activo**

Propiedad|Valor|Ejemplos y notas
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Auto marca de tiempo de hello Azure tabla 2016-09-09T22:43:42.241Z
Tipo|Tipo|Canal
Nombre|Nombre|ChannelHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|Identificador de servicio|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
TrackType|Tipo de pista: audio, vídeo o texto|Audio y vídeo
TrackName|Nombre de la pista de Hola|vídeo/audio_1
Bitrate|Velocidad de bits de la pista|785000
CustomAttributes||   
IncomingBitrate|Velocidad de bits entrante real|784548
OverlapCount|Superposición de Hola de introducción|0
DiscontinuityCount|Interrupción de la pista|0
LastTimestamp|Última marca de tiempo de los datos integrados|1800488800
NonincreasingCount|Recuento de los fragmentos se descarta debido aumentar toonon marca de tiempo|2
UnalignedKeyFrames|Si se reciben fragmentos (en los distintos niveles de calidad) en los que los fotogramas clave no están alineados |True
UnalignedPresentationTime|Si se reciben fragmentos (en los distintos niveles de calidad y pistas) en los que no se encuentra el tiempo de presentación|True
UnexpectedBitrate|True, si la velocidad de bits calculada o real de la pista de audio o vídeo es superior a 40 000 bps, y si el valor de IncomingBitrate es 0 o los valores de IncomingBitrate y actualBitrate difieren en un 50 % |True
Healthy|True, si los valores de <br/>overlapCount, <br/>DiscontinuityCount, <br/>NonIncreasingCount, <br/>UnalignedKeyFrames, <br/>UnalignedPresentationTime y <br/>UnexpectedBitrate<br/> son 0|True<br/><br/>Correcto, es una función compuesta que devuelve false cuando se da alguna de hello después de la suspensión de condiciones:<br/><br/>- OverlapCount > 0<br/>- DiscontinuityCount > 0<br/>- NonincreasingCount > 0<br/>- UnalignedKeyFrames == True<br/>- UnalignedPresentationTime == True<br/>- UnexpectedBitrate == True

**Archivo activo**

Propiedad|Valor|Ejemplos y notas
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Auto marca de tiempo de hello Azure tabla 2016-09-09T22:43:42.241Z
Tipo|Tipo|Archivar
Nombre|Nombre|ArchiveHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|Identificador de servicio|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
ManifestName|URL de programa|asset-eb149703-ed0a-483c-91c4-e4066e72cce3/a0a5cfbf-71ec-4bd2-8c01-a92a2b38c9ba.ism
TrackName|Nombre de la pista de Hola|audio_1
TrackType|Tipo de pista de Hola|Audio y vídeo
CustomAttribute|Cadena hexadecimal que distingue entre pistas diferentes con el mismo nombre y la misma velocidad de bits (ángulos multicámara)|
Bitrate|Velocidad de bits de la pista|785000
Healthy|True, si el valor de FragmentDiscardedCount es 0 y el de ArchiveAcquisitionError, False|True (estos dos valores no están presentes en la métrica de hello pero están presentes en el evento de origen de hello)<br/><br/>Correcto, es una función compuesta que devuelve false cuando se da alguna de hello después de la suspensión de condiciones:<br/><br/>- FragmentDiscardedCount > 0<br/>- ArchiveAcquisitionError == True

## <a name="general-qa"></a>Preguntas y respuestas generales

### <a name="how-tooconsume-metrics-data"></a>¿Cómo los datos de métricas de tooconsume?

Datos de métricas se almacenan como una serie de tablas de Azure en la cuenta de almacenamiento del cliente de Hola. Estos datos pueden utilizarse con hello siguientes herramientas:

- SDK DE AMS
- Explorador de almacenamiento de Microsoft Azure (compatible con formato de valores separados por toocomma de exportación y procesado en Excel)
- API de REST

### <a name="how-toofind-average-bandwidth-consumption"></a>¿Cómo toofind promedio de consumo de ancho de banda?

consumo de ancho de banda promedio de Hello es Media de Hola de BytesSent sobre un intervalo de tiempo.

### <a name="how-toodefine-streaming-unit-count"></a>¿Cómo contar toodefine unidad de streaming?

Hola, número de unidades de transmisión por secuencias se puede definir como Hola máximo rendimiento desde los extremos de streaming del servicio de hello dividido por el rendimiento de máximo de Hola de un extremo de streaming. Hola pico utilizable el rendimiento de un extremo de streaming es de 160 Mbps.
Por ejemplo, suponga que el rendimiento de máximo de Hola de servicio de un cliente es 40 MBps (Hola valor máximo de BytesSent sobre un intervalo de tiempo). A continuación, hello recuento de unidad de transmisión por secuencias es igual too(40 MBps) * /(160 Mbps) (8 bits/bytes) = 2 unidades de transmisión por secuencias.

### <a name="how-toofind-average-requestssecond"></a>¿La media de toofind solicitudes/segundo?

promedio hello toofind de solicitudes por segundo, calcula el número promedio de Hola de solicitudes (RequestCount) sobre un intervalo de tiempo.

### <a name="how-toodefine-channel-health"></a>¿Cómo toodefine canal mantenimiento?

Estado de canal se puede definir como una función booleana de composición que sea false cuando cualquiera de las condiciones siguientes de Hola mantiene:

- OverlapCount > 0
- DiscontinuityCount > 0
- NonincreasingCount > 0
- UnalignedKeyFrames == True 
- UnalignedPresentationTime == True 
- UnexpectedBitrate == True


### <a name="how-toodetect-discontinuities"></a>¿Cómo toodetect discontinuidades?

discontinuidades toodetect, buscar todas las entradas de datos de canal donde DiscontinuityCount > 0. marca de tiempo de Hello correspondiente ObservedTime indica las horas de hello en que se produjo discontinuidades Hola.

### <a name="how-toodetect-timestamp-overlaps"></a>¿Cómo se superpone a marca de tiempo de toodetect?

superposiciones de marca de tiempo toodetect, buscar todas las entradas de datos de canal donde OverlapCount > 0. marca de tiempo de Hello correspondiente ObservedTime indica Hola veces en qué Hola se superpone a marca de tiempo se ha producido.

### <a name="how-toofind-streaming-request-failures-and-reasons"></a>¿Cómo toofind streaming solicitar errores y motivos?

errores de solicitud de transmisión por secuencias de toofind y motivos, buscar todas las entradas de datos de transmisión por secuencias extremo donde ResultCode no se tooS_OK igual. campo de StatusCode correspondiente de Hola indica la razón de Hola de error en la solicitud Hola.

### <a name="how-tooconsume-data-with-external-tools"></a>¿Cómo tooconsume datos con herramientas externas?

Datos telemetric pueden procesar y visualizar con hello siguientes herramientas:

- PowerBI
- Application Insights
- Azure Monitor (anteriormente conocido como Shoebox)
- El panel en tiempo real de AMS
- Azure Portal (pendiente de publicación)

### <a name="how-toomanage-data-retention"></a>¿La retención de datos de toomanage?

sistema de telemetría de Hello no proporciona administración de la retención de datos o la eliminación automática anterior registros. Por lo tanto, es necesario toomanage y elimine manualmente los registros antiguos de la tabla de almacenamiento de Hola. Puede hacer referencia toostorage SDK para saber cómo toodo lo.

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
