---
title: "Conexión de Raspberry Pi al Conjunto de aplicaciones de IoT de Azure mediante C para admitir las actualizaciones de firmware | Microsoft Docs"
description: "Use el Starter Kit de IoT de Microsoft Azure para Raspberry Pi 3 y el Conjunto de aplicaciones de IoT de Azure. Use C para conectar su Raspberry Pi a la solución de supervisión remota, enviar telemetría desde sensores a la nube y realizar una actualización de firmware remota."
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
ms.openlocfilehash: f36f6512bb30e4b109b1bd1c3cdab10300f4edc9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a><span data-ttu-id="a82a2-104">Conexión de Raspberry Pi 3 a la solución de supervisión remota y habilitación de las actualizaciones de firmware remotas mediante C</span><span class="sxs-lookup"><span data-stu-id="a82a2-104">Connect your Raspberry Pi 3 to the remote monitoring solution and enable remote firmware updates using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="a82a2-105">Este tutorial muestra cómo usar el Starter Kit de IoT de Microsoft Azure para Raspberry Pi 3 para:</span><span class="sxs-lookup"><span data-stu-id="a82a2-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="a82a2-106">Desarrollar un lector de temperatura y humedad que pueda comunicarse con la nube.</span><span class="sxs-lookup"><span data-stu-id="a82a2-106">Develop a temperature and humidity reader that can communicate with the cloud.</span></span>
* <span data-ttu-id="a82a2-107">Habilitar y realizar una actualización de firmware remota para actualizar la aplicación cliente en Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="a82a2-107">Enable and perform a remote firmware update to update the client application on the Raspberry Pi.</span></span>

<span data-ttu-id="a82a2-108">El tutorial usa:</span><span class="sxs-lookup"><span data-stu-id="a82a2-108">The tutorial uses:</span></span>

* <span data-ttu-id="a82a2-109">El SO Raspbian, el lenguaje de programación C y el SDK de IoT de Microsoft Azure para C para implementar un dispositivo de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a82a2-109">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span></span>
* <span data-ttu-id="a82a2-110">La solución preconfigurada de supervisión remota del Conjunto de aplicaciones de IoT como el back-end basado en la nube.</span><span class="sxs-lookup"><span data-stu-id="a82a2-110">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="a82a2-111">Información general</span><span class="sxs-lookup"><span data-stu-id="a82a2-111">Overview</span></span>

<span data-ttu-id="a82a2-112">En este tutorial, va a completar los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="a82a2-112">In this tutorial, you complete the following steps:</span></span>

* <span data-ttu-id="a82a2-113">Implemente una instancia de la solución preconfigurada de supervisión remota en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a82a2-113">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="a82a2-114">Este paso implementa y configura varios servicios de Azure automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a82a2-114">This step automatically deploys and configures multiple Azure services.</span></span>
* <span data-ttu-id="a82a2-115">Configure el dispositivo y los sensores para que se comunique con el equipo y la solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="a82a2-115">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
* <span data-ttu-id="a82a2-116">Actualice el código del dispositivo de ejemplo para que se conecte a la solución de supervisión remota y envíe telemetría que aparezca en el panel de soluciones.</span><span class="sxs-lookup"><span data-stu-id="a82a2-116">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>
* <span data-ttu-id="a82a2-117">Use el código de dispositivo de ejemplo para actualizar la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="a82a2-117">Use the sample device code to update the client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="a82a2-118">La solución de supervisión remota proporciona un conjunto de servicios de Azure de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a82a2-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="a82a2-119">La implementación refleja una arquitectura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="a82a2-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="a82a2-120">Para evitar cobros de consumo innecesarios de Azure, elimine la instancia de la solución preconfigurada en azureiotsuite.com cuando haya terminado con ella.</span><span class="sxs-lookup"><span data-stu-id="a82a2-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="a82a2-121">Si necesita la solución preconfigurada de nuevo, puede crearla fácilmente.</span><span class="sxs-lookup"><span data-stu-id="a82a2-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="a82a2-122">Para más información sobre cómo reducir el consumo mientras se ejecuta la solución de supervisión remota, consulte [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configuración de soluciones preconfiguradas del Conjunto de aplicaciones de IoT de Azure para fines de demostración).</span><span class="sxs-lookup"><span data-stu-id="a82a2-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="a82a2-123">Descarga y configuración del ejemplo</span><span class="sxs-lookup"><span data-stu-id="a82a2-123">Download and configure the sample</span></span>

