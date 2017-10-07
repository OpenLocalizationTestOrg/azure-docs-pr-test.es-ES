---
title: "Conexión de datos: entradas de flujo de datos desde una transmisión de eventos | Microsoft Docs"
description: "Obtenga información acerca de cómo configurar una tooStream de conexión de datos denominado 'entradas' del análisis. Entre las entradas se incluyen una transmisión de datos de los eventos y también datos de referencia."
keywords: "transmisión de datos, conexión de datos, transmisión de eventos"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 8155823c-9dd8-4a6b-8393-34452d299b68
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/05/2017
ms.author: samacha
ms.openlocfilehash: be2008f159061c5c9be9d0314c27fa67193e3269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-connection-learn-about-data-stream-inputs-from-events-toostream-analytics"></a>Conexión de datos: Obtenga información acerca de los datos entradas de flujo de eventos tooStream análisis
trabajo de análisis de transmisiones de datos conexión tooa Hello es una secuencia de eventos de un origen de datos, que es lo que se conoce tooas Hola trabajo *entrada*. Stream Analytics cuenta con integración de primera clase con orígenes de flujo de datos de Azure, como, por ejemplo, [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) y [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/). Estos orígenes pueden ser de Hola de entrada misma suscripción de Azure como su trabajo de análisis o de otra suscripción.

## <a name="data-input-types-data-stream-and-reference-data"></a>Tipos de entrada de datos: datos de referencia y de transmisión de datos
Cuando se insertan datos tooa origen de datos, es ha consumido por el trabajo de análisis de transmisiones de Hola y el procesamiento en tiempo real. Las entradas se dividen en dos tipos distintos: entradas de flujo de datos y entradas de datos de referencia.

### <a name="data-stream-inputs"></a>Entradas de secuencia de datos
Un flujo de datos es una secuencia ilimitada de eventos a lo largo del tiempo. Los trabajos de Stream Analytics deben incluir, como mínimo, una entrada de flujo de datos. Event Hubs, IoT Hub y and Blob Storage se admiten como orígenes de entrada de flujo de datos. Los concentradores de eventos son toocollect usa secuencias de eventos desde varios dispositivos y servicios. Es posible que estos flujos incluyan fuentes de actividades de redes sociales, información bursátil o datos de sensores. Centros de IoT son datos toocollect optimizada de los dispositivos conectados en escenarios de Internet de las cosas (IoT).  Blob Storage puede usarse como origen de entrada para la ingesta de conjuntos masivos de datos en forma de flujo, como, por ejemplo, archivos de registro.  

### <a name="reference-data"></a>Datos de referencia
Stream Analytics también admite la entrada de *datos de referencia*. Se trata de datos auxiliares que son estáticos o cambian lentamente. Suelen usarse para realizar correlaciones y búsquedas. Por ejemplo, podría unir los datos en el flujo de datos Hola entrada toodata en los datos de referencia de hello, hasta realizaría una toolook de combinación SQL valores estáticos. Almacenamiento de blobs de Azure está actualmente Hola solo admitido el origen de entrada de datos de referencia. BLOB de origen de datos de referencia se limitan too100 MB de tamaño.

toolearn toocreate entradas de datos de referencia, vea [utilizar datos de referencia](stream-analytics-use-reference-data.md).  

## <a name="create-data-stream-input-from-event-hubs"></a>Creación de una entrada de flujo de datos desde Event Hubs

Azure Event Hubs ofrece consumidores de eventos de publicación y suscripción muy escalables. Un concentrador de eventos puede recopilar millones de eventos por segundo, por lo que le permitirán procesar y analizar Hola grandes cantidades de datos generados por los dispositivos conectados y las aplicaciones. Event Hubs y Stream Analytics juntos ofrecen una solución de extremo a extremo para el análisis en tiempo real: Event Hubs permite introducir eventos en Azure en tiempo real y los trabajos de Stream Analytics pueden procesarlos en tiempo real. Por ejemplo, puede enviar clics en web, las lecturas del sensor o tooEvent de eventos de registro en línea los concentradores. Puede crear trabajos de análisis de transmisiones toouse centros de eventos como secuencias de datos de entrada de hello en tiempo real filtrar, agregar y correlación.

