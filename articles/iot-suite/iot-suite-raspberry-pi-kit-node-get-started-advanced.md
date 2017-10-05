---
title: "Conexión de Raspberry Pi al Conjunto de aplicaciones de IoT de Azure mediante Node.js para admitir las actualizaciones de firmware | Microsoft Docs"
description: "Use el Starter Kit de IoT de Microsoft Azure para Raspberry Pi 3 y el Conjunto de aplicaciones de IoT de Azure. Utilice Node.js para conectar su Raspberry Pi a la solución de supervisión remota, enviar telemetría desde sensores a la nube y realizar una actualización de firmware remota."
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
ms.openlocfilehash: 54503d5d6a636239d240509d7d09cf334234bac7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a><span data-ttu-id="0a127-104">Conexión de Raspberry Pi 3 a la solución de supervisión remota y habilitación de las actualizaciones de firmware remotas mediante Node.js</span><span class="sxs-lookup"><span data-stu-id="0a127-104">Connect your Raspberry Pi 3 to the remote monitoring solution and enable remote firmware updates using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="0a127-105">Este tutorial muestra cómo usar el Starter Kit de IoT de Microsoft Azure para Raspberry Pi 3 para:</span><span class="sxs-lookup"><span data-stu-id="0a127-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="0a127-106">Desarrollar un lector de temperatura y humedad que pueda comunicarse con la nube.</span><span class="sxs-lookup"><span data-stu-id="0a127-106">Develop a temperature and humidity reader that can communicate with the cloud.</span></span>
* <span data-ttu-id="0a127-107">Habilitar y realizar una actualización de firmware remota para actualizar la aplicación cliente en Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0a127-107">Enable and perform a remote firmware update to update the client application on the Raspberry Pi.</span></span>

<span data-ttu-id="0a127-108">El tutorial usa:</span><span class="sxs-lookup"><span data-stu-id="0a127-108">The tutorial uses:</span></span>

- <span data-ttu-id="0a127-109">El SO Raspbian, el lenguaje de programación Node.js y el SDK de IoT de Microsoft Azure para Node.js para implementar un dispositivo de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0a127-109">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="0a127-110">La solución preconfigurada de supervisión remota del Conjunto de aplicaciones de IoT como el back-end basado en la nube.</span><span class="sxs-lookup"><span data-stu-id="0a127-110">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="0a127-111">Información general</span><span class="sxs-lookup"><span data-stu-id="0a127-111">Overview</span></span>

<span data-ttu-id="0a127-112">En este tutorial, va a completar los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="0a127-112">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="0a127-113">Implemente una instancia de la solución preconfigurada de supervisión remota en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="0a127-113">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="0a127-114">Este paso implementa y configura varios servicios de Azure automáticamente.</span><span class="sxs-lookup"><span data-stu-id="0a127-114">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="0a127-115">Configure el dispositivo y los sensores para que se comunique con el equipo y la solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="0a127-115">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="0a127-116">Actualice el código del dispositivo de ejemplo para que se conecte a la solución de supervisión remota y envíe telemetría que aparezca en el panel de soluciones.</span><span class="sxs-lookup"><span data-stu-id="0a127-116">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>
- <span data-ttu-id="0a127-117">Use el código de dispositivo de ejemplo para actualizar la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="0a127-117">Use the sample device code to update the client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="0a127-118">La solución de supervisión remota proporciona un conjunto de servicios de Azure de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="0a127-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="0a127-119">La implementación refleja una arquitectura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="0a127-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="0a127-120">Para evitar cobros de consumo innecesarios de Azure, elimine la instancia de la solución preconfigurada en azureiotsuite.com cuando haya terminado con ella.</span><span class="sxs-lookup"><span data-stu-id="0a127-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="0a127-121">Si necesita la solución preconfigurada de nuevo, puede crearla fácilmente.</span><span class="sxs-lookup"><span data-stu-id="0a127-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="0a127-122">Para más información sobre cómo reducir el consumo mientras se ejecuta la solución de supervisión remota, consulte [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configuración de soluciones preconfiguradas del Conjunto de aplicaciones de IoT de Azure para fines de demostración).</span><span class="sxs-lookup"><span data-stu-id="0a127-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="0a127-123">Descarga y configuración del ejemplo</span><span class="sxs-lookup"><span data-stu-id="0a127-123">Download and configure the sample</span></span>

