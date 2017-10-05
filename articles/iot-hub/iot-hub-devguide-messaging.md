---
title: "Información sobre la mensajería de IoT Hub de Azure | Microsoft Docs"
description: "Guía del desarrollador: mensajería de dispositivo a nube y de nube a dispositivo con IoT Hub Incluye información sobre los formatos de mensaje y protocolos de comunicación compatibles."
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
ms.openlocfilehash: f54398d7ac46bf178d2bb603669b399d25370736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a>Mensajería de dispositivo a nube y de nube a dispositivo con IoT Hub

Use la mensajería de IoT Hub para comunicarse con los dispositivos de los siguientes modos:

* Enviando mensajes [de dispositivo a nube][lnk-d2c] desde los dispositivos al back-end de su solución.
* Enviando mensajes [de nube a dispositivo][lnk-c2d] desde la solución de back-end a sus dispositivos.

Las propiedades básicas de la funcionalidad de mensajería del Centro de IoT son la confiabilidad y durabilidad de los mensajes. Estas propiedades permiten la resistencia a la conectividad intermitente en el dispositivo y a los picos de carga del procesamiento de eventos en la nube. El Centro de IoT implementa *al menos una vez* garantías de entrega para la mensajería del dispositivo a la nube y de la nube al dispositivo.

Para obtener una introducción a las funciones de IoT Hub, consulte los artículos [Azure y el Internet de las cosas][lnk-azure-iot] e [Introducción al servicio Azure IoT Hub][lnk-iot-hub-overview].

## <a name="when-to-use-iot-hub-messaging"></a>Cuándo se debe usar la mensajería de IoT Hub

Los mensajes de dispositivo a nube se utilizan para enviar telemetría y alertas de series temporales desde la aplicación para dispositivo y los mensajes de nube a dispositivo, para las notificaciones unidireccionales a su aplicación para dispositivo.

* Si duda entre el uso de mensajes de dispositivo a nube, propiedades notificadas o carga de archivos, consulte la [Guía de comunicación de dispositivo a nube][lnk-d2c-guidance].
* Si duda entre el uso de mensajes de nube a dispositivo, propiedades deseadas o métodos directos, consulte la [Guía de comunicación de nube a dispositivo][lnk-c2d-guidance].

## <a name="next-steps"></a>Pasos siguientes

* Obtenga más información acerca de la [mensajería de dispositivo a nube][lnk-d2c] de IoT Hub.
* Obtenga más información acerca de la [mensajería de nube a dispositivo][lnk-c2d] de IoT Hub.

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md