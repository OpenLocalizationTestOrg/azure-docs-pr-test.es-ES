---
title: "Conexión de Raspberry Pi (C) a Azure IoT: Lección 4: Modificación de la aplicación | Microsoft Docs"
description: Personalice los mensajes para cambiar el comportamiento de encendido y apagado del LED.
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
ms.openlocfilehash: b1e441b20e161f4a03d4c2c300b21aca4fedb2a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="680e3-104">Modificación del comportamiento de encendido y apagado del LED</span><span class="sxs-lookup"><span data-stu-id="680e3-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="680e3-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="680e3-105">What you will do</span></span>
<span data-ttu-id="680e3-106">Personalice los mensajes para cambiar el comportamiento de encendido y apagado del LED.</span><span class="sxs-lookup"><span data-stu-id="680e3-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="680e3-107">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="680e3-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="680e3-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="680e3-108">What you will learn</span></span>
<span data-ttu-id="680e3-109">Utilice las funciones adicionales de Node.js para cambiar el comportamiento de encendido y apagado del LED.</span><span class="sxs-lookup"><span data-stu-id="680e3-109">Use additional Node.js functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="680e3-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="680e3-110">What you need</span></span>
<span data-ttu-id="680e3-111">Para seguir este procedimiento, debe haber completado correctamente el tutorial sobre la [ejecución de una aplicación de ejemplo en Raspberry Pi para recibir mensajes de nube a dispositivo](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="680e3-111">You must have successfully completed [Run a sample application on Raspberry Pi to receive cloud to device messages](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-functions-to-mainc-and-gulpfilejs"></a><span data-ttu-id="680e3-112">Adición de funciones a main.c y gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="680e3-112">Add functions to main.c and gulpfile.js</span></span>
1. <span data-ttu-id="680e3-113">Abra la aplicación de ejemplo en Visual Studio Code ejecutando los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="680e3-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="680e3-114">Abra el archivo `main.c` y, luego, agregue las siguientes funciones después de blinkLED():</span><span class="sxs-lookup"><span data-stu-id="680e3-114">Open the `main.c` file, and then add the following functions after blinkLED() function:</span></span>

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
3. <span data-ttu-id="680e3-116">Agregue las siguientes condiciones antes de la predeterminada en el bloque `if` de la función `receiveMessageCallback`:</span><span class="sxs-lookup"><span data-stu-id="680e3-116">Add the following conditions before the default one in the `if` block of the `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="680e3-117">Ahora ha configurado la aplicación de ejemplo para responder a más instrucciones a través de mensajes.</span><span class="sxs-lookup"><span data-stu-id="680e3-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="680e3-118">La instrucción "on" enciende el LED, mientras que la instrucción "off" lo apaga.</span><span class="sxs-lookup"><span data-stu-id="680e3-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="680e3-119">Abra el archivo gulpfile.js y, después, agregue una función nueva antes de la función `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="680e3-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

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
5. <span data-ttu-id="680e3-121">En la función `sendMessage`, reemplace la línea `var message = buildMessage(sentMessageCount);` por la nueva línea que se muestra en el siguiente fragmento:</span><span class="sxs-lookup"><span data-stu-id="680e3-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="680e3-122">Guarde todos los cambios.</span><span class="sxs-lookup"><span data-stu-id="680e3-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="680e3-123">Implementación y ejecución de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="680e3-123">Deploy and run the sample application</span></span>
<span data-ttu-id="680e3-124">Implemente y ejecute la aplicación de ejemplo en PI mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="680e3-124">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="680e3-125">El LED debería encenderse durante dos segundos y apagarse después otros dos segundos.</span><span class="sxs-lookup"><span data-stu-id="680e3-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="680e3-126">El último mensaje "stop" detiene la ejecución de la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="680e3-126">The last "stop" message stops the sample application from running.</span></span>

![Aplicación de ejemplo con mensajes de encendido y apagado](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

<span data-ttu-id="680e3-128">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="680e3-128">Congratulations!</span></span> <span data-ttu-id="680e3-129">Ha personalizado correctamente los mensajes que se envían a Pi desde IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="680e3-129">You’ve successfully customized the messages that are sent to Pi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="680e3-130">Resumen</span><span class="sxs-lookup"><span data-stu-id="680e3-130">Summary</span></span>
<span data-ttu-id="680e3-131">En esta sección opcional, se explica cómo personalizar los mensajes para que la aplicación de ejemplo pueda controlar el comportamiento de encendido y apagado del LED de manera diferente.</span><span class="sxs-lookup"><span data-stu-id="680e3-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>
