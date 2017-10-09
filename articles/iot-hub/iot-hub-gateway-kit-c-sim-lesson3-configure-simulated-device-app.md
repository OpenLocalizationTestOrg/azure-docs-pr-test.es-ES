---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 3: Ejecución de la aplicación de ejemplo | Microsoft Docs"
description: "Ejecutar un centro de IoT dispositivo simulado ejemplo aplicación toosend temperatura datos tooyour"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: toocloud de datos
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
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="2feec-104">Configuración y ejecución de una aplicación de ejemplo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="2feec-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2feec-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="2feec-105">What you will do</span></span>

- <span data-ttu-id="2feec-106">Repositorio de ejemplo de Hola de clonación.</span><span class="sxs-lookup"><span data-stu-id="2feec-106">Clone hello sample repository.</span></span>
- <span data-ttu-id="2feec-107">Utilice hello Azure CLI tooget su información de dispositivo lógico y el centro de IoT para aplicación de ejemplo de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="2feec-107">Use hello Azure CLI tooget your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="2feec-108">Configure y ejecute la aplicación de ejemplo de Hola simulada dispositivos.</span><span class="sxs-lookup"><span data-stu-id="2feec-108">Configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="2feec-109">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2feec-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2feec-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="2feec-110">What you will learn</span></span>

<span data-ttu-id="2feec-111">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2feec-111">In this article, you will learn:</span></span>

- <span data-ttu-id="2feec-112">Cómo tooconfigure y ejecución Hola simulan la aplicación de ejemplo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2feec-112">How tooconfigure and run hello simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2feec-113">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="2feec-113">What you need</span></span>

<span data-ttu-id="2feec-114">Debe haber completado correctamente los siguientes tutoriales:</span><span class="sxs-lookup"><span data-stu-id="2feec-114">You must have successfully completed</span></span>

- [<span data-ttu-id="2feec-115">Creación de una instancia de IoT Hub y registro del dispositivo</span><span class="sxs-lookup"><span data-stu-id="2feec-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="2feec-116">Equipo de host de clon Hola ejemplo repositorio toohello</span><span class="sxs-lookup"><span data-stu-id="2feec-116">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="2feec-117">repositorio de ejemplo de Hola tooclone, siga estos pasos en el equipo de host de hello:</span><span class="sxs-lookup"><span data-stu-id="2feec-117">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="2feec-118">Abra una ventana del símbolo del sistema en Windows o abra un terminal de macOS o Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="2feec-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="2feec-119">Ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="2feec-119">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a><span data-ttu-id="2feec-120">Configurar dispositivo simulado de Hola y su NUC</span><span class="sxs-lookup"><span data-stu-id="2feec-120">Configure hello simulated device and your NUC</span></span>

1. <span data-ttu-id="2feec-121">Archivo de configuración abierto hello `config.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2feec-121">Open hello configuration file `config.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="2feec-122">Reemplazar `"has_sensortag": true` con `"has_sensortag": false`</span><span class="sxs-lookup"><span data-stu-id="2feec-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![Configurar un dispositivo de SensorTag de TI si no lo tiene](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="2feec-124">Inicializar el archivo de configuración de hello ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="2feec-124">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="2feec-125">Abra `config-gateway.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2feec-125">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="2feec-126">Busque Hola después de la línea de código y reemplace `[device hostname or IP address]` con el nombre de host o dirección IP de hello NUC de Intel.</span><span class="sxs-lookup"><span data-stu-id="2feec-126">Locate hello following line of code and replace `[device hostname or IP address]` with IP address or host name of hello Intel NUC.</span></span>
   <span data-ttu-id="2feec-127">![captura de pantalla de puerta de enlace de configuración](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="2feec-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="2feec-128">Obtener la cadena de conexión de Hola de su dispositivo lógico de centro de IoT</span><span class="sxs-lookup"><span data-stu-id="2feec-128">Get hello connection string of your IoT hub logical device</span></span>

<span data-ttu-id="2feec-129">Hola tooget cadena de conexión de base de datos central de IoT de Azure del dispositivo lógico, ejecute hello siguiente comando en el equipo de host de hello:</span><span class="sxs-lookup"><span data-stu-id="2feec-129">tooget hello Azure IoT hub connection string of your logical device, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="2feec-130">`{IoT hub name}`es el nombre del centro de IoT Hola que ha usado.</span><span class="sxs-lookup"><span data-stu-id="2feec-130">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="2feec-131">Usar puerta de enlace de iot como valor de Hola de `{resource group name}` y use mydevice como valor de Hola de `{device id}` si no cambia el valor de hello en la lección 2.</span><span class="sxs-lookup"><span data-stu-id="2feec-131">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="2feec-132">Configuración de aplicación de ejemplo de carga de hello simulada dispositivos en la nube</span><span class="sxs-lookup"><span data-stu-id="2feec-132">Configure hello simulated device cloud upload sample application</span></span>

<span data-ttu-id="2feec-133">tooconfigure y ejecución Hola simular dispositivos nube cargar la aplicación de ejemplo, siga estos pasos en el equipo de host de hello:</span><span class="sxs-lookup"><span data-stu-id="2feec-133">tooconfigure and run hello simulated device cloud upload sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="2feec-134">Abra `config-sensortag.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2feec-134">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![captura de sensortag configurado](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="2feec-136">Asegúrese de hello después reemplazos en el código de hello:</span><span class="sxs-lookup"><span data-stu-id="2feec-136">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="2feec-137">Reemplace `[IoT hub name]` con el nombre del centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="2feec-137">Replace `[IoT hub name]` with hello IoT hub name.</span></span>
   - <span data-ttu-id="2feec-138">Reemplace `[IoT device connection string]` con cadena de conexión de Hola de su dispositivo lógico de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="2feec-138">Replace `[IoT device connection string]` with hello connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="2feec-139">Ejecute la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="2feec-139">Run hello application.</span></span>

   <span data-ttu-id="2feec-140">Implementar y ejecutar la aplicación hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2feec-140">Deploy and run hello application by running hello following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a><span data-ttu-id="2feec-141">Compruebe que funciona de aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="2feec-141">Verify hello sample application works</span></span>

<span data-ttu-id="2feec-142">Ahora debería ver resultados similares a Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="2feec-142">You should now see output like hello following:</span></span>

![resultado de la aplicación de ejemplo del dispositivo simulado](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="2feec-144">aplicación Hello envía temperatura datos tooyour centro de IoT, que tiene una validez de 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="2feec-144">hello application sends temperature data tooyour IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="2feec-145">Resumen</span><span class="sxs-lookup"><span data-stu-id="2feec-145">Summary</span></span>

<span data-ttu-id="2feec-146">Ha configurado correctamente y ejecución Hola simula la aplicación de ejemplo de carga de nube de dispositivo que envía el centro de IoT de tooyour de datos con el dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="2feec-146">You've successfully configured and run hello simulated device cloud upload sample application which sends data tooyour IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2feec-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2feec-147">Next steps</span></span>
[<span data-ttu-id="2feec-148">Lectura de mensajes en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="2feec-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)