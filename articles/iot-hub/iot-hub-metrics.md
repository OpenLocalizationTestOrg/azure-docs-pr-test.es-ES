---
title: "las métricas de aaaUse toomonitor centro de IoT de Azure | Documentos de Microsoft"
description: "Cómo supervisar y toouse centro de IoT de Azure métricas tooassess Hola estado general de los centros de IoT."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a47108fd-f994-4105-b21d-5b8f697b699c
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7d045013fb0229f488e72c93a6f668048b9d5c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-iot-hub-metrics"></a>Comprender las métricas de IoT Hub
Las métricas de centro de IoT ofrecen mejores datos acerca del estado de Hola de recursos de Azure IoT hello en su suscripción de Azure. Habilitar las métricas de centro de IoT se tooassess Hola estado general de los dispositivos de Hola y Hola servicio del centro de IoT conectado tooit. Estadísticas de cara al usuario son importantes porque ayudarle a ver lo que ocurre con los problemas de causa raíz IoT hub- and ayuda sin necesidad de toocontact soporte técnico de Azure.

Las métricas están habilitadas de forma predeterminada. Puede ver las métricas de centro de IoT de hello portal de Azure.

## <a name="how-tooview-iot-hub-metrics"></a>¿Cómo tooview las métricas de centro de IoT
1. Cree un Centro de IoT. Encontrará instrucciones sobre cómo toocreate un centro de IoT en hello [Introducción] [ lnk-get-started] guía.
2. Abra la hoja de Hola de su centro de IoT. Desde aquí, haga clic en **Métricas**.
   
    ![][1]
3. Desde la hoja de métricas de hello, puede ver las métricas de hello para el centro de IoT y crear vistas personalizadas de las métricas. Puede elegir el punto de conexión de los centros de eventos de métricas datos tooan o una cuenta de almacenamiento de Azure toosend haciendo clic en **configuración de diagnóstico**.
   
    ![][2]

