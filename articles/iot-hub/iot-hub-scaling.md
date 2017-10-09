---
title: ajuste de escala de centro de IoT aaaAzure | Documentos de Microsoft
description: "Cómo tooscale su toosupport de centro de IoT el rendimiento de los mensajes previsto. Incluye un resumen de rendimiento de hello admitido para cada nivel y las opciones de particionamiento."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a>Escalado de la solución de IoT Hub
Centro de IoT de Azure puede admitir la tooa millones de dispositivos conectados al mismo tiempo. Para obtener más información, vea [Precios de IoT Hub][lnk-pricing]. Cada unidad de IoT Hub permite un número determinado de mensajes diarios.

tooproperly escalar su solución, considere la posibilidad de su uso particular del centro de IoT. En concreto, tenga en cuenta el rendimiento de máximo de hello necesario para hello siguientes categorías de operaciones:

* Mensajes de dispositivo a nube
* Mensajes de nube a dispositivo
* Operaciones de registro de identidad

En información de rendimiento de toothis de adición, vea [centro de IoT cuotas y aceleradores] [ IoT Hub quotas and throttles] y diseñar la solución según corresponda.

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a>Capacidad de procesamiento para los mensajes de dispositivo a nube y de nube a dispositivo
Hola mejor manera toosize una solución de centro de IoT es tráfico de hello tooevaluate según una por unidad.

Los mensajes de dispositivo a nube siguen estas directrices de capacidad de procesamiento sostenida.

| Nivel: | Capacidad de procesamiento sostenida | Velocidad de envío sostenida |
| --- | --- | --- |
| S1 |Seguridad too1111 KB por minuto por unidad<br/>(1,5 GB/día/unidad) |Promedio de 278 mensajes/minuto por unidad<br/>(400 000 mensajes/día por unidad) |
| S2 |Seguridad too16 MB por minuto por unidad<br/>(22,8 GB/día/unidad) |Promedio de 4167 mensajes/minuto por unidad<br/>(6 millones de mensajes/día por unidad) |
| S3 |Seguridad too814 MB por minuto por unidad<br/>(1144,4 GB/día/unidad) |Promedio de 208.333 mensajes/minuto por unidad<br/>(300 millones de mensajes/día por unidad) |

## <a name="identity-registry-operation-throughput"></a>Capacidad de procesamiento para las operaciones de registro de identidad
Las operaciones del registro de identidad de centro de IoT no deberían toobe operaciones en tiempo de ejecución, ya que son principalmente aprovisionamiento toodevice relacionado.

Vea las cifras de rendimiento de ráfaga específicas en [Cuotas y limitaciones de IoT Hub][IoT Hub quotas and throttles].

## <a name="sharding"></a>Clave de particionamiento
Mientras que un único centro de IoT puede escalar toomillions de dispositivos, a veces la solución necesita características de rendimiento específicas que no puede garantizar un único centro de IoT. En ese caso, se recomienda realizar particiones de los dispositivos en varios centros de IoT. Varios centros de IoT suavizar ráfagas de tráfico y obtener el rendimiento necesario Hola o los tipos de operación que se necesitan.

## <a name="next-steps"></a>Pasos siguientes
toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Guía para desarrolladores de IoT Hub][lnk-devguide]
* [Simular un dispositivo con Azure IoT Edge][lnk-iotedge]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
