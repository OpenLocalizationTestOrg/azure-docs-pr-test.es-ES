---
title: "Conexión de Intel Edison (C) a Azure IoT: Lección 4: Parpadeo del LED | Microsoft Docs"
description: Personalice los mensajes para cambiar el comportamiento de encendido y apagado del LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: control del LED con Arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 9826c55a-0e24-4296-ae54-29b7fe66436a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4852b1cca4c6186ef4857b903b771f76cc20adb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="f5a6d-104">Modificación del comportamiento de encendido y apagado del LED</span><span class="sxs-lookup"><span data-stu-id="f5a6d-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="f5a6d-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="f5a6d-105">What you will do</span></span>
<span data-ttu-id="f5a6d-106">Personalice los mensajes para cambiar el comportamiento de encendido y apagado del LED.</span><span class="sxs-lookup"><span data-stu-id="f5a6d-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="f5a6d-107">Si tiene problemas, busque soluciones en [esta página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="f5a6d-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f5a6d-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="f5a6d-108">What you will learn</span></span>
<span data-ttu-id="f5a6d-109">Utilice las funciones adicionales para cambiar el comportamiento de encendido y apagado del LED.</span><span class="sxs-lookup"><span data-stu-id="f5a6d-109">Use additional functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f5a6d-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="f5a6d-110">What you need</span></span>
<span data-ttu-id="f5a6d-111">Para seguir este procedimiento, debe haber completado correctamente el tutorial sobre la [ejecución de una aplicación de ejemplo en Intel Edison para recibir mensajes de nube a dispositivo][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="f5a6d-111">You must have successfully completed [Run a sample application on Intel Edison to receive cloud to device messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-to-mainc-and-gulpfilejs"></a><span data-ttu-id="f5a6d-112">Adición de funciones a main.c y gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="f5a6d-112">Add functions to main.c and gulpfile.js</span></span>
1. <span data-ttu-id="f5a6d-113">Abra la aplicación de ejemplo en Visual Studio Code ejecutando los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f5a6d-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="f5a6d-114">Abra el archivo `main.c` y, luego, agregue las siguientes funciones después de blinkLED():</span><span class="sxs-lookup"><span data-stu-id="f5a6d-114">Open the `main.c` file, and then add the following functions after blinkLED() function:</span></span>

   ```c
   static void turnOnLED()
   {
     mraa_gpio_write(context, 1);
   }

   static void turnOffLED()
   {
     mraa_gpio_write(context, 0);
   }
   ```

   ![Archivo main.c con funciones agregadas](media/iot-hub-intel-edison-lessons/lesson4/updated_app_c.png)

3. <span data-ttu-id="f5a6d-116">Agregue las siguientes condiciones antes del bloqueo `else if` de la función `receiveMessageCallback`:</span><span class="sxs-lookup"><span data-stu-id="f5a6d-116">Add the following conditions before the `else if` block of the `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="f5a6d-117">Ahora ha configurado la aplicación de ejemplo para responder a más instrucciones a través de mensajes.</span><span class="sxs-lookup"><span data-stu-id="f5a6d-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="f5a6d-118">La instrucción "on" enciende el LED, mientras que la instrucción "off" lo apaga.</span><span class="sxs-lookup"><span data-stu-id="f5a6d-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="f5a6d-119">Abra el archivo gulpfile.js y, después, agregue una función nueva antes de la función `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="f5a6d-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

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
5. <span data-ttu-id="f5a6d-121">En la función `sendMessage`, reemplace la línea `var message = buildMessage(sentMessageCount);` por la nueva línea que se muestra en el siguiente fragmento:</span><span class="sxs-lookup"><span data-stu-id="f5a6d-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="f5a6d-122">Guarde todos los cambios.</span><span class="sxs-lookup"><span data-stu-id="f5a6d-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="f5a6d-123">Implementación y ejecución de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f5a6d-123">Deploy and run the sample application</span></span>
<span data-ttu-id="f5a6d-124">Implemente y ejecute la aplicación de ejemplo en Edison usando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="f5a6d-124">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="f5a6d-125">El LED debería encenderse durante dos segundos y apagarse después otros dos segundos.</span><span class="sxs-lookup"><span data-stu-id="f5a6d-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="f5a6d-126">El último mensaje "stop" detiene la ejecución de la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f5a6d-126">The last "stop" message stops the sample application from running.</span></span>

![Encendido y apagado][on-and-off]

<span data-ttu-id="f5a6d-128">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="f5a6d-128">Congratulations!</span></span> <span data-ttu-id="f5a6d-129">Ha personalizado correctamente los mensajes que se envían a Edison desde IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f5a6d-129">You’ve successfully customized the messages that are sent to Edison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="f5a6d-130">Resumen</span><span class="sxs-lookup"><span data-stu-id="f5a6d-130">Summary</span></span>
<span data-ttu-id="f5a6d-131">En esta sección opcional, se explica cómo personalizar los mensajes para que la aplicación de ejemplo pueda controlar el comportamiento de encendido y apagado del LED de manera diferente.</span><span class="sxs-lookup"><span data-stu-id="f5a6d-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png