<span data-ttu-id="0a127-124">Ahora puede descargar y configurar la aplicación de cliente de supervisión remota en su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0a127-124">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="0a127-125">Instalación de Node.js</span><span class="sxs-lookup"><span data-stu-id="0a127-125">Install Node.js</span></span>

<span data-ttu-id="0a127-126">Si aún no lo ha hecho, instale Node.js en su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0a127-126">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="0a127-127">El SDK de IoT para Node.js requiere la versión 0.11.5 de Node.js o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="0a127-127">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="0a127-128">Los pasos siguientes muestran cómo instalar Node.js v6.10.2 en Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="0a127-128">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="0a127-129">Use el siguiente comando para actualizar Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="0a127-129">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="0a127-130">Use el siguiente comando para descargar los archivos binarios de Node.js en Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="0a127-130">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="0a127-131">Use el siguiente comando para los binarios:</span><span class="sxs-lookup"><span data-stu-id="0a127-131">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="0a127-132">Use el siguiente comando para comprobar que ha instalado Node.js v6.10.2 correctamente:</span><span class="sxs-lookup"><span data-stu-id="0a127-132">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="0a127-133">Clonación de repositorios</span><span class="sxs-lookup"><span data-stu-id="0a127-133">Clone the repositories</span></span>

<span data-ttu-id="0a127-134">Si aún no lo ha hecho, clone los repositorios necesarios mediante la ejecución de los siguientes comandos en Pi:</span><span class="sxs-lookup"><span data-stu-id="0a127-134">If you haven't done so already, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="0a127-135">Actualización de la cadena de conexión de dispositivo</span><span class="sxs-lookup"><span data-stu-id="0a127-135">Update the device connection string</span></span>

<span data-ttu-id="0a127-136">Abra el archivo de configuración de ejemplo en el editor **nano** con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0a127-136">Open the sample configuration file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="0a127-137">Reemplace los valores de marcador de posición por el identificador de dispositivo y la información de IoT Hub que creó y guardó al principio de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="0a127-137">Replace the placeholder values with the device id and IoT Hub information you created and saved at the start of this tutorial.</span></span>

<span data-ttu-id="0a127-138">Cuando haya terminado, el contenido del archivo e información del dispositivo debe ser similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0a127-138">When you are done, the contents of the deviceinfo file should look like the following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="0a127-139">Guarde los cambios (**Ctrl-O**, **ENTRAR**) y salga del editor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="0a127-139">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="0a127-140">Ejecución del ejemplo</span><span class="sxs-lookup"><span data-stu-id="0a127-140">Run the sample</span></span>

<span data-ttu-id="0a127-141">Ejecute los comandos siguientes para instalar los paquetes de requisitos previos para el ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0a127-141">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

<span data-ttu-id="0a127-142">Ahora puede ejecutar el programa de ejemplo en Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0a127-142">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="0a127-143">Escriba el comando:</span><span class="sxs-lookup"><span data-stu-id="0a127-143">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

<span data-ttu-id="0a127-144">La salida de ejemplo siguiente es un ejemplo de la salida que se ve en el símbolo del sistema en Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="0a127-144">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Salida de la aplicación Raspberry Pi][img-raspberry-output]

<span data-ttu-id="0a127-146">Presione **Ctrl-C** para salir del programa en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="0a127-146">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="0a127-147">En el panel de soluciones, haga clic en **Dispositivos** para visitar la página **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="0a127-147">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="0a127-148">Seleccione su Raspberry Pi en la **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="0a127-148">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="0a127-149">A continuación, elija **Métodos**:</span><span class="sxs-lookup"><span data-stu-id="0a127-149">Then choose **Methods**:</span></span>

    ![Lista de dispositivos en el panel][img-list-devices]

1. <span data-ttu-id="0a127-151">En la página **Invocar método**, elija **InitiateFirmwareUpdate** en la lista desplegable **Método**.</span><span class="sxs-lookup"><span data-stu-id="0a127-151">On the **Invoke Method** page, choose **InitiateFirmwareUpdate** in the **Method** dropdown.</span></span>

1. <span data-ttu-id="0a127-152">En el campo **FWPackageURI**, escriba **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span><span class="sxs-lookup"><span data-stu-id="0a127-152">In the **FWPackageURI** field, enter **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span></span> <span data-ttu-id="0a127-153">Este archivo contiene la implementación de la versión 2.0 del firmware.</span><span class="sxs-lookup"><span data-stu-id="0a127-153">This file contains the implementation of version 2.0 of the firmware.</span></span>

