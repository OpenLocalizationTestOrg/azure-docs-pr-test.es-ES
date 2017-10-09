---
title: "Connect Arduino (C) tooAzure IoT - lección 4: modificar la aplicación | Documentos de Microsoft"
description: Personalizar Hola de toochange de mensajes de Hola LED de activar y desactivar el comportamiento.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: control del LED con Arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: d7a25430-450e-43c4-a3ed-1eed995b8b7e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8cc438650f01ae4335d91c94df6a29e0ffbdc508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Cambiar Hola activar y desactivar el comportamiento de hello LED
## <a name="what-you-will-do"></a>Lo que hará
Personalizar Hola de toochange de mensajes de Hola LED de activar y desactivar el comportamiento. Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) de su placa Adafruit compacto M0 Wi-Fi Arduino.

## <a name="what-you-will-learn"></a>Lo qué aprenderá
Utilice adicional Hola de toochange funciones Arduino LED de activar y desactivar el comportamiento.

## <a name="what-you-need"></a>Lo que necesita
Debe haber completado correctamente [ejecutar una aplicación de ejemplo en la nube de tooreceive Arduino panel mensajes toodevice][receive-cloud-to-device-messages].

## <a name="add-functions-toomainc-and-gulpfilejs"></a>Agregar gulpfile.js y toomain.c de funciones
1. Aplicación de ejemplo de Hola abierto en el código de Visual Studio mediante la ejecución de hello siguientes comandos:

   ```bash
   cd Lesson4
   code .
   ```
2. Abra hello `app.ino` de archivos y después agregue Hola siguientes funciones después de la función blinkLED():

   ```arduino
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![Archivo app.js con funciones agregadas][app-ino-file]
3. Agregar Hola siguientes condiciones antes de hello `else if` bloque de hello `receiveMessageCallback` función:

   ```arduino
   else if (strcmp((const char*)value, "\"on\"") == 0)
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\"") == 0)
   {
       turnOffLED();
   }
   ```

   Ahora ha configurado instrucciones toomore toorespond de aplicación de ejemplo de Hola a través de mensajes. Hola "en" instrucción activa el LED de Hola y Hola "off" instrucción desactiva Hola LED.
4. Abra el archivo gulpfile.js de hello y, a continuación, agregar una nueva función antes de la función hello `sendMessage`:

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   };
   ```

   ![Archivo Gulpfile.js con una función agregada][gulp-file-js]
5. Hola `sendMessage` función, reemplace la línea hello `var message = buildMessage(sentMessageCount);` con la nueva línea de saludo se muestra en el siguiente fragmento de código de hello:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Guarde todos los cambios de Hola.

### <a name="deploy-and-run-hello-sample-application"></a>Implementar y ejecutar la aplicación de ejemplo de Hola
Implementar y ejecutar la aplicación de ejemplo de Hola en el panel de Arduino ejecutando Hola siguiente comando:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

Debería ver Hola LED activar durante dos segundos y, a continuación, desactive para otro dos segundos. mensaje de "stop" último Hola deja de aplicación de ejemplo de Hola de ejecución.

![Encendido y apagado][on-and-off]

¡Enhorabuena! Mensajes de saludo que se envían tooyour Arduino panel desde el centro de IoT se personalizó correctamente.

### <a name="summary"></a>Resumen
Esta sección opcional muestra cómo toocustomize mensajes para que la aplicación de ejemplo de Hola puedan controlar Hola activar y desactivar el comportamiento de hello LED de forma diferente.

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png