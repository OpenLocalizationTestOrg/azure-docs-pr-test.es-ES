---
title: un conjunto de IoT de frambuesa Pi tooAzure aaaConnect con Node.js sensores reales | Documentos de Microsoft
description: "Utilice hello IoT Starter Kit de Microsoft Azure para hello frambuesa Pi 3 y conjunto de IoT de Azure. Usar Node.js tooconnect la solución de supervisión remota toohello de frambuesa Pi, enviar telemetría desde sensores toohello en la nube y responder toomethods invocado desde el panel de la solución de Hola."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 7ffb4a7a8c04b424a1f29170f4739d89f39a2429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a><span data-ttu-id="3aa10-104">Conectar la solución de supervisión remota toohello de frambuesa Pi 3 y enviar telemetría desde un sensor real mediante Node.js</span><span class="sxs-lookup"><span data-stu-id="3aa10-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="3aa10-105">Este tutorial muestra cómo toouse Hola IoT Starter Kit de Microsoft Azure para frambuesa Pi 3 toodevelop un lector de temperatura y humedad que puede comunicarse con la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aa10-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="3aa10-106">tutorial de Hello usa:</span><span class="sxs-lookup"><span data-stu-id="3aa10-106">hello tutorial uses:</span></span>

- <span data-ttu-id="3aa10-107">SO Raspbian, Hola Node.js lenguaje de programación y hello IoT de Microsoft Azure SDK para Node.js tooimplement un dispositivo de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3aa10-107">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="3aa10-108">supervisión remota de Hello IoT conjunto había preconfigurado solución como back-end de hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="3aa10-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="3aa10-109">Información general</span><span class="sxs-lookup"><span data-stu-id="3aa10-109">Overview</span></span>

<span data-ttu-id="3aa10-110">En este tutorial, se realizará Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3aa10-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="3aa10-111">Implemente una instancia de hello remoto supervisión solución preconfigurada tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3aa10-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="3aa10-112">Este paso implementa y configura varios servicios de Azure automáticamente.</span><span class="sxs-lookup"><span data-stu-id="3aa10-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="3aa10-113">Configurar el dispositivo y sensores toocommunicate con el equipo y Hola remoto de solución de supervisión.</span><span class="sxs-lookup"><span data-stu-id="3aa10-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="3aa10-114">Actualizar Hola ejemplo dispositivo código tooconnect toohello solución de supervisión y enviar telemetría que se puede ver en el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="3aa10-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="3aa10-115">Hola disposiciones de solución de supervisión remoto un conjunto de servicios de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3aa10-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="3aa10-116">implementación de Hello refleja una arquitectura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="3aa10-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="3aa10-117">tooavoid cargos de consumo innecesario de Azure, elimine la instancia de la solución de hello preconfigurado en azureiotsuite.com cuando haya terminado con él.</span><span class="sxs-lookup"><span data-stu-id="3aa10-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="3aa10-118">Si necesita hello solución preconfigurada de nuevo, puede crearla fácilmente.</span><span class="sxs-lookup"><span data-stu-id="3aa10-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="3aa10-119">Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="3aa10-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="3aa10-120">Descargar y configurar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="3aa10-120">Download and configure hello sample</span></span>

<span data-ttu-id="3aa10-121">Ahora puede descargar y configurar la aplicación de cliente de supervisión remota de hello en el instalador de plataforma de frambuesa.</span><span class="sxs-lookup"><span data-stu-id="3aa10-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="3aa10-122">Instalación de Node.js</span><span class="sxs-lookup"><span data-stu-id="3aa10-122">Install Node.js</span></span>

<span data-ttu-id="3aa10-123">Instale Node.js en Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="3aa10-123">Install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="3aa10-124">Hola IoT SDK para Node.js requiere la versión 0.11.5 de Node.js o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="3aa10-124">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="3aa10-125">Hello pasos siguientes muestran cómo tooinstall Node.js v6.10.2 en el instalador de plataforma de frambuesa:</span><span class="sxs-lookup"><span data-stu-id="3aa10-125">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="3aa10-126">Usar hello después tooupdate de comando su Pi frambuesa:</span><span class="sxs-lookup"><span data-stu-id="3aa10-126">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="3aa10-127">Usar hello después comando toodownload hello Node.js binarios tooyour frambuesa Pi:</span><span class="sxs-lookup"><span data-stu-id="3aa10-127">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="3aa10-128">Usar hello siguiendo los archivos binarios de comando tooinstall hello:</span><span class="sxs-lookup"><span data-stu-id="3aa10-128">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="3aa10-129">Usar hello después tooverify comando v6.10.2 Node.js se ha instalado correctamente:</span><span class="sxs-lookup"><span data-stu-id="3aa10-129">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="3aa10-130">Clonar repositorios de Hola</span><span class="sxs-lookup"><span data-stu-id="3aa10-130">Clone hello repositories</span></span>

<span data-ttu-id="3aa10-131">Si aún no lo ha hecho, Hola clon necesario repositorios ejecutando Hola siga los comandos en el instalador de plataforma:</span><span class="sxs-lookup"><span data-stu-id="3aa10-131">If you haven't already done so, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="3aa10-132">Actualizar la cadena de conexión de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="3aa10-132">Update hello device connection string</span></span>

<span data-ttu-id="3aa10-133">Archivo de código fuente de ejemplo de Hola abierto en hello **nano** editor mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="3aa10-133">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="3aa10-134">Busque la línea de saludo:</span><span class="sxs-lookup"><span data-stu-id="3aa10-134">Find hello line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="3aa10-135">Reemplace los valores de marcador de posición de Hola por hello información de dispositivos y centro de IoT creado y guardado en el inicio de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="3aa10-135">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="3aa10-136">Guarde los cambios (**O Ctrl**, **ENTRAR**) y salga del editor hello (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="3aa10-136">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="3aa10-137">Ejecutar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="3aa10-137">Run hello sample</span></span>

<span data-ttu-id="3aa10-138">Siguiente ejecución Hola comandos paquetes de requisitos previos de hello tooinstall de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="3aa10-138">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

<span data-ttu-id="3aa10-139">Ahora puede ejecutar el programa de ejemplo de Hola en hello frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="3aa10-139">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="3aa10-140">Escriba el comando de hello:</span><span class="sxs-lookup"><span data-stu-id="3aa10-140">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="3aa10-141">Hello resultados del ejemplo siguiente es un ejemplo de salida de hello, vea en línea de comandos de hello en hello frambuesa Pi:</span><span class="sxs-lookup"><span data-stu-id="3aa10-141">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Salida de la aplicación Raspberry Pi][img-raspberry-output]

<span data-ttu-id="3aa10-143">Presione **Ctrl-C** programa Hola de tooexit en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="3aa10-143">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="3aa10-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3aa10-144">Next steps</span></span>

<span data-ttu-id="3aa10-145">Visite hello [centro de desarrollo de Azure IoT](https://azure.microsoft.com/develop/iot/) para obtener más ejemplos y documentación sobre IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="3aa10-145">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
