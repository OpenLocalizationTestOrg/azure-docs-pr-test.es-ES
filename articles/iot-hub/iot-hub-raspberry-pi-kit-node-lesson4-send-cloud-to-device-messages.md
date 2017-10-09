---
featureFlags: usabilla
title: "Conectar frambuesa Pi (nodo) tooAzure IoT - lección 4: en la nube al dispositivo | Documentos de Microsoft"
description: "aplicación de ejemplo de Hola se ejecuta en Pi y supervisa los mensajes entrantes desde el centro de IoT. Una nueva tarea de gulp envía mensajes tooPi desde su hello tooblink de centro de IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: en la nube toodevice, mensaje de nube
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d69ded4e30c27378481ab2a4fb9c5b73be7bd44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="e20e1-105">Ejecutar mensajes de Hola ejemplo aplicación tooreceive en la nube al dispositivo</span><span class="sxs-lookup"><span data-stu-id="e20e1-105">Run hello sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="e20e1-106">En este artículo, implementará una aplicación de ejemplo en Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="e20e1-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="e20e1-107">aplicación de ejemplo de Hola supervisa los mensajes entrantes desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e20e1-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="e20e1-108">También permite ejecutar una tarea de gulp en su tooPi de mensajes de toosend de equipo, el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e20e1-108">You also run a gulp task on your computer toosend messages tooPi from your IoT hub.</span></span> <span data-ttu-id="e20e1-109">Cuando la aplicación de ejemplo de Hola recibe mensajes de Hola, parpadea Hola LED.</span><span class="sxs-lookup"><span data-stu-id="e20e1-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="e20e1-110">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e20e1-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e20e1-111">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="e20e1-111">What you will do</span></span>
* <span data-ttu-id="e20e1-112">Conectar el centro de IoT de tooyour de aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e20e1-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="e20e1-113">Implemente y ejecute la aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e20e1-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="e20e1-114">Enviar mensajes desde su Hola de IoT hub tooPi tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="e20e1-114">Send messages from your IoT hub tooPi tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e20e1-115">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="e20e1-115">What you will learn</span></span>
<span data-ttu-id="e20e1-116">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e20e1-116">In this article, you will learn:</span></span>
* <span data-ttu-id="e20e1-117">Cómo los mensajes entrantes de toomonitor desde el centro de IoT</span><span class="sxs-lookup"><span data-stu-id="e20e1-117">How toomonitor incoming messages from your IoT hub</span></span>
* <span data-ttu-id="e20e1-118">¿Cómo toosend en la nube al dispositivo mensajes desde su tooPi de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e20e1-118">How toosend cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e20e1-119">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="e20e1-119">What you need</span></span>
* <span data-ttu-id="e20e1-120">Un dispositivo Raspberry Pi 3, con la configuración lista para utilizarse.</span><span class="sxs-lookup"><span data-stu-id="e20e1-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="e20e1-121">toolearn tooset seguridad Pi, vea [configurar el dispositivo](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="e20e1-121">toolearn how tooset up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="e20e1-122">Una instancia de IoT Hub creada en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="e20e1-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="e20e1-123">toolearn cómo toocreate su centro de IoT, consulte [crear su centro de IoT y registrar frambuesa Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="e20e1-123">toolearn how toocreate your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="e20e1-124">Conectar el centro de IoT de tooyour de aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="e20e1-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="e20e1-125">Asegúrese de que se encuentra en la carpeta de repositorio de hello `iot-hub-node-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="e20e1-125">Make sure that you're in hello repo folder `iot-hub-node-raspberrypi-getting-started`.</span></span> <span data-ttu-id="e20e1-126">Abra la aplicación de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e20e1-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
   
   <span data-ttu-id="e20e1-127">Hola aviso `app.js` archivo Hola `app` subcarpeta.</span><span class="sxs-lookup"><span data-stu-id="e20e1-127">Notice hello `app.js` file in hello `app` subfolder.</span></span> <span data-ttu-id="e20e1-128">Hola `app.js` es archivo de origen de la clave de Hola que contiene código de hello toomonitor mensajes entrantes Hola centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e20e1-128">hello `app.js` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="e20e1-129">Hola `blinkLED` función parpadea Hola LED.</span><span class="sxs-lookup"><span data-stu-id="e20e1-129">hello `blinkLED` function blinks hello LED.</span></span>
   
   ![Estructura de repositorio en la aplicación de ejemplo de Hola](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. <span data-ttu-id="e20e1-131">Inicializar el archivo de configuración de hello mediante Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e20e1-131">Initialize hello configuration file by using hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
   
   <span data-ttu-id="e20e1-132">Si completó los pasos de hello en [crear una cuenta de aplicación y el almacenamiento de Azure función](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) en este equipo, se heredan todas las configuraciones de hello, por lo que puede omitir toohello tarea de implementar y ejecutar la aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e20e1-132">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on this computer, all hello configurations are inherited, so you can skip toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="e20e1-133">Si completó los pasos de hello en [crear una cuenta de aplicación y el almacenamiento de Azure función](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) en un equipo diferente, deberá marcadores de posición de tooreplace Hola Hola `config-raspberrypi.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="e20e1-133">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on a different computer, you need tooreplace hello placeholders in hello `config-raspberrypi.json` file.</span></span> <span data-ttu-id="e20e1-134">Hola `config-raspberrypi.json` archivo se encuentra en la subcarpeta de Hola de su carpeta principal.</span><span class="sxs-lookup"><span data-stu-id="e20e1-134">hello `config-raspberrypi.json` file is in hello subfolder of your home folder.</span></span>
   
   ![Contenido del archivo de configuración raspberrypi.json Hola](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="e20e1-136">Reemplace **[nombre de host de dispositivo o dirección IP]** con la dirección IP de hello Pi o hello de nombre de host que obtiene mediante la ejecución de hello `devdisco list --eth` comando.</span><span class="sxs-lookup"><span data-stu-id="e20e1-136">Replace **[device hostname or IP address]** with hello IP address of Pi or hello host name that you get by running hello `devdisco list --eth` command.</span></span>
* <span data-ttu-id="e20e1-137">Reemplace **[cadena de conexión de dispositivos de IoT]** con cadena de conexión de dispositivo de Hola que obtiene mediante la ejecución de hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` comando.</span><span class="sxs-lookup"><span data-stu-id="e20e1-137">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="e20e1-138">Reemplace **[cadena de conexión de base de datos central de IoT]** con la cadena de conexión de base de datos central de IoT que obtiene mediante la ejecución de Hola Hola `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` comando.</span><span class="sxs-lookup"><span data-stu-id="e20e1-138">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="e20e1-139">Ejecute también **gulp install-tools** si no lo hizo en la lección 1.</span><span class="sxs-lookup"><span data-stu-id="e20e1-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="e20e1-140">Implementar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="e20e1-140">Deploy and run hello sample application</span></span>
<span data-ttu-id="e20e1-141">Implementar y ejecutar la aplicación de ejemplo de Hola en Pi ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e20e1-141">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="e20e1-142">comando de Hello implementa tooPi de aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e20e1-142">hello command deploys hello sample application tooPi.</span></span> <span data-ttu-id="e20e1-143">A continuación, se ejecuta aplicación hello en Pi y una tarea independiente en su host de equipo toosend 20 parpadeo mensajes tooPi desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e20e1-143">Then, it runs hello application on Pi and a separate task on your host computer toosend 20 blink messages tooPi from your IoT hub.</span></span>

<span data-ttu-id="e20e1-144">Después de ejecuta la aplicación de ejemplo de Hola, empieza a escuchar toomessages desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e20e1-144">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="e20e1-145">Mientras tanto, hello gulp tarea puede enviar varios mensajes "blink" de su tooPi de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e20e1-145">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooPi.</span></span> <span data-ttu-id="e20e1-146">Para cada mensaje parpadeo que recibe de Pi, aplicación de ejemplo de Hola llama hello `blinkLED` hello de la función tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="e20e1-146">For each blink message that Pi receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="e20e1-147">Verá parpadear LED de hello cada dos segundos como hello gulp tarea envía 20 mensajes desde su tooPi de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e20e1-147">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooPi.</span></span> <span data-ttu-id="e20e1-148">Hello en último lugar uno es un mensaje de "stop" que indica toostop de aplicación Hola ejecutando.</span><span class="sxs-lookup"><span data-stu-id="e20e1-148">hello last one is a "stop" message that tells hello application toostop running.</span></span>

![Aplicación de ejemplo con comandos de Gulp y mensajes de parpadeo](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a><span data-ttu-id="e20e1-150">Resumen</span><span class="sxs-lookup"><span data-stu-id="e20e1-150">Summary</span></span>
<span data-ttu-id="e20e1-151">Ha enviado correctamente los mensajes desde su Hola de IoT hub tooPi tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="e20e1-151">You’ve successfully sent messages from your IoT hub tooPi tooblink hello LED.</span></span> <span data-ttu-id="e20e1-152">Hola siguiente tarea es opcional: cambie Hola activar y desactivar el comportamiento de hello LED.</span><span class="sxs-lookup"><span data-stu-id="e20e1-152">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e20e1-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e20e1-153">Next steps</span></span>
[<span data-ttu-id="e20e1-154">Cambiar Hola activar y desactivar el comportamiento de hello LED</span><span class="sxs-lookup"><span data-stu-id="e20e1-154">Change hello on and off behavior of hello LED</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

