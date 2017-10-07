---
title: "dispositivo de nube de Azure IoT Hub aaaManage mensajería con el centro de IOT explorador | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola mensajes toocloud (D2C) de dispositivo de toomonitor de herramienta de explorador el centro de IOT CLI y enviar mensajes de toodevice (C2D) de nube en el centro de IoT de Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "el centro de IOT explorador, mensajería, de nube dispositivo toodevice de nube del centro de iot, toodevice de mensajería en la nube"
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a>Usar el centro de IOT explorador toosend y recibir mensajes entre el dispositivo y el centro de IoT

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[iothub-explorer](https://github.com/azure/iothub-explorer) tiene una serie de comandos que facilitan la administración de IoT Hub. Este tutorial se centra en cómo toouse el centro de IOT explorador toosend y recibir mensajes entre el dispositivo y el centro de IoT.

## <a name="what-you-will-learn"></a>Lo qué aprenderá

Aprenderá cómo toouse mensajes de dispositivo para la nube de explorador el centro de IOT toomonitor y toosend en la nube al dispositivo. Mensajes del dispositivo a la nube pudieron ser datos de sensor que el dispositivo se recopila y, a continuación, envía tooyour centro de IoT. Mensajes de la nube al dispositivo pudieron ser comandos que el centro de IoT envía tooyour dispositivo tooblink un LED que está conectado tooyour dispositivo.

## <a name="what-you-will-do"></a>Lo que hará

- Utilizar el centro de IOT explorador toomonitor dispositivo a la nube mensajes.
- Utilizar el centro de IOT explorador toosend en la nube al dispositivo mensajes.

## <a name="what-you-need"></a>Lo que necesita

- Tutorial [configurar su dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completado donde abordan las Hola según los requisitos:
  - Una suscripción de Azure activa.
  - Un centro de Azure IoT en su suscripción.
  - Una aplicación de cliente que envía el centro de IoT de Azure de tooyour de mensajes.
- iothub-explorer ([instalación de iothub-explorer](https://github.com/azure/iothub-explorer)).

## <a name="monitor-device-to-cloud-messages"></a>Supervisión de mensajes de dispositivo a nube

toomonitor mensajes que se envían desde el centro de IoT tooyour de dispositivo, siga estos pasos:

1. Abra una ventana de la consola.
1. Ejecute el siguiente comando de hello:

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > Obtenga `<device-id>` y `<IoTHubConnectionString>` desde el IoT Hub. Asegúrese de que haya terminado de tutorial anterior Hola. O bien puede intentar toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` si tienes `HostName`, `SharedAccessKeyName` y `SharedAccessKey`.

## <a name="send-cloud-to-device-messages"></a>Envío de mensajes de nube a dispositivo

toosend un mensaje desde su dispositivo tooyour del centro de IoT, siga estos pasos:

1. Abra una ventana de la consola.
1. Iniciar una sesión en el centro de IoT ejecutando Hola siguiente comando:

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. Enviar un dispositivo de tooyour de mensaje mediante la ejecución de hello siguiente comando:

   ```bash
   iothub-explorer send <device-id> <message>
   ```

comando Hello parpadea Hola LED que está conectado tooyour dispositivo y envía el dispositivo de tooyour de mensaje de Hola.

> [!Note]
> No es necesario para hello dispositivo toosend un centro de IoT de confirmación independiente comando tooyour atrás tras la recepción de mensajes de bienvenida.

## <a name="next-steps"></a>Pasos siguientes

Ahora sabe cómo toomonitor dispositivo a la nube mensajes y enviar mensajes en la nube al dispositivo entre los dispositivos de IoT y el centro de IoT de Azure.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
