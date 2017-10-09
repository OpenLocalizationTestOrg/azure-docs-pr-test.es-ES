---
title: "Conectar frambuesa Pi (nodo) tooAzure IoT - lección 4: modificar la aplicación | Documentos de Microsoft"
description: Personalizar Hola de toochange de mensajes de Hola LED de activar y desactivar el comportamiento.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: controlar el led con raspberry pi, control del led de raspberry pi, led de control de raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 3b42a4ad-0197-42f6-8ca9-04c883e879e8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 99b542fcb8639add0f5a0f7a49dd8abd0e224a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Cambiar Hola activar y desactivar el comportamiento de hello LED
## <a name="what-you-will-do"></a>Lo que hará
Personalizar Hola de toochange de mensajes de Hola LED de activar y desactivar el comportamiento. Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá
Usar adicional hello de toochange de funciones de Node.js LED de activar y desactivar el comportamiento.

## <a name="what-you-need"></a>Lo que necesita
Debe haber completado correctamente [ejecutar una aplicación de ejemplo en frambuesa Pi tooreceive mensajes en la nube al dispositivo](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).

## <a name="add-nodejs-functions"></a>Adición de funciones de Node.js
1. Aplicación de ejemplo de Hola abierto en el código de Visual Studio mediante la ejecución de hello siguientes comandos:
   
   ```bash
   cd Lesson4
   code .
   ```
2. Abra hello `app.js` de archivos y después agregue Hola siguientes funciones al final de hello:
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![Archivo App.js con funciones agregadas](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. Agregar Hola siguientes condiciones antes de hello seleccionado de modo predeterminado en bloque de caso de conmutador de Hola de hello `receiveMessageCallback` función:
   
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
   
   ![Archivo Gulpfile.js con una función agregada](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile.png)
5. Hola `sendMessage` función, reemplace la línea hello `var message = buildMessage(sentMessageCount);` con la nueva línea de saludo se muestra en el siguiente fragmento de código de hello:
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Guarde todos los cambios de Hola.

### <a name="deploy-and-run-hello-sample-application"></a>Implementar y ejecutar la aplicación de ejemplo de Hola
Implementar y ejecutar la aplicación de ejemplo de Hola en Pi ejecutando Hola siguiente comando:

```bash
gulp deploy && gulp run
```

Debería ver Hola LED activar durante dos segundos y, a continuación, desactive para otro dos segundos. mensaje de "stop" último Hola deja de aplicación de ejemplo de Hola de ejecución.

![Aplicación de ejemplo con mensajes de encendido y apagado](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

¡Enhorabuena! Mensajes de saludo que se envían tooPi desde el centro de IoT se personalizó correctamente.

### <a name="summary"></a>Resumen
Esta sección opcional muestra cómo toocustomize mensajes para que la aplicación de ejemplo de Hola puedan controlar Hola activar y desactivar el comportamiento de hello LED de forma diferente.

