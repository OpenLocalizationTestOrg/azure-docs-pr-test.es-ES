---
title: "Connect Arduino (C) tooAzure IoT - lección 4: en la nube al dispositivo | Documentos de Microsoft"
description: "Una aplicación de ejemplo se ejecuta en Adafruit Feather M0 WiFi y supervisa los mensajes entrantes de IoT Hub. Una nueva tarea de gulp envía mensajes tooAdafruit Wi-Fi de desvanecimiento M0 desde su hello tooblink de centro de IoT LED."
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
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="8f899-105">Ejecutar un tooreceive de la aplicación de ejemplo en la nube al dispositivo mensajes</span><span class="sxs-lookup"><span data-stu-id="8f899-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="8f899-106">En este artículo, se implementa una aplicación de ejemplo en la placa Adafruit Feather M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="8f899-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="8f899-107">aplicación de ejemplo de Hola supervisa los mensajes entrantes desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="8f899-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="8f899-108">También permite ejecutar una tarea de gulp en los mensajes de toosend equipo tooyour Arduino panel, desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="8f899-108">You also run a gulp task on your computer toosend messages tooyour Arduino board from your IoT hub.</span></span> <span data-ttu-id="8f899-109">Cuando la aplicación de ejemplo de Hola recibe mensajes de Hola, parpadea Hola LED.</span><span class="sxs-lookup"><span data-stu-id="8f899-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="8f899-110">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="8f899-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="8f899-111">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="8f899-111">What you will do</span></span>
* <span data-ttu-id="8f899-112">Conectar el centro de IoT de tooyour de aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f899-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="8f899-113">Implemente y ejecute la aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f899-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="8f899-114">Enviar mensajes desde su Hola IoT hub tooyour Arduino panel tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="8f899-114">Send messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8f899-115">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="8f899-115">What you will learn</span></span>
<span data-ttu-id="8f899-116">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8f899-116">In this article, you will learn:</span></span>
* <span data-ttu-id="8f899-117">Cómo los mensajes entrantes de toomonitor desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="8f899-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="8f899-118">¿Cómo toosend en la nube al dispositivo mensajes desde su tooyour de centro de IoT Arduino panel.</span><span class="sxs-lookup"><span data-stu-id="8f899-118">How toosend cloud-to-device messages from your IoT hub tooyour Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8f899-119">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="8f899-119">What you need</span></span>
* <span data-ttu-id="8f899-120">La placa de Arduino, configurada para su uso.</span><span class="sxs-lookup"><span data-stu-id="8f899-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="8f899-121">toolearn tooset de su placa Arduino, vea [configurar su dispositivo][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="8f899-121">toolearn how tooset up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="8f899-122">Una instancia de IoT Hub creada en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f899-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="8f899-123">toolearn cómo toocreate su centro de IoT, consulte [crea el centro de IoT de Azure][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="8f899-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="8f899-124">Conectar el centro de IoT de tooyour de aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="8f899-124">Connect hello sample application tooyour IoT hub</span></span>

