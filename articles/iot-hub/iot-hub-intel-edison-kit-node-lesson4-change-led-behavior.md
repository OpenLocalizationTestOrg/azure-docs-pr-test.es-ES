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
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="936c6-104">Cambiar Hola activar y desactivar el comportamiento de hello LED</span><span class="sxs-lookup"><span data-stu-id="936c6-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="936c6-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="936c6-105">What you will do</span></span>
<span data-ttu-id="936c6-106">Personalizar Hola de toochange de mensajes de Hola LED de activar y desactivar el comportamiento.</span><span class="sxs-lookup"><span data-stu-id="936c6-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="936c6-107">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="936c6-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="936c6-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="936c6-108">What you will learn</span></span>
<span data-ttu-id="936c6-109">Utilice Hola de funciones adicionales toochange LED de activar y desactivar el comportamiento.</span><span class="sxs-lookup"><span data-stu-id="936c6-109">Use additional functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="936c6-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="936c6-110">What you need</span></span>
<span data-ttu-id="936c6-111">Debe haber completado correctamente [ejecutar una aplicación de ejemplo en la nube de Intel Edison tooreceive mensajes toodevice][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="936c6-111">You must have successfully completed [Run a sample application on Intel Edison tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-tooappjs-and-gulpfilejs"></a><span data-ttu-id="936c6-112">Agregar gulpfile.js y tooapp.js de funciones</span><span class="sxs-lookup"><span data-stu-id="936c6-112">Add functions tooapp.js and gulpfile.js</span></span>
1. <span data-ttu-id="936c6-113">Aplicación de ejemplo de Hola abierto en el código de Visual Studio mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="936c6-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="936c6-114">Abra hello `app.js` de archivos y después agregue Hola siguientes funciones después de la función blinkLED():</span><span class="sxs-lookup"><span data-stu-id="936c6-114">Open hello `app.js` file, and then add hello following functions after blinkLED() function:</span></span>

   ```javascript
   function turnOnLED() {
     myLed.write(1);
   }

   function turnOffLED() {
     myLed.write(0);
   }
   ```

   ![Archivo app.js con funciones agregadas](media/iot-hub-intel-edison-lessons/lesson4/updated_app_node.png)
3. <span data-ttu-id="936c6-116">Agregar hello las siguientes condiciones antes de hello 'blink' caso en el bloque de caso de conmutador de Hola de hello `receiveMessageCallback` función:</span><span class="sxs-lookup"><span data-stu-id="936c6-116">Add hello following conditions before hello 'blink' case in hello switch-case block of hello `receiveMessageCallback` function:</span></span>

   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```

   <span data-ttu-id="936c6-117">Ahora ha configurado instrucciones toomore toorespond de aplicación de ejemplo de Hola a través de mensajes.</span><span class="sxs-lookup"><span data-stu-id="936c6-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="936c6-118">Hola "en" instrucción activa el LED de Hola y Hola "off" instrucción desactiva Hola LED.</span><span class="sxs-lookup"><span data-stu-id="936c6-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="936c6-119">Abra el archivo gulpfile.js de hello y, a continuación, agregar una nueva función antes de la función hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="936c6-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="936c6-121">Hola `sendMessage` función, reemplace la línea hello `var message = buildMessage(sentMessageCount);` con la nueva línea de saludo se muestra en el siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="936c6-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="936c6-122">Guarde todos los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="936c6-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="936c6-123">Implementar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="936c6-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="936c6-124">Implementar y ejecutar la aplicación de ejemplo de Hola en Edison ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="936c6-124">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="936c6-125">Debería ver Hola LED activar durante dos segundos y, a continuación, desactive para otro dos segundos.</span><span class="sxs-lookup"><span data-stu-id="936c6-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="936c6-126">mensaje de "stop" último Hola deja de aplicación de ejemplo de Hola de ejecución.</span><span class="sxs-lookup"><span data-stu-id="936c6-126">hello last "stop" message stops hello sample application from running.</span></span>

![Encendido y apagado][on-and-off]

<span data-ttu-id="936c6-128">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="936c6-128">Congratulations!</span></span> <span data-ttu-id="936c6-129">Mensajes de saludo que se envían tooEdison desde el centro de IoT se personalizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="936c6-129">You’ve successfully customized hello messages that are sent tooEdison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="936c6-130">Resumen</span><span class="sxs-lookup"><span data-stu-id="936c6-130">Summary</span></span>
<span data-ttu-id="936c6-131">Esta sección opcional muestra cómo toocustomize mensajes para que la aplicación de ejemplo de Hola puedan controlar Hola activar y desactivar el comportamiento de hello LED de forma diferente.</span><span class="sxs-lookup"><span data-stu-id="936c6-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_node.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_node.png
