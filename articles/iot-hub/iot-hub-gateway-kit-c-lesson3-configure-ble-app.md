---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Lección 3: Ejecución de la aplicación de ejemplo | Microsoft Docs"
description: "Ejecutar un datos de tooreceive habilitar la aplicación de ejemplo de Bilitar SensorTag y desde el centro de IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Habilitar aplicación, aplicación monitor de sensor, recopilación de datos de sensor, datos de los sensores, toocloud de datos de sensor"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="2d1da-104">Configuración y ejecución de la aplicación de ejemplo BLE</span><span class="sxs-lookup"><span data-stu-id="2d1da-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2d1da-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="2d1da-105">What you will do</span></span>

- <span data-ttu-id="2d1da-106">Repositorio de ejemplo de Hola de clonación.</span><span class="sxs-lookup"><span data-stu-id="2d1da-106">Clone hello sample repository.</span></span> 
- <span data-ttu-id="2d1da-107">Configurar la conectividad de hello entre SensorTag y NUC de Intel.</span><span class="sxs-lookup"><span data-stu-id="2d1da-107">Set up hello connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="2d1da-108">Utilice hello Azure CLI tooget del centro de IoT y la información de SensorTag para una aplicación de ejemplo Bilitar (Bluetooth baja energía).</span><span class="sxs-lookup"><span data-stu-id="2d1da-108">Use hello Azure CLI tooget your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="2d1da-109">Configurar y ejecutar la aplicación de ejemplo de Hola BLE.</span><span class="sxs-lookup"><span data-stu-id="2d1da-109">And configure and run hello BLE sample application.</span></span> 

<span data-ttu-id="2d1da-110">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2d1da-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2d1da-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="2d1da-111">What you will learn</span></span>

<span data-ttu-id="2d1da-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2d1da-112">In this article, you will learn:</span></span>

- <span data-ttu-id="2d1da-113">¿Cómo tooconfigure y ejecución Hola habilitar aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2d1da-113">How tooconfigure and run hello BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2d1da-114">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="2d1da-114">What you need</span></span>

<span data-ttu-id="2d1da-115">Debe haber completado correctamente los siguientes tutoriales:</span><span class="sxs-lookup"><span data-stu-id="2d1da-115">You must have successfully completed</span></span>