<span data-ttu-id="a82a2-124">Ahora puede descargar y configurar la aplicación de cliente de supervisión remota en su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="a82a2-124">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-the-repositories"></a><span data-ttu-id="a82a2-125">Clonación de repositorios</span><span class="sxs-lookup"><span data-stu-id="a82a2-125">Clone the repositories</span></span>

<span data-ttu-id="a82a2-126">Si aún no lo ha hecho, clone los repositorios necesarios mediante la ejecución de los siguientes comandos en Pi:</span><span class="sxs-lookup"><span data-stu-id="a82a2-126">If you haven't done so already, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="a82a2-127">Actualización de la cadena de conexión de dispositivo</span><span class="sxs-lookup"><span data-stu-id="a82a2-127">Update the device connection string</span></span>

<span data-ttu-id="a82a2-128">Abra el archivo de configuración de ejemplo en el editor **nano** con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="a82a2-128">Open the sample configuration file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="a82a2-129">Reemplace los valores de marcador de posición por el identificador de dispositivo y la información de IoT Hub que creó y guardó al principio de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a82a2-129">Replace the placeholder values with the device ID and IoT Hub information you created and saved at the start of this tutorial.</span></span>

<span data-ttu-id="a82a2-130">Cuando haya terminado, el contenido del archivo e información del dispositivo debe ser similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a82a2-130">When you are done, the contents of the deviceinfo file should look like the following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="a82a2-131">Guarde los cambios (**Ctrl-O**, **ENTRAR**) y salga del editor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="a82a2-131">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="build-the-sample"></a><span data-ttu-id="a82a2-132">Compilación del ejemplo</span><span class="sxs-lookup"><span data-stu-id="a82a2-132">Build the sample</span></span>

<span data-ttu-id="a82a2-133">Si todavía no lo ha hecho, instale los paquetes de requisitos previos para el SDK de dispositivo IoT de Microsoft Azure para C ejecutando los comandos siguientes en un terminal en Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="a82a2-133">If you have not already done so, install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="a82a2-134">Ahora puede compilar la solución de ejemplo en Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="a82a2-134">You can now build the sample solution on the Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

<span data-ttu-id="a82a2-135">Ahora puede ejecutar el programa de ejemplo en Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="a82a2-135">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="a82a2-136">Escriba el comando:</span><span class="sxs-lookup"><span data-stu-id="a82a2-136">Enter the command:</span></span>

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

<span data-ttu-id="a82a2-137">La salida de ejemplo siguiente es un ejemplo de la salida que se ve en el símbolo del sistema en Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="a82a2-137">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Salida de la aplicación Raspberry Pi][img-raspberry-output]

<span data-ttu-id="a82a2-139">Presione **Ctrl-C** para salir del programa en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="a82a2-139">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="a82a2-140">En el panel de soluciones, haga clic en **Dispositivos** para visitar la página **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="a82a2-140">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="a82a2-141">Seleccione su Raspberry Pi en la **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="a82a2-141">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="a82a2-142">A continuación, elija **Métodos**:</span><span class="sxs-lookup"><span data-stu-id="a82a2-142">Then choose **Methods**:</span></span>

    ![Lista de dispositivos en el panel][img-list-devices]

1. <span data-ttu-id="a82a2-144">En la página **Invocar método**, elija **InitiateFirmwareUpdate** en la lista desplegable **Método**.</span><span class="sxs-lookup"><span data-stu-id="a82a2-144">On the **Invoke Method** page, choose **InitiateFirmwareUpdate** in the **Method** dropdown.</span></span>

1. <span data-ttu-id="a82a2-145">En el campo **FWPackageURI**, escriba **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span><span class="sxs-lookup"><span data-stu-id="a82a2-145">In the **FWPackageURI** field, enter **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span></span> <span data-ttu-id="a82a2-146">Este archivo contiene la implementación de la versión 2.0 del firmware.</span><span class="sxs-lookup"><span data-stu-id="a82a2-146">This archive file contains the implementation of version 2.0 of the firmware.</span></span>

