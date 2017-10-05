---
title: Opciones de nube a dispositivo de IoT Hub de Azure | Microsoft Docs
description: "Guía del desarrollador: una guía sobre cuándo usar métodos directos, propiedades notificadas del dispositivo gemelo o mensajes de nube a dispositivo para comunicaciones de este mismo tipo."
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
ms.openlocfilehash: e6cd4880c9bfcc670bd116d3dd8e5245d70f85cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-to-device-communications-guidance"></a>Guía de comunicación de nube a dispositivo
IoT Hub proporciona tres opciones para aplicaciones de dispositivo que exponen funcionalidades a una aplicación de back-end:

* [Métodos directos][lnk-methods], para las comunicaciones que requieren confirmación inmediata del resultado. Los métodos directos se utilizan frecuentemente para el control interactivo de dispositivos, como la activación de un ventilador.
* [Propiedades deseadas del dispositivo gemelo][lnk-twins], para comandos de ejecución prolongada destinados a poner el dispositivo en un determinado estado deseado. Por ejemplo, establecer el intervalo de envío de telemetría en 30 minutos.
* [Mensajes de nube a dispositivo][lnk-c2d], para notificaciones unidireccionales a la aplicación de dispositivo.

Esta es una comparación detallada de las distintas opciones de comunicación de nube a dispositivo.

|  | Métodos directos | Propiedades deseadas del dispositivo gemelo | Mensajes de nube a dispositivo |
| ---- | ------- | ---------- | ---- |
| Escenario | Comandos que necesitan confirmación inmediata, por ejemplo, encender un ventilador. | Comandos de ejecución prolongada destinados a poner el dispositivo en un determinado estado deseado. Por ejemplo, establecer el intervalo de envío de telemetría en 30 minutos. | Notificaciones unidireccionales a la aplicación de dispositivo. |
| flujo de datos | Bidireccional. La aplicación de dispositivo puede responder al método inmediatamente. El back-end de solución recibe el resultado contextualmente a la solicitud. | Unidireccional. La aplicación de dispositivo recibe una notificación con el cambio de propiedad. | Unidireccional. La aplicación de dispositivo recibe el mensaje.
| Durabilidad. | No se establece contacto con los dispositivos desconectados. Se notifica al back-end de la solución que el dispositivo no está conectado. | Se conservan los valores de propiedad en el dispositivo gemelo. El dispositivo los leerá en la siguiente reconexión. Los valores de propiedad son recuperables con el [lenguaje de consulta de IoT Hub][lnk-query]. | IoT Hub puede conservar los mensajes durante 48 horas como máximo. |
| Destinos | Un único dispositivo que usa **deviceId**, o varios dispositivos que usan [trabajos][lnk-jobs]. | Un único dispositivo que usa **deviceId**, o varios dispositivos que usan [trabajos][lnk-jobs]. | Dispositivo único por **deviceId**. |
| Tamaño | Hasta 8 KB de solicitudes y 8 KB de respuestas. | El tamaño máximo de propiedades deseadas es 8 KB. | Mensajes de hasta 64 kB. |
| Frecuencia | Alta. Para más información, consulte los [Límites de IoT Hub][lnk-quotas]. | Mediana. Para más información, consulte los [Límites de IoT Hub][lnk-quotas]. | Baja. Para más información, consulte los [Límites de IoT Hub][lnk-quotas]. |
| Protocol | Actualmente solo está disponible cuando se usa MQTT. | Actualmente solo está disponible cuando se usa MQTT. | Disponible en todos los protocolos. El dispositivo debe sondear al utilizar HTTP. |

Aprenda a usar métodos directos, propiedades deseadas y mensajes de nube a dispositivo en los siguientes tutoriales:

* [Uso de métodos directos][lnk-methods-tutorial], para métodos directos.
* [Uso de propiedades deseadas para configurar dispositivos][lnk-twin-properties], para propiedades deseadas del dispositivo gemelo. 
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
