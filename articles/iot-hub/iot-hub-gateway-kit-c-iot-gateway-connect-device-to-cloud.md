---
title: Usar una puerta de enlace de IoT para conectar un dispositivo a Azure IoT Hub | Microsoft Docs
description: Aprenda a usar Intel NUC como una puerta de enlace de IoT para conectar un SensorTag de TI y enviar datos del sensor a Azure IoT Hub en la nube.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: puerta de enlace de IOT conectar dispositivo a la nube
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 4fb77ed0241d15338c2574fd22828507c3e40cb3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-iot-gateway-to-connect-things-to-the-cloud---sensortag-to-azure-iot-hub"></a><span data-ttu-id="c7961-104">Usar una puerta de enlace de IoT para conectar dispositivos a la nube: SensorTag a Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="c7961-104">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="c7961-105">Antes de empezar este tutorial, asegúrese de haber completado [Set up Intel NUC as an IoT gateway (Configurar Intel NUC como una puerta de enlace de IoT)](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="c7961-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="c7961-106">En [Set up Intel NUC as an IoT gateway (Configurar Intel NUC como una puerta de enlace de IoT)](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), se configura el dispositivo Intel NUC como una puerta de enlace de IoT.</span><span class="sxs-lookup"><span data-stu-id="c7961-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up the Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c7961-107">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="c7961-107">What you will learn</span></span>

<span data-ttu-id="c7961-108">Aprenda a usar una puerta de enlace de IoT para conectar un SensorTag de Texas Instruments (CC2650STK) a Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c7961-108">You learn how to use an IoT gateway to connect a Texas Instruments SensorTag (CC2650STK) to Azure IoT Hub.</span></span> <span data-ttu-id="c7961-109">La puerta de enlace de IoT envía datos de temperatura y humedad recopilados del SensorTag a Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c7961-109">The IoT gateway sends temperature and humidity data collected from the SensorTag to Azure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="c7961-110">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="c7961-110">What you will do</span></span>

- <span data-ttu-id="c7961-111">Cree un Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c7961-111">Create an IoT hub.</span></span>
- <span data-ttu-id="c7961-112">Registre un dispositivo en IoT Hub para el SensorTag.</span><span class="sxs-lookup"><span data-stu-id="c7961-112">Register a device in the IoT hub for the SensorTag.</span></span>
- <span data-ttu-id="c7961-113">Habilite la conexión entre la puerta de enlace de IoT y el SensorTag.</span><span class="sxs-lookup"><span data-stu-id="c7961-113">Enable the connection between the IoT gateway and the SensorTag.</span></span>
- <span data-ttu-id="c7961-114">Ejecute una aplicación de ejemplo BLE para enviar datos del SensorTag a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c7961-114">Run a BLE sample application to send SensorTag data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c7961-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="c7961-115">What you need</span></span>

