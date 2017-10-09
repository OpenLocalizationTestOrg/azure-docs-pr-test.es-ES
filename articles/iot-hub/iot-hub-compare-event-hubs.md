---
title: Centro de IoT de Azure de aaaCompare tooAzure centros de eventos | Documentos de Microsoft
description: "Una comparación de hello centro de IoT y resaltar las diferencias funcionales y casos de uso de servicios de Azure de los centros de eventos. comparación de Hello incluye protocolos admitidos, la administración de dispositivos, supervisión, y cargas de archivos."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: aeddea62-8302-48e2-9aad-c5a0e5f5abe9
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: e5f546b54e29860498d540abfc86a41c4662c0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-of-azure-iot-hub-and-azure-event-hubs"></a>Comparación entre IoT Hub de Azure y Azure Event Hubs
Uno de los casos de uso principales de hello para el centro de IoT es toogather telemetría de dispositivos. Por esta razón, centro de IoT a menudo se compara demasiado[centros de eventos de Azure][Azure Event Hubs]. Al igual que el centro de IoT, centros de eventos es un servicio que permite la entrada de telemetría y eventos de procesamiento de evento toohello en la nube a escala masiva, con baja latencia y alta fiabilidad.

Sin embargo, los servicios de hello tienen muchas diferencias, que se detallan en hello en la tabla siguiente:

| Ámbito | IoT Hub | Event Hubs |
| --- | --- | --- |
| Patrones de comunicación | Permite las [comunicaciones de dispositivo a nube] [lnk-d2c-guidance] (mensajería, cargas de archivos y propiedades notificadas) y [comunicaciones de nube a dispositivo] [lnk-c2d-guidance] (métodos directos, propiedades deseadas, mensajería). |Solo se habilita la entrada de eventos (normalmente se consideran escenarios dispositivo a nube). |
| Información de estado de dispositivo | Los [dispositivos gemelos][lnk-twins] pueden almacenar y consultar la información de estado del dispositivo. | Sin embargo, esta información no se puede almacenar. |
| Compatibilidad con protocolos de dispositivo |Se admite MQTT, MQTT sobre WebSockets, AMQP, AMQP sobre WebSockets y HTTP. Además, el centro de IoT funciona con hello [puerta de enlace de IoT de Azure protocolo][lnk-azure-protocol-gateway], un protocolos personalizados del toosupport de implementación de protocolo personalizable puerta de enlace. |Admite AMQP, AMQP sobre WebSockets y HTTP. |
| Seguridad |Ofrece identidad por dispositivo y control de acceso revocable. Vea hello [sección de seguridad de la Guía del desarrollador de centro de IoT hello]. |Ofrece [directivas de acceso compartido][Event Hubs - security] en todo Event Hubs, con compatibilidad limitada para revocación mediante [directivas del publicador][Event Hubs publisher policies]. IoT soluciones suelen ser las credenciales necesarias tooimplement una toosupport solución personalizada por dispositivo y medidas contra suplantación de identidad. |
| Supervisión de operaciones |Permite IoT soluciones toosubscribe tooa amplio conjunto de eventos de conectividad y administración de identidad de dispositivo como errores de autenticación de dispositivos individuales, limitación y excepciones de formato incorrecto. Estos eventos le permiten tooquickly identificar problemas de conectividad en el nivel de dispositivo de Hola. |Muestra solo las métricas agregadas. |
| Escala |Está optimizado toosupport millones de dispositivos conectados al mismo tiempo. |Metros Hola conexiones según [las cuotas de los centros de eventos de Azure][Azure Event Hubs quotas]. En Hola otra parte, los concentradores de eventos permite partición de hello toospecify para cada mensaje enviado. |
| SDK de dispositivo |Proporciona [dispositivo SDK] [ Azure IoT SDKs] para una gran variedad de plataformas y los idiomas en suma toodirect MQTT, AMQP y HTTP APIs. |Se admite en. NET, Java y C, en suma tooAMQP e interfaces de envío HTTP. |
| Carga de archivos |Permite que los archivos de tooupload IoT soluciones de nube de toohello de dispositivos. Incluye un punto de conexión de notificación de archivos para la integración del flujo de trabajo y una categoría de supervisión de operaciones para la compatibilidad con la depuración. | No compatible. |
| Enrutar mensajes a puntos de conexión de toomultiple | Se admiten extremos personalizados hasta too10. Las reglas determinan cómo los mensajes se toocustom enrutado extremos. Para más información, consulte [Envío y recepción de mensajes con IoT Hub][lnk-devguide-messaging]. | Requiere código adicional toobe escrito y hospedado para el envío de mensajes. |

En resumen, aunque Hola único caso de uso es la entrada de telemetría de dispositivo a la nube, centro de IoT proporciona un servicio que está diseñado para la conectividad de dispositivos de IoT. Continúa propuestas de valor de hello tooexpand para estos escenarios con características específicas de IoT. Los concentradores de eventos está diseñado para la entrada de evento en una escala masiva, tanto en el contexto de Hola de escenarios de centro de datos entre redes y dentro de un centro de datos.

No es raro que toouse centro de IoT y concentradores de eventos de Hola misma solución. Centro de IoT controla la comunicación de dispositivos a la nube de Hola y centros de eventos controla la entrada de evento de fase posterior en los motores de procesamiento en tiempo real.

### <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de la planeación de la implementación del centro de IoT, consulte [ajuste de escala, alta disponibilidad y recuperación ante desastres][lnk-scaling].

toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Guía para desarrolladores de IoT Hub][lnk-devguide]
* [Simular un dispositivo con IoT Edge][lnk-iotedge]

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[Azure Event Hubs]: ../event-hubs/event-hubs-what-is-event-hubs.md
[sección de seguridad de la Guía del desarrollador de centro de IoT hello]: iot-hub-devguide-security.md
[Event Hubs - security]: ../event-hubs/event-hubs-authentication-and-security-model-overview.md
[Event Hubs publisher policies]: ../event-hubs/event-hubs-features.md#event-publishers
[Azure Event Hubs quotas]: ../event-hubs/event-hubs-quotas.md
[Azure IoT SDKs]: https://github.com/Azure/azure-iot-sdks
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
