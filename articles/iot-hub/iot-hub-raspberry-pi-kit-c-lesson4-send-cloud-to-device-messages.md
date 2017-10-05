---
title: "Conexión de Raspberry Pi (C) a Azure IoT: Lección 4: De la nube al dispositivo | Microsoft Docs"
description: "La aplicación de ejemplo se ejecuta en Pi y supervisa los mensajes entrantes de IoT Hub. Una nueva tarea de Gulp envía mensajes a Pi desde su centro de IoT para que parpadee el LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: de la nube al dispositivo, mensaje de la nube
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fcbc0dd0-cae3-47b0-8e58-240e4f406f75
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 86c7be931319d9995c2a7311267c7e7c03c3c1b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="1e190-105">Ejecución de la aplicación de ejemplo para recibir mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="1e190-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="1e190-106">En este artículo, implementará una aplicación de ejemplo en Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="1e190-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="1e190-107">La aplicación de ejemplo supervisa los mensajes entrantes de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1e190-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="1e190-108">También ejecutará una tarea de Gulp en el equipo para enviar mensajes a Pi desde IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1e190-108">You also run a gulp task on your computer to send messages to Pi from your IoT hub.</span></span> <span data-ttu-id="1e190-109">Cuando la aplicación de ejemplo reciba los mensajes, el LED parpadeará.</span><span class="sxs-lookup"><span data-stu-id="1e190-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="1e190-110">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1e190-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="1e190-111">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="1e190-111">What you will do</span></span>
* <span data-ttu-id="1e190-112">Conecte la aplicación de ejemplo a su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1e190-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="1e190-113">Implemente y ejecute la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1e190-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="1e190-114">Envíe mensajes desde el centro de IoT Hub a Pi para que el LED parpadee.</span><span class="sxs-lookup"><span data-stu-id="1e190-114">Send messages from your IoT hub to Pi to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1e190-115">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="1e190-115">What you will learn</span></span>
<span data-ttu-id="1e190-116">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1e190-116">In this article, you will learn:</span></span>
* <span data-ttu-id="1e190-117">Cómo supervisar los mensajes entrantes desde IoT Hub</span><span class="sxs-lookup"><span data-stu-id="1e190-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="1e190-118">Envío a Pi de mensajes de la nube al dispositivo desde IoT Hub</span><span class="sxs-lookup"><span data-stu-id="1e190-118">How to send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1e190-119">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="1e190-119">What you need</span></span>
* <span data-ttu-id="1e190-120">Un dispositivo Raspberry Pi 3, con la configuración lista para utilizarse.</span><span class="sxs-lookup"><span data-stu-id="1e190-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="1e190-121">Para aprender a configurar Pi, consulte [Configure your device](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md) (Configuración del dispositivo).</span><span class="sxs-lookup"><span data-stu-id="1e190-121">To learn how to set up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="1e190-122">Una instancia de IoT Hub creada en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e190-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="1e190-123">Para aprender a crear la instancia de IoT Hub, consulte [Creación de un centro de IoT y registro de Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="1e190-123">To learn how to create your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="1e190-124">Conexión de la aplicación de ejemplo con el centro de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="1e190-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="1e190-125">Asegúrese de que se encuentra en la carpeta del repositorio `iot-hub-c-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="1e190-125">Make sure that you're in the repo folder `iot-hub-c-raspberrypi-getting-started`.</span></span> <span data-ttu-id="1e190-126">Abra la aplicación de ejemplo en Visual Studio Code ejecutando los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1e190-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="1e190-127">Observe el archivo `app.c` en la subcarpeta `app`.</span><span class="sxs-lookup"><span data-stu-id="1e190-127">Notice the `app.c` file in the `app` subfolder.</span></span> <span data-ttu-id="1e190-128">El archivo `app.c` es el archivo de origen de la clave y contiene el código para supervisar los mensajes entrantes de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1e190-128">The `app.c` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="1e190-129">La función `blinkLED` hace parpadear el LED.</span><span class="sxs-lookup"><span data-stu-id="1e190-129">The `blinkLED` function blinks the LED.</span></span>

   ![Estructura del repositorio en la aplicación de ejemplo](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. <span data-ttu-id="1e190-131">Inicialice el archivo de configuración con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="1e190-131">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="1e190-132">Si completó el tutorial [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) (Creación de una instancia de Azure Function App y una cuenta de almacenamiento) en este equipo, se heredarán todas las configuraciones, por lo que no tendrá que implementar ni ejecutar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1e190-132">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on this computer, all the configurations are inherited, so you can skip to step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="1e190-133">Si completó el tutorial [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) (Creación de una instancia de Azure Function App y una cuenta de almacenamiento) en otro equipo, tendrá que reemplazar los marcadores de posición del archivo `config-raspberrypi.json`.</span><span class="sxs-lookup"><span data-stu-id="1e190-133">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on a different computer, you need to replace the placeholders in the `config-raspberrypi.json` file.</span></span> <span data-ttu-id="1e190-134">El archivo `config-raspberrypi.json` se encuentra en la subcarpeta de la carpeta principal.</span><span class="sxs-lookup"><span data-stu-id="1e190-134">The `config-raspberrypi.json` file is in the subfolder of your home folder.</span></span>

   ![Contenido del archivo config-raspberrypi.json](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="1e190-136">Reemplace **[device hostname or IP address]** por la dirección IP o el nombre de host de Pi que obtendrá ejecutando el comando `devdisco list --eth`.</span><span class="sxs-lookup"><span data-stu-id="1e190-136">Replace **[device hostname or IP address]** with Pi’s IP address or host name that you get by running the `devdisco list --eth` command.</span></span>
* <span data-ttu-id="1e190-137">Sustituya **[IoT device connection string]** por la cadena de conexión del dispositivo que obtendrá al ejecutar el comando `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="1e190-137">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="1e190-138">Sustituya **[IoT hub connection string]** por la cadena de conexión de IoT Hub que obtendrá al ejecutar el comando `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="1e190-138">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="1e190-139">Ejecute también **gulp install-tools** si no lo hizo en la lección 1.</span><span class="sxs-lookup"><span data-stu-id="1e190-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="1e190-140">Implementación y ejecución de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1e190-140">Deploy and run the sample application</span></span>
<span data-ttu-id="1e190-141">Implemente y ejecute la aplicación de ejemplo en Pi mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="1e190-141">Deploy and run the sample application on Pi by running the following commands:</span></span>

```
gulp deploy && gulp run
```

<span data-ttu-id="1e190-142">El comando gulp primero ejecuta la tarea de instalación de herramientas.</span><span class="sxs-lookup"><span data-stu-id="1e190-142">The gulp command runs the install-tools task first.</span></span> <span data-ttu-id="1e190-143">A continuación, implementa la aplicación de ejemplo en Pi.</span><span class="sxs-lookup"><span data-stu-id="1e190-143">Then it deploys the sample application to Pi.</span></span> <span data-ttu-id="1e190-144">Finalmente, ejecuta la aplicación en Pi. También ejecuta una tarea independiente en el equipo host que envía 20 mensajes de parpadeo a Pi desde IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1e190-144">Finally, it runs the application on Pi and a separate task on your host computer to send 20 blink messages to Pi from your IoT hub.</span></span>

<span data-ttu-id="1e190-145">Una vez que se ejecuta, la aplicación de ejemplo empieza a escuchar los mensajes de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1e190-145">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="1e190-146">Mientras tanto, la tarea de Gulp envía a Pi varios mensajes de parpadeo desde el centro de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1e190-146">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Pi.</span></span> <span data-ttu-id="1e190-147">Cada vez que Pi recibe un mensaje de parpadeo, la aplicación de ejemplo llama a la función `blinkLED` para hacer parpadear el LED.</span><span class="sxs-lookup"><span data-stu-id="1e190-147">For each blink message that Pi receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="1e190-148">A medida que la tarea de Gulp envía a Pi los 20 mensajes desde el centro de IoT Hub, el LED debería parpadear cada dos segundos.</span><span class="sxs-lookup"><span data-stu-id="1e190-148">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Pi.</span></span> <span data-ttu-id="1e190-149">El último es un mensaje "stop" que indica a la aplicación que deje de ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="1e190-149">The last one is a "stop" message that stops the application from running.</span></span>

![Aplicación de ejemplo con comandos de Gulp y mensajes de parpadeo](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a><span data-ttu-id="1e190-151">Resumen</span><span class="sxs-lookup"><span data-stu-id="1e190-151">Summary</span></span>
<span data-ttu-id="1e190-152">Ha enviado correctamente mensajes desde el centro de IoT Hub a Pi para que el LED parpadee.</span><span class="sxs-lookup"><span data-stu-id="1e190-152">You’ve successfully sent messages from your IoT hub to Pi to blink the LED.</span></span> <span data-ttu-id="1e190-153">La siguiente tarea es optativa y consiste en cambiar el comportamiento de encendido y apagado del LED.</span><span class="sxs-lookup"><span data-stu-id="1e190-153">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e190-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1e190-154">Next steps</span></span>
[<span data-ttu-id="1e190-155">Modificación del comportamiento de encendido y apagado del LED</span><span class="sxs-lookup"><span data-stu-id="1e190-155">Change the on and off behavior of the LED</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)
