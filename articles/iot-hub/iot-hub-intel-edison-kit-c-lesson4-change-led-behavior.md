---
title: "Connect Intel Edison (C) tooAzure IoT - lección 4: hacer parpadear LED de hello | Documentos de Microsoft"
description: Personalizar Hola de toochange de mensajes de Hola LED de activar y desactivar el comportamiento.
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
ms.openlocfilehash: c51acb42aa297ca91cfe76d7b0361ad95e2fb2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="45bcf-104">Cambiar Hola activar y desactivar el comportamiento de hello LED</span><span class="sxs-lookup"><span data-stu-id="45bcf-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="45bcf-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="45bcf-105">What you will do</span></span>
<span data-ttu-id="45bcf-106">Personalizar Hola de toochange de mensajes de Hola LED de activar y desactivar el comportamiento.</span><span class="sxs-lookup"><span data-stu-id="45bcf-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="45bcf-107">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="45bcf-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="45bcf-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="45bcf-108">What you will learn</span></span>
<span data-ttu-id="45bcf-109">Utilice Hola de funciones adicionales toochange LED de activar y desactivar el comportamiento.</span><span class="sxs-lookup"><span data-stu-id="45bcf-109">Use additional functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="45bcf-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="45bcf-110">What you need</span></span>
<span data-ttu-id="45bcf-111">Debe haber completado correctamente [ejecutar una aplicación de ejemplo en la nube de Intel Edison tooreceive mensajes toodevice][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="45bcf-111">You must have successfully completed [Run a sample application on Intel Edison tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="45bcf-112">Agregar gulpfile.js y toomain.c de funciones</span><span class="sxs-lookup"><span data-stu-id="45bcf-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="45bcf-113">Aplicación de ejemplo de Hola abierto en el código de Visual Studio mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="45bcf-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="45bcf-114">Abra hello `main.c` de archivos y después agregue Hola siguientes funciones después de la función blinkLED():</span><span class="sxs-lookup"><span data-stu-id="45bcf-114">Open hello `main.c` file, and then add hello following functions after blinkLED() function:</span></span>

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

3. <span data-ttu-id="45bcf-116">Agregar Hola siguientes condiciones antes de hello `else if` bloque de hello `receiveMessageCallback` función:</span><span class="sxs-lookup"><span data-stu-id="45bcf-116">Add hello following conditions before hello `else if` block of hello `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="45bcf-117">Ahora ha configurado instrucciones toomore toorespond de aplicación de ejemplo de Hola a través de mensajes.</span><span class="sxs-lookup"><span data-stu-id="45bcf-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="45bcf-118">Hola "en" instrucción activa el LED de Hola y Hola "off" instrucción desactiva Hola LED.</span><span class="sxs-lookup"><span data-stu-id="45bcf-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="45bcf-119">Abra el archivo gulpfile.js de hello y, a continuación, agregar una nueva función antes de la función hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="45bcf-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="45bcf-121">Hola `sendMessage` función, reemplace la línea hello `var message = buildMessage(sentMessageCount);` con la nueva línea de saludo se muestra en el siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="45bcf-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="45bcf-122">Guarde todos los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="45bcf-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="45bcf-123">Implementar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="45bcf-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="45bcf-124">Implementar y ejecutar la aplicación de ejemplo de Hola en Edison ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="45bcf-124">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="45bcf-125">Debería ver Hola LED activar durante dos segundos y, a continuación, desactive para otro dos segundos.</span><span class="sxs-lookup"><span data-stu-id="45bcf-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="45bcf-126">mensaje de "stop" último Hola deja de aplicación de ejemplo de Hola de ejecución.</span><span class="sxs-lookup"><span data-stu-id="45bcf-126">hello last "stop" message stops hello sample application from running.</span></span>

![Encendido y apagado][on-and-off]

<span data-ttu-id="45bcf-128">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="45bcf-128">Congratulations!</span></span> <span data-ttu-id="45bcf-129">Mensajes de saludo que se envían tooEdison desde el centro de IoT se personalizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="45bcf-129">You’ve successfully customized hello messages that are sent tooEdison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="45bcf-130">Resumen</span><span class="sxs-lookup"><span data-stu-id="45bcf-130">Summary</span></span>
<span data-ttu-id="45bcf-131">Esta sección opcional muestra cómo toocustomize mensajes para que la aplicación de ejemplo de Hola puedan controlar Hola activar y desactivar el comportamiento de hello LED de forma diferente.</span><span class="sxs-lookup"><span data-stu-id="45bcf-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png
