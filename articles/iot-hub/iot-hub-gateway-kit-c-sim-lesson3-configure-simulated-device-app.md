---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 3: Ejecución de la aplicación de ejemplo | Microsoft Docs"
description: "Ejecución de una aplicación de ejemplo de dispositivo simulado para enviar datos sobre temperatura a IoT Hub"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: datos a la nube
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7df2d730c38a9f715e0fd57b4d436724a5727760
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="f1356-104">Configuración y ejecución de una aplicación de ejemplo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="f1356-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="f1356-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="f1356-105">What you will do</span></span>

- <span data-ttu-id="f1356-106">Clone el repositorio de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f1356-106">Clone the sample repository.</span></span>
- <span data-ttu-id="f1356-107">Use la CLI de Azure para obtener la información sobre dispositivos lógicos y sobre IoT Hub para la aplicación de ejemplo de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="f1356-107">Use the Azure CLI to get your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="f1356-108">Configure y ejecute la aplicación de ejemplo de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="f1356-108">Configure and run the simulated device sample application.</span></span>

<span data-ttu-id="f1356-109">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f1356-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f1356-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="f1356-110">What you will learn</span></span>

<span data-ttu-id="f1356-111">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f1356-111">In this article, you will learn:</span></span>

- <span data-ttu-id="f1356-112">Cómo configurar y ejecutar la aplicación de muestra de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="f1356-112">How to configure and run the simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f1356-113">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="f1356-113">What you need</span></span>

<span data-ttu-id="f1356-114">Debe haber completado correctamente los siguientes tutoriales:</span><span class="sxs-lookup"><span data-stu-id="f1356-114">You must have successfully completed</span></span>

- [<span data-ttu-id="f1356-115">Creación de un IoT Hub y registro del dispositivo</span><span class="sxs-lookup"><span data-stu-id="f1356-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="f1356-116">Clonar el repositorio de ejemplo en el equipo host</span><span class="sxs-lookup"><span data-stu-id="f1356-116">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="f1356-117">Para clonar el repositorio de ejemplo, siga estos pasos en el equipo host:</span><span class="sxs-lookup"><span data-stu-id="f1356-117">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="f1356-118">Abra una ventana del símbolo del sistema en Windows o abra un terminal de macOS o Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f1356-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="f1356-119">Ejecute los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f1356-119">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-the-simulated-device-and-your-nuc"></a><span data-ttu-id="f1356-120">Configurar el dispositivo simulado y su NUC</span><span class="sxs-lookup"><span data-stu-id="f1356-120">Configure the simulated device and your NUC</span></span>

1. <span data-ttu-id="f1356-121">Abra el archivo de configuración `config.json` en Visual Studio Code con este comando:</span><span class="sxs-lookup"><span data-stu-id="f1356-121">Open the configuration file `config.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="f1356-122">Reemplazar `"has_sensortag": true` con `"has_sensortag": false`</span><span class="sxs-lookup"><span data-stu-id="f1356-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![Configurar un dispositivo de SensorTag de TI si no lo tiene](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="f1356-124">Inicialice el archivo de configuración con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="f1356-124">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="f1356-125">Abra `config-gateway.json` en Visual Studio Code mediante la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f1356-125">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="f1356-126">Busque la siguiente línea de código y reemplace `[device hostname or IP address]` con el nombre de host o la dirección IP de Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="f1356-126">Locate the following line of code and replace `[device hostname or IP address]` with IP address or host name of the Intel NUC.</span></span>
   <span data-ttu-id="f1356-127">![captura de pantalla de puerta de enlace de configuración](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="f1356-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-the-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="f1356-128">Obtener la cadena de conexión del dispositivo lógico de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="f1356-128">Get the connection string of your IoT hub logical device</span></span>

<span data-ttu-id="f1356-129">Para obtener la cadena de conexión de Azure IoT Hub del dispositivo lógico, ejecute el siguiente comando en el equipo host:</span><span class="sxs-lookup"><span data-stu-id="f1356-129">To get the Azure IoT hub connection string of your logical device, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="f1356-130">`{IoT hub name}` es el nombre del IoT Hub utilizado.</span><span class="sxs-lookup"><span data-stu-id="f1356-130">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="f1356-131">Use iot-gateway como el valor de `{resource group name}` y utilice mydevice como el valor de `{device id}` si no lo ha cambiado en la lección 2.</span><span class="sxs-lookup"><span data-stu-id="f1356-131">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="f1356-132">Configurar la aplicación de ejemplo de carga en la nube del dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="f1356-132">Configure the simulated device cloud upload sample application</span></span>

<span data-ttu-id="f1356-133">Para configurar y ejecutar la aplicación de ejemplo de carga en la nube del dispositivo simulado, siga estos pasos en el equipo host:</span><span class="sxs-lookup"><span data-stu-id="f1356-133">To configure and run the simulated device cloud upload sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="f1356-134">Abra `config-sensortag.json` en Visual Studio Code mediante la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f1356-134">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![captura de sensortag configurado](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="f1356-136">Realice las sustituciones siguientes en el código:</span><span class="sxs-lookup"><span data-stu-id="f1356-136">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="f1356-137">Reemplace `[IoT hub name]` con el nombre de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f1356-137">Replace `[IoT hub name]` with the IoT hub name.</span></span>
   - <span data-ttu-id="f1356-138">Reemplace `[IoT device connection string]` con la cadena de conexión del dispositivo lógico de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f1356-138">Replace `[IoT device connection string]` with the connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="f1356-139">Ejecute la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f1356-139">Run the application.</span></span>

   <span data-ttu-id="f1356-140">Implemente y ejecute la aplicación mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="f1356-140">Deploy and run the application by running the following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-the-sample-application-works"></a><span data-ttu-id="f1356-141">Comprobación del funcionamiento de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f1356-141">Verify the sample application works</span></span>

<span data-ttu-id="f1356-142">Ahora debe aparecer un resultado parecido al siguiente:</span><span class="sxs-lookup"><span data-stu-id="f1356-142">You should now see output like the following:</span></span>

![resultado de la aplicación de ejemplo del dispositivo simulado](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="f1356-144">La aplicación envía datos sobre temperatura a IoT Hub, una tarea que dura 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="f1356-144">The application sends temperature data to your IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="f1356-145">Resumen</span><span class="sxs-lookup"><span data-stu-id="f1356-145">Summary</span></span>

<span data-ttu-id="f1356-146">Ha configurado y ejecutado correctamente la aplicación de ejemplo de carga en la nube del dispositivo simulado que envía datos a IoT Hub con el dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="f1356-146">You've successfully configured and run the simulated device cloud upload sample application which sends data to your IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1356-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f1356-147">Next steps</span></span>
[<span data-ttu-id="f1356-148">Lectura de mensajes en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="f1356-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)