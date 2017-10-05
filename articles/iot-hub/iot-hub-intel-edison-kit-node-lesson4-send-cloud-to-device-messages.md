---
title: "Conexión de Intel Edison (Node) a Azure IoT: Lección 4: Recepción de mensajes | Microsoft Docs"
description: "Una aplicación de ejemplo se ejecuta en Edison y supervisa los mensajes entrantes provenientes desde su instancia de IoT Hub. Una nueva tarea de Gulp envía mensajes a Edison desde su instancia de IoT Hub para que parpadee el LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "control de led de arduino desde web, control de led de arduino a través de web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 76ea59acd848f60663a0c821bff42166aac5823a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="5b03b-105">Ejecución de una aplicación de ejemplo para recibir mensajes de la nube al dispositivo</span><span class="sxs-lookup"><span data-stu-id="5b03b-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="5b03b-106">En este artículo se implementará una aplicación de ejemplo en Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="5b03b-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="5b03b-107">La aplicación de ejemplo supervisa los mensajes entrantes de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5b03b-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="5b03b-108">También ejecutará una tarea de Gulp en el equipo para enviar mensajes a Edison desde su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5b03b-108">You also run a gulp task on your computer to send messages to Edison from your IoT hub.</span></span> <span data-ttu-id="5b03b-109">Cuando la aplicación de ejemplo reciba los mensajes, el LED parpadeará.</span><span class="sxs-lookup"><span data-stu-id="5b03b-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="5b03b-110">Si tiene problemas, busque soluciones en la [página de solución de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="5b03b-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5b03b-111">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="5b03b-111">What you will do</span></span>
* <span data-ttu-id="5b03b-112">Conecte la aplicación de ejemplo a su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5b03b-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="5b03b-113">Implemente y ejecute la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5b03b-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="5b03b-114">Envíe mensajes desde su instancia de IoT Hub a Edison para que el LED parpadee.</span><span class="sxs-lookup"><span data-stu-id="5b03b-114">Send messages from your IoT hub to Edison to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5b03b-115">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="5b03b-115">What you will learn</span></span>
<span data-ttu-id="5b03b-116">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5b03b-116">In this article, you will learn:</span></span>
* <span data-ttu-id="5b03b-117">Cómo supervisar los mensajes entrantes desde IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5b03b-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="5b03b-118">Envío a Edison de mensajes de la nube al dispositivo desde su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5b03b-118">How to send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5b03b-119">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="5b03b-119">What you need</span></span>
* <span data-ttu-id="5b03b-120">Intel Edison, configurado para su uso.</span><span class="sxs-lookup"><span data-stu-id="5b03b-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="5b03b-121">Para obtener información sobre cómo configurar Edison, consulte [Configuración del dispositivo][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="5b03b-121">To learn how to set up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="5b03b-122">Una instancia de IoT Hub creada en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b03b-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="5b03b-123">Para obtener información sobre cómo crear su instancia de IoT Hub, consulte [Creación de su instancia de IoT Hub de Azure][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="5b03b-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="5b03b-124">Conexión de la aplicación de ejemplo con el centro de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5b03b-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="5b03b-125">Asegúrese de que se encuentra en la carpeta del repositorio `iot-hub-node-edison-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="5b03b-125">Make sure that you're in the repo folder `iot-hub-node-edison-getting-started`.</span></span> <span data-ttu-id="5b03b-126">Abra la aplicación de ejemplo en Visual Studio Code ejecutando los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5b03b-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="5b03b-127">El archivo que se encuentra en la carpeta `app` es el archivo de origen de la clave que contiene el código para supervisar los mensajes entrantes desde la instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5b03b-127">The file in the `app` subfolder is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="5b03b-128">La función `blinkLED` hace parpadear el LED.</span><span class="sxs-lookup"><span data-stu-id="5b03b-128">The `blinkLED` function blinks the LED.</span></span>

   ![Estructura del repositorio en la aplicación de ejemplo][repo-structure]
2. <span data-ttu-id="5b03b-130">Inicialice el archivo de configuración con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="5b03b-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="5b03b-131">Si completó los pasos que aparecen en [Creación de una instancia de Azure Function App y una cuenta de Azure Storage][create-an-azure-function-app-and-storage-account] en este equipo, se heredarán todas las configuraciones, por lo que no tendrá que implementar ni ejecutar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5b03b-131">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="5b03b-132">Si completó los pasos que aparecen en [Creación de una instancia de Azure Function App y una cuenta de Azure Storage][create-an-azure-function-app-and-storage-account] en otro equipo, debe reemplazar los marcadores de posición en el archivo `config-edison.json`.</span><span class="sxs-lookup"><span data-stu-id="5b03b-132">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-edison.json` file.</span></span> <span data-ttu-id="5b03b-133">El archivo `config-edison.json` se encuentra en la subcarpeta de la carpeta principal.</span><span class="sxs-lookup"><span data-stu-id="5b03b-133">The `config-edison.json` file is in the subfolder of your home folder.</span></span>

   ![Contenido del archivo config-edison.json](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="5b03b-135">Sustituya **[device hostname or IP address]** por la dirección IP del dispositivo que anotó cuando configuró el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5b03b-135">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="5b03b-136">Sustituya **[IoT device connection string]** por la cadena de conexión del dispositivo que obtendrá al ejecutar el comando `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}`.</span><span class="sxs-lookup"><span data-stu-id="5b03b-136">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="5b03b-137">Sustituya **[IoT hub connection string]** por la cadena de conexión de IoT Hub que obtendrá al ejecutar el comando `az iot hub show-connection-string --name {my hub name}`.</span><span class="sxs-lookup"><span data-stu-id="5b03b-137">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="5b03b-138">Implementación y ejecución de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5b03b-138">Deploy and run the sample application</span></span>
<span data-ttu-id="5b03b-139">Implemente y ejecute la aplicación de ejemplo en Edison usando los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5b03b-139">Deploy and run the sample application on Edison by running the following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="5b03b-140">El comando de Gulp implementa la aplicación de ejemplo en Edison.</span><span class="sxs-lookup"><span data-stu-id="5b03b-140">The gulp command deploys the sample application to Edison.</span></span> <span data-ttu-id="5b03b-141">Luego, ejecuta la aplicación en Edison y una tarea independiente en el equipo host para enviar 20 mensajes de parpadeo a Edison desde su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5b03b-141">Then, it runs the application on Edison and a separate task on your host computer to send 20 blink messages to Edison from your IoT hub.</span></span>

<span data-ttu-id="5b03b-142">Una vez que se ejecuta, la aplicación de ejemplo empieza a escuchar los mensajes de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5b03b-142">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="5b03b-143">Mientras tanto, la tarea de Gulp envía varios mensajes de parpadeo desde su instancia de IoT Hub a Edison.</span><span class="sxs-lookup"><span data-stu-id="5b03b-143">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Edison.</span></span> <span data-ttu-id="5b03b-144">Cada vez que Edison recibe un mensaje de parpadeo, la aplicación de ejemplo llama a la función `blinkLED` para hacer parpadear el LED.</span><span class="sxs-lookup"><span data-stu-id="5b03b-144">For each blink message that Edison receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="5b03b-145">A medida que la tarea de Gulp envía 20 mensajes a Edison desde su instancia de IoT Hub, el LED debería parpadear cada dos segundos.</span><span class="sxs-lookup"><span data-stu-id="5b03b-145">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Edison.</span></span> <span data-ttu-id="5b03b-146">El último es un mensaje "stop" que indica a la aplicación que deje de ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="5b03b-146">The last one is a "stop" message that stops the application from running.</span></span>

![Aplicación de ejemplo con comandos de Gulp y mensajes de parpadeo][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="5b03b-148">Resumen</span><span class="sxs-lookup"><span data-stu-id="5b03b-148">Summary</span></span>
<span data-ttu-id="5b03b-149">Envió correctamente mensajes desde su instancia de IoT Hub a Edison para que el LED parpadee.</span><span class="sxs-lookup"><span data-stu-id="5b03b-149">You’ve successfully sent messages from your IoT hub to Edison to blink the LED.</span></span> <span data-ttu-id="5b03b-150">La siguiente tarea es optativa y consiste en cambiar el comportamiento de encendido y apagado del LED.</span><span class="sxs-lookup"><span data-stu-id="5b03b-150">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b03b-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5b03b-151">Next steps</span></span>
<span data-ttu-id="5b03b-152">[Modificación del comportamiento de encendido y apagado del LED][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="5b03b-152">[Change the on and off behavior of the LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md