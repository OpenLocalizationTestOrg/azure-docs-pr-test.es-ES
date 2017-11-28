---
title: "aaaConnect un tooAzure de frambuesa Pi IoT Suite con C simulada telemetría | Documentos de Microsoft"
description: "Utilice hello IoT Starter Kit de Microsoft Azure para hello frambuesa Pi 3 y conjunto de IoT de Azure. Use C tooconnect la solución de supervisión remota toohello de frambuesa Pi, enviar telemetría simulada toohello en la nube y responder toomethods invocado desde el panel de la solución de Hola."
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
ms.openlocfilehash: 3c4fa43b381385d1a7896cada34aa3aa0b8e5fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-c"></a><span data-ttu-id="086d2-104">Conectar la solución de supervisión remota toohello de frambuesa Pi 3 y enviar telemetría simulada mediante C</span><span class="sxs-lookup"><span data-stu-id="086d2-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send simulated telemetry using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="086d2-105">Este tutorial muestra cómo toouse Hola frambuesa Pi 3 toosimulate temperatura y humedad datos toosend toohello en la nube.</span><span class="sxs-lookup"><span data-stu-id="086d2-105">This tutorial shows you how toouse hello Raspberry Pi 3 toosimulate temperature and humidity data toosend toohello cloud.</span></span> <span data-ttu-id="086d2-106">tutorial de Hello usa:</span><span class="sxs-lookup"><span data-stu-id="086d2-106">hello tutorial uses:</span></span>

- <span data-ttu-id="086d2-107">Raspbian OS, lenguaje de programación de C de Hola y Hola IoT de Microsoft Azure SDK para C tooimplement un dispositivo de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="086d2-107">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
- <span data-ttu-id="086d2-108">supervisión remota de Hello IoT conjunto había preconfigurado solución como back-end de hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="086d2-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="086d2-109">Hola disposiciones de solución de supervisión remoto un conjunto de servicios de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="086d2-109">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="086d2-110">implementación de Hello refleja una arquitectura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="086d2-110">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="086d2-111">tooavoid cargos de consumo innecesario de Azure, elimine la instancia de la solución de hello preconfigurado en azureiotsuite.com cuando haya terminado con él.</span><span class="sxs-lookup"><span data-stu-id="086d2-111">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="086d2-112">Si necesita hello solución preconfigurada de nuevo, puede crearla fácilmente.</span><span class="sxs-lookup"><span data-stu-id="086d2-112">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="086d2-113">Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="086d2-113">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="086d2-114">Descargar y configurar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="086d2-114">Download and configure hello sample</span></span>

<span data-ttu-id="086d2-115">Ahora puede descargar y configurar la aplicación de cliente de supervisión remota de hello en el instalador de plataforma de frambuesa.</span><span class="sxs-lookup"><span data-stu-id="086d2-115">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="086d2-116">Clonar repositorios de Hola</span><span class="sxs-lookup"><span data-stu-id="086d2-116">Clone hello repositories</span></span>

<span data-ttu-id="086d2-117">Si aún no lo ha hecho, Hola clon necesario repositorios ejecutando Hola siguiente comandos en un terminal de su Pi:</span><span class="sxs-lookup"><span data-stu-id="086d2-117">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="086d2-118">Actualizar la cadena de conexión de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="086d2-118">Update hello device connection string</span></span>

<span data-ttu-id="086d2-119">Archivo de código fuente de ejemplo de Hola abierto en hello **nano** editor mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="086d2-119">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="086d2-120">Busque Hola siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="086d2-120">Locate hello following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="086d2-121">Reemplace los valores de marcador de posición de Hola por hello información de dispositivos y centro de IoT creado y guardado en el inicio de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="086d2-121">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="086d2-122">Guarde los cambios (**O Ctrl**, **ENTRAR**) y salga del editor hello (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="086d2-122">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="086d2-123">Compilar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="086d2-123">Build hello sample</span></span>

<span data-ttu-id="086d2-124">Instale los paquetes de requisitos previos de Hola para hello SDK de dispositivos de IoT de Azure de Microsoft para C con hello siguiente comandos en un terminal de hello frambuesa Pi:</span><span class="sxs-lookup"><span data-stu-id="086d2-124">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="086d2-125">Ahora puede compilar soluciones de ejemplo de Hola actualizado en hello frambuesa Pi:</span><span class="sxs-lookup"><span data-stu-id="086d2-125">You can now build hello updated sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
```

<span data-ttu-id="086d2-126">Ahora puede ejecutar el programa de ejemplo de Hola en hello frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="086d2-126">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="086d2-127">Escriba el comando de hello:</span><span class="sxs-lookup"><span data-stu-id="086d2-127">Enter hello command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="086d2-128">Hello resultados del ejemplo siguiente es un ejemplo de salida de hello, vea en línea de comandos de hello en hello frambuesa Pi:</span><span class="sxs-lookup"><span data-stu-id="086d2-128">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Salida de la aplicación Raspberry Pi][img-raspberry-output]

<span data-ttu-id="086d2-130">Presione **Ctrl-C** programa Hola de tooexit en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="086d2-130">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="086d2-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="086d2-131">Next steps</span></span>

<span data-ttu-id="086d2-132">Visite hello [centro de desarrollo de Azure IoT](https://azure.microsoft.com/develop/iot/) para obtener más ejemplos y documentación sobre IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="086d2-132">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-simulator/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
