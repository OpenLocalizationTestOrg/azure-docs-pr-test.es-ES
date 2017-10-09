---
title: trabajos de centro de IoT de Azure aaaUnderstand | Documentos de Microsoft
description: "Guía del desarrollador - programar trabajos toorun en varios dispositivos conectados tooyour centro de IoT. Trabajos pueden actualizar las etiquetas y propiedades que desee y llamar a métodos directas en varios dispositivos."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a>Programación de trabajos en varios dispositivos
## <a name="overview"></a>Información general
Como se describe en artículos anteriores, Azure IoT Hub permite un número de bloques de creación ([etiquetas y propiedades de dispositivos gemelos][lnk-twin-devguide] y [métodos directos][lnk-dev-methods]).  Por lo general, aplicaciones de back-end habilitar tooupdate de administradores y operadores de dispositivo e interactúan con dispositivos de IoT de forma masiva y a la hora programada.  Trabajos de encapsulan la ejecución de hello de dispositivo gemelas actualizaciones y métodos directos con un conjunto de dispositivos en un tiempo de programación.  Por ejemplo, un operador podría usar una aplicación de back-end que se inician y realizar un seguimiento de un tooreboot de trabajo un conjunto de dispositivos en la creación de 43 y floor 3 a la vez que no son perjudiciales toohello operaciones de creación de hello.

### <a name="when-toouse"></a>Cuando toouse
Considere la posibilidad de usar trabajos cuando: una solución back-end necesidades tooschedule y realizar un seguimiento de progreso cualquiera de hello actividades que siguen en un conjunto de dispositivos:

* Actualizar las propiedades deseadas
* Actualizar etiquetas
* Invocar métodos directos

## <a name="job-lifecycle"></a>Ciclo de vida de trabajo
Los trabajos se inicia back-end de soluciones de Hola y mantenidos por centro de IoT.  Puede iniciar un trabajo a través de un URI orientado a servicios (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) y una consulta para el progreso de un trabajo en ejecución a través de un URI orientado a servicios (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).  Una vez que se inicia un trabajo, la consulta de trabajos permite estado de hello aplicaciones back-end toorefresh Hola de trabajos en ejecución.

> [!NOTE]
> Cuando se inicia un trabajo, valores y nombres de propiedad solo pueden contener US-ASCII imprimible alfanumérico, excepto los Hola siguiendo conjunto: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

## <a name="reference-topics"></a>Temas de referencia:
Hola temas de referencia siguientes proporciona más información acerca del uso de trabajos.

## <a name="jobs-tooexecute-direct-methods"></a>Métodos directos de trabajos tooexecute
Hello aquí te mostramos detalles de la solicitud de hello HTTP 1.1 para ejecutar un [método directo] [ lnk-dev-methods] en un conjunto de dispositivos mediante un trabajo:

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
condición de consulta de Hello también puede ser un Id. de dispositivo único o en una lista de identificadores de dispositivo tal y como se muestra a continuación

**Ejemplos**
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
[Lenguaje de consulta de IoT Hub][lnk-query] aborda el lenguaje de consulta de IoT Hub con más detalle.

## <a name="jobs-tooupdate-device-twin-properties"></a>Propiedades de gemelas del dispositivo de tooupdate de trabajos
Hola te mostramos detalles de la solicitud de HTTP 1.1 Hola para actualizar las propiedades de dispositivo gemelas con un trabajo:

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a>Consulta del progreso de los trabajos
Hello aquí te mostramos Hola detalles de la solicitud de HTTP 1.1 para [consultar trabajos][lnk-query]:

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

Hola continuationToken se proporciona de respuesta de Hola.  

## <a name="jobs-properties"></a>Propiedades de trabajos
Hola mostramos una lista de propiedades y las descripciones correspondientes, que pueden utilizarse al consultar para trabajos o los resultados del trabajo.

| Propiedad | Descripción |
| --- | --- |
| **jobId** |Aplicación Id. proporcionado para el trabajo de Hola. |
| **startTime** |Hora de inicio de aplicación proporcionado (ISO-8601) para el trabajo de Hola. |
| **endTime** |Centro de IoT proporciona fecha (ISO-8601) de terminación del trabajo de Hola. Válido solo una vez trabajo Hola permanece hello 'completada'. |
| **type** |Tipos de trabajos: |
| **scheduledUpdateTwin**: un tooupdate de trabajo que se utiliza un conjunto de propiedades que desee o etiquetas. | |
| **scheduledDeviceMethod**: un tooinvoke de trabajo que se utiliza un método de dispositivo en un conjunto de: los gemelos de dispositivo. | |
| **estado** |Estado actual del trabajo de Hola. Posibles valores para el estado: |
| **pendiente** : programada y espera toobe recogido por el servicio de trabajo de Hola. | |
| **programado** : programada para una hora en hello futuras. | |
| **running**: trabajo activo actualmente. | |
| **cancelled**: el trabajo se ha cancelado. | |
| **failed**: trabajo erróneo. | |
| **completed**: el trabajo se ha completado. | |
| **deviceJobStatistics** |Estadísticas sobre la ejecución del trabajo de Hola. |

Propiedades **deviceJobStatistics**.

| Propiedad | Descripción |
| --- | --- |
| **deviceJobStatistics.deviceCount** |Número de dispositivos de trabajo de Hola. |
| **deviceJobStatistics.failedCount** |Número de dispositivos que no se pudo trabajo Hola. |
| **deviceJobStatistics.succeededCount** |Número de dispositivos donde se realizó correctamente el trabajo de Hola. |
| **deviceJobStatistics.runningCount** |Número de dispositivos que se están ejecutando trabajo de Hola. |
| **deviceJobStatistics.pendingCount** |Número de dispositivos que están pendientes de trabajo de hello toorun. |

### <a name="additional-reference-material"></a>Material de referencia adicional
Otros temas de referencia en la Guía del desarrollador de centro de IoT Hola incluyen:

* [Los extremos del centro de IoT] [ lnk-endpoints] describe Hola varios extremos que cada centro de IoT expone las operaciones de tiempo de ejecución y administración.
* [Limitación y las cuotas] [ lnk-quotas] describe las cuotas de Hola que se aplican toohello servicio del centro de IoT y Hola limitación tooexpect de comportamiento cuando se usa el servicio de Hola.
* [SDK de dispositivos y servicios de Azure IoT] [ lnk-sdks] listas Hola lenguaje varios SDK puede usar cuando se desarrollan aplicaciones de dispositivos y servicios que interactúan con el centro de IoT.
* [Lenguaje de consulta de centro de IoT para: los gemelos de dispositivo, los trabajos y el enrutamiento de mensajes] [ lnk-query] describe Hola lenguaje de consultas del centro de IoT puede usar información de tooretrieve centro de IoT de: los gemelos de dispositivo y trabajos.
* [Compatibilidad de IoT Hub MQTT] [ lnk-devguide-mqtt] proporciona más información acerca del soporte técnico de centro de IoT para el protocolo MQTT Hola.

## <a name="next-steps"></a>Pasos siguientes
Si desea que tootry algunos de los conceptos de hello descritos en este artículo, es posible que interesa Hola sigue tutorial del centro de IoT:

* [Schedule and broadcast jobs][lnk-jobs-tutorial] (Programación y difusión de trabajos)

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
