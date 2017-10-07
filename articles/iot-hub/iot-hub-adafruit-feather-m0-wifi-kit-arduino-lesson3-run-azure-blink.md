---
title: "Connect Arduino (C) tooAzure IoT - lección 3: ejecutar el ejemplo | Documentos de Microsoft"
description: "Implemente y ejecute un tooAdafruit de aplicación de ejemplo Wi-Fi de desvanecimiento M0 que envía el centro de IoT tooyour de mensajes y parpadea Hola LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servicio de nube de IOT, arduino enviar datos toocloud
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
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="c02a9-104">Ejecutar un toosend de la aplicación de ejemplo mensajes del dispositivo a la nube</span><span class="sxs-lookup"><span data-stu-id="c02a9-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="c02a9-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="c02a9-105">What you will do</span></span>
<span data-ttu-id="c02a9-106">En este artículo le mostrará cómo toodeploy y ejecute una aplicación de ejemplo en su Arduino de Wi-Fi Adafruit compacto M0 ese centro de IoT envía mensajes tooyour del panel.</span><span class="sxs-lookup"><span data-stu-id="c02a9-106">This article will show you how toodeploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages tooyour IoT hub.</span></span>

<span data-ttu-id="c02a9-107">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="c02a9-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c02a9-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="c02a9-108">What you will learn</span></span>
<span data-ttu-id="c02a9-109">Obtendrá información sobre cómo hello toouse gulp toodeploy de herramienta y ejecutar la aplicación de Arduino de ejemplo de Hola en el panel de Arduino.</span><span class="sxs-lookup"><span data-stu-id="c02a9-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c02a9-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="c02a9-110">What you need</span></span>
* <span data-ttu-id="c02a9-111">Antes de iniciar esta tarea, debe haber completado correctamente [crear una aplicación de Azure de función y un centro de IoT de almacenamiento cuenta tooprocess y el almacén de mensajes][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="c02a9-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="c02a9-112">Obtención de las cadenas de conexión de IoT Hub y del dispositivo</span><span class="sxs-lookup"><span data-stu-id="c02a9-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="c02a9-113">Hola la cadena de conexión de dispositivo es tooconnect usado en su centro de IoT Arduino tooyour de panel.</span><span class="sxs-lookup"><span data-stu-id="c02a9-113">hello device connection string is used tooconnect your Arduino board tooyour IoT hub.</span></span> <span data-ttu-id="c02a9-114">cadena de conexión de base de datos central de Hello IoT es tooconnect usado su identidad de dispositivos de IoT hub toohello que representa su Arduino del panel de centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="c02a9-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents your Arduino board in hello IoT hub.</span></span>

* <span data-ttu-id="c02a9-115">Lista de todos los centros de IoT. en el grupo de recursos si ejecuta Hola siguiente comando de CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="c02a9-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="c02a9-116">Use `iot-sample` como valor de Hola de `{resource group name}` si no cambia el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="c02a9-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="c02a9-117">Obtener la cadena de conexión de base de datos central de hello IoT ejecutando el siguiente comando de CLI de Azure de hello:</span><span class="sxs-lookup"><span data-stu-id="c02a9-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="c02a9-118">`{my hub name}`es el nombre de Hola que especificó cuando creó el centro de IoT y había registrado en el panel de Arduino.</span><span class="sxs-lookup"><span data-stu-id="c02a9-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="c02a9-119">Obtener la cadena de conexión de dispositivo de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c02a9-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="c02a9-120">Use `mym0wifi` como valor de Hola de `{device id}` si no cambia el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="c02a9-120">Use `mym0wifi` as hello value of `{device id}` if you didn't change hello value.</span></span>
## <a name="configure-hello-device-connection"></a><span data-ttu-id="c02a9-121">Configurar conexión de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="c02a9-121">Configure hello device connection</span></span>
<span data-ttu-id="c02a9-122">tooconfigure Hola conexión del dispositivo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c02a9-122">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="c02a9-123">Obtener el puerto serie de hello de dispositivo de hello con cli de detección de dispositivos de hello:</span><span class="sxs-lookup"><span data-stu-id="c02a9-123">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="c02a9-124">Debe ver un resultado similar siguiente toohello y encontrar Hola usb puerto COM de su placa de Arduino:</span><span class="sxs-lookup"><span data-stu-id="c02a9-124">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![Detección de dispositivos][device-discovery]

2. <span data-ttu-id="c02a9-126">Archivo abierto hello `config.json` en Hola carpeta lección y agregar valor Hola de hello encuentra el número de puerto COM:</span><span class="sxs-lookup"><span data-stu-id="c02a9-126">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="c02a9-128">Para el puerto de hello COM, en la plataforma Windows, tiene un formato de hello `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="c02a9-128">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="c02a9-129">En macOS o Ubuntu, empieza por `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="c02a9-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="c02a9-130">Inicializar el archivo de configuración de hello ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="c02a9-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="c02a9-131">Archivo de configuración de dispositivos de hello abierto `config-arduino.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c02a9-131">Open hello device configuration file `config-arduino.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. <span data-ttu-id="c02a9-133">Realizar Hola después reemplazos en hello `config-arduino.json` archivo:</span><span class="sxs-lookup"><span data-stu-id="c02a9-133">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   * <span data-ttu-id="c02a9-134">Reemplace **[Wi-Fi SSID]** con el SSID de Wi-Fi que conectado toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="c02a9-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="c02a9-135">Reemplace **[Wi-Fi password]** por su contraseña de Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="c02a9-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="c02a9-136">Quite la cadena de hello si su Wi-Fi no requiere una contraseña.</span><span class="sxs-lookup"><span data-stu-id="c02a9-136">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="c02a9-137">Reemplace **[cadena de conexión de dispositivos de IoT]** con hello `device connection string` obtenidas.</span><span class="sxs-lookup"><span data-stu-id="c02a9-137">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="c02a9-138">Reemplace **[cadena de conexión de base de datos central de IoT]** con hello `iot hub connection string` obtenidas.</span><span class="sxs-lookup"><span data-stu-id="c02a9-138">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c02a9-139">`azure_storage_connection_string` no es necesario en este artículo.</span><span class="sxs-lookup"><span data-stu-id="c02a9-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="c02a9-140">Déjelo como está.</span><span class="sxs-lookup"><span data-stu-id="c02a9-140">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="c02a9-141">Implementar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="c02a9-141">Deploy and run hello sample application</span></span>
<span data-ttu-id="c02a9-142">Implementar y ejecutar la aplicación de ejemplo de Hola en el panel de Arduino ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c02a9-142">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="c02a9-143">Hello predeterminado gulp tarea ejecuta `install-tools` y `run` las tareas de forma secuencial.</span><span class="sxs-lookup"><span data-stu-id="c02a9-143">hello default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="c02a9-144">Cuando se [implementar aplicación de intermitencia hello][deployed-the-blink-app], ejecutar estas tareas por separado.</span><span class="sxs-lookup"><span data-stu-id="c02a9-144">When you [deployed hello blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="c02a9-145">Compruebe que la aplicación de ejemplo de Hola funciona</span><span class="sxs-lookup"><span data-stu-id="c02a9-145">Verify that hello sample application works</span></span>
<span data-ttu-id="c02a9-146">Debería ver Hola GPIO #0 a bordo LED parpadea cada dos segundos.</span><span class="sxs-lookup"><span data-stu-id="c02a9-146">You should see hello GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="c02a9-147">Cada vez que Hola LED parpadea, aplicación de ejemplo de Hola envía un centro de IoT tooyour de mensaje y comprueba que ese mensaje Hola se ha enviado correctamente tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c02a9-147">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="c02a9-148">Además, cada mensaje recibido por el centro de IoT Hola se imprime en la ventana de la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="c02a9-148">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="c02a9-149">aplicación de ejemplo de Hola finaliza automáticamente después de enviar 20 mensajes.</span><span class="sxs-lookup"><span data-stu-id="c02a9-149">hello sample application terminates automatically after sending 20 messages.</span></span>

![Aplicación de ejemplo con mensajes enviados y recibidos][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="c02a9-151">Resumen</span><span class="sxs-lookup"><span data-stu-id="c02a9-151">Summary</span></span>
<span data-ttu-id="c02a9-152">Ha implementado y ejecutar aplicación de ejemplo de Hola nueva parpadeo en su centro de IoT Arduino panel toosend mensajes del dispositivo a la nube tooyour.</span><span class="sxs-lookup"><span data-stu-id="c02a9-152">You've deployed and run hello new blink sample application on your Arduino board toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="c02a9-153">Ahora, supervisar los mensajes tal y como se escriben toohello cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c02a9-153">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c02a9-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c02a9-154">Next steps</span></span>
<span data-ttu-id="c02a9-155">[Lectura de los mensajes que se conservan en Azure Storage][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="c02a9-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md