1. <span data-ttu-id="0a127-154">Elija **Invocar método**.</span><span class="sxs-lookup"><span data-stu-id="0a127-154">Choose **InvokeMethod**.</span></span> <span data-ttu-id="0a127-155">La aplicación en Raspberry Pi envía una confirmación de vuelta al panel de soluciones.</span><span class="sxs-lookup"><span data-stu-id="0a127-155">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard.</span></span> <span data-ttu-id="0a127-156">Después, inicia el proceso de actualización de firmware mediante la descarga de la nueva versión del firmware:</span><span class="sxs-lookup"><span data-stu-id="0a127-156">It then starts the firmware update process by downloading the new version of the firmware:</span></span>

    ![Mostrar el historial de métodos][img-method-history]

## <a name="observe-the-firmware-update-process"></a><span data-ttu-id="0a127-158">Observar el proceso de actualización de firmware</span><span class="sxs-lookup"><span data-stu-id="0a127-158">Observe the firmware update process</span></span>

<span data-ttu-id="0a127-159">Puede observar el proceso de actualización del firmware a medida que se ejecuta en el dispositivo y ver las propiedades notificadas en el panel de la solución:</span><span class="sxs-lookup"><span data-stu-id="0a127-159">You can observe the firmware update process as it runs on the device and by viewing the reported properties in the solution dashboard:</span></span>

1. <span data-ttu-id="0a127-160">Puede ver el progreso en el proceso de actualización en Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="0a127-160">You can view the progress in of the update process on the Raspberry Pi:</span></span>

    ![Mostrar el progreso de la actualización][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="0a127-162">La aplicación de supervisión remota se reinicia automáticamente cuando finaliza la actualización.</span><span class="sxs-lookup"><span data-stu-id="0a127-162">The remote monitoring app restarts silently when the update completes.</span></span> <span data-ttu-id="0a127-163">Use el comando `ps -ef` para comprobar que se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="0a127-163">Use the command `ps -ef` to verify it is running.</span></span> <span data-ttu-id="0a127-164">Si desea terminar el proceso, use el comando `kill` con el identificador de proceso.</span><span class="sxs-lookup"><span data-stu-id="0a127-164">If you want to terminate the process, use the `kill` command with the process id.</span></span>

1. <span data-ttu-id="0a127-165">Puede ver el estado de la actualización del firmware, tal y como lo notifica el dispositivo, en el portal de solución.</span><span class="sxs-lookup"><span data-stu-id="0a127-165">You can view the status of the firmware update, as reported by the device, in the solution portal.</span></span> <span data-ttu-id="0a127-166">La captura de pantalla siguiente muestra el estado y la duración de cada fase del proceso de actualización y la nueva versión de firmware:</span><span class="sxs-lookup"><span data-stu-id="0a127-166">The following screenshot shows the status and duration of each stage of the update process, and the new firmware version:</span></span>

    ![Mostrar estado del trabajo][img-job-status]

    <span data-ttu-id="0a127-168">Si retrocede al panel, puede comprobar que el dispositivo todavía está enviando telemetría tras la actualización del firmware.</span><span class="sxs-lookup"><span data-stu-id="0a127-168">If you navigate back to the dashboard, you can verify the device is still sending telemetry following the firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="0a127-169">Si deja la solución de supervisión remota ejecutándose en su cuenta de Azure, se le cobra por el tiempo que se ejecute.</span><span class="sxs-lookup"><span data-stu-id="0a127-169">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="0a127-170">Para más información sobre cómo reducir el consumo mientras se ejecuta la solución de supervisión remota, consulte [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configuración de soluciones preconfiguradas del Conjunto de aplicaciones de IoT de Azure para fines de demostración).</span><span class="sxs-lookup"><span data-stu-id="0a127-170">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="0a127-171">Elimine la solución preconfigurada de su cuenta de Azure cuando haya terminado de usarla.</span><span class="sxs-lookup"><span data-stu-id="0a127-171">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a127-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0a127-172">Next steps</span></span>

<span data-ttu-id="0a127-173">Visite el [Centro para desarrolladores de IoT de Azure](https://azure.microsoft.com/develop/iot/) para obtener más ejemplos y la documentación de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="0a127-173">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md