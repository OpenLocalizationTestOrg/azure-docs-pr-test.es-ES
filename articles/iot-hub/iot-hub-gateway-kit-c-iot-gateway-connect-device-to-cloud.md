---
title: aaaUse un tooconnect de puerta de enlace de IoT un centro de IoT de dispositivo tooAzure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Intel NUC como un tooconnect de puerta de enlace de IoT un SensorTag de TI y envío sensor datos tooAzure centro de IoT en hello en la nube."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: puerta de enlace de IOT conectar dispositivo toocloud
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a><span data-ttu-id="0ea9c-104">Usar IoT puerta de enlace tooconnect cosas toohello cloud - SensorTag tooAzure centro de IoT</span><span class="sxs-lookup"><span data-stu-id="0ea9c-104">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="0ea9c-105">Antes de empezar este tutorial, asegúrese de haber completado [Set up Intel NUC as an IoT gateway (Configurar Intel NUC como una puerta de enlace de IoT)](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="0ea9c-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="0ea9c-106">En [configurar Intel NUC como una puerta de enlace de IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), configura Hola Intel NUC dispositivo como una puerta de enlace de IoT.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up hello Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0ea9c-107">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="0ea9c-107">What you will learn</span></span>

<span data-ttu-id="0ea9c-108">Aprenderá cómo toouse una tooconnect de puerta de enlace de IoT un centro de IoT de tooAzure Texas instrumentos SensorTag (CC2650STK).</span><span class="sxs-lookup"><span data-stu-id="0ea9c-108">You learn how toouse an IoT gateway tooconnect a Texas Instruments SensorTag (CC2650STK) tooAzure IoT Hub.</span></span> <span data-ttu-id="0ea9c-109">puerta de enlace de IoT Hola envía temperatura y recopilan los datos de humedad de hello SensorTag tooAzure centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-109">hello IoT gateway sends temperature and humidity data collected from hello SensorTag tooAzure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="0ea9c-110">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="0ea9c-110">What you will do</span></span>

- <span data-ttu-id="0ea9c-111">Cree un Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-111">Create an IoT hub.</span></span>
- <span data-ttu-id="0ea9c-112">Registrar un dispositivo en el centro de IoT de Hola para hello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-112">Register a device in hello IoT hub for hello SensorTag.</span></span>
- <span data-ttu-id="0ea9c-113">Habilitar conexión Hola entre la puerta de enlace de IoT de Hola y Hola SensorTag.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-113">Enable hello connection between hello IoT gateway and hello SensorTag.</span></span>
- <span data-ttu-id="0ea9c-114">Ejecute un centro de IoT Bilitar ejemplo aplicación toosend SensorTag datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-114">Run a BLE sample application toosend SensorTag data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0ea9c-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="0ea9c-115">What you need</span></span>

- <span data-ttu-id="0ea9c-116">Tutorial [Set up Intel NUC as an IoT gateway (Configurar Intel NUC como una puerta de enlace de IoT)](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completado en el que haya configurado Intel NUC como una puerta de enlace de IoT.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="0ea9c-117">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-117">An active Azure subscription.</span></span> <span data-ttu-id="0ea9c-118">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="0ea9c-119">Un cliente de SSH que se ejecute en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="0ea9c-120">En Windows se recomienda PuTTY.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="0ea9c-121">Linux y macOS ya vienen con un cliente de SSH.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="0ea9c-122">dirección IP de Hola y Hola username y password tooaccess Hola puerta de enlace de cliente de SSH Hola.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-122">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
- <span data-ttu-id="0ea9c-123">Una conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="0ea9c-124">Aquí se registra este nuevo dispositivo para el SensorTag</span><span class="sxs-lookup"><span data-stu-id="0ea9c-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a><span data-ttu-id="0ea9c-125">Habilitar conexión Hola entre la puerta de enlace de IoT de Hola y Hola SensorTag</span><span class="sxs-lookup"><span data-stu-id="0ea9c-125">Enable hello connection between hello IoT gateway and hello SensorTag</span></span>

<span data-ttu-id="0ea9c-126">En esta sección, realizar Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="0ea9c-126">In this section, you perform hello following tasks:</span></span>

- <span data-ttu-id="0ea9c-127">Obtener dirección MAC de Hola de hello SensorTag conexión Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-127">Get hello MAC address of hello SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="0ea9c-128">Iniciar una conexión de Bluetooth de toohello de puerta de enlace de IoT de hello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-128">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag.</span></span>

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a><span data-ttu-id="0ea9c-129">Obtener dirección MAC de Hola de hello SensorTag para conexión de Bluetooth</span><span class="sxs-lookup"><span data-stu-id="0ea9c-129">Get hello MAC address of hello SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="0ea9c-130">En el equipo de host de hello, ejecutar el cliente de SSH de Hola y conectar la puerta de enlace de IoT toohello.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-130">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="0ea9c-131">Desbloquear Bluetooth ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0ea9c-131">Unblock Bluetooth by running hello following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="0ea9c-132">Iniciar el servicio de Bluetooth de hello en la puerta de enlace de IoT de Hola y escriba un tooconfigure de shell de Bluetooth Bluetooth ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="0ea9c-132">Start hello Bluetooth service on hello IoT gateway and enter a Bluetooth shell tooconfigure Bluetooth by running hello following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="0ea9c-133">Encendido de controlador de Bluetooth Hola ejecutando Hola siguiente comando en hello Bluetooth shell:</span><span class="sxs-lookup"><span data-stu-id="0ea9c-133">Power on hello Bluetooth controller by running hello following command at hello Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![encendido de controlador de Bluetooth hello en puerta de enlace de IoT de hello con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="0ea9c-135">Iniciar buscar dispositivos Bluetooth cercanos ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0ea9c-135">Start scanning for nearby Bluetooth devices by running hello following command:</span></span>

   ```bash
   scan on
   ```

   ![Buscar dispositivos Bluetooth cercanos con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="0ea9c-137">Presione el botón en hello SensorTag de emparejamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-137">Press hello pairing button on hello SensorTag.</span></span> <span data-ttu-id="0ea9c-138">Hola verde LED en hello SensorTag parpadea.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-138">hello green LED on hello SensorTag flashes.</span></span>
1. <span data-ttu-id="0ea9c-139">En el shell de Bluetooth hello, debería ver Hola que sensortag se encuentra.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-139">At hello Bluetooth shell, you should see hello SensorTag is found.</span></span> <span data-ttu-id="0ea9c-140">Tome nota de hello dirección MAC de hello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-140">Make a note of hello MAC address of hello SensorTag.</span></span> <span data-ttu-id="0ea9c-141">En este ejemplo, hello dirección MAC de hello SensorTag es `24:71:89:C0:7F:82`.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-141">In this example, hello MAC address of hello SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="0ea9c-142">Desactivar el examen de hello ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="0ea9c-142">Turn off hello scan by running hello following command:</span></span>

   ```bash
   scan off
   ```

   ![Detener la detección de dispositivos Bluetooth cercanos con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a><span data-ttu-id="0ea9c-144">Iniciar una conexión de Bluetooth de toohello de puerta de enlace de IoT de hello SensorTag</span><span class="sxs-lookup"><span data-stu-id="0ea9c-144">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag</span></span>

1. <span data-ttu-id="0ea9c-145">Conectarse toohello SensorTag, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="0ea9c-145">Connect toohello SensorTag by running hello following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![Conectar toohello SensorTag con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="0ea9c-147">Desconectarse de hello SensorTag y ejecutar salir del shell de Bluetooth Hola Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="0ea9c-147">Disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![Desconectarse de hello SensorTag con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="0ea9c-149">Conexión Hola entre la puerta de enlace de IoT de Hola y Hola SensorTag haya habilitado correctamente.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-149">You've successfully enabled hello connection between hello SensorTag and hello IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a><span data-ttu-id="0ea9c-150">Ejecutar un centro de IoT Bilitar ejemplo aplicación toosend SensorTag datos tooyour</span><span class="sxs-lookup"><span data-stu-id="0ea9c-150">Run a BLE sample application toosend SensorTag data tooyour IoT hub</span></span>

<span data-ttu-id="0ea9c-151">Borde de IoT de Azure proporciona Hola aplicación de ejemplo de Bluetooth baja energía (n).</span><span class="sxs-lookup"><span data-stu-id="0ea9c-151">hello Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="0ea9c-152">aplicación de ejemplo de Hola recopila datos de conexión Bilitar y centro de IoT de hello datos tooyou de envío.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-152">hello sample application collects data from BLE connection and send hello data tooyou IoT hub.</span></span> <span data-ttu-id="0ea9c-153">aplicación de ejemplo de Hola toorun, debe:</span><span class="sxs-lookup"><span data-stu-id="0ea9c-153">toorun hello sample application, you need to:</span></span>

1. <span data-ttu-id="0ea9c-154">Configurar la aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-154">Configure hello sample application.</span></span>
1. <span data-ttu-id="0ea9c-155">Ejecutar la aplicación de ejemplo de Hola en puerta de enlace de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-155">Run hello sample application on hello IoT gateway.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="0ea9c-156">Configurar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="0ea9c-156">Configure hello sample application</span></span>

1. <span data-ttu-id="0ea9c-157">Vaya toohello carpeta de aplicación de ejemplo de Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0ea9c-157">Go toohello folder of hello sample application by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="0ea9c-158">Abra el archivo de configuración de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0ea9c-158">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="0ea9c-159">En el archivo de configuración de hello, rellene Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="0ea9c-159">In hello configuration file, fill in hello following values:</span></span>

   <span data-ttu-id="0ea9c-160">**IoTHubName**: nombre de Hola de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-160">**IoTHubName**: hello name of your IoT hub.</span></span>

   <span data-ttu-id="0ea9c-161">**IoTHubSuffix**: IoTHubSuffix obtener de la clave principal Hola de cadena de conexión de dispositivo de Hola que anotó hacia abajo.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-161">**IoTHubSuffix**: Get IoTHubSuffix from hello primary key of hello device connection string that you noted down.</span></span> <span data-ttu-id="0ea9c-162">Asegurarse de que obtener la clave principal de Hola de cadena de conexión de dispositivo de hello, no Hola clave principal de la cadena de conexión de base de datos central de IoT.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-162">Ensure that you get hello primary key of hello device connection string, not hello primary key of your IoT hub connection string.</span></span> <span data-ttu-id="0ea9c-163">clave principal de Hola de cadena de conexión de dispositivo de hello está en formato de Hola de `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-163">hello primary key of hello device connection string is in hello format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="0ea9c-164">**Transporte**: valor predeterminado de hello es `amqp`.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-164">**Transport**: hello default value is `amqp`.</span></span> <span data-ttu-id="0ea9c-165">Este valor muestra el protocolo de Hola durante transpotation.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-165">This value shows hello protocol during transpotation.</span></span> <span data-ttu-id="0ea9c-166">Podría ser `http`, `amqp` o `mqtt`.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="0ea9c-167">**macAddress**: Hola dirección MAC de hello SensorTag que anotó hacia abajo.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-167">**macAddress**: hello MAC address of hello SensorTag that you noted down.</span></span>

   <span data-ttu-id="0ea9c-168">**Id. de dispositivo**: Id. de dispositivo de Hola que creó en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-168">**deviceID**: ID of hello device that you created in your IoT hub.</span></span>

   <span data-ttu-id="0ea9c-169">**deviceKey**: clave principal de Hola de cadena de conexión de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-169">**deviceKey**: hello primary key of hello device connection string.</span></span>

   ![Archivo de configuración de hello completa del programa Hola a aplicación de ejemplo BLE](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="0ea9c-171">Presione `ESC` y el tipo de `:wq` archivo de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-171">Press `ESC` and type `:wq` toosave hello file.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="0ea9c-172">Ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="0ea9c-172">Run hello sample application</span></span>

1. <span data-ttu-id="0ea9c-173">Asegúrese de hello seguro que sensortag está encendida.</span><span class="sxs-lookup"><span data-stu-id="0ea9c-173">Make sure hello SensorTag is powered on.</span></span>
1. <span data-ttu-id="0ea9c-174">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="0ea9c-174">Run hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="0ea9c-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0ea9c-175">Next steps</span></span>

[<span data-ttu-id="0ea9c-176">Usar la puerta de enlace de IoT para la transformación de datos de sensor con Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="0ea9c-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
