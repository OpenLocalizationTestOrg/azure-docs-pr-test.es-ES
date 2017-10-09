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
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="fc6aa-104">Cambiar Hola activar y desactivar el comportamiento de hello LED</span><span class="sxs-lookup"><span data-stu-id="fc6aa-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="fc6aa-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="fc6aa-105">What you will do</span></span>
<span data-ttu-id="fc6aa-106">Personalizar Hola de toochange de mensajes de Hola LED de activar y desactivar el comportamiento.</span><span class="sxs-lookup"><span data-stu-id="fc6aa-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="fc6aa-107">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="fc6aa-107">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fc6aa-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="fc6aa-108">What you will learn</span></span>
<span data-ttu-id="fc6aa-109">Usar adicional hello de toochange de funciones de Node.js LED de activar y desactivar el comportamiento.</span><span class="sxs-lookup"><span data-stu-id="fc6aa-109">Use additional Node.js functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fc6aa-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="fc6aa-110">What you need</span></span>
<span data-ttu-id="fc6aa-111">Debe haber completado correctamente [ejecutar una aplicación de ejemplo en frambuesa Pi tooreceive mensajes en la nube al dispositivo](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="fc6aa-111">You must have successfully completed [Run a sample application on Raspberry Pi tooreceive cloud-to-device messages](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-nodejs-functions"></a><span data-ttu-id="fc6aa-112">Adición de funciones de Node.js</span><span class="sxs-lookup"><span data-stu-id="fc6aa-112">Add Node.js functions</span></span>
1. <span data-ttu-id="fc6aa-113">Aplicación de ejemplo de Hola abierto en el código de Visual Studio mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="fc6aa-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="fc6aa-114">Abra hello `app.js` de archivos y después agregue Hola siguientes funciones al final de hello:</span><span class="sxs-lookup"><span data-stu-id="fc6aa-114">Open hello `app.js` file, and then add hello following functions at hello end:</span></span>
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![Archivo App.js con funciones agregadas](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. <span data-ttu-id="fc6aa-116">Agregar Hola siguientes condiciones antes de hello seleccionado de modo predeterminado en bloque de caso de conmutador de Hola de hello `receiveMessageCallback` función:</span><span class="sxs-lookup"><span data-stu-id="fc6aa-116">Add hello following conditions before hello default one in hello switch-case block of hello `receiveMessageCallback` function:</span></span>
   
   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```
   
   <span data-ttu-id="fc6aa-117">Ahora ha configurado instrucciones toomore toorespond de aplicación de ejemplo de Hola a través de mensajes.</span><span class="sxs-lookup"><span data-stu-id="fc6aa-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="fc6aa-118">Hola "en" instrucción activa el LED de Hola y Hola "off" instrucción desactiva Hola LED.</span><span class="sxs-lookup"><span data-stu-id="fc6aa-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="fc6aa-119">Abra el archivo gulpfile.js de hello y, a continuación, agregar una nueva función antes de la función hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="fc6aa-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>
   
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
5. <span data-ttu-id="fc6aa-121">Hola `sendMessage` función, reemplace la línea hello `var message = buildMessage(sentMessageCount);` con la nueva línea de saludo se muestra en el siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="fc6aa-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="fc6aa-122">Guarde todos los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc6aa-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="fc6aa-123">Implementar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="fc6aa-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="fc6aa-124">Implementar y ejecutar la aplicación de ejemplo de Hola en Pi ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fc6aa-124">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="fc6aa-125">Debería ver Hola LED activar durante dos segundos y, a continuación, desactive para otro dos segundos.</span><span class="sxs-lookup"><span data-stu-id="fc6aa-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="fc6aa-126">mensaje de "stop" último Hola deja de aplicación de ejemplo de Hola de ejecución.</span><span class="sxs-lookup"><span data-stu-id="fc6aa-126">hello last "stop" message stops hello sample application from running.</span></span>

![Aplicación de ejemplo con mensajes de encendido y apagado](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

<span data-ttu-id="fc6aa-128">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="fc6aa-128">Congratulations!</span></span> <span data-ttu-id="fc6aa-129">Mensajes de saludo que se envían tooPi desde el centro de IoT se personalizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="fc6aa-129">You’ve successfully customized hello messages that are sent tooPi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="fc6aa-130">Resumen</span><span class="sxs-lookup"><span data-stu-id="fc6aa-130">Summary</span></span>
<span data-ttu-id="fc6aa-131">Esta sección opcional muestra cómo toocustomize mensajes para que la aplicación de ejemplo de Hola puedan controlar Hola activar y desactivar el comportamiento de hello LED de forma diferente.</span><span class="sxs-lookup"><span data-stu-id="fc6aa-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

