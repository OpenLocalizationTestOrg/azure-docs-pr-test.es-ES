---
title: Opciones de nube al dispositivo de centro de IoT aaaAzure | Documentos de Microsoft
description: "Guía del desarrollador - instrucciones sobre cuando toouse dirigir métodos, propiedades deseadas del doble del dispositivo o mensajes en la nube al dispositivo para las comunicaciones de nube al dispositivo."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: bb95445054fa2711e34fc1d928c3665e0246c81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-to-device-communications-guidance"></a>Guía de comunicación de nube a dispositivo
Centro de IoT proporciona tres opciones para aplicaciones de dispositivo aplicaciones tooexpose funcionalidad tooa back-end:

* [Dirigir métodos] [ lnk-methods] para las comunicaciones que necesitan confirmación inmediata del resultado de hello. Los métodos directos se utilizan frecuentemente para el control interactivo de dispositivos, como la activación de un ventilador.
* [Dos de las propiedades adecuadas] [ lnk-twins] para comandos de ejecución prolongada que se vayan tooput dispositivo de hello en un determinado estado de deseado. Por ejemplo, establezca los minutos too30 Hola telemetría envío intervalo.
* [En la nube al dispositivo mensajes] [ lnk-c2d] para notificaciones unidireccional toohello del dispositivo.

Aquí es una comparación detallada de hello diversas opciones de comunicación en la nube al dispositivo.

|  | Métodos directos | Propiedades deseadas del dispositivo gemelo | Mensajes de nube a dispositivo |
| ---- | ------- | ---------- | ---- |
| Escenario | Comandos que necesitan confirmación inmediata, por ejemplo, encender un ventilador. | Comandos de ejecución prolongada habían pensado tooput dispositivo de hello en un cierto estado deseado. Por ejemplo, establezca los minutos too30 Hola telemetría envío intervalo. | Notificaciones unidireccional toohello del dispositivo. |
| flujo de datos | Bidireccional. aplicación de dispositivo de Hello puede responder toohello método inmediatamente. Hola solución back-end recibe el resultado de hello como toohello solicitud. | Unidireccional. aplicación de dispositivo de Hello recibe una notificación de cambio de propiedad de Hola. | Unidireccional. aplicación de dispositivo de Hello recibe mensajes de bienvenida
| Durabilidad. | No se establece contacto con los dispositivos desconectados. Hola solución back-end se notifica que ese dispositivo hello no está conectado. | Valores de propiedad se conservan en gemelas de dispositivo de Hola. El dispositivo los leerá en la siguiente reconexión. Los valores de propiedad son recuperables con hello [lenguaje de consultas del centro de IoT][lnk-query]. | Los mensajes se pueden conservar IoT hub para too48 horas. |
| Destinos | Un único dispositivo que usa **deviceId**, o varios dispositivos que usan [trabajos][lnk-jobs]. | Un único dispositivo que usa **deviceId**, o varios dispositivos que usan [trabajos][lnk-jobs]. | Dispositivo único por **deviceId**. |
| Tamaño | Too8KB solicitudes y respuestas de 8KB. | El tamaño máximo de propiedades deseadas es 8 KB. | Los mensajes de too64KB. |
| Frecuencia | Alta. Para más información, consulte los [Límites de IoT Hub][lnk-quotas]. | Mediana. Para más información, consulte los [Límites de IoT Hub][lnk-quotas]. | Baja. Para más información, consulte los [Límites de IoT Hub][lnk-quotas]. |
| Protocol | Actualmente solo está disponible cuando se usa MQTT. | Actualmente solo está disponible cuando se usa MQTT. | Disponible en todos los protocolos. El dispositivo debe sondear al utilizar HTTP. |

Obtenga información acerca de cómo dirigir toouse métodos, propiedades deseadas y mensajes en la nube al dispositivo en hello tutoriales:

* [Uso de métodos directos][lnk-methods-tutorial], para métodos directos.
* [Usar dispositivos de propiedades que desee tooconfigure][lnk-twin-properties], para gemelas de dispositivo que desea propiedades; 
* [Envío de mensajes de nube a dispositivo][lnk-c2d-tutorial], para mensajes de nube a dispositivo.

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-tutorial]: iot-hub-node-node-c2d.md
