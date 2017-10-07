---
title: un conjunto de IoT de frambuesa Pi tooAzure aaaConnect utilizando C con sensores reales | Documentos de Microsoft
description: "Utilice hello IoT Starter Kit de Microsoft Azure para hello frambuesa Pi 3 y conjunto de IoT de Azure. Use C tooconnect la solución de supervisión remota toohello de frambuesa Pi, enviar telemetría desde sensores toohello en la nube y responder toomethods invocado desde el panel de la solución de Hola."
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
ms.openlocfilehash: 7dac55ae5fde4c6f8e3ea6a7debf9a6822dc07ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a><span data-ttu-id="e77d7-104">Conectar la solución de supervisión remota toohello de frambuesa Pi 3 y enviar telemetría desde un sensor real mediante C</span><span class="sxs-lookup"><span data-stu-id="e77d7-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="e77d7-105">Este tutorial muestra cómo toouse Hola IoT Starter Kit de Microsoft Azure para frambuesa Pi 3 toodevelop un lector de temperatura y humedad que puede comunicarse con la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="e77d7-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="e77d7-106">tutorial de Hello usa:</span><span class="sxs-lookup"><span data-stu-id="e77d7-106">hello tutorial uses:</span></span>

- <span data-ttu-id="e77d7-107">Raspbian OS, lenguaje de programación de C de Hola y Hola IoT de Microsoft Azure SDK para C tooimplement un dispositivo de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e77d7-107">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
- <span data-ttu-id="e77d7-108">supervisión remota de Hello IoT conjunto había preconfigurado solución como back-end de hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="e77d7-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="e77d7-109">Información general</span><span class="sxs-lookup"><span data-stu-id="e77d7-109">Overview</span></span>

<span data-ttu-id="e77d7-110">En este tutorial, se realizará Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e77d7-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="e77d7-111">Implemente una instancia de hello remoto supervisión solución preconfigurada tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="e77d7-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="e77d7-112">Este paso implementa y configura varios servicios de Azure automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e77d7-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="e77d7-113">Configurar el dispositivo y sensores toocommunicate con el equipo y Hola remoto de solución de supervisión.</span><span class="sxs-lookup"><span data-stu-id="e77d7-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="e77d7-114">Actualizar Hola ejemplo dispositivo código tooconnect toohello solución de supervisión y enviar telemetría que se puede ver en el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="e77d7-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="e77d7-115">Hola disposiciones de solución de supervisión remoto un conjunto de servicios de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="e77d7-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="e77d7-116">implementación de Hello refleja una arquitectura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="e77d7-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="e77d7-117">tooavoid cargos de consumo innecesario de Azure, elimine la instancia de la solución de hello preconfigurado en azureiotsuite.com cuando haya terminado con él.</span><span class="sxs-lookup"><span data-stu-id="e77d7-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="e77d7-118">Si necesita hello solución preconfigurada de nuevo, puede crearla fácilmente.</span><span class="sxs-lookup"><span data-stu-id="e77d7-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="e77d7-119">Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="e77d7-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="e77d7-120">Descargar y configurar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="e77d7-120">Download and configure hello sample</span></span>

<span data-ttu-id="e77d7-121">Ahora puede descargar y configurar la aplicación de cliente de supervisión remota de hello en el instalador de plataforma de frambuesa.</span><span class="sxs-lookup"><span data-stu-id="e77d7-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="e77d7-122">Clonar repositorios de Hola</span><span class="sxs-lookup"><span data-stu-id="e77d7-122">Clone hello repositories</span></span>

<span data-ttu-id="e77d7-123">Si aún no lo ha hecho, Hola clon necesario repositorios ejecutando Hola siguiente comandos en un terminal de su Pi:</span><span class="sxs-lookup"><span data-stu-id="e77d7-123">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="e77d7-124">Actualizar la cadena de conexión de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="e77d7-124">Update hello device connection string</span></span>

<span data-ttu-id="e77d7-125">Archivo de código fuente de ejemplo de Hola abierto en hello **nano** editor mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e77d7-125">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="e77d7-126">Busque Hola siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="e77d7-126">Locate hello following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="e77d7-127">Reemplace los valores de marcador de posición de Hola por hello información de dispositivos y centro de IoT creado y guardado en el inicio de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e77d7-127">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="e77d7-128">Guarde los cambios (**O Ctrl**, **ENTRAR**) y salga del editor hello (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="e77d7-128">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="e77d7-129">Compilar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="e77d7-129">Build hello sample</span></span>

<span data-ttu-id="e77d7-130">Instale los paquetes de requisitos previos de Hola para hello SDK de dispositivos de IoT de Azure de Microsoft para C con hello siguiente comandos en un terminal de hello frambuesa Pi:</span><span class="sxs-lookup"><span data-stu-id="e77d7-130">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="e77d7-131">Ahora puede compilar soluciones de ejemplo de Hola actualizado en hello frambuesa Pi:</span><span class="sxs-lookup"><span data-stu-id="e77d7-131">You can now build hello updated sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

<span data-ttu-id="e77d7-132">Ahora puede ejecutar el programa de ejemplo de Hola en hello frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="e77d7-132">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="e77d7-133">Escriba el comando de hello:</span><span class="sxs-lookup"><span data-stu-id="e77d7-133">Enter hello command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="e77d7-134">Hello resultados del ejemplo siguiente es un ejemplo de salida de hello, vea en línea de comandos de hello en hello frambuesa Pi:</span><span class="sxs-lookup"><span data-stu-id="e77d7-134">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Salida de la aplicación Raspberry Pi][img-raspberry-output]

<span data-ttu-id="e77d7-136">Presione **Ctrl-C** programa Hola de tooexit en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="e77d7-136">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="e77d7-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e77d7-137">Next steps</span></span>

<span data-ttu-id="e77d7-138">Visite hello [centro de desarrollo de Azure IoT](https://azure.microsoft.com/develop/iot/) para obtener más ejemplos y documentación sobre IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="e77d7-138">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
