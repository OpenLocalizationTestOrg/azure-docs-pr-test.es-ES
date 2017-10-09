---
featureFlags: usabilla
title: "Conectar frambuesa Pi (nodo) tooAzure IoT - lección 4: en la nube al dispositivo | Documentos de Microsoft"
description: "aplicación de ejemplo de Hola se ejecuta en Pi y supervisa los mensajes entrantes desde el centro de IoT. Una nueva tarea de gulp envía mensajes tooPi desde su hello tooblink de centro de IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: en la nube toodevice, mensaje de nube
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d69ded4e30c27378481ab2a4fb9c5b73be7bd44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-tooreceive-cloud-to-device-messages"></a>Ejecutar mensajes de Hola ejemplo aplicación tooreceive en la nube al dispositivo
En este artículo, implementará una aplicación de ejemplo en Raspberry Pi 3. aplicación de ejemplo de Hola supervisa los mensajes entrantes desde el centro de IoT. También permite ejecutar una tarea de gulp en su tooPi de mensajes de toosend de equipo, el centro de IoT. Cuando la aplicación de ejemplo de Hola recibe mensajes de Hola, parpadea Hola LED. Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-do"></a>Lo que hará
* Conectar el centro de IoT de tooyour de aplicación de ejemplo de Hola.
* Implemente y ejecute la aplicación de ejemplo de Hola.
* Enviar mensajes desde su Hola de IoT hub tooPi tooblink LED.

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:
* Cómo los mensajes entrantes de toomonitor desde el centro de IoT
* ¿Cómo toosend en la nube al dispositivo mensajes desde su tooPi de centro de IoT.

## <a name="what-you-need"></a>Lo que necesita
* Un dispositivo Raspberry Pi 3, con la configuración lista para utilizarse. toolearn tooset seguridad Pi, vea [configurar el dispositivo](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).
* Una instancia de IoT Hub creada en su suscripción de Azure. toolearn cómo toocreate su centro de IoT, consulte [crear su centro de IoT y registrar frambuesa Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Conectar el centro de IoT de tooyour de aplicación de ejemplo de Hola
1. Asegúrese de que se encuentra en la carpeta de repositorio de hello `iot-hub-node-raspberrypi-getting-started`. Abra la aplicación de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:
   
   ```bash
   cd Lesson4
   code .
   ```
   
   Hola aviso `app.js` archivo Hola `app` subcarpeta. Hola `app.js` es archivo de origen de la clave de Hola que contiene código de hello toomonitor mensajes entrantes Hola centro de IoT. Hola `blinkLED` función parpadea Hola LED.
   
   ![Estructura de repositorio en la aplicación de ejemplo de Hola](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. Inicializar el archivo de configuración de hello mediante Hola siguientes comandos:
   
   ```bash
   npm install
   gulp init
   ```
   
   Si completó los pasos de hello en [crear una cuenta de aplicación y el almacenamiento de Azure función](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) en este equipo, se heredan todas las configuraciones de hello, por lo que puede omitir toohello tarea de implementar y ejecutar la aplicación de ejemplo de Hola. Si completó los pasos de hello en [crear una cuenta de aplicación y el almacenamiento de Azure función](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) en un equipo diferente, deberá marcadores de posición de tooreplace Hola Hola `config-raspberrypi.json` archivo. Hola `config-raspberrypi.json` archivo se encuentra en la subcarpeta de Hola de su carpeta principal.
   
   ![Contenido del archivo de configuración raspberrypi.json Hola](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* Reemplace **[nombre de host de dispositivo o dirección IP]** con la dirección IP de hello Pi o hello de nombre de host que obtiene mediante la ejecución de hello `devdisco list --eth` comando.
* Reemplace **[cadena de conexión de dispositivos de IoT]** con cadena de conexión de dispositivo de Hola que obtiene mediante la ejecución de hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` comando.
* Reemplace **[cadena de conexión de base de datos central de IoT]** con la cadena de conexión de base de datos central de IoT que obtiene mediante la ejecución de Hola Hola `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` comando.

> [!NOTE]
> Ejecute también **gulp install-tools** si no lo hizo en la lección 1.

## <a name="deploy-and-run-hello-sample-application"></a>Implementar y ejecutar la aplicación de ejemplo de Hola
Implementar y ejecutar la aplicación de ejemplo de Hola en Pi ejecutando Hola siguiente comando:

```bash
gulp deploy && gulp run
```

comando de Hello implementa tooPi de aplicación de ejemplo de Hola. A continuación, se ejecuta aplicación hello en Pi y una tarea independiente en su host de equipo toosend 20 parpadeo mensajes tooPi desde el centro de IoT.

Después de ejecuta la aplicación de ejemplo de Hola, empieza a escuchar toomessages desde el centro de IoT. Mientras tanto, hello gulp tarea puede enviar varios mensajes "blink" de su tooPi de centro de IoT. Para cada mensaje parpadeo que recibe de Pi, aplicación de ejemplo de Hola llama hello `blinkLED` hello de la función tooblink LED.

Verá parpadear LED de hello cada dos segundos como hello gulp tarea envía 20 mensajes desde su tooPi de centro de IoT. Hello en último lugar uno es un mensaje de "stop" que indica toostop de aplicación Hola ejecutando.

![Aplicación de ejemplo con comandos de Gulp y mensajes de parpadeo](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a>Resumen
Ha enviado correctamente los mensajes desde su Hola de IoT hub tooPi tooblink LED. Hola siguiente tarea es opcional: cambie Hola activar y desactivar el comportamiento de hello LED.

## <a name="next-steps"></a>Pasos siguientes
[Cambiar Hola activar y desactivar el comportamiento de hello LED](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

