---
title: aaaConnect un tooAzure frambuesa Pi Suite IoT con Node.js toosupport firmware actualiza | Documentos de Microsoft
description: "Utilice hello IoT Starter Kit de Microsoft Azure para hello frambuesa Pi 3 y conjunto de IoT de Azure. Usar Node.js tooconnect la solución de supervisión remota toohello de frambuesa Pi, enviar telemetría desde sensores toohello en la nube y realizar una actualización de firmware remoto."
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
ms.openlocfilehash: 43bd3f16ee3d292cd9cffa8bfe7d4ca721e5c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a><span data-ttu-id="fc513-104">Conectar la solución de supervisión remota toohello de frambuesa Pi 3 y habilitar las actualizaciones de firmware remotas mediante Node.js</span><span class="sxs-lookup"><span data-stu-id="fc513-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and enable remote firmware updates using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="fc513-105">Este tutorial muestra cómo toouse Hola IoT Starter Kit de Microsoft Azure para frambuesa Pi 3 para:</span><span class="sxs-lookup"><span data-stu-id="fc513-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="fc513-106">Desarrollar un lector de temperatura y humedad que puede comunicarse con la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc513-106">Develop a temperature and humidity reader that can communicate with hello cloud.</span></span>
* <span data-ttu-id="fc513-107">Habilitar y realice una aplicación de cliente remoto firmware update tooupdate Hola Hola frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="fc513-107">Enable and perform a remote firmware update tooupdate hello client application on hello Raspberry Pi.</span></span>

<span data-ttu-id="fc513-108">tutorial de Hello usa:</span><span class="sxs-lookup"><span data-stu-id="fc513-108">hello tutorial uses:</span></span>

- <span data-ttu-id="fc513-109">SO Raspbian, Hola Node.js lenguaje de programación y hello IoT de Microsoft Azure SDK para Node.js tooimplement un dispositivo de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="fc513-109">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="fc513-110">supervisión remota de Hello IoT conjunto había preconfigurado solución como back-end de hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="fc513-110">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="fc513-111">Información general</span><span class="sxs-lookup"><span data-stu-id="fc513-111">Overview</span></span>

<span data-ttu-id="fc513-112">En este tutorial, se realizará Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="fc513-112">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="fc513-113">Implemente una instancia de hello remoto supervisión solución preconfigurada tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc513-113">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="fc513-114">Este paso implementa y configura varios servicios de Azure automáticamente.</span><span class="sxs-lookup"><span data-stu-id="fc513-114">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="fc513-115">Configurar el dispositivo y sensores toocommunicate con el equipo y Hola remoto de solución de supervisión.</span><span class="sxs-lookup"><span data-stu-id="fc513-115">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="fc513-116">Actualizar Hola ejemplo dispositivo código tooconnect toohello solución de supervisión y enviar telemetría que se puede ver en el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc513-116">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>
- <span data-ttu-id="fc513-117">Usar dispositivos de ejemplo Hola código tooupdate Hola cliente aplicación.</span><span class="sxs-lookup"><span data-stu-id="fc513-117">Use hello sample device code tooupdate hello client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="fc513-118">Hola disposiciones de solución de supervisión remoto un conjunto de servicios de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc513-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="fc513-119">implementación de Hello refleja una arquitectura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="fc513-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="fc513-120">tooavoid cargos de consumo innecesario de Azure, elimine la instancia de la solución de hello preconfigurado en azureiotsuite.com cuando haya terminado con él.</span><span class="sxs-lookup"><span data-stu-id="fc513-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="fc513-121">Si necesita hello solución preconfigurada de nuevo, puede crearla fácilmente.</span><span class="sxs-lookup"><span data-stu-id="fc513-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="fc513-122">Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="fc513-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="fc513-123">Descargar y configurar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="fc513-123">Download and configure hello sample</span></span>

<span data-ttu-id="fc513-124">Ahora puede descargar y configurar la aplicación de cliente de supervisión remota de hello en el instalador de plataforma de frambuesa.</span><span class="sxs-lookup"><span data-stu-id="fc513-124">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="fc513-125">Instalación de Node.js</span><span class="sxs-lookup"><span data-stu-id="fc513-125">Install Node.js</span></span>

