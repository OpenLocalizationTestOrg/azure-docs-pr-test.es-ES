---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Lección 3: Ejecución de la aplicación de ejemplo | Microsoft Docs"
description: "Ejecute una aplicación de ejemplo BLE para recibir datos de SensorTag para BLE y del IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "aplicación ble, aplicación para monitor de sensores, colección de datos del sensor, datos del sensor, datos del sensor a la nube"
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
ms.openlocfilehash: f6fa158dbe1d48be7d493efa6217e1e0a759d2f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="a0da2-104">Configuración y ejecución de la aplicación de ejemplo BLE</span><span class="sxs-lookup"><span data-stu-id="a0da2-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a0da2-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="a0da2-105">What you will do</span></span>

- <span data-ttu-id="a0da2-106">Clone el repositorio de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a0da2-106">Clone the sample repository.</span></span> 
- <span data-ttu-id="a0da2-107">Configure la conectividad entre SensorTag e Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="a0da2-107">Set up the connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="a0da2-108">Use la CLI de Azure para obtener la información de SensorTag para una aplicación de ejemplo BLE (Bluetooth de bajo consumo).</span><span class="sxs-lookup"><span data-stu-id="a0da2-108">Use the Azure CLI to get your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="a0da2-109">Y configure y ejecute la aplicación de ejemplo BLE.</span><span class="sxs-lookup"><span data-stu-id="a0da2-109">And configure and run the BLE sample application.</span></span> 

<span data-ttu-id="a0da2-110">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a0da2-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a0da2-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="a0da2-111">What you will learn</span></span>

<span data-ttu-id="a0da2-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a0da2-112">In this article, you will learn:</span></span>

- <span data-ttu-id="a0da2-113">Cómo configurar y ejecutar la aplicación de ejemplo BLE.</span><span class="sxs-lookup"><span data-stu-id="a0da2-113">How to configure and run the BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a0da2-114">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="a0da2-114">What you need</span></span>

<span data-ttu-id="a0da2-115">Debe haber completado correctamente los siguientes tutoriales:</span><span class="sxs-lookup"><span data-stu-id="a0da2-115">You must have successfully completed</span></span>

