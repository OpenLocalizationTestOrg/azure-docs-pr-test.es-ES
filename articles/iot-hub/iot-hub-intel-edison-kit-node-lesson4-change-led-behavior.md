---
title: "Conectar Intel Edison (nodo) tooAzure IoT - lección 4: hacer parpadear LED de hello | Documentos de Microsoft"
description: Personalizar Hola de toochange de mensajes de Hola LED de activar y desactivar el comportamiento.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: control del LED con Arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 387cd97e-b05e-43c4-b252-f68ad45d524a
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: caeabe311fd1698f298c6d2b4a203ecad80ef7df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Cambiar Hola activar y desactivar el comportamiento de hello LED
## <a name="what-you-will-do"></a>Lo que hará
Personalizar Hola de toochange de mensajes de Hola LED de activar y desactivar el comportamiento. Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].

## <a name="what-you-will-learn"></a>Lo qué aprenderá
Utilice Hola de funciones adicionales toochange LED de activar y desactivar el comportamiento.

## <a name="what-you-need"></a>Lo que necesita
Debe haber completado correctamente [ejecutar una aplicación de ejemplo en la nube de Intel Edison tooreceive mensajes toodevice][receive-cloud-to-device-messages].

## <a name="add-functions-tooappjs-and-gulpfilejs"></a>Agregar gulpfile.js y tooapp.js de funciones
1. Aplicación de ejemplo de Hola abierto en el código de Visual Studio mediante la ejecución de hello siguientes comandos:

   ```bash
   cd Lesson4
   code .
   ```
2. Abra hello `app.js` de archivos y después agregue Hola siguientes funciones después de la función blinkLED():

   ```javascript
   function turnOnLED() {
     myLed.write(1);
   }

   function turnOffLED() {
     myLed.write(0);
   }
   ```

   ![Archivo app.js con funciones agregadas](media/iot-hub-intel-edison-lessons/lesson4/updated_app_node.png)
3. Agregar hello las siguientes condiciones antes de hello 'blink' caso en el bloque de caso de conmutador de Hola de hello `receiveMessageCallback` función:

   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
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
   }
   ```

   ![Archivo Gulpfile.js con una función agregada][gulpfile]
5. Hola `sendMessage` función, reemplace la línea hello `var message = buildMessage(sentMessageCount);` con la nueva línea de saludo se muestra en el siguiente fragmento de código de hello:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Guarde todos los cambios de Hola.

### <a name="deploy-and-run-hello-sample-application"></a>Implementar y ejecutar la aplicación de ejemplo de Hola
Implementar y ejecutar la aplicación de ejemplo de Hola en Edison ejecutando Hola siguiente comando:

```bash
gulp deploy && gulp run
```

Debería ver Hola LED activar durante dos segundos y, a continuación, desactive para otro dos segundos. mensaje de "stop" último Hola deja de aplicación de ejemplo de Hola de ejecución.

![Encendido y apagado][on-and-off]

¡Enhorabuena! Mensajes de saludo que se envían tooEdison desde el centro de IoT se personalizó correctamente.

### <a name="summary"></a>Resumen
Esta sección opcional muestra cómo toocustomize mensajes para que la aplicación de ejemplo de Hola puedan controlar Hola activar y desactivar el comportamiento de hello LED de forma diferente.

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_node.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_node.png
