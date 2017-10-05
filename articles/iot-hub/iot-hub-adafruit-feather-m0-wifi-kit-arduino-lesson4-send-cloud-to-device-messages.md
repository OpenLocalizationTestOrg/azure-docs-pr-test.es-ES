---
title: "Conexión de Arduino (C) a Azure IoT: Lección 4: De la nube al dispositivo | Microsoft Docs"
description: "Una aplicación de ejemplo se ejecuta en Adafruit Feather M0 WiFi y supervisa los mensajes entrantes de IoT Hub. Una nueva tarea de Gulp envía mensajes a Adafruit Feather M0 WiFi desde IoT Hub para que parpadee el LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "control de led de arduino desde web, control de led de arduino a través de web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b4f4c1d86b10b64c104ac812d1f650d723322be8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="459f9-105">Ejecución de una aplicación de ejemplo para recibir mensajes de la nube al dispositivo</span><span class="sxs-lookup"><span data-stu-id="459f9-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="459f9-106">En este artículo, se implementa una aplicación de ejemplo en la placa Adafruit Feather M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="459f9-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="459f9-107">La aplicación de ejemplo supervisa los mensajes entrantes de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="459f9-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="459f9-108">También se ejecuta una tarea de Gulp en el equipo para enviar mensajes a la placa de Arduino desde IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="459f9-108">You also run a gulp task on your computer to send messages to your Arduino board from your IoT hub.</span></span> <span data-ttu-id="459f9-109">Cuando la aplicación de ejemplo reciba los mensajes, el LED parpadeará.</span><span class="sxs-lookup"><span data-stu-id="459f9-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="459f9-110">Si tiene problemas, busque soluciones en la [página de solución de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="459f9-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="459f9-111">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="459f9-111">What you will do</span></span>
* <span data-ttu-id="459f9-112">Conecte la aplicación de ejemplo a su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="459f9-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="459f9-113">Implemente y ejecute la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="459f9-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="459f9-114">Envíe mensajes desde su instancia de IoT Hub a la placa de Arduino para que parpadee el LED.</span><span class="sxs-lookup"><span data-stu-id="459f9-114">Send messages from your IoT hub to your Arduino board to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="459f9-115">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="459f9-115">What you will learn</span></span>
<span data-ttu-id="459f9-116">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="459f9-116">In this article, you will learn:</span></span>
* <span data-ttu-id="459f9-117">Cómo supervisar los mensajes entrantes desde IoT Hub</span><span class="sxs-lookup"><span data-stu-id="459f9-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="459f9-118">Cómo enviar mensajes de la nube al dispositivo desde IoT Hub a su placa de Arduino.</span><span class="sxs-lookup"><span data-stu-id="459f9-118">How to send cloud-to-device messages from your IoT hub to your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="459f9-119">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="459f9-119">What you need</span></span>
* <span data-ttu-id="459f9-120">La placa de Arduino, configurada para su uso.</span><span class="sxs-lookup"><span data-stu-id="459f9-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="459f9-121">Para obtener información sobre cómo configurar la placa Arduino, consulte [Configuración del dispositivo][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="459f9-121">To learn how to set up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="459f9-122">Una instancia de IoT Hub creada en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="459f9-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="459f9-123">Para obtener información sobre cómo crear su instancia de IoT Hub, consulte [Creación de su instancia de IoT Hub de Azure][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="459f9-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="459f9-124">Conexión de la aplicación de ejemplo con el centro de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="459f9-124">Connect the sample application to your IoT hub</span></span>

1. <span data-ttu-id="459f9-125">Asegúrese de que se encuentra en la carpeta del repositorio `iot-hub-c-feather-m0-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="459f9-125">Make sure that you're in the repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="459f9-126">Abra la aplicación de ejemplo en Visual Studio Code ejecutando los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="459f9-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="459f9-127">Observe el archivo `app.ino` en la subcarpeta `app`.</span><span class="sxs-lookup"><span data-stu-id="459f9-127">Notice the `app.ino` file in the `app` subfolder.</span></span> <span data-ttu-id="459f9-128">El archivo `app.ino` es el archivo de origen de la clave y contiene el código para supervisar los mensajes entrantes de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="459f9-128">The `app.ino` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="459f9-129">La función `blinkLED` hace parpadear el LED.</span><span class="sxs-lookup"><span data-stu-id="459f9-129">The `blinkLED` function blinks the LED.</span></span>

   ![Estructura del repositorio en la aplicación de ejemplo][repo-structure]

2. <span data-ttu-id="459f9-131">Obtenga el puerto serie del dispositivo con la CLI de detección de dispositivos:</span><span class="sxs-lookup"><span data-stu-id="459f9-131">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="459f9-132">Debe ver un resultado similar al siguiente y localizar el puerto COM USB de la placa de Arduino:</span><span class="sxs-lookup"><span data-stu-id="459f9-132">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![Detección de dispositivos][device-discovery]

3. <span data-ttu-id="459f9-134">Abra el archivo `config.json` de la carpeta lesson y agregue el valor del número de puerto COM encontrado:</span><span class="sxs-lookup"><span data-stu-id="459f9-134">Open the file `config.json` in the lesson folder and input the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="459f9-136">Para el puerto COM, en la plataforma Windows tiene el formato de `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="459f9-136">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="459f9-137">En Mac OS o Ubuntu, empezará por `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="459f9-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="459f9-138">Inicialice el archivo de configuración con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="459f9-138">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="459f9-139">Realice las sustituciones siguientes en el archivo `config-arduino.json`:</span><span class="sxs-lookup"><span data-stu-id="459f9-139">Make the following replacements in the `config-arduino.json` file:</span></span>

   <span data-ttu-id="459f9-140">Si completó los pasos que aparecen en [Creación de una instancia de Azure Function App y una cuenta de Azure Storage][create-an-azure-function-app-and-storage-account] en este equipo, se heredarán todas las configuraciones, por lo que no tendrá que implementar ni ejecutar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="459f9-140">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="459f9-141">Si completó los pasos que aparecen en [Creación de una instancia de Azure Function App y una cuenta de Azure Storage][create-an-azure-function-app-and-storage-account] en otro equipo, debe reemplazar los marcadores de posición en el archivo `config-arduino.json`.</span><span class="sxs-lookup"><span data-stu-id="459f9-141">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-arduino.json` file.</span></span> <span data-ttu-id="459f9-142">El archivo `config-arduino.json` se encuentra en la subcarpeta de la carpeta principal.</span><span class="sxs-lookup"><span data-stu-id="459f9-142">The `config-arduino.json` file is in the subfolder of your home folder.</span></span>

   ![Contenido del archivo config-arduino.json][config-arduino-json]

   * <span data-ttu-id="459f9-144">Reemplace **[Wi-Fi SSID]** por el SSID Wi-Fi que se conectó a Internet.</span><span class="sxs-lookup"><span data-stu-id="459f9-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="459f9-145">Reemplace **[Wi-Fi password]** por su contraseña de Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="459f9-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="459f9-146">Quite la cadena si su Wi-Fi no necesita contraseña.</span><span class="sxs-lookup"><span data-stu-id="459f9-146">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="459f9-147">Sustituya **[IoT device connection string]** por la cadena de conexión del dispositivo que obtendrá al ejecutar el comando `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}`.</span><span class="sxs-lookup"><span data-stu-id="459f9-147">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="459f9-148">Sustituya **[IoT hub connection string]** por la cadena de conexión de IoT Hub que obtendrá al ejecutar el comando `az iot hub show-connection-string --name {my hub name}`.</span><span class="sxs-lookup"><span data-stu-id="459f9-148">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="459f9-149">Implementación y ejecución de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="459f9-149">Deploy and run the sample application</span></span>
<span data-ttu-id="459f9-150">Implemente y ejecute la aplicación de ejemplo en la placa de Arduino ejecutando los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="459f9-150">Deploy and run the sample application on your Arduino board by running the following commands:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="459f9-151">El comando de Gulp implementa la aplicación de ejemplo en la placa de Arduino.</span><span class="sxs-lookup"><span data-stu-id="459f9-151">The gulp command deploys the sample application to your Arduino board.</span></span> <span data-ttu-id="459f9-152">Luego, ejecuta la aplicación en la placa de Arduino y una tarea independiente en el equipo host para enviar 20 mensajes de intermitencia a la placa de Arduino desde IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="459f9-152">Then, it runs the application on your Arduino board and a separate task on your host computer to send 20 blink messages to your Arduino board from your IoT hub.</span></span>

<span data-ttu-id="459f9-153">Una vez que se ejecuta, la aplicación de ejemplo empieza a escuchar los mensajes de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="459f9-153">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="459f9-154">Mientras tanto, la tarea de Gulp envía varios mensajes de intermitencia desde IoT Hub a la placa de Arduino.</span><span class="sxs-lookup"><span data-stu-id="459f9-154">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="459f9-155">Cada vez que la placa recibe un mensaje de intermitencia, la aplicación de ejemplo llama a la función `blinkLED` para hacer parpadear el LED.</span><span class="sxs-lookup"><span data-stu-id="459f9-155">For each blink message that the board receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="459f9-156">A medida que la tarea de Gulp envía a la placa de Arduino los 20 mensajes desde el centro de IoT Hub, el LED debería parpadear cada dos segundos.</span><span class="sxs-lookup"><span data-stu-id="459f9-156">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="459f9-157">El último es un mensaje "stop" que indica a la aplicación que deje de ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="459f9-157">The last one is a "stop" message that stops the application from running.</span></span>

![Aplicación de ejemplo con comandos de Gulp y mensajes de parpadeo][sample-application]

## <a name="summary"></a><span data-ttu-id="459f9-159">Resumen</span><span class="sxs-lookup"><span data-stu-id="459f9-159">Summary</span></span>
<span data-ttu-id="459f9-160">Ya ha enviado correctamente mensajes desde su instancia de IoT Hub para que la placa de Arduino haga parpadear el LED.</span><span class="sxs-lookup"><span data-stu-id="459f9-160">You’ve successfully sent messages from your IoT hub to your Arduino board to blink the LED.</span></span> <span data-ttu-id="459f9-161">La siguiente tarea es optativa y consiste en cambiar el comportamiento de encendido y apagado del LED.</span><span class="sxs-lookup"><span data-stu-id="459f9-161">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="459f9-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="459f9-162">Next steps</span></span>
<span data-ttu-id="459f9-163">[Modificación del comportamiento de encendido y apagado del LED][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="459f9-163">[Change the on and off behavior of the LED][change-the-on-and-off-led-behavior]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md