- [<span data-ttu-id="2d1da-116">Cree un IoT Hub y registre SensorTag</span><span class="sxs-lookup"><span data-stu-id="2d1da-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="2d1da-117">Equipo de host de clon Hola ejemplo repositorio toohello</span><span class="sxs-lookup"><span data-stu-id="2d1da-117">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="2d1da-118">repositorio de ejemplo de Hola tooclone, siga estos pasos en el equipo de host de hello:</span><span class="sxs-lookup"><span data-stu-id="2d1da-118">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="2d1da-119">Abra una ventana del símbolo del sistema en Windows o abra un terminal de macOS o Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="2d1da-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="2d1da-120">Ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="2d1da-120">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="2d1da-121">Configurar la conectividad de hello entre SensorTag y NUC de Intel</span><span class="sxs-lookup"><span data-stu-id="2d1da-121">Set up hello connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="2d1da-122">tooset la conectividad de hello, siga estos pasos en el equipo de host de hello:</span><span class="sxs-lookup"><span data-stu-id="2d1da-122">tooset up hello connectivity, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="2d1da-123">Inicializar el archivo de configuración de hello ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="2d1da-123">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="2d1da-124">Abra `config-gateway.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2d1da-124">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="2d1da-125">Busque Hola después de la línea de código y reemplace `[device hostname or IP address]` con el nombre de host o dirección IP de Hola de NUC de Intel.</span><span class="sxs-lookup"><span data-stu-id="2d1da-125">Locate hello following line of code and replace `[device hostname or IP address]` with hello IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="2d1da-126">![captura de pantalla de puerta de enlace de configuración](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="2d1da-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="2d1da-127">Instalar herramientas auxiliares en Intel NUC ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2d1da-127">Install helper tools on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="2d1da-128">Activar SensorTag presionando el botón de encendido de hello como después de la imagen de Hola y Hola que debe parpadear LED verde.</span><span class="sxs-lookup"><span data-stu-id="2d1da-128">Turn on SensorTag by pressing hello power button as hello following picture, and hello green LED should blink.</span></span>

   ![activar SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="2d1da-130">Examinar SensorTag dispositivos mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="2d1da-130">Scan SensorTag devices by running hello following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="2d1da-131">Probar la conectividad de hello entre hello SensorTag y NUC de Intel mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2d1da-131">Test hello connectivity between hello SensorTag and Intel NUC by running hello following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="2d1da-132">Reemplace `{mac address}` con dirección MAC que obtuvo en el paso anterior de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="2d1da-132">Replace `{mac address}` with hello MAC address that you obtained in hello previous step.</span></span>

## <a name="get-hello-connection-string-of-sensortag"></a><span data-ttu-id="2d1da-133">Obtener la cadena de conexión de Hola de SensorTag</span><span class="sxs-lookup"><span data-stu-id="2d1da-133">Get hello connection string of SensorTag</span></span>

<span data-ttu-id="2d1da-134">Hola tooget cadena de conexión de base de datos central de IoT de Azure de SensorTag, ejecute hello siguiente comando en el equipo de host de hello:</span><span class="sxs-lookup"><span data-stu-id="2d1da-134">tooget hello Azure IoT hub connection string of SensorTag, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="2d1da-135">`{IoT hub name}`es el nombre del centro de IoT Hola que ha usado.</span><span class="sxs-lookup"><span data-stu-id="2d1da-135">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="2d1da-136">Usar puerta de enlace de iot como valor de Hola de `{resource group name}` y use mydevice como valor de Hola de `{device id}` si no cambia el valor de hello en la lección 2.</span><span class="sxs-lookup"><span data-stu-id="2d1da-136">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-ble-sample-application"></a><span data-ttu-id="2d1da-137">Configurar la aplicación de ejemplo de Hola BLE</span><span class="sxs-lookup"><span data-stu-id="2d1da-137">Configure hello BLE sample application</span></span>

<span data-ttu-id="2d1da-138">tooconfigure y ejecución Hola aplicación de ejemplo BLE, siga estos pasos en el equipo de host de hello:</span><span class="sxs-lookup"><span data-stu-id="2d1da-138">tooconfigure and run hello BLE sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="2d1da-139">Abra `config-sensortag.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2d1da-139">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![captura de sensortag configurado](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="2d1da-141">Asegúrese de hello después reemplazos en el código de hello:</span><span class="sxs-lookup"><span data-stu-id="2d1da-141">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="2d1da-142">Reemplace `[IoT hub name]` con el nombre del centro de IoT Hola que ha usado.</span><span class="sxs-lookup"><span data-stu-id="2d1da-142">Replace `[IoT hub name]` with hello IoT hub name that you used.</span></span>
   - <span data-ttu-id="2d1da-143">Reemplace `[IoT device connection string]` con cadena de conexión de Hola de SensorTag que ha adquirido.</span><span class="sxs-lookup"><span data-stu-id="2d1da-143">Replace `[IoT device connection string]` with hello connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="2d1da-144">Reemplace `[device_mac_address]` con hello dirección MAC de hello SensorTag que ha adquirido.</span><span class="sxs-lookup"><span data-stu-id="2d1da-144">Replace `[device_mac_address]` with hello MAC address of hello SensorTag that you obtained.</span></span>

3. <span data-ttu-id="2d1da-145">Ejecute la aplicación de ejemplo de Hola BLE.</span><span class="sxs-lookup"><span data-stu-id="2d1da-145">Run hello BLE sample application.</span></span>

   <span data-ttu-id="2d1da-146">Hola toorun aplicación de ejemplo BLE, siga estos pasos en el equipo de host de hello:</span><span class="sxs-lookup"><span data-stu-id="2d1da-146">toorun hello BLE sample application, follow these steps on hello host computer:</span></span>

   1. <span data-ttu-id="2d1da-147">Active SensorTag.</span><span class="sxs-lookup"><span data-stu-id="2d1da-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="2d1da-148">Implementar y ejecutar la aplicación de ejemplo de Hola BLE en Intel NUC ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="2d1da-148">Deploy and run hello BLE sample application on Intel NUC by running hello following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a><span data-ttu-id="2d1da-149">Compruebe que la aplicación de ejemplo de Hola Bilitar funciona</span><span class="sxs-lookup"><span data-stu-id="2d1da-149">Verify that hello BLE sample application works</span></span>

<span data-ttu-id="2d1da-150">Ahora debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="2d1da-150">You should now see an output like hello following:</span></span>

![Resultado de la aplicación de ejemplo BLE](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="2d1da-152">aplicación de ejemplo de Hola mantiene la recopilación de datos de temperatura y enviarlo tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="2d1da-152">hello sample application keeps collecting temperature data and sent it tooyour IoT hub.</span></span> <span data-ttu-id="2d1da-153">aplicación de ejemplo de Hola finaliza automáticamente después de enviar 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="2d1da-153">hello sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="2d1da-154">Resumen</span><span class="sxs-lookup"><span data-stu-id="2d1da-154">Summary</span></span>

<span data-ttu-id="2d1da-155">Correctamente ha configurar la conectividad de hello entre SensorTag y NUC de Intel y ejecutar una aplicación de ejemplo Bilitar que recopila y envía los datos SensorTag tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="2d1da-155">You've successfully set up hello connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag tooyour IoT hub.</span></span> <span data-ttu-id="2d1da-156">Está listo toolearn cómo tooverify que ha recibido su centro de IoT Hola datos.</span><span class="sxs-lookup"><span data-stu-id="2d1da-156">You're ready toolearn how tooverify that your IoT hub has received hello data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d1da-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2d1da-157">Next steps</span></span>
[<span data-ttu-id="2d1da-158">Lectura de mensajes en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="2d1da-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)