marca de tiempo de saludo predeterminado de eventos procedentes de concentradores de eventos de análisis de transmisiones es llegó marca de tiempo de Hola que Hola evento de concentrador de eventos de hello, que es `EventEnqueuedUtcTime`. tooprocess Hola datos como una secuencia con una marca de tiempo de carga del evento hello, debe utilizar hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) palabra clave.

### <a name="consumer-groups"></a>Grupos de consumidores
Debe configurar cada toohave de entrada de concentrador de eventos de análisis de transmisiones en su propio grupo de consumidores. Cuando un trabajo contiene una autocombinación o tiene varias entradas, es posible que alguna entrada pueda leerla más de un lector de bajada. Esta situación afecta al número de Hola de lectores en un grupo único consumidor. tooavoid que sobrepasen Hola centros de eventos límite de cinco lectores por grupo de consumidores por partición, es un toodesignate de práctica recomendada un consumidor de grupo para cada trabajo de análisis de transmisiones. Además, hay un límite de 20 grupos de consumidores por centro de eventos. Para más información, vea la [Guía de programación de Event Hubs](../event-hubs/event-hubs-programming-guide.md).

### <a name="configure-an-event-hub-as-a-data-stream-input"></a>Configuración de un centro de eventos como entrada de flujo de datos
Hello tabla siguiente explica cada propiedad hello **nueva entrada** hoja Hola portal de Azure cuando se configura un concentrador de eventos como entrada.

| Propiedad | Descripción |
| --- | --- |
| **Alias de entrada** |Un nombre descriptivo que se utiliza en tooreference de consulta del trabajo de hello esta entrada. |
| **Espacio de nombres de Service Bus** |Espacio de nombres de Azure Service Bus, que es un contenedor para un conjunto de entidades de mensajería. Al crear un centro de eventos, también se crea un espacio de nombres de Service Bus. |
| **Nombre del centro de eventos** |nombre de Hola de hello toouse de concentrador de eventos como entrada. |
| **Nombre de directiva de centro de eventos** |Hola directiva de acceso compartido que proporciona el concentrador de eventos de acceso toohello. Cada directiva de acceso compartido tiene un nombre, los permisos establecidos y las claves de acceso. |
| **Grupo de consumidores del centro de eventos** (opcional) |Hola consumidor toouse tooingest datos del grupo de centro de eventos de Hola. Si no se especifica ningún grupo de consumidores, trabajo de análisis de transmisiones de hello usa el grupo de consumidores predeterminado de Hola. Se recomienda usar un grupo de consumidores distinto para cada trabajo de Stream Analytics. |
| **Formato de serialización de eventos** |Hola formato de serialización (JSON, CSV o Avro) Hola entrantes del flujo de datos. |
| **Encoding** | UTF-8 está actualmente en formato de codificación de hello solo admitido. |

Cuando los datos proceden de un concentrador de eventos, deberá toohello de acceso después de campos de metadatos en la consulta de análisis de transmisiones:

| Propiedad | Descripción |
| --- | --- |
| **EventProcessedUtcTime** |hora y fecha de hello ese evento Hola procesó análisis de transmisiones. |
| **EventEnqueuedUtcTime** |hora y fecha de hello ese evento Hola recibió los concentradores de eventos. |
| **PartitionId** |Identificador de partición basado en cero de Hello para el adaptador de entrada de Hola. |

Por ejemplo, uso de estos campos, puede escribir una consulta es similar al siguiente ejemplo de Hola:

````
SELECT
    EventProcessedUtcTime,
    EventEnqueuedUtcTime,
    PartitionId
FROM Input
````

## <a name="create-data-stream-input-from-iot-hub"></a>Creación de una entrada de flujo de datos desde IoT Hub
El centro de Iot de Azure es un servicio de introducción de eventos de suscripción-publicación altamente escalable optimizado para escenarios de IoT.

marca de tiempo de saludo predeterminado de eventos procedentes de un centro de IoT en análisis de transmisiones es marca de tiempo de Hola que Hola eventos llegaron en Centro de IoT hello, que es `EventEnqueuedUtcTime`. tooprocess Hola datos como una secuencia con una marca de tiempo de carga del evento hello, debe utilizar hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) palabra clave.

> [!NOTE]
> Solo pueden procesarse los mensajes enviados con una propiedad `DeviceClient`.
> 
> 

