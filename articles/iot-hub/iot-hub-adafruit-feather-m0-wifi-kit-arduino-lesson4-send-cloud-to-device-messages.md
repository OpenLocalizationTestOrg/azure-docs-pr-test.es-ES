---
title: "Connect Arduino (C) tooAzure IoT - lección 4: en la nube al dispositivo | Documentos de Microsoft"
description: "Una aplicación de ejemplo se ejecuta en Adafruit Feather M0 WiFi y supervisa los mensajes entrantes de IoT Hub. Una nueva tarea de gulp envía mensajes tooAdafruit Wi-Fi de desvanecimiento M0 desde su hello tooblink de centro de IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "control de led de arduino desde web, control de led de arduino a través de web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Ejecutar un tooreceive de la aplicación de ejemplo en la nube al dispositivo mensajes
En este artículo, se implementa una aplicación de ejemplo en la placa Adafruit Feather M0 WiFi Arduino.

aplicación de ejemplo de Hola supervisa los mensajes entrantes desde el centro de IoT. También permite ejecutar una tarea de gulp en los mensajes de toosend equipo tooyour Arduino panel, desde el centro de IoT. Cuando la aplicación de ejemplo de Hola recibe mensajes de Hola, parpadea Hola LED. Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].

## <a name="what-you-will-do"></a>Lo que hará
* Conectar el centro de IoT de tooyour de aplicación de ejemplo de Hola.
* Implemente y ejecute la aplicación de ejemplo de Hola.
* Enviar mensajes desde su Hola IoT hub tooyour Arduino panel tooblink LED.

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:
* Cómo los mensajes entrantes de toomonitor desde el centro de IoT.
* ¿Cómo toosend en la nube al dispositivo mensajes desde su tooyour de centro de IoT Arduino panel.

## <a name="what-you-need"></a>Lo que necesita
* La placa de Arduino, configurada para su uso. toolearn tooset de su placa Arduino, vea [configurar su dispositivo][configure-your-device].
* Una instancia de IoT Hub creada en su suscripción de Azure. toolearn cómo toocreate su centro de IoT, consulte [crea el centro de IoT de Azure][create-your-azure-iot-hub].

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Conectar el centro de IoT de tooyour de aplicación de ejemplo de Hola

1. Asegúrese de que se encuentra en la carpeta de repositorio de hello `iot-hub-c-feather-m0-getting-started`.

   Abra la aplicación de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:

   ```bash
   cd Lesson4
   code .
   ```

   Hola aviso `app.ino` archivo Hola `app` subcarpeta. Hola `app.ino` es archivo de origen de la clave de Hola que contiene código de hello toomonitor mensajes entrantes Hola centro de IoT. Hola `blinkLED` función parpadea Hola LED.

   ![Estructura de repositorio en la aplicación de ejemplo de Hola][repo-structure]

2. Obtener el puerto serie de hello de dispositivo de hello con cli de detección de dispositivos de hello:

   ```bash
   devdisco list --usb
   ```

   Debe ver un resultado similar siguiente toohello y encontrar Hola usb puerto COM de su placa de Arduino:

   ![Detección de dispositivos][device-discovery]

3. Archivo abierto hello `config.json` en carpeta de lección Hola y el valor de entrada Hola de hello encuentra el número de puerto COM:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > Para el puerto de hello COM, en la plataforma Windows, tiene un formato de hello `COM1, COM2, ...`. En Mac OS o Ubuntu, empezará por `/dev/`.

4. Inicializar el archivo de configuración de hello ejecutando Hola siguientes comandos:

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. Realizar Hola después reemplazos en hello `config-arduino.json` archivo:

   Si completó los pasos de hello en [crear una cuenta de aplicación y el almacenamiento de Azure función] [ create-an-azure-function-app-and-storage-account] en este equipo, se heredan todas las configuraciones de hello, por lo que puede omitir la tarea de toohello hello paso de la implementación de y ejecutar la aplicación de ejemplo de Hola. Si completó los pasos de hello en [crear una cuenta de aplicación y el almacenamiento de Azure función] [ create-an-azure-function-app-and-storage-account] en un equipo diferente, deberá marcadores de posición de tooreplace Hola Hola `config-arduino.json` archivo. Hola `config-arduino.json` archivo se encuentra en la subcarpeta de Hola de su carpeta principal.

   ![Contenido del archivo de configuración arduino.json Hola][config-arduino-json]

   * Reemplace **[Wi-Fi SSID]** con el SSID de Wi-Fi que conectado toohello Internet.
   * Reemplace **[Wi-Fi password]** por su contraseña de Wi-Fi. Quite la cadena de hello si su Wi-Fi no requiere una contraseña.
   * Reemplace **[cadena de conexión de dispositivos de IoT]** con cadena de conexión de dispositivo de Hola que obtiene mediante la ejecución de hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` comando.
   * Reemplace **[cadena de conexión de base de datos central de IoT]** con la cadena de conexión de base de datos central de IoT que obtiene mediante la ejecución de Hola Hola `az iot hub show-connection-string --name {my hub name}` comando.

## <a name="deploy-and-run-hello-sample-application"></a>Implementar y ejecutar la aplicación de ejemplo de Hola
Implementar y ejecutar aplicaciones de ejemplo de Hola en el panel de Arduino ejecutando Hola siguientes comandos:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

comando de Hello gulp implementa tooyour Arduino placa de hello ejemplo aplicación. A continuación, se ejecuta aplicación hello en el panel de Arduino y una tarea independiente en el host tooyour Arduino placa de equipo toosend 20 parpadeo mensajes desde el centro de IoT.

Después de ejecuta la aplicación de ejemplo de Hola, empieza a escuchar toomessages desde el centro de IoT. Mientras tanto, hello gulp tarea puede enviar varios mensajes "blink" de su tooyour de centro de IoT Arduino panel. Para cada mensaje de intermitencia Hola panel recibe, aplicación de ejemplo de Hola llama hello `blinkLED` hello de la función tooblink LED.

Debería ver Hola LED parpadea cada dos segundos como tarea de hello gulp envía 20 mensajes desde su tooyour de centro de IoT Arduino panel. Hello en último lugar uno es un mensaje de "stop" que detiene la aplicación hello se ejecute.

![Aplicación de ejemplo con comandos de Gulp y mensajes de parpadeo][sample-application]

## <a name="summary"></a>Resumen
Ha enviado correctamente los mensajes desde su Hola IoT hub tooyour Arduino panel tooblink LED. Hola siguiente tarea es opcional: cambie Hola activar y desactivar el comportamiento de hello LED.

## <a name="next-steps"></a>Pasos siguientes
[Cambiar Hola activar y desactivar el comportamiento de hello LED][change-the-on-and-off-led-behavior]


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md