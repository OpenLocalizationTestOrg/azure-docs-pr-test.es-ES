---
title: "Conexión de Arduino (C) a Azure IoT: Lección 3: Ejecución del ejemplo | Microsoft Docs"
description: "Implemente y ejecute una aplicación de ejemplo para Adafruit Feather M0 WiFi que envíe mensajes a su instancia de IoT Hub y haga parpadear el LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "servicio en la nube de IoT, envío de datos de Arduino a la nube"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0c17fe74dbd78abca955f7789a1674ed6333367f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="f6cee-104">Ejecución de una aplicación de ejemplo para enviar mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="f6cee-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="f6cee-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="f6cee-105">What you will do</span></span>
<span data-ttu-id="f6cee-106">En este artículo se explica cómo implementar y ejecutar una aplicación de ejemplo en el panel de Adafruit Feather M0 WiFi Arduino que envía mensajes a su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f6cee-106">This article will show you how to deploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages to your IoT hub.</span></span>

<span data-ttu-id="f6cee-107">Si tiene problemas, busque soluciones en [esta página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="f6cee-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f6cee-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="f6cee-108">What you will learn</span></span>
<span data-ttu-id="f6cee-109">Aprenderá a usar la herramienta de Gulp para implementar y ejecutar la aplicación de ejemplo de Arduino en el panel de Arduino.</span><span class="sxs-lookup"><span data-stu-id="f6cee-109">You will learn how to use the gulp tool to deploy and run the sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f6cee-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="f6cee-110">What you need</span></span>
* <span data-ttu-id="f6cee-111">Para comenzar esta tarea, debe haber completado correctamente el tutorial [Creación de una instancia de Azure Function App y una cuenta de Azure Storage para procesar y guardar mensajes de IoT Hub][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="f6cee-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="f6cee-112">Obtención de las cadenas de conexión de IoT Hub y del dispositivo</span><span class="sxs-lookup"><span data-stu-id="f6cee-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="f6cee-113">La cadena de conexión del dispositivo se usa para conectar el panel de Arduino con su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f6cee-113">The device connection string is used to connect your Arduino board to your IoT hub.</span></span> <span data-ttu-id="f6cee-114">La cadena de conexión de IoT Hub se usa para conectar su instancia de IoT Hub con la identidad de dispositivo que representa el panel de Arduino en la instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f6cee-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents your Arduino board in the IoT hub.</span></span>

* <span data-ttu-id="f6cee-115">Enumere todos los centros de IoT del grupo de recursos ejecutando el siguiente comando de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="f6cee-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="f6cee-116">Use `iot-sample` como valor de `{resource group name}`, si no lo modificó previamente.</span><span class="sxs-lookup"><span data-stu-id="f6cee-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="f6cee-117">Obtenga la cadena de conexión de IoT Hub ejecutando el siguiente comando de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="f6cee-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="f6cee-118">`{my hub name}` es el nombre que especificó cuando creó su instancia de IoT Hub y registró el panel de Arduino.</span><span class="sxs-lookup"><span data-stu-id="f6cee-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="f6cee-119">Obtenga la cadena de conexión de dispositivos ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f6cee-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="f6cee-120">Use `mym0wifi` como valor de `{device id}`, si no lo modificó previamente.</span><span class="sxs-lookup"><span data-stu-id="f6cee-120">Use `mym0wifi` as the value of `{device id}` if you didn't change the value.</span></span>
## <a name="configure-the-device-connection"></a><span data-ttu-id="f6cee-121">Configuración de la conexión de dispositivos</span><span class="sxs-lookup"><span data-stu-id="f6cee-121">Configure the device connection</span></span>
<span data-ttu-id="f6cee-122">Para configurar la conexión de dispositivos, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f6cee-122">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="f6cee-123">Obtenga el puerto serie del dispositivo con la CLI de detección de dispositivos:</span><span class="sxs-lookup"><span data-stu-id="f6cee-123">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="f6cee-124">Debe ver un resultado similar al siguiente y localizar el puerto COM USB de la placa de Arduino:</span><span class="sxs-lookup"><span data-stu-id="f6cee-124">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![Detección de dispositivos][device-discovery]

2. <span data-ttu-id="f6cee-126">Abra el archivo `config.json` en la carpeta de lecciones y agregue el valor del número de puerto COM encontrado:</span><span class="sxs-lookup"><span data-stu-id="f6cee-126">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="f6cee-128">Para el puerto COM, en la plataforma Windows tiene el formato de `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="f6cee-128">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="f6cee-129">En macOS o Ubuntu, empieza por `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="f6cee-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="f6cee-130">Inicialice el archivo de configuración con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="f6cee-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="f6cee-131">Abra el archivo de configuración de dispositivos `config-arduino.json` en Visual Studio Code ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="f6cee-131">Open the device configuration file `config-arduino.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. <span data-ttu-id="f6cee-133">Realice las sustituciones siguientes en el archivo `config-arduino.json`:</span><span class="sxs-lookup"><span data-stu-id="f6cee-133">Make the following replacements in the `config-arduino.json` file:</span></span>

   * <span data-ttu-id="f6cee-134">Reemplace **[Wi-Fi SSID]** por el SSID Wi-Fi que se conectó a Internet.</span><span class="sxs-lookup"><span data-stu-id="f6cee-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="f6cee-135">Reemplace **[Wi-Fi password]** por su contraseña de Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="f6cee-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="f6cee-136">Quite la cadena si su Wi-Fi no necesita contraseña.</span><span class="sxs-lookup"><span data-stu-id="f6cee-136">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="f6cee-137">Reemplace **[IoT device connection string]** con el valor de `device connection string` que ha obtenido.</span><span class="sxs-lookup"><span data-stu-id="f6cee-137">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="f6cee-138">Reemplace **[IoT hub connection string]** con el valor de `iot hub connection string` que ha obtenido.</span><span class="sxs-lookup"><span data-stu-id="f6cee-138">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f6cee-139">`azure_storage_connection_string` no es necesario en este artículo.</span><span class="sxs-lookup"><span data-stu-id="f6cee-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="f6cee-140">Déjelo como está.</span><span class="sxs-lookup"><span data-stu-id="f6cee-140">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="f6cee-141">Implementación y ejecución de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f6cee-141">Deploy and run the sample application</span></span>
<span data-ttu-id="f6cee-142">Implemente y ejecute la aplicación de ejemplo en la placa de Arduino ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="f6cee-142">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="f6cee-143">La tarea de Gulp ejecuta las tareas `install-tools` y `run` de forma secuencial.</span><span class="sxs-lookup"><span data-stu-id="f6cee-143">The default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="f6cee-144">Cuando [implementó la aplicación de intermitencia][deployed-the-blink-app], ejecutó estas tareas por separado.</span><span class="sxs-lookup"><span data-stu-id="f6cee-144">When you [deployed the blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="f6cee-145">Comprobación del funcionamiento de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f6cee-145">Verify that the sample application works</span></span>
<span data-ttu-id="f6cee-146">Debería ver que el LED de GPIO 0 en el panel parpadea cada dos segundos.</span><span class="sxs-lookup"><span data-stu-id="f6cee-146">You should see the GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="f6cee-147">Cada vez que el LED parpadea, la aplicación de ejemplo envía un mensaje a IoT Hub y comprueba que el mensaje se envió correctamente a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f6cee-147">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="f6cee-148">Además, todos los mensajes que reciba IoT Hub se imprimirán en la ventana de consola.</span><span class="sxs-lookup"><span data-stu-id="f6cee-148">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="f6cee-149">La aplicación de ejemplo se finaliza automáticamente después de enviar 20 mensajes.</span><span class="sxs-lookup"><span data-stu-id="f6cee-149">The sample application terminates automatically after sending 20 messages.</span></span>

![Aplicación de ejemplo con mensajes enviados y recibidos][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="f6cee-151">Resumen</span><span class="sxs-lookup"><span data-stu-id="f6cee-151">Summary</span></span>
<span data-ttu-id="f6cee-152">Implementó y ejecutó la nueva aplicación de ejemplo de intermitencia en el panel de Arduino para enviar mensajes de dispositivo a nube a su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f6cee-152">You've deployed and run the new blink sample application on your Arduino board to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="f6cee-153">Ahora, puede supervisar los mensajes a medida que se escriben en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f6cee-153">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6cee-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f6cee-154">Next steps</span></span>
<span data-ttu-id="f6cee-155">[Lectura de los mensajes que se conservan en Azure Storage][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="f6cee-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md