<span data-ttu-id="fc513-126">Si aún no lo ha hecho, instale Node.js en su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="fc513-126">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="fc513-127">Hola IoT SDK para Node.js requiere la versión 0.11.5 de Node.js o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="fc513-127">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="fc513-128">Hello pasos siguientes muestran cómo tooinstall Node.js v6.10.2 en el instalador de plataforma de frambuesa:</span><span class="sxs-lookup"><span data-stu-id="fc513-128">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="fc513-129">Usar hello después tooupdate de comando su Pi frambuesa:</span><span class="sxs-lookup"><span data-stu-id="fc513-129">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="fc513-130">Usar hello después comando toodownload hello Node.js binarios tooyour frambuesa Pi:</span><span class="sxs-lookup"><span data-stu-id="fc513-130">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="fc513-131">Usar hello siguiendo los archivos binarios de comando tooinstall hello:</span><span class="sxs-lookup"><span data-stu-id="fc513-131">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="fc513-132">Usar hello después tooverify comando v6.10.2 Node.js se ha instalado correctamente:</span><span class="sxs-lookup"><span data-stu-id="fc513-132">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="fc513-133">Clonar repositorios de Hola</span><span class="sxs-lookup"><span data-stu-id="fc513-133">Clone hello repositories</span></span>

<span data-ttu-id="fc513-134">Si aún no lo ha hecho lo ha hecho, Hola clon necesario repositorios ejecutando Hola siga los comandos en el instalador de plataforma:</span><span class="sxs-lookup"><span data-stu-id="fc513-134">If you haven't done so already, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="fc513-135">Actualizar la cadena de conexión de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="fc513-135">Update hello device connection string</span></span>

<span data-ttu-id="fc513-136">Archivo de configuración de ejemplo de Hola abierto en hello **nano** editor mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fc513-136">Open hello sample configuration file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="fc513-137">Reemplace los valores de marcador de posición de hello con Id. de dispositivo de Hola y la información de centro de IoT creado y guardado en el inicio de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="fc513-137">Replace hello placeholder values with hello device id and IoT Hub information you created and saved at hello start of this tutorial.</span></span>

<span data-ttu-id="fc513-138">Cuando haya terminado, contenido de hello del archivo de deviceinfo hello debería ser similar Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fc513-138">When you are done, hello contents of hello deviceinfo file should look like hello following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="fc513-139">Guarde los cambios (**O Ctrl**, **ENTRAR**) y salga del editor hello (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="fc513-139">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="fc513-140">Ejecutar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="fc513-140">Run hello sample</span></span>

<span data-ttu-id="fc513-141">Siguiente ejecución Hola comandos paquetes de requisitos previos de hello tooinstall de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="fc513-141">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

<span data-ttu-id="fc513-142">Ahora puede ejecutar el programa de ejemplo de Hola en hello frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="fc513-142">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="fc513-143">Escriba el comando de hello:</span><span class="sxs-lookup"><span data-stu-id="fc513-143">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

<span data-ttu-id="fc513-144">Hello resultados del ejemplo siguiente es un ejemplo de salida de hello, vea en línea de comandos de hello en hello frambuesa Pi:</span><span class="sxs-lookup"><span data-stu-id="fc513-144">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Salida de la aplicación Raspberry Pi][img-raspberry-output]

<span data-ttu-id="fc513-146">Presione **Ctrl-C** programa Hola de tooexit en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="fc513-146">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="fc513-147">En el panel de la solución de hello, haga clic en **dispositivos** toovisit hello **dispositivos** página.</span><span class="sxs-lookup"><span data-stu-id="fc513-147">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="fc513-148">Seleccione el instalador de plataforma de frambuesa Hola **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="fc513-148">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="fc513-149">A continuación, elija **Métodos**:</span><span class="sxs-lookup"><span data-stu-id="fc513-149">Then choose **Methods**:</span></span>

    ![Lista de dispositivos en el panel][img-list-devices]

1. <span data-ttu-id="fc513-151">En hello **invocar método** página, elija **InitiateFirmwareUpdate** en hello **método** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="fc513-151">On hello **Invoke Method** page, choose **InitiateFirmwareUpdate** in hello **Method** dropdown.</span></span>

