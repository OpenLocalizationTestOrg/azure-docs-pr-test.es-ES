---
title: "Connect Raspberry PI (C) tooAzure IoT - lección 4: modificar la aplicación | Documentos de Microsoft"
description: Personalizar Hola de toochange de mensajes de Hola LED de activar y desactivar el comportamiento.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: controlar el led con raspberry pi, control del led de raspberry pi, led de control de raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 0201b8ed-d5e6-4445-9a4d-1305003d1eff
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f4739c4e9a58b4b0fe964b5c3c81e5918982099f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Cambiar Hola activar y desactivar el comportamiento de hello LED
## <a name="what-you-will-do"></a>Lo que hará
Personalizar Hola de toochange de mensajes de Hola LED de activar y desactivar el comportamiento. Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá
Usar adicional hello de toochange de funciones de Node.js LED de activar y desactivar el comportamiento.

## <a name="what-you-need"></a>Lo que necesita
Debe haber completado correctamente [ejecutar una aplicación de ejemplo en la nube de frambuesa Pi tooreceive toodevice mensajes](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).

## <a name="add-functions-toomainc-and-gulpfilejs"></a>Agregar gulpfile.js y toomain.c de funciones
1. Aplicación de ejemplo de Hola abierto en el código de Visual Studio mediante la ejecución de hello siguientes comandos:

   ```bash
   cd Lesson4
   code .
   ```
2. Abra hello `main.c` de archivos y después agregue Hola siguientes funciones después de la función blinkLED():

   ```c
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![Archivo main.c con funciones agregadas](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_c.png)
3. Agregar Hola siguientes condiciones antes de hello seleccionado de modo predeterminado en hello `if` bloque de hello `receiveMessageCallback` función:

   ```c
   else if (0 == strcmp((const char*)value, "\"on\""))
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\""))
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
   }
   ```

   ![Archivo Gulpfile.js con una función agregada](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile_c.png)
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

![Aplicación de ejemplo con mensajes de encendido y apagado](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

¡Enhorabuena! Mensajes de saludo que se envían tooPi desde el centro de IoT se personalizó correctamente.

### <a name="summary"></a>Resumen
Esta sección opcional muestra cómo toocustomize mensajes para que la aplicación de ejemplo de Hola puedan controlar Hola activar y desactivar el comportamiento de hello LED de forma diferente.