1. <span data-ttu-id="8f899-125">Asegúrese de que se encuentra en la carpeta de repositorio de hello `iot-hub-c-feather-m0-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="8f899-125">Make sure that you're in hello repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="8f899-126">Abra la aplicación de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="8f899-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="8f899-127">Hola aviso `app.ino` archivo Hola `app` subcarpeta.</span><span class="sxs-lookup"><span data-stu-id="8f899-127">Notice hello `app.ino` file in hello `app` subfolder.</span></span> <span data-ttu-id="8f899-128">Hola `app.ino` es archivo de origen de la clave de Hola que contiene código de hello toomonitor mensajes entrantes Hola centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="8f899-128">hello `app.ino` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="8f899-129">Hola `blinkLED` función parpadea Hola LED.</span><span class="sxs-lookup"><span data-stu-id="8f899-129">hello `blinkLED` function blinks hello LED.</span></span>

   ![Estructura de repositorio en la aplicación de ejemplo de Hola][repo-structure]

2. <span data-ttu-id="8f899-131">Obtener el puerto serie de hello de dispositivo de hello con cli de detección de dispositivos de hello:</span><span class="sxs-lookup"><span data-stu-id="8f899-131">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="8f899-132">Debe ver un resultado similar siguiente toohello y encontrar Hola usb puerto COM de su placa de Arduino:</span><span class="sxs-lookup"><span data-stu-id="8f899-132">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![Detección de dispositivos][device-discovery]

3. <span data-ttu-id="8f899-134">Archivo abierto hello `config.json` en carpeta de lección Hola y el valor de entrada Hola de hello encuentra el número de puerto COM:</span><span class="sxs-lookup"><span data-stu-id="8f899-134">Open hello file `config.json` in hello lesson folder and input hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="8f899-136">Para el puerto de hello COM, en la plataforma Windows, tiene un formato de hello `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="8f899-136">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="8f899-137">En Mac OS o Ubuntu, empezará por `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="8f899-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="8f899-138">Inicializar el archivo de configuración de hello ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="8f899-138">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="8f899-139">Realizar Hola después reemplazos en hello `config-arduino.json` archivo:</span><span class="sxs-lookup"><span data-stu-id="8f899-139">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   <span data-ttu-id="8f899-140">Si completó los pasos de hello en [crear una cuenta de aplicación y el almacenamiento de Azure función] [ create-an-azure-function-app-and-storage-account] en este equipo, se heredan todas las configuraciones de hello, por lo que puede omitir la tarea de toohello hello paso de la implementación de y ejecutar la aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f899-140">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="8f899-141">Si completó los pasos de hello en [crear una cuenta de aplicación y el almacenamiento de Azure función] [ create-an-azure-function-app-and-storage-account] en un equipo diferente, deberá marcadores de posición de tooreplace Hola Hola `config-arduino.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="8f899-141">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-arduino.json` file.</span></span> <span data-ttu-id="8f899-142">Hola `config-arduino.json` archivo se encuentra en la subcarpeta de Hola de su carpeta principal.</span><span class="sxs-lookup"><span data-stu-id="8f899-142">hello `config-arduino.json` file is in hello subfolder of your home folder.</span></span>

   ![Contenido del archivo de configuración arduino.json Hola][config-arduino-json]

   * <span data-ttu-id="8f899-144">Reemplace **[Wi-Fi SSID]** con el SSID de Wi-Fi que conectado toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="8f899-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="8f899-145">Reemplace **[Wi-Fi password]** por su contraseña de Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="8f899-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="8f899-146">Quite la cadena de hello si su Wi-Fi no requiere una contraseña.</span><span class="sxs-lookup"><span data-stu-id="8f899-146">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="8f899-147">Reemplace **[cadena de conexión de dispositivos de IoT]** con cadena de conexión de dispositivo de Hola que obtiene mediante la ejecución de hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` comando.</span><span class="sxs-lookup"><span data-stu-id="8f899-147">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="8f899-148">Reemplace **[cadena de conexión de base de datos central de IoT]** con la cadena de conexión de base de datos central de IoT que obtiene mediante la ejecución de Hola Hola `az iot hub show-connection-string --name {my hub name}` comando.</span><span class="sxs-lookup"><span data-stu-id="8f899-148">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="8f899-149">Implementar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="8f899-149">Deploy and run hello sample application</span></span>
<span data-ttu-id="8f899-150">Implementar y ejecutar aplicaciones de ejemplo de Hola en el panel de Arduino ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="8f899-150">Deploy and run hello sample application on your Arduino board by running hello following commands:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="8f899-151">comando de Hello gulp implementa tooyour Arduino placa de hello ejemplo aplicación.</span><span class="sxs-lookup"><span data-stu-id="8f899-151">hello gulp command deploys hello sample application tooyour Arduino board.</span></span> <span data-ttu-id="8f899-152">A continuación, se ejecuta aplicación hello en el panel de Arduino y una tarea independiente en el host tooyour Arduino placa de equipo toosend 20 parpadeo mensajes desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="8f899-152">Then, it runs hello application on your Arduino board and a separate task on your host computer toosend 20 blink messages tooyour Arduino board from your IoT hub.</span></span>

<span data-ttu-id="8f899-153">Después de ejecuta la aplicación de ejemplo de Hola, empieza a escuchar toomessages desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="8f899-153">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="8f899-154">Mientras tanto, hello gulp tarea puede enviar varios mensajes "blink" de su tooyour de centro de IoT Arduino panel.</span><span class="sxs-lookup"><span data-stu-id="8f899-154">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="8f899-155">Para cada mensaje de intermitencia Hola panel recibe, aplicación de ejemplo de Hola llama hello `blinkLED` hello de la función tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="8f899-155">For each blink message that hello board receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="8f899-156">Debería ver Hola LED parpadea cada dos segundos como tarea de hello gulp envía 20 mensajes desde su tooyour de centro de IoT Arduino panel.</span><span class="sxs-lookup"><span data-stu-id="8f899-156">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="8f899-157">Hello en último lugar uno es un mensaje de "stop" que detiene la aplicación hello se ejecute.</span><span class="sxs-lookup"><span data-stu-id="8f899-157">hello last one is a "stop" message that stops hello application from running.</span></span>

![Aplicación de ejemplo con comandos de Gulp y mensajes de parpadeo][sample-application]

## <a name="summary"></a><span data-ttu-id="8f899-159">Resumen</span><span class="sxs-lookup"><span data-stu-id="8f899-159">Summary</span></span>
<span data-ttu-id="8f899-160">Ha enviado correctamente los mensajes desde su Hola IoT hub tooyour Arduino panel tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="8f899-160">You’ve successfully sent messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="8f899-161">Hola siguiente tarea es opcional: cambie Hola activar y desactivar el comportamiento de hello LED.</span><span class="sxs-lookup"><span data-stu-id="8f899-161">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f899-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8f899-162">Next steps</span></span>
<span data-ttu-id="8f899-163">[Cambiar Hola activar y desactivar el comportamiento de hello LED][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="8f899-163">[Change hello on and off behavior of hello LED][change-the-on-and-off-led-behavior]</span></span>


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