### <a name="consumer-groups"></a>Grupos de consumidores
Debe configurar cada toohave entrada del centro de IoT de análisis de transmisiones en su propio grupo de consumidores. Cuando un trabajo contiene una autocombinación o tiene varias entradas, es posible que alguna entrada pueda leerla más de un lector de bajada. Esta situación afecta al número de Hola de lectores en un grupo único consumidor. tooavoid que sobrepasen hello Azure IoT Hub límite de cinco lectores por grupo de consumidores por partición, es un toodesignate de práctica recomendada un consumidor de grupo para cada trabajo de análisis de transmisiones.

### <a name="configure-an-iot-hub-as-a-data-stream-input"></a>Configuración de una instancia de IoT Hub como entrada de flujo de datos
Hello tabla siguiente explica cada propiedad hello **nueva entrada** hoja Hola portal de Azure cuando se configura un centro de IoT como entrada.

| Propiedad | Descripción |
| --- | --- |
| **Alias de entrada** |Un nombre descriptivo que se utiliza en tooreference de consulta del trabajo de hello esta entrada.|
| **IoT Hub** |nombre de Hola de hello IoT hub toouse como entrada. |
| **Extremo** |punto de conexión de Hello para el centro de IoT Hola.|
| **Nombre de directiva de acceso compartido** |Directiva de acceso de Hello compartido que proporciona acceso toohello IoT concentrador. Cada directiva de acceso compartido tiene un nombre, los permisos establecidos y las claves de acceso. |
| **Clave de directiva de acceso compartido** |clave de acceso compartido de Hello usa centro de IoT de tooauthorize acceso toohello. |
| **Grupo de consumidores** (opcional) |Hola consumidor toouse tooingest datos del grupo de centro de IoT Hola. Si no se especifica ningún grupo de consumidores, un trabajo de análisis de transmisiones usa el grupo de consumidores de hello predeterminado. Se recomienda usar un grupo de consumidores distinto para cada trabajo de Stream Analytics. |
| **Formato de serialización de eventos** |Hola formato de serialización (JSON, CSV o Avro) Hola entrantes del flujo de datos. |
| **Encoding** |UTF-8 está actualmente en formato de codificación de hello solo admitido. |

Cuando los datos proceden de un centro de IoT, deberá toohello de acceso después de campos de metadatos en la consulta de análisis de transmisiones:

| Propiedad | Descripción |
| --- | --- |
| **EventProcessedUtcTime** |Hola fecha y hora se procesó dicho evento Hola. |
| **EventEnqueuedUtcTime** |hora y fecha de hello ese evento Hola recibió centro de IoT Hola. |
| **PartitionId** |Identificador de partición basado en cero de Hello para el adaptador de entrada de Hola. |
| **IoTHub.MessageId** | Un identificador que ha utilizado la comunicación bidireccional toocorrelate en Centro de IoT. |
| **IoTHub.CorrelationId** |Identificador que se usa en las respuestas a mensajes y en los comentarios en IoT Hub. |
| **IoTHub.ConnectionDeviceId** |Identificador de la autenticación de Hello usa toosend este mensaje. Este valor se marca en los mensajes servicebound por centro de IoT Hola. |
| **IoTHub.ConnectionDeviceGenerationId** |Id. de generación de Hola de hello había autenticado dispositivo que usa toosend este mensaje. Este valor se marca en los mensajes servicebound por centro de IoT Hola. |
| **IoTHub.EnqueuedTime** |hora de Hello cuando recibió mensajes de bienvenida del centro de IoT Hola. |
| **IoTHub.StreamId** |Una propiedad de evento personalizado agregada por dispositivo de remitente de Hola. |


## <a name="create-data-stream-input-from-blob-storage"></a>Creación de una entrada de flujo de datos desde Blob Storage
Para escenarios con grandes cantidades de datos no estructurados toostore en la nube de hello, almacenamiento de blobs de Azure ofrece una solución escalable y rentable. Los datos de Blob Storage suelen considerarse datos en reposo. Pero, Stream Analytics puede procesarlos como flujo de datos. Un escenario típico de entradas de Blob Storage con Stream Analytics es el procesamiento de registros. En este escenario, los datos de telemetría se ha capturado desde un sistema y necesidades toobe analiza y procesa datos con significado tooextract.

Hola marca de tiempo predeterminado de los eventos de almacenamiento de blobs de análisis de transmisiones es marca de tiempo de Hola que Hola blob se modificó por última vez, que es `BlobLastModifiedUtcTime`. tooprocess Hola datos como una secuencia con una marca de tiempo de carga del evento hello, debe utilizar hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) palabra clave.