1. <span data-ttu-id="a82a2-147">Elija **Invocar método**.</span><span class="sxs-lookup"><span data-stu-id="a82a2-147">Choose **InvokeMethod**.</span></span> <span data-ttu-id="a82a2-148">La aplicación en Raspberry Pi envía una confirmación de vuelta al panel de soluciones.</span><span class="sxs-lookup"><span data-stu-id="a82a2-148">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard.</span></span> <span data-ttu-id="a82a2-149">Después, inicia el proceso de actualización de firmware mediante la descarga de la nueva versión del firmware:</span><span class="sxs-lookup"><span data-stu-id="a82a2-149">It then starts the firmware update process by downloading the new version of the firmware:</span></span>

    ![Mostrar el historial de métodos][img-method-history]

## <a name="observe-the-firmware-update-process"></a><span data-ttu-id="a82a2-151">Observar el proceso de actualización de firmware</span><span class="sxs-lookup"><span data-stu-id="a82a2-151">Observe the firmware update process</span></span>

<span data-ttu-id="a82a2-152">Puede observar el proceso de actualización del firmware a medida que se ejecuta en el dispositivo y ver las propiedades notificadas en el panel de la solución:</span><span class="sxs-lookup"><span data-stu-id="a82a2-152">You can observe the firmware update process as it runs on the device and by viewing the reported properties in the solution dashboard:</span></span>

1. <span data-ttu-id="a82a2-153">Puede ver el progreso en el proceso de actualización en Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="a82a2-153">You can view the progress in of the update process on the Raspberry Pi:</span></span>

    ![Mostrar el progreso de la actualización][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="a82a2-155">La aplicación de supervisión remota se reinicia automáticamente cuando finaliza la actualización.</span><span class="sxs-lookup"><span data-stu-id="a82a2-155">The remote monitoring app restarts silently when the update completes.</span></span> <span data-ttu-id="a82a2-156">Use el comando `ps -ef` para comprobar que se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="a82a2-156">Use the command `ps -ef` to verify it is running.</span></span> <span data-ttu-id="a82a2-157">Si desea terminar el proceso, use el comando `kill` con el identificador de proceso.</span><span class="sxs-lookup"><span data-stu-id="a82a2-157">If you want to terminate the process, use the `kill` command with the process id.</span></span>

1. <span data-ttu-id="a82a2-158">Puede ver el estado de la actualización del firmware, tal y como lo notifica el dispositivo, en el portal de solución.</span><span class="sxs-lookup"><span data-stu-id="a82a2-158">You can view the status of the firmware update, as reported by the device, in the solution portal.</span></span> <span data-ttu-id="a82a2-159">La captura de pantalla siguiente muestra el estado y la duración de cada fase del proceso de actualización y la nueva versión de firmware:</span><span class="sxs-lookup"><span data-stu-id="a82a2-159">The following screenshot shows the status and duration of each stage of the update process, and the new firmware version:</span></span>

    ![Mostrar estado del trabajo][img-job-status]

    <span data-ttu-id="a82a2-161">Si retrocede al panel, puede comprobar que el dispositivo todavía está enviando telemetría tras la actualización del firmware.</span><span class="sxs-lookup"><span data-stu-id="a82a2-161">If you navigate back to the dashboard, you can verify the device is still sending telemetry following the firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="a82a2-162">Si deja la solución de supervisión remota ejecutándose en su cuenta de Azure, se le cobra por el tiempo que se ejecute.</span><span class="sxs-lookup"><span data-stu-id="a82a2-162">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="a82a2-163">Para más información sobre cómo reducir el consumo mientras se ejecuta la solución de supervisión remota, consulte [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configuración de soluciones preconfiguradas del Conjunto de aplicaciones de IoT de Azure para fines de demostración).</span><span class="sxs-lookup"><span data-stu-id="a82a2-163">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="a82a2-164">Elimine la solución preconfigurada de su cuenta de Azure cuando haya terminado de usarla.</span><span class="sxs-lookup"><span data-stu-id="a82a2-164">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a82a2-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a82a2-165">Next steps</span></span>

<span data-ttu-id="a82a2-166">Visite el [Centro para desarrolladores de IoT de Azure](https://azure.microsoft.com/develop/iot/) para obtener más ejemplos y la documentación de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="a82a2-166">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md