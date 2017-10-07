---
title: "mensajería de aaaUnderstand centro de IoT de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: a610741e23e243f392f1c042f9ab4a00d42f734f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a>Mensajería de dispositivo a nube y de nube a dispositivo con IoT Hub

Usar el centro de IoT mensajería toocommunicate con los dispositivos por:

* Enviar [dispositivo a la nube] [ lnk-d2c] mensajes de la solución de tooyour dispositivos back-end.
* Enviar [en la nube al dispositivo] [ lnk-c2d] mensajes de nuevo la solución Hola finalización tooyour dispositivos.

Propiedades básicas de funcionalidad de mensajería del centro de IoT son Hola fiabilidad y durabilidad de los mensajes. Estas propiedades permiten conectividad toointermittent de resistencia en el lado del dispositivo de Hola y tooload tiene un pico en el lado de la nube de Hola de procesamiento de eventos. El Centro de IoT implementa *al menos una vez* garantías de entrega para la mensajería del dispositivo a la nube y de la nube al dispositivo.

Para una introducción toohello las capacidades de centro de IoT, vea los artículos de hello [Azure y Internet de las cosas] [ lnk-azure-iot] y [información general de hello servicio del centro de IoT de Azure] [lnk-iot-hub-overview].

## <a name="when-toouse-iot-hub-messaging"></a>Cuando toouse centro de IoT mensajería

Usar mensajes de dispositivo a la nube para enviar telemetría de series de tiempo y alertas desde la aplicación de dispositivo y los mensajes en la nube al dispositivo para notificaciones unidireccional tooyour del dispositivo.

* Consulte demasiado[Guía de comunicación de dispositivos a la nube] [ lnk-d2c-guidance] si está en duda entre el uso de mensajes del dispositivo a la nube, las propiedades notificados o cargar el archivo.
* Consulte demasiado[orientación para la comunicación en la nube para dispositivos] [ lnk-c2d-guidance] si está en duda entre el uso de mensajes en la nube al dispositivo, deseados propiedades o métodos directos.

## <a name="next-steps"></a>Pasos siguientes

* Obtenga más información acerca de la [mensajería de dispositivo a nube][lnk-d2c] de IoT Hub.
* Obtenga más información acerca de la [mensajería de nube a dispositivo][lnk-c2d] de IoT Hub.

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md