## <a name="iot-hub-metrics-and-how-toouse-them"></a>Las métricas de centro de IoT y cómo toouse ellos
Centro de IoT proporciona varias estadísticas de toogive es una visión general del estado de Hola de su centro y Hola número total de dispositivos conectados. Puede combinar información de varias métricas toopaint una imagen más grande del estado de Hola de centro de IoT Hola. Hello en la tabla siguiente describe las métricas de hello que realiza un seguimiento de cada centro de IoT y cómo cada métrica relaciona toohello general estado de Hola centro de IoT.

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|Intentos de envío de mensajes de telemetría|Recuento|Total|Número de toobe intento de telemetría de dispositivo para la nube mensajes enviados tooyour centro de IoT|
|d2c.telemetry.ingress.success|Mensajes de telemetría enviados|Recuento|Total|Número de mensajes de telemetría de dispositivo para la nube enviado correctamente el centro de IoT tooyour|
|c2d.commands.egress.complete.success|Comandos completados|Recuento|Total|Número de comandos en la nube al dispositivo que se completó correctamente por dispositivo de Hola|
|c2d.commands.egress.abandon.success|Comandos abandonados|Recuento|Total|Número de comandos en la nube al dispositivo abandonados por el dispositivo de Hola|
|c2d.commands.egress.reject.success|Comandos rechazados|Recuento|Total|Número de comandos en la nube al dispositivo rechazado por dispositivo de Hola|
|devices.totalDevices|Número total de dispositivos|Recuento|Total|Número de dispositivos registrados tooyour centro de IoT|
|devices.connectedDevices.allProtocol|Dispositivos conectados|Recuento|Total|Centro de IoT tooyour el número de dispositivos conectados|
|d2c.telemetry.egress.success|Mensajes de telemetría entregados|Recuento|Total|Número de veces que los mensajes se han escrito correctamente tooendpoints (total)|
|d2c.telemetry.egress.dropped|Mensajes descartados|Recuento|Total|Número de mensajes quitados porque no coincidían con las rutas y se deshabilitó la ruta de reserva de Hola|
|d2c.telemetry.egress.orphaned|Mensajes huérfanos|Recuento|Total|recuento de Hola de mensajes no coincide con ninguna ruta incluida la ruta de reserva de Hola|
|d2c.telemetry.egress.invalid|Mensajes no válidos|Recuento|Total|Hello número de mensajes no entregados debido tooincompatibility con punto de conexión de Hola|
|d2c.telemetry.egress.fallback|Mensajes que coinciden con la condición de reserva|Recuento|Total|Número de mensajes enviados de extremo de reserva toohello|
|d2c.endpoints.egress.eventHubs|Mensajes entregan tooEvent los extremos del centro|Recuento|Total|Número de veces que los mensajes se trataban tooEvent escrito correctamente los extremos del centro|
|d2c.endpoints.latency.eventHubs|Latencia de mensajes para los puntos de conexión del Centro de eventos|Milisegundos|Media|Hola promedio de latencia entre la entrada de mensaje y el centro de IoT toohello de mensaje de entrada en un punto de conexión de concentrador de eventos, en milisegundos|
|d2c.endpoints.egress.serviceBusQueues|Mensajes entregan tooService puntos de conexión de la cola de Bus|Recuento|Total|Número de veces mensajes se trataban como puntos de conexión de la cola de Bus tooService escrito correctamente|
|d2c.endpoints.latency.serviceBusQueues|Latencia de mensajes para los puntos de conexión de la cola de Service Bus|Milisegundos|Media|Hola promedio de latencia entre la entrada de mensaje y el centro de IoT toohello de mensaje de entrada en un punto de conexión de la cola de Bus de servicio, en milisegundos|
|d2c.endpoints.egress.serviceBusTopics|Mensajes entregan tooService puntos de conexión de tema de Bus|Recuento|Total|Número de veces mensajes se trataban como puntos de conexión de tema de Bus tooService escrito correctamente|
|d2c.endpoints.latency.serviceBusTopics|Latencia de mensajes para los puntos de conexión del tema de Service Bus|Milisegundos|Media|Hola promedio de latencia entre la entrada de mensaje y el centro de IoT toohello de mensaje de entrada en un punto de conexión de tema de Bus de servicio, en milisegundos|
|d2c.endpoints.egress.builtIn.events|Mensajes entregados extremo predefinido toohello (mensajes y eventos)|Recuento|Total|Número de veces que los mensajes se trataban extremo predefinido toohello correctamente escrito (mensajes y eventos)|
|d2c.endpoints.latency.builtIn.events|Latencia de mensajes para punto de conexión Hola integrados (mensajes y eventos)|Milisegundos|Media|Hola promedio de latencia entre la entrada de mensaje y el centro de IoT de mensaje de entrada toohello en extremo predefinido hello (mensajes y eventos), en milisegundos |
|d2c.twin.read.success|Lecturas gemelas correctas de los dispositivos|Recuento|Total|recuento de Hola de correctamente todas las lecturas gemelos iniciadas por el dispositivo.|
|d2c.twin.read.failure|Lecturas gemelas con error de los dispositivos|Recuento|Total|recuento de Hola de todas las no pudo lecturas gemelos iniciadas por el dispositivo.|
|d2c.twin.read.size|Tamaño de la respuesta de las lecturas gemelas de dispositivos|Bytes|Media|promedio de Hello, min y max del todo correcta iniciadas por el dispositivo dos lecturas.|
|d2c.twin.update.success|Actualizaciones gemelas correctas de los dispositivos|Recuento|Total|recuento de Hola de correctamente todas las actualizaciones de gemelas iniciadas por el dispositivo.|
|d2c.twin.update.failure|Actualizaciones gemelas con error de los dispositivos|Recuento|Total|recuento de Hola de todas las actualizaciones de gemelas iniciadas por el dispositivo con error.|
|d2c.twin.update.size|Tamaño de las actualizaciones gemelas de los dispositivos|Bytes|Media|Hola average, min y el tamaño máximo de todos los correcta iniciadas por el dispositivo dos actualizaciones.|
|c2d.methods.success|Invocaciones correctas al método directo|Recuento|Total|recuento de Hola de correctamente todas las llamadas a métodos directas.|
|c2d.methods.failure|Invocaciones al método directo con error|Recuento|Total|recuento de Hola de todas las no pudo llamadas directas.|
|c2d.methods.requestSize|Tamaño de la solicitud de las invocaciones a métodos directos|Bytes|Media|Hola average, min y número máximo de solicitudes de método directo todas correctas.|
|c2d.methods.responseSize|Tamaño de la respuesta de las invocaciones a métodos directos|Bytes|Media|promedio de Hello, min y max de todas las respuestas de método directo correcta.|
|c2d.twin.read.success|Lecturas gemelas correctas del back-end|Recuento|Total|recuento de Hola de correctamente todas las lecturas gemelos iniciado por back-end.|
|c2d.twin.read.failure|Lecturas gemelas con error del back-end|Recuento|Total|recuento de Hola de todas las no pudo lecturas gemelos iniciado por back-end.|
|c2d.twin.read.size|Tamaño de la respuesta de las lecturas gemelas del back-end|Bytes|Media|promedio de Hello, min y max del todo correcta iniciadas por el back end dos lecturas.|
|c2d.twin.update.success|Actualizaciones gemelas correctas del back-end|Recuento|Total|recuento de Hola de correctamente todas las actualizaciones de gemelas iniciado por back-end.|
|c2d.twin.update.failure|Actualizaciones gemelas con error del back-end|Recuento|Total|recuento de Hola de todas las actualizaciones de gemelas iniciado por back-end con error.|
|c2d.twin.update.size|Tamaño de las actualizaciones gemelas del back-end|Bytes|Media|Hola average, min y tamaño máximo de todos los correcta iniciadas por el back end dos actualizaciones.|
|twinQueries.success|Consultas gemelas correctas|Recuento|Total|recuento de Hola de todas las consultas de gemelas correcta.|
|twinQueries.failure|Consultas gemelas con error|Recuento|Total|recuento de Hola de todas las consultas de dos errores.|
|twinQueries.resultSize|Tamaño de resultado de consultas gemelas|Bytes|Media|Hola average, min y máximo de tamaño de los resultados de todas las consultas de gemelas correcta Hola.|
|jobs.createTwinUpdateJob.success|Creaciones correctas de trabajos de actualización gemelos|Recuento|Total|recuento de Hola de toda la creación correcta de los trabajos de actualización gemelas.|
|jobs.createTwinUpdateJob.failure|Creaciones con error de trabajos de actualización gemelos|Recuento|Total|recuento de Hola de todos los error en la creación de trabajos de actualización de gemelas.|
|jobs.createDirectMethodJob.success|Creaciones correctas de trabajos de invocación de método|Recuento|Total|recuento de Hola de toda la creación correcta de los trabajos de invocación de método directo.|
|jobs.createDirectMethodJob.failure|Creaciones con error de trabajos de invocación de método|Recuento|Total|recuento de Hola de todos los error en la creación de trabajos de invocación de método directo.|
|jobs.listJobs.success|Trabajos de toolist de llamadas correctas|Recuento|Total|recuento de Hola de todos los trabajos de toolist de llamadas correctas.|
|jobs.listJobs.failure|Errores llamadas toolist trabajos|Recuento|Total|recuento de Hola de todos los trabajos de toolist de errores de llamadas.|
|jobs.cancelJob.success|Cancelaciones de trabajos correctas|Recuento|Total|recuento de Hello correctos todas las llamadas a toocancel un trabajo.|
|jobs.cancelJob.failure|Cancelaciones de trabajos con error|Recuento|Total|recuento de Hola de todos los errores llamadas toocancel un trabajo.|
|jobs.queryJobs.success|Consultas de trabajo correctas|Recuento|Total|recuento de Hola de todos los trabajos de tooquery de llamadas correctas.|
|jobs.queryJobs.failure|Consultas de trabajo con error|Recuento|Total|recuento de Hola de todos los trabajos de tooquery de errores de llamadas.|
|jobs.completed|Trabajos completados|Recuento|Total|recuento de Hola de todos los trabajos completados.|
|jobs.failed|Trabajos con error|Recuento|Total|recuento de Hola de todos los trabajos con errores.|

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha visto una visión general de las métricas de centro de IoT, siga este toolearn de vínculo más acerca de cómo administrar el centro de IoT de Azure:

* [Supervisión de operaciones][lnk-monitor]

toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Guía para desarrolladores de IoT Hub][lnk-devguide]
* [Simular un dispositivo con Azure IoT Edge][lnk-iotedge]

<!-- Links and images -->
[1]: media/iot-hub-metrics/enable-metrics-1.png
[2]: media/iot-hub-metrics/enable-metrics-2.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-operations-monitoring]: iot-hub-operations-monitoring.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