1. <span data-ttu-id="fc513-152">Hola **FWPackageURI** , escriba **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span><span class="sxs-lookup"><span data-stu-id="fc513-152">In hello **FWPackageURI** field, enter **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span></span> <span data-ttu-id="fc513-153">Este archivo contiene la implementación de hello de la versión 2.0 del firmware de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc513-153">This file contains hello implementation of version 2.0 of hello firmware.</span></span>

1. <span data-ttu-id="fc513-154">Elija **Invocar método**.</span><span class="sxs-lookup"><span data-stu-id="fc513-154">Choose **InvokeMethod**.</span></span> <span data-ttu-id="fc513-155">aplicación de Hello en hello frambuesa Pi envía un panel de solución de toohello espera de confirmación.</span><span class="sxs-lookup"><span data-stu-id="fc513-155">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard.</span></span> <span data-ttu-id="fc513-156">A continuación, inicia el proceso de actualización de firmware de hello descargando la nueva versión del firmware de Hola de hello:</span><span class="sxs-lookup"><span data-stu-id="fc513-156">It then starts hello firmware update process by downloading hello new version of hello firmware:</span></span>

    ![Mostrar el historial de métodos][img-method-history]

## <a name="observe-hello-firmware-update-process"></a><span data-ttu-id="fc513-158">Observar el proceso de actualización de firmware de Hola</span><span class="sxs-lookup"><span data-stu-id="fc513-158">Observe hello firmware update process</span></span>

<span data-ttu-id="fc513-159">Puede observar el proceso de actualización de firmware de hello mientras se ejecuta en el dispositivo de Hola y viendo Hola notificado propiedades en el panel de la solución de hello:</span><span class="sxs-lookup"><span data-stu-id="fc513-159">You can observe hello firmware update process as it runs on hello device and by viewing hello reported properties in hello solution dashboard:</span></span>

1. <span data-ttu-id="fc513-160">Puede ver el progreso de hello en del proceso de actualización de hello en hello frambuesa Pi:</span><span class="sxs-lookup"><span data-stu-id="fc513-160">You can view hello progress in of hello update process on hello Raspberry Pi:</span></span>

    ![Mostrar el progreso de la actualización][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="fc513-162">aplicación de supervisión remoto Hello en modo silencioso reinicia cuando se completa la actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc513-162">hello remote monitoring app restarts silently when hello update completes.</span></span> <span data-ttu-id="fc513-163">Use el comando de hello `ps -ef` tooverify se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="fc513-163">Use hello command `ps -ef` tooverify it is running.</span></span> <span data-ttu-id="fc513-164">Si desea que el proceso de hello tooterminate, use hello `kill` comando con Id. de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc513-164">If you want tooterminate hello process, use hello `kill` command with hello process id.</span></span>

1. <span data-ttu-id="fc513-165">Puede ver estado de Hola de actualización de firmware de hello, indicados por dispositivo de hello, en el portal de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc513-165">You can view hello status of hello firmware update, as reported by hello device, in hello solution portal.</span></span> <span data-ttu-id="fc513-166">Hello captura de pantalla siguiente muestra el estado de Hola y la duración de cada fase del proceso de actualización de hello y la nueva versión de firmware de hello:</span><span class="sxs-lookup"><span data-stu-id="fc513-166">hello following screenshot shows hello status and duration of each stage of hello update process, and hello new firmware version:</span></span>

    ![Mostrar estado del trabajo][img-job-status]

    <span data-ttu-id="fc513-168">Si navega toohello back-panel, puede comprobar dispositivo Hola todavía esté enviando telemetría después de la actualización de firmware de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc513-168">If you navigate back toohello dashboard, you can verify hello device is still sending telemetry following hello firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="fc513-169">Si deja Hola supervisión de solución que se ejecuta en su cuenta de Azure remota, se le facturará por vez Hola que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="fc513-169">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="fc513-170">Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="fc513-170">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="fc513-171">Eliminar soluciones Hola preconfigurado de su cuenta de Azure cuando termine de usarlo.</span><span class="sxs-lookup"><span data-stu-id="fc513-171">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc513-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fc513-172">Next steps</span></span>

<span data-ttu-id="fc513-173">Visite hello [centro de desarrollo de Azure IoT](https://azure.microsoft.com/develop/iot/) para obtener más ejemplos y documentación sobre IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc513-173">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
