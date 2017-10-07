---
title: "Conectar Intel Edison (nodo) tooAzure IoT - lección 4: recibir mensajes | Documentos de Microsoft"
description: "Una aplicación de ejemplo se ejecuta en Edison y supervisa los mensajes entrantes provenientes desde su instancia de IoT Hub. Una nueva tarea de gulp envía mensajes tooEdison desde su hello tooblink de centro de IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "control de led de arduino desde web, control de led de arduino a través de web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: aab0ced4810dd3d4f5ba636940b06563f1db9241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Ejecutar un tooreceive de la aplicación de ejemplo en la nube al dispositivo mensajes
En este artículo se implementará una aplicación de ejemplo en Intel Edison. aplicación de ejemplo de Hola supervisa los mensajes entrantes desde el centro de IoT. También permite ejecutar una tarea de gulp en su tooEdison de mensajes de toosend de equipo, el centro de IoT. Cuando la aplicación de ejemplo de Hola recibe mensajes de Hola, parpadea Hola LED. Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].

## <a name="what-you-will-do"></a>Lo que hará
* Conectar el centro de IoT de tooyour de aplicación de ejemplo de Hola.
* Implemente y ejecute la aplicación de ejemplo de Hola.
* Enviar mensajes desde su Hola de IoT hub tooEdison tooblink LED.

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:
* Cómo los mensajes entrantes de toomonitor desde el centro de IoT.
* ¿Cómo toosend en la nube al dispositivo mensajes desde su tooEdison de centro de IoT.

## <a name="what-you-need"></a>Lo que necesita
* Intel Edison, configurado para su uso. toolearn tooset seguridad Edison, vea [configurar su dispositivo][configure-your-device].
* Una instancia de IoT Hub creada en su suscripción de Azure. toolearn cómo toocreate su centro de IoT, consulte [crea el centro de IoT de Azure][create-your-azure-iot-hub].

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Conectar el centro de IoT de tooyour de aplicación de ejemplo de Hola
1. Asegúrese de que se encuentra en la carpeta de repositorio de hello `iot-hub-node-edison-getting-started`. Abra la aplicación de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:

   ```bash
   cd Lesson4
   code .
   ```

   archivo de Hello en hello `app` subcarpeta es el archivo de origen de la clave de Hola que contiene código de hello toomonitor mensajes entrantes Hola centro de IoT. Hola `blinkLED` función parpadea Hola LED.

   ![Estructura de repositorio en la aplicación de ejemplo de Hola][repo-structure]
2. Inicializar el archivo de configuración de hello ejecutando Hola siguientes comandos:

   ```bash
   npm install
   gulp init
   ```

   Si completó los pasos de hello en [crear una cuenta de aplicación y el almacenamiento de Azure función] [ create-an-azure-function-app-and-storage-account] en este equipo, se heredan todas las configuraciones de hello, por lo que puede omitir la tarea de toohello hello paso de la implementación de y ejecutar la aplicación de ejemplo de Hola. Si completó los pasos de hello en [crear una cuenta de aplicación y el almacenamiento de Azure función] [ create-an-azure-function-app-and-storage-account] en un equipo diferente, deberá marcadores de posición de tooreplace Hola Hola `config-edison.json` archivo. Hola `config-edison.json` archivo se encuentra en la subcarpeta de Hola de su carpeta principal.

   ![Contenido del archivo de configuración edison.json Hola](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * Reemplace **[nombre de host de dispositivo o dirección IP]** con la dirección IP del dispositivo Hola marcados como inactivos cuando se configura el dispositivo.
   * Reemplace **[cadena de conexión de dispositivos de IoT]** con cadena de conexión de dispositivo de Hola que obtiene mediante la ejecución de hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` comando.
   * Reemplace **[cadena de conexión de base de datos central de IoT]** con la cadena de conexión de base de datos central de IoT que obtiene mediante la ejecución de Hola Hola `az iot hub show-connection-string --name {my hub name}` comando.

## <a name="deploy-and-run-hello-sample-application"></a>Implementar y ejecutar la aplicación de ejemplo de Hola
Implementar y ejecutar la aplicación de ejemplo de Hola en Edison ejecutando Hola siguientes comandos:

```bash
gulp deploy && gulp run
```

comando de Hello gulp implementa tooEdison de aplicación de ejemplo de Hola. A continuación, se ejecuta aplicación hello en Edison y una tarea independiente en su host de equipo toosend 20 parpadeo mensajes tooEdison desde el centro de IoT.

Después de ejecuta la aplicación de ejemplo de Hola, empieza a escuchar toomessages desde el centro de IoT. Mientras tanto, hello gulp tarea puede enviar varios mensajes "blink" de su tooEdison de centro de IoT. Para cada mensaje de intermitencia Edison recibe, aplicación de ejemplo de Hola llama hello `blinkLED` hello de la función tooblink LED.

Verá parpadear LED de hello cada dos segundos como hello gulp tarea envía 20 mensajes desde su tooEdison de centro de IoT. Hello en último lugar uno es un mensaje de "stop" que detiene la aplicación hello se ejecute.

![Aplicación de ejemplo con comandos de Gulp y mensajes de parpadeo][gulp-command-and-blink-messages]

## <a name="summary"></a>Resumen
Ha enviado correctamente los mensajes desde su Hola de IoT hub tooEdison tooblink LED. Hola siguiente tarea es opcional: cambie Hola activar y desactivar el comportamiento de hello LED.

## <a name="next-steps"></a>Pasos siguientes
[Cambiar Hola activar y desactivar el comportamiento de hello LED][change-the-on-and-off-behavior-of-the-led]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md