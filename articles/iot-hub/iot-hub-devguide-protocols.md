---
title: "comunicación de centro de IoT aaaAzure protocolos y puertos | Documentos de Microsoft"
description: "Guía del desarrollador - describe Hola admite protocolos de comunicación para las comunicaciones de dispositivo para la nube y en la nube al dispositivo y los números de puerto de Hola que deben estar abiertos."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 31cb948f1d30edd87edb13ad0dd859c02bcc3239
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# Referencia: elección de un protocolo de comunicación

Centro de IoT permite dispositivos toouse [MQTT][lnk-mqtt], MQTT a través de WebSockets, [AMQP][lnk-amqp], AMQP a través de HTTP y WebSockets protocolos de lado del dispositivo comunicaciones. Para información sobre cómo estos protocolos admiten características específicas de IoT Hub, consulte [Guía de comunicación de dispositivo a nube][lnk-d2c-guidance] y [Guía de comunicación de nube a dispositivo][lnk-c2d-guidance].

Hello tabla siguiente proporciona recomendaciones de alto nivel de Hola para su elección del protocolo:

| Protocol | Cuándo elegir este protocolo |
| --- | --- |
| MQTT <br> MQTT sobre WebSocket |Usar varios dispositivos (cada uno con sus propias credenciales por dispositivo) en todos los dispositivos que no requieren tooconnect sobre Hola misma conexión TLS. |
| AMQP <br> AMQP sobre WebSocket |Usar en el campo y la nube ventaja de tootake de puertas de enlace de conexión multiplexación en todos los dispositivos. |
| HTTP |Usar con dispositivos que no admiten otros protocolos. |

Considere la posibilidad de hello siguientes puntos al elegir el protocolo para las comunicaciones del dispositivo:

* **Patrón de nube a dispositivo**. HTTP no tiene una inserción de servidor tooimplement de manera eficaz. Por lo tanto, cuando se usa HTTP, los dispositivos sondean los mensajes de nube a dispositivo en IoT Hub. Este enfoque es ineficiente para dispositivos de Hola y centro de IoT. Según las directrices actuales de HTTP, cada dispositivo sondeará si hay mensajes cada 25 minutos o más. En Hola otra parte, MQTT y AMQP admiten la inserción de servidor cuando se reciben mensajes en la nube al dispositivo. Le permiten inserciones inmediatas de mensajes del dispositivo de toohello centro de IoT. Si la latencia de entrega es un problema, MQTT o AMQP son Hola mejor protocolos toouse. Para dispositivos conectados en raras ocasiones, HTTP funciona bien.
* **Puertas de enlace de campo**. Cuando se usa HTTP y MQTT, no se puede conectar varios dispositivos (cada uno con sus propias credenciales por dispositivo) utilizando Hola la misma conexión de TLS. Por lo tanto, para [escenarios de puerta de enlace de campo][lnk-azure-gateway-guidance], estos protocolos no sean óptimos que requieren una conexión TLS entre la puerta de enlace de campo de Hola y centro de IoT para cada puerta de enlace de campo de dispositivo toohello conectado.
* **Dispositivos con bajos recursos**. Hola MQTT y bibliotecas HTTP no tienen una superficie menor que las bibliotecas AMQP de Hola. Por lo tanto, si hello dispositivo limitó recursos (por ejemplo, menor que 1 MB de RAM), estos protocolos puede Hola única implementación del protocolo disponible.
* **Cruce seguro de red**. protocolo estándar de AMQP de Hello usa el puerto 5671, mientras MQTT escucha en el puerto 8883, lo que puede provocar problemas en redes que son protocolos HTTP toonon cerrado. MQTT a través de WebSockets, AMQP a través de HTTP y WebSockets son toobe disponible utilizado en este escenario.
* **Tamaño de carga**. MQTT y AMQP son protocolos binarios que producen cargas más compactas que HTTP.

> [!WARNING]
> Cuando se usa HTTP, cada dispositivo sondeará si hay mensajes de la nube a dispositivo cada 25 minutos o más. Sin embargo, durante el desarrollo, es aceptable toopoll con más frecuencia que cada 25 minutos.

## Números de puerto

Los dispositivos pueden comunicarse con el Centro de IoT en Azure mediante diversos protocolos. Por lo general, la elección de Hola de protocolo se basa en requisitos específicos de Hola de solución de Hola. Hello tabla siguiente enumeran los puertos de salida de hello que deben estar abiertos para un toouse de capaz de toobe un protocolo específico de dispositivo:

| Protocol | Port |
| --- | --- |
| MQTT |8883 |
| MQTT sobre WebSockets |443 |
| AMQP |5671 |
| AMQP sobre WebSockets |443 |
| HTTP |443 |

Una vez haya creado un centro de IoT en una región de Azure, hello mantiene de centro de IoT Hola misma dirección IP para la duración de Hola de ese centro de IoT. Sin embargo, toomaintain calidad de servicio, si mueve Microsoft unidad de escalado distinta de hello IoT hub tooa, a continuación, que se asigna una nueva dirección IP.


## Pasos siguientes

toolearn más información acerca de cómo centro de IoT implementa el protocolo MQTT hello, consulte [comunicar con el centro de IoT mediante Protocolo de hello MQTT][lnk-mqtt-support].

[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-mqtt-support]: iot-hub-mqtt-support.md
[lnk-amqp]: http://docs.oasis-open.org/amqp/core/v1.0/os/amqp-core-complete-v1.0-os.pdf
[lnk-mqtt]: http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.pdf
[lnk-azure-gateway-guidance]: iot-hub-devguide-endpoints.md#field-gateways