- <span data-ttu-id="c7961-116">Tutorial [Set up Intel NUC as an IoT gateway (Configurar Intel NUC como una puerta de enlace de IoT)](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completado en el que haya configurado Intel NUC como una puerta de enlace de IoT.</span><span class="sxs-lookup"><span data-stu-id="c7961-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="c7961-117">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="c7961-117">An active Azure subscription.</span></span> <span data-ttu-id="c7961-118">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="c7961-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="c7961-119">Un cliente de SSH que se ejecute en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="c7961-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="c7961-120">En Windows se recomienda PuTTY.</span><span class="sxs-lookup"><span data-stu-id="c7961-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="c7961-121">Linux y macOS ya vienen con un cliente de SSH.</span><span class="sxs-lookup"><span data-stu-id="c7961-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="c7961-122">La dirección IP y el nombre de usuario y la contraseña para acceder a la puerta de enlace desde el cliente de SSH.</span><span class="sxs-lookup"><span data-stu-id="c7961-122">The IP address and the username and password to access the gateway from the SSH client.</span></span>
- <span data-ttu-id="c7961-123">Una conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="c7961-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="c7961-124">Aquí se registra este nuevo dispositivo para el SensorTag</span><span class="sxs-lookup"><span data-stu-id="c7961-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-the-connection-between-the-iot-gateway-and-the-sensortag"></a><span data-ttu-id="c7961-125">Habilitar la conexión entre la puerta de enlace de IoT y el SensorTag</span><span class="sxs-lookup"><span data-stu-id="c7961-125">Enable the connection between the IoT gateway and the SensorTag</span></span>

<span data-ttu-id="c7961-126">En esta sección se realizarán las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="c7961-126">In this section, you perform the following tasks:</span></span>

- <span data-ttu-id="c7961-127">Obtener la dirección MAC del SensorTag para la conexión Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="c7961-127">Get the MAC address of the SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="c7961-128">Iniciar una conexión Bluetooth desde la puerta de enlace de IoT al SensorTag.</span><span class="sxs-lookup"><span data-stu-id="c7961-128">Initiate a Bluetooth connection from the IoT gateway to the SensorTag.</span></span>

### <a name="get-the-mac-address-of-the-sensortag-for-bluetooth-connection"></a><span data-ttu-id="c7961-129">Obtener la dirección MAC del SensorTag para la conexión Bluetooth</span><span class="sxs-lookup"><span data-stu-id="c7961-129">Get the MAC address of the SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="c7961-130">En el equipo host, ejecute el cliente de SSH y conéctelo a la puerta de enlace de IoT.</span><span class="sxs-lookup"><span data-stu-id="c7961-130">On the host computer, run the SSH client and connect to the IoT gateway.</span></span>
1. <span data-ttu-id="c7961-131">Desbloquee Bluetooth al ejecutar el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c7961-131">Unblock Bluetooth by running the following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="c7961-132">Inicie el servicio Bluetooth en la puerta de enlace de IoT y escriba un shell de Bluetooth para configurar Bluetooth al ejecutar los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7961-132">Start the Bluetooth service on the IoT gateway and enter a Bluetooth shell to configure Bluetooth by running the following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="c7961-133">Encienda el controlador Bluetooth al ejecutar el siguiente comando en el shell de Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="c7961-133">Power on the Bluetooth controller by running the following command at the Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![Encender el controlador Bluetooth en la puerta de enlace de IoT con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="c7961-135">Inicie la detección de dispositivos Bluetooth cercanos al ejecutar el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="c7961-135">Start scanning for nearby Bluetooth devices by running the following command:</span></span>

   ```bash
   scan on
   ```

   ![Buscar dispositivos Bluetooth cercanos con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="c7961-137">Presione el botón de emparejamiento en el SensorTag.</span><span class="sxs-lookup"><span data-stu-id="c7961-137">Press the pairing button on the SensorTag.</span></span> <span data-ttu-id="c7961-138">El LED verde del SensorTag parpadea.</span><span class="sxs-lookup"><span data-stu-id="c7961-138">The green LED on the SensorTag flashes.</span></span>
1. <span data-ttu-id="c7961-139">En el shell de Bluetooth debería ver que se ha encontrado el SensorTag.</span><span class="sxs-lookup"><span data-stu-id="c7961-139">At the Bluetooth shell, you should see the SensorTag is found.</span></span> <span data-ttu-id="c7961-140">Anote la dirección MAC del SensorTag.</span><span class="sxs-lookup"><span data-stu-id="c7961-140">Make a note of the MAC address of the SensorTag.</span></span> <span data-ttu-id="c7961-141">En este ejemplo, la dirección MAC del SensorTag es `24:71:89:C0:7F:82`.</span><span class="sxs-lookup"><span data-stu-id="c7961-141">In this example, the MAC address of the SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="c7961-142">Detenga la detección al ejecutar el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="c7961-142">Turn off the scan by running the following command:</span></span>

   ```bash
   scan off
   ```

   ![Detener la detección de dispositivos Bluetooth cercanos con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-the-iot-gateway-to-the-sensortag"></a><span data-ttu-id="c7961-144">Iniciar una conexión Bluetooth desde la puerta de enlace de IoT al SensorTag</span><span class="sxs-lookup"><span data-stu-id="c7961-144">Initiate a Bluetooth connection from the IoT gateway to the SensorTag</span></span>

1. <span data-ttu-id="c7961-145">Conéctese al SensorTag mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="c7961-145">Connect to the SensorTag by running the following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![Conectarse al SensorTag con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="c7961-147">Desconéctese del SensorTag y salga del shell de Bluetooth al ejecutar los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7961-147">Disconnect from the SensorTag and exit the Bluetooth shell by running the following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![Desconectarse del SensorTag con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="c7961-149">Ha habilitado correctamente la conexión entre la puerta de enlace de IoT y el SensorTag.</span><span class="sxs-lookup"><span data-stu-id="c7961-149">You've successfully enabled the connection between the SensorTag and the IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-to-send-sensortag-data-to-your-iot-hub"></a><span data-ttu-id="c7961-150">Ejecutar una aplicación de ejemplo BLE para enviar datos del SensorTag a IoT Hub</span><span class="sxs-lookup"><span data-stu-id="c7961-150">Run a BLE sample application to send SensorTag data to your IoT hub</span></span>

<span data-ttu-id="c7961-151">Azure IoT Edge proporciona la aplicación de ejemplo Bluetooth Low Energy (BLE).</span><span class="sxs-lookup"><span data-stu-id="c7961-151">The Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="c7961-152">La aplicación de ejemplo recopila datos de la conexión BLE y los envía a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c7961-152">The sample application collects data from BLE connection and send the data to you IoT hub.</span></span> <span data-ttu-id="c7961-153">Para ejecutar la aplicación de ejemplo, tiene que:</span><span class="sxs-lookup"><span data-stu-id="c7961-153">To run the sample application, you need to:</span></span>

1. <span data-ttu-id="c7961-154">Configurar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c7961-154">Configure the sample application.</span></span>
1. <span data-ttu-id="c7961-155">Ejecutar la aplicación de ejemplo en la puerta de enlace de IoT.</span><span class="sxs-lookup"><span data-stu-id="c7961-155">Run the sample application on the IoT gateway.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="c7961-156">Configurar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c7961-156">Configure the sample application</span></span>

1. <span data-ttu-id="c7961-157">Vaya a la carpeta de la aplicación de ejemplo al ejecutar el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="c7961-157">Go to the folder of the sample application by running the following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="c7961-158">Abra el archivo de configuración al ejecutar el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c7961-158">Open the configuration file by running the following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="c7961-159">En el archivo de configuración, rellene los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="c7961-159">In the configuration file, fill in the following values:</span></span>

   <span data-ttu-id="c7961-160">**IoTHubName**: nombre del IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c7961-160">**IoTHubName**: The name of your IoT hub.</span></span>

   <span data-ttu-id="c7961-161">**IoTHubSuffix**: obtenga IoTHubSuffix de la clave principal de la cadena de conexión del dispositivo que ha anotado.</span><span class="sxs-lookup"><span data-stu-id="c7961-161">**IoTHubSuffix**: Get IoTHubSuffix from the primary key of the device connection string that you noted down.</span></span> <span data-ttu-id="c7961-162">Asegúrese de que obtiene la clave principal de la cadena de conexión del dispositivo y no la clave principal de la cadena de conexión de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c7961-162">Ensure that you get the primary key of the device connection string, not the primary key of your IoT hub connection string.</span></span> <span data-ttu-id="c7961-163">La clave principal de la cadena de conexión del dispositivo tiene el formato `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span><span class="sxs-lookup"><span data-stu-id="c7961-163">The primary key of the device connection string is in the format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="c7961-164">**Transport**: el valor predeterminada es `amqp`.</span><span class="sxs-lookup"><span data-stu-id="c7961-164">**Transport**: The default value is `amqp`.</span></span> <span data-ttu-id="c7961-165">Este valor muestra el protocolo durante el transporte.</span><span class="sxs-lookup"><span data-stu-id="c7961-165">This value shows the protocol during transpotation.</span></span> <span data-ttu-id="c7961-166">Podría ser `http`, `amqp` o `mqtt`.</span><span class="sxs-lookup"><span data-stu-id="c7961-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="c7961-167">**macAddress**: dirección MAC del SensorTag que ha anotado.</span><span class="sxs-lookup"><span data-stu-id="c7961-167">**macAddress**: The MAC address of the SensorTag that you noted down.</span></span>

   <span data-ttu-id="c7961-168">**deviceID**: identificador del dispositivo que ha creado en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c7961-168">**deviceID**: ID of the device that you created in your IoT hub.</span></span>

   <span data-ttu-id="c7961-169">**deviceKey**: clave principal de la cadena de conexión del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c7961-169">**deviceKey**: The primary key of the device connection string.</span></span>

   ![Completar el archivo config de la aplicación de ejemplo BLE](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="c7961-171">Presione `ESC` y escriba `:wq` para guardar el archivo.</span><span class="sxs-lookup"><span data-stu-id="c7961-171">Press `ESC` and type `:wq` to save the file.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="c7961-172">Ejecutar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c7961-172">Run the sample application</span></span>

1. <span data-ttu-id="c7961-173">Asegúrese de que el SensorTag está encendido.</span><span class="sxs-lookup"><span data-stu-id="c7961-173">Make sure the SensorTag is powered on.</span></span>
1. <span data-ttu-id="c7961-174">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c7961-174">Run the following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="c7961-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c7961-175">Next steps</span></span>

[<span data-ttu-id="c7961-176">Usar la puerta de enlace de IoT para la transformación de datos de sensor con Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="c7961-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
