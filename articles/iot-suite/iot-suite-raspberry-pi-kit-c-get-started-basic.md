---
title: "Conexión de Raspberry Pi al Conjunto de aplicaciones de IoT de Azure mediante C con sensores reales | Microsoft Docs"
description: "Use el Starter Kit de IoT de Microsoft Azure para Raspberry Pi 3 y el Conjunto de aplicaciones de IoT de Azure. Use C para conectar su Raspberry Pi a la solución de supervisión remota, enviar telemetría desde sensores a la nube y responder a los métodos invocados desde el panel de la solución."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 418108e8236518d2671abca0f06f1ae8159d6442
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a><span data-ttu-id="8c418-104">Conexión de Raspberry Pi 3 a la solución de supervisión remota y envío de telemetría desde un sensor real mediante C</span><span class="sxs-lookup"><span data-stu-id="8c418-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send telemetry from a real sensor using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="8c418-105">Este tutorial muestra cómo usar el Starter Kit de IoT de Microsoft Azure para Raspberry Pi 3 para desarrollar un lector de temperatura y humedad que pueda comunicarse con la nube.</span><span class="sxs-lookup"><span data-stu-id="8c418-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to develop a temperature and humidity reader that can communicate with the cloud.</span></span> <span data-ttu-id="8c418-106">El tutorial usa:</span><span class="sxs-lookup"><span data-stu-id="8c418-106">The tutorial uses:</span></span>

- <span data-ttu-id="8c418-107">El SO Raspbian, el lenguaje de programación C y el SDK de IoT de Microsoft Azure para C para implementar un dispositivo de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8c418-107">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span></span>
- <span data-ttu-id="8c418-108">La solución preconfigurada de supervisión remota del Conjunto de aplicaciones de IoT como el back-end basado en la nube.</span><span class="sxs-lookup"><span data-stu-id="8c418-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="8c418-109">Información general</span><span class="sxs-lookup"><span data-stu-id="8c418-109">Overview</span></span>

<span data-ttu-id="8c418-110">En este tutorial, va a completar los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="8c418-110">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="8c418-111">Implemente una instancia de la solución preconfigurada de supervisión remota en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="8c418-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="8c418-112">Este paso implementa y configura varios servicios de Azure automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8c418-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="8c418-113">Configure el dispositivo y los sensores para que se comunique con el equipo y la solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="8c418-113">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="8c418-114">Actualice el código del dispositivo de ejemplo para que se conecte a la solución de supervisión remota y envíe telemetría que aparezca en el panel de soluciones.</span><span class="sxs-lookup"><span data-stu-id="8c418-114">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="8c418-115">La solución de supervisión remota proporciona un conjunto de servicios de Azure de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="8c418-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="8c418-116">La implementación refleja una arquitectura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="8c418-116">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="8c418-117">Para evitar cobros de consumo innecesarios de Azure, elimine la instancia de la solución preconfigurada en azureiotsuite.com cuando haya terminado con ella.</span><span class="sxs-lookup"><span data-stu-id="8c418-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="8c418-118">Si necesita la solución preconfigurada de nuevo, puede crearla fácilmente.</span><span class="sxs-lookup"><span data-stu-id="8c418-118">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="8c418-119">Para más información sobre cómo reducir el consumo mientras se ejecuta la solución de supervisión remota, consulte [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configuración de soluciones preconfiguradas del Conjunto de aplicaciones de IoT de Azure para fines de demostración).</span><span class="sxs-lookup"><span data-stu-id="8c418-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="8c418-120">Descarga y configuración del ejemplo</span><span class="sxs-lookup"><span data-stu-id="8c418-120">Download and configure the sample</span></span>

<span data-ttu-id="8c418-121">Ahora puede descargar y configurar la aplicación de cliente de supervisión remota en su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="8c418-121">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-the-repositories"></a><span data-ttu-id="8c418-122">Clonación de repositorios</span><span class="sxs-lookup"><span data-stu-id="8c418-122">Clone the repositories</span></span>

<span data-ttu-id="8c418-123">Si aún no lo ha hecho, clone los repositorios necesarios mediante la ejecución de los siguientes comandos en un terminal en su Pi:</span><span class="sxs-lookup"><span data-stu-id="8c418-123">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="8c418-124">Actualización de la cadena de conexión de dispositivo</span><span class="sxs-lookup"><span data-stu-id="8c418-124">Update the device connection string</span></span>

<span data-ttu-id="8c418-125">Abra el archivo de código fuente de ejemplo en el editor **nano** con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="8c418-125">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="8c418-126">Busque las líneas siguientes:</span><span class="sxs-lookup"><span data-stu-id="8c418-126">Locate the following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="8c418-127">Reemplace los valores de marcador de posición por el dispositivo y la información de IoT Hub que creó y guardó al principio de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8c418-127">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="8c418-128">Guarde los cambios (**Ctrl-O**, **ENTRAR**) y salga del editor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="8c418-128">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="build-the-sample"></a><span data-ttu-id="8c418-129">Compilación del ejemplo</span><span class="sxs-lookup"><span data-stu-id="8c418-129">Build the sample</span></span>

<span data-ttu-id="8c418-130">Instale los paquetes de requisitos previos para el SDK de dispositivo IoT de Microsoft Azure para C ejecutando los comandos siguientes en un terminal en Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="8c418-130">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="8c418-131">Ahora puede compilar la solución de ejemplo actualizada en Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="8c418-131">You can now build the updated sample solution on the Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

<span data-ttu-id="8c418-132">Ahora puede ejecutar el programa de ejemplo en Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="8c418-132">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="8c418-133">Escriba el comando:</span><span class="sxs-lookup"><span data-stu-id="8c418-133">Enter the command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="8c418-134">La salida de ejemplo siguiente es un ejemplo de la salida que se ve en el símbolo del sistema en Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="8c418-134">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Salida de la aplicación Raspberry Pi][img-raspberry-output]

<span data-ttu-id="8c418-136">Presione **Ctrl-C** para salir del programa en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="8c418-136">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="8c418-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8c418-137">Next steps</span></span>

<span data-ttu-id="8c418-138">Visite el [Centro para desarrolladores de IoT de Azure](https://azure.microsoft.com/develop/iot/) para obtener más ejemplos y la documentación de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="8c418-138">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md