- [<span data-ttu-id="a0da2-116">Cree un IoT Hub y registre SensorTag</span><span class="sxs-lookup"><span data-stu-id="a0da2-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="a0da2-117">Clonar el repositorio de ejemplo en el equipo host</span><span class="sxs-lookup"><span data-stu-id="a0da2-117">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="a0da2-118">Para clonar el repositorio de ejemplo, siga estos pasos en el equipo host:</span><span class="sxs-lookup"><span data-stu-id="a0da2-118">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="a0da2-119">Abra una ventana del símbolo del sistema en Windows o abra un terminal de macOS o Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="a0da2-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="a0da2-120">Ejecute los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a0da2-120">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-the-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="a0da2-121">Configurar la conectividad entre SensorTag e Intel NUC</span><span class="sxs-lookup"><span data-stu-id="a0da2-121">Set up the connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="a0da2-122">Para configurar la conectividad, siga estos pasos en el equipo host:</span><span class="sxs-lookup"><span data-stu-id="a0da2-122">To set up the connectivity, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="a0da2-123">Inicialice el archivo de configuración con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a0da2-123">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="a0da2-124">Abra `config-gateway.json` en Visual Studio Code mediante la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a0da2-124">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="a0da2-125">Busque la siguiente línea de código y reemplace `[device hostname or IP address]` con el nombre de host o la dirección IP de Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="a0da2-125">Locate the following line of code and replace `[device hostname or IP address]` with the IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="a0da2-126">![captura de pantalla de puerta de enlace de configuración](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="a0da2-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="a0da2-127">Instale herramientas auxiliares en Intel NUC mediante la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a0da2-127">Install helper tools on Intel NUC by running the following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="a0da2-128">Active SensorTag; para ello, presione el botón de encendido como en la imagen siguiente y, a continuación, el LED verde debe parpadear.</span><span class="sxs-lookup"><span data-stu-id="a0da2-128">Turn on SensorTag by pressing the power button as the following picture, and the green LED should blink.</span></span>

   ![activar SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="a0da2-130">Examine los dispositivos SensorTag mediante la ejecución de los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a0da2-130">Scan SensorTag devices by running the following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="a0da2-131">Pruebe la conectividad entre SensorTag e Intel NUC mediante la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a0da2-131">Test the connectivity between the SensorTag and Intel NUC by running the following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="a0da2-132">Reemplace `{mac address}` por la dirección MAC obtenida en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="a0da2-132">Replace `{mac address}` with the MAC address that you obtained in the previous step.</span></span>

## <a name="get-the-connection-string-of-sensortag"></a><span data-ttu-id="a0da2-133">Obtener la cadena de conexión de SensorTag</span><span class="sxs-lookup"><span data-stu-id="a0da2-133">Get the connection string of SensorTag</span></span>

<span data-ttu-id="a0da2-134">Para obtener la cadena de conexión de Azure IoT Hub para SensorTag, ejecute el siguiente comando en el equipo host:</span><span class="sxs-lookup"><span data-stu-id="a0da2-134">To get the Azure IoT hub connection string of SensorTag, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="a0da2-135">`{IoT hub name}` es el nombre del IoT Hub utilizado.</span><span class="sxs-lookup"><span data-stu-id="a0da2-135">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="a0da2-136">Use iot-gateway como el valor de `{resource group name}` y utilice mydevice como el valor de `{device id}` si no lo ha cambiado en la lección 2.</span><span class="sxs-lookup"><span data-stu-id="a0da2-136">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-ble-sample-application"></a><span data-ttu-id="a0da2-137">Configurar la aplicación de ejemplo BLE</span><span class="sxs-lookup"><span data-stu-id="a0da2-137">Configure the BLE sample application</span></span>

<span data-ttu-id="a0da2-138">Para configurar y ejecutar la aplicación de ejemplo BLE, siga estos pasos en el equipo host:</span><span class="sxs-lookup"><span data-stu-id="a0da2-138">To configure and run the BLE sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="a0da2-139">Abra `config-sensortag.json` en Visual Studio Code mediante la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a0da2-139">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![captura de sensortag configurado](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="a0da2-141">Realice las sustituciones siguientes en el código:</span><span class="sxs-lookup"><span data-stu-id="a0da2-141">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="a0da2-142">Reemplace `[IoT hub name]` con el nombre de IoT Hub utilizado.</span><span class="sxs-lookup"><span data-stu-id="a0da2-142">Replace `[IoT hub name]` with the IoT hub name that you used.</span></span>
   - <span data-ttu-id="a0da2-143">Reemplace `[IoT device connection string]` con la cadena de conexión de SensorTag obtenida.</span><span class="sxs-lookup"><span data-stu-id="a0da2-143">Replace `[IoT device connection string]` with the connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="a0da2-144">Reemplace `[device_mac_address]` con la dirección MAC de SensorTag obtenida.</span><span class="sxs-lookup"><span data-stu-id="a0da2-144">Replace `[device_mac_address]` with the MAC address of the SensorTag that you obtained.</span></span>

3. <span data-ttu-id="a0da2-145">Ejecute la aplicación de ejemplo BLE.</span><span class="sxs-lookup"><span data-stu-id="a0da2-145">Run the BLE sample application.</span></span>

   <span data-ttu-id="a0da2-146">Para ejecutar la aplicación de ejemplo BLE, siga estos pasos en el equipo host:</span><span class="sxs-lookup"><span data-stu-id="a0da2-146">To run the BLE sample application, follow these steps on the host computer:</span></span>

   1. <span data-ttu-id="a0da2-147">Active SensorTag.</span><span class="sxs-lookup"><span data-stu-id="a0da2-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="a0da2-148">Implemente y ejecute la aplicación de ejemplo BLE en Inter NUC mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="a0da2-148">Deploy and run the BLE sample application on Intel NUC by running the following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-the-ble-sample-application-works"></a><span data-ttu-id="a0da2-149">Verificación del funcionamiento de la aplicación de ejemplo BLE</span><span class="sxs-lookup"><span data-stu-id="a0da2-149">Verify that the BLE sample application works</span></span>

<span data-ttu-id="a0da2-150">Ahora debe aparecer algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a0da2-150">You should now see an output like the following:</span></span>

![Resultado de la aplicación de ejemplo BLE](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="a0da2-152">La aplicación de ejemplo continúa recopilando datos de temperatura y los envía a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a0da2-152">The sample application keeps collecting temperature data and sent it to your IoT hub.</span></span> <span data-ttu-id="a0da2-153">La aplicación de ejemplo finaliza automáticamente después de realizar envíos durante 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="a0da2-153">The sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="a0da2-154">Resumen</span><span class="sxs-lookup"><span data-stu-id="a0da2-154">Summary</span></span>

<span data-ttu-id="a0da2-155">Ha configurado correctamente la conectividad entre SensorTag e Intel NUC y ha ejecutado una aplicación de ejemplo BLE que recopila y envía datos desde SensorTag al IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a0da2-155">You've successfully set up the connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag to your IoT hub.</span></span> <span data-ttu-id="a0da2-156">Está listo para aprender a verificar si IoT Hube ha recibido los datos.</span><span class="sxs-lookup"><span data-stu-id="a0da2-156">You're ready to learn how to verify that your IoT hub has received the data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0da2-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a0da2-157">Next steps</span></span>
[<span data-ttu-id="a0da2-158">Lectura de mensajes en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="a0da2-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)