El formato CSV entradas *requieren* un toodefine de fila de encabezado campos de conjunto de datos de Hola. Además, todos los campos de fila de encabezado deben ser únicos.

> [!NOTE]
> Análisis de transmisiones no admite la adición de tooan contenido de blob existente. Análisis de transmisiones van a ver un blob en una sola vez y no se procesan los posibles cambios producidos en el blob de hello después de que el trabajo de hello ha leído los datos de Hola. Una práctica recomendada está tooupload todos los datos de hello una vez y, a continuación, no agregar el almacén de blobs de toothat de eventos.
> 

### <a name="configure-blob-storage-as-a-data-stream-input"></a>Configuración de Blob Storage como entrada de flujo de datos

Hello tabla siguiente explica cada propiedad hello **nueva entrada** hoja Hola portal de Azure cuando se configura el almacenamiento de blobs como entrada.

| Propiedad | Descripción |
| --- | --- |
| **Alias de entrada** | Un nombre descriptivo que se utiliza en tooreference de consulta del trabajo de hello esta entrada. |
| **Cuenta de almacenamiento** | nombre de Hola de cuenta de almacenamiento de Hola donde se encuentran los archivos de blob de Hola. |
| **Clave de cuenta de almacenamiento** | clave secreta de Hello asociado a la cuenta de almacenamiento de Hola. |
| **Contenedor** | contenedor de Hello para la entrada de blob de Hola. Los contenedores proporcionan una agrupación lógica para los blobs almacenados en hello servicio de blobs de Microsoft Azure. Al cargar un servicio de almacenamiento de blobs de Azure de blob toohello, debe especificar un contenedor para dicho blob. |
| **Patrón de ruta de acceso** (opcional) | ruta de acceso de archivo Hello usa blobs de hello toolocate dentro del contenedor especificado de Hola. En la ruta de acceso de hello, puede especificar una o más instancias de hello después de tres variables: `{date}`, `{time}`, o`{partition}`<br/><br/>Ejemplo 1: `cluster1/logs/{date}/{time}/{partition}`<br/><br/>Ejemplo 2: `cluster1/logs/{date}`<br/><br/>Hola `*` carácter no es un valor permitido para el prefijo de ruta de acceso de Hola. Solo se permiten <a HREF="https://msdn.microsoft.com/library/azure/dd135715.aspx">caracteres de Blob de Azure</a>. |
| **Formato de fecha** (opcional) | Si usa Hola fecha variable de ruta de acceso de hello, Hola en qué Hola se organizan los archivos de formato de fecha. Ejemplo: `YYYY/MM/DD` |
| **Formato de hora** (opcional) |  Si usas variable en tiempo de hello en la ruta de acceso de hello, Hola en qué Hola se organizan los archivos de formato de hora. Actualmente, el valor de hello solo admitido es `HH`. |
| **Formato de serialización de eventos** | Hola formato de serialización (JSON, CSV o Avro) para las secuencias de datos entrantes. |
| **Encoding** | Para CSV y JSON, UTF-8 es actualmente Hola solo admitido formato de codificación. |

Cuando los datos proceden de un origen de almacenamiento de blobs, deberá toohello de acceso después de campos de metadatos en la consulta de análisis de transmisiones:

| Propiedad | Descripción |
| --- | --- |
| **BlobName** |nombre de Hello del blob de entrada de Hola que Hola eventos que proviene. |
| **EventProcessedUtcTime** |hora y fecha de hello ese evento Hola procesó análisis de transmisiones. |
| **BlobLastModifiedUtcTime** |hora y fecha de hello blob Hola se modificó por última vez. |
| **PartitionId** |Identificador de partición basado en cero de Hello para el adaptador de entrada de Hola. |

Por ejemplo, uso de estos campos, puede escribir una consulta es similar al siguiente ejemplo de Hola:

````
SELECT
    BlobName,
    EventProcessedUtcTime,
    BlobLastModifiedUtcTime
FROM Input
````

## <a name="get-help"></a>Obtener ayuda
Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes
Ha obtenido información sobre las opciones de conexión de datos de Azure para sus trabajos de Análisis de transmisiones. toolearn más información sobre análisis de transmisiones, consulte:

* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
