---
title: Conectar una puerta de enlace al Conjunto de aplicaciones de IoT de Azure con Intel NUC | Documentos de Microsoft
description: "Use el Kit de puerta de enlace comercial de Microsoft IoT y la solución preconfigurada de supervisión remota. Use la puerta de enlace de Azure IoT Edge para conectarse a la solución de supervisión remota, enviar telemetría simulada a la nube y responder a los métodos invocados desde el panel de soluciones."
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
ms.openlocfilehash: 9ed57d3c23e2adbd42c054f33c8ed46e3d6c9792
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-azure-iot-edge-gateway-to-the-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a><span data-ttu-id="bae89-104">Conectar la puerta de enlace de Azure IoT Edge a la solución preconfigurada de supervisión remota y enviar telemetría simulada</span><span class="sxs-lookup"><span data-stu-id="bae89-104">Connect your Azure IoT Edge gateway to the remote monitoring preconfigured solution and send simulated telemetry</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="bae89-105">En este tutorial se muestra cómo usar Azure IoT Edge para simular datos de temperatura y humedad y enviarlos a la solución preconfigurada de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="bae89-105">This tutorial shows you how to use Azure IoT Edge to simulate temperature and humidity data to send to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="bae89-106">El tutorial usa:</span><span class="sxs-lookup"><span data-stu-id="bae89-106">The tutorial uses:</span></span>

- <span data-ttu-id="bae89-107">Azure IoT Edge para implementar una puerta de enlace de muestra.</span><span class="sxs-lookup"><span data-stu-id="bae89-107">Azure IoT Edge to implement a sample gateway.</span></span>
- <span data-ttu-id="bae89-108">La solución preconfigurada de supervisión remota del Conjunto de aplicaciones de IoT como el back-end basado en la nube.</span><span class="sxs-lookup"><span data-stu-id="bae89-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="bae89-109">Información general</span><span class="sxs-lookup"><span data-stu-id="bae89-109">Overview</span></span>

<span data-ttu-id="bae89-110">En este tutorial, va a completar los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="bae89-110">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="bae89-111">Implemente una instancia de la solución preconfigurada de supervisión remota en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="bae89-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="bae89-112">Este paso implementa y configura varios servicios de Azure automáticamente.</span><span class="sxs-lookup"><span data-stu-id="bae89-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="bae89-113">Configure el dispositivo de puerta de enlace Intel NUC para que se comunique con el equipo y la solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="bae89-113">Set up your Intel NUC gateway device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="bae89-114">Configure la puerta de enlace de IoT Edge para enviar telemetría simulada que se puede ver en el panel de soluciones.</span><span class="sxs-lookup"><span data-stu-id="bae89-114">Configure the IoT Edge gateway to send simulated telemetry that you can view on the solution dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="bae89-115">La solución de supervisión remota proporciona un conjunto de servicios de Azure de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="bae89-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="bae89-116">La implementación refleja una arquitectura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="bae89-116">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="bae89-117">Para evitar cobros de consumo innecesarios de Azure, elimine la instancia de la solución preconfigurada en azureiotsuite.com cuando haya terminado con ella.</span><span class="sxs-lookup"><span data-stu-id="bae89-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="bae89-118">Si necesita la solución preconfigurada de nuevo, puede crearla fácilmente.</span><span class="sxs-lookup"><span data-stu-id="bae89-118">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="bae89-119">Para más información sobre cómo reducir el consumo mientras se ejecuta la solución de supervisión remota, consulte [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configuración de soluciones preconfiguradas del Conjunto de aplicaciones de IoT de Azure para fines de demostración).</span><span class="sxs-lookup"><span data-stu-id="bae89-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

<span data-ttu-id="bae89-120">Repita los pasos anteriores para agregar un segundo dispositivo con un id. de dispositivo como **device02**.</span><span class="sxs-lookup"><span data-stu-id="bae89-120">Repeat the previous steps to add a second device using a Device ID such as **device02**.</span></span> <span data-ttu-id="bae89-121">La muestra envía datos procedentes de dos dispositivos simulados en la puerta de enlace a la solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="bae89-121">The sample sends data from two simulated devices in the gateway to the remote monitoring solution.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-the-custom-iot-edge-module"></a><span data-ttu-id="bae89-122">Generar el módulo de IoT Edge personalizado</span><span class="sxs-lookup"><span data-stu-id="bae89-122">Build the custom IoT Edge module</span></span>

<span data-ttu-id="bae89-123">Ahora puede generar el módulo personalizado de IoT Edge que permite que la puerta de enlace envíe mensajes a la solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="bae89-123">You can now build the custom IoT Edge module that enables the gateway to send messages to the remote monitoring solution.</span></span> <span data-ttu-id="bae89-124">Para obtener más información sobre cómo configurar una puerta de enlace y los módulos de IoT Edge, consulte [Conceptos de Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="bae89-124">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="bae89-125">Descargue el código fuente para los módulos personalizados de IoT Edge desde GitHub con los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bae89-125">Download the source code for the custom IoT Edge modules from GitHub using the following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="bae89-126">Cree el módulo personalizado de IoT Edge con los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bae89-126">Build the custom IoT Edge module using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="bae89-127">El script de compilación coloca el módulo personalizado de IoT Edge libsimulator.so en la carpeta de compilación.</span><span class="sxs-lookup"><span data-stu-id="bae89-127">The build script places the libsimulator.so custom IoT Edge module in the build folder.</span></span>

## <a name="configure-and-run-the-iot-edge-gateway"></a><span data-ttu-id="bae89-128">Configurar y ejecutar la puerta de enlace de IoT Edge</span><span class="sxs-lookup"><span data-stu-id="bae89-128">Configure and run the IoT Edge gateway</span></span>

<span data-ttu-id="bae89-129">Ahora puede configurar la puerta de enlace de IoT Edge para enviar telemetría simulada al panel de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="bae89-129">You can now configure the IoT Edge gateway to send simulated telemetry to your remote monitoring dashboard.</span></span> <span data-ttu-id="bae89-130">Para obtener más información sobre cómo configurar una puerta de enlace y los módulos de IoT Edge, consulte [Conceptos de Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="bae89-130">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="bae89-131">En este tutorial, use el editor de texto `vi` estándar en Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="bae89-131">In this tutorial, you use the standard `vi` text editor on the Intel NUC.</span></span> <span data-ttu-id="bae89-132">Si no ha usado `vi` antes, complete un tutorial introductorio, como [Unix - The vi Editor Tutorial][lnk-vi-tutorial] (Unix: el tutorial de editor vi) para familiarizarse con este editor.</span><span class="sxs-lookup"><span data-stu-id="bae89-132">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - The vi Editor Tutorial][lnk-vi-tutorial] to familiarize yourself with this editor.</span></span> <span data-ttu-id="bae89-133">Como alternativa, puede instalar el editor [nano](https://www.nano-editor.org/) fácil de usar con el comando `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="bae89-133">Alternatively, you can install the more user-friendly [nano](https://www.nano-editor.org/) editor using the command `smart install nano -y`.</span></span>

<span data-ttu-id="bae89-134">Abra el archivo de configuración de ejemplo en el editor **vi** con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="bae89-134">Open the sample configuration file in the **vi** editor using the following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

<span data-ttu-id="bae89-135">Busque las líneas siguientes en la configuración del módulo de IoTHub:</span><span class="sxs-lookup"><span data-stu-id="bae89-135">Locate the following lines in the configuration for the IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="bae89-136">Reemplace los valores de marcador de posición con la información de IoT Hub que creó y guardó al principio de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="bae89-136">Replace the placeholder values with the IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="bae89-137">El valor de IoTHubName es similar a **yourrmsolution37e08** y el valor de IoTSuffix suele ser **azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="bae89-137">The value for IoTHubName looks like **yourrmsolution37e08**, and the value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="bae89-138">Busque las líneas siguientes en la configuración del módulo de asignación:</span><span class="sxs-lookup"><span data-stu-id="bae89-138">Locate the following lines in the configuration for the mapping module:</span></span>

```json
args": [
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="bae89-139">Reemplace los marcadores de posición **deviceID** y **deviceKey** con los identificadores y las claves para los dos dispositivos que creó anteriormente en la solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="bae89-139">Replace the **deviceID** and **deviceKey** placeholders with the IDs and keys for the two devices you created in the remote monitoring solution previously.</span></span>

<span data-ttu-id="bae89-140">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="bae89-140">Save your changes.</span></span>

<span data-ttu-id="bae89-141">Ahora puede usar estos comandos para ejecutar la puerta de enlace de IoT Edge:</span><span class="sxs-lookup"><span data-stu-id="bae89-141">You can now run the IoT Edge gateway using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

<span data-ttu-id="bae89-142">La puerta de enlace se inicia en Intel NUC y envía telemetría simulada a la solución de supervisión remota:</span><span class="sxs-lookup"><span data-stu-id="bae89-142">The gateway starts on the Intel NUC and sends simulated telemetry to the remote monitoring solution:</span></span>

![La puerta de enlace de IoT Edge genera telemetría simulada.][img-simulated telemetry]

<span data-ttu-id="bae89-144">Presione **Ctrl-C** para salir del programa en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="bae89-144">Press **Ctrl-C** to exit the program at any time.</span></span>

## <a name="view-the-telemetry"></a><span data-ttu-id="bae89-145">Visualización de la telemetría</span><span class="sxs-lookup"><span data-stu-id="bae89-145">View the telemetry</span></span>

<span data-ttu-id="bae89-146">La puerta de enlace de IoT Edge ahora está enviando telemetría simulada a la solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="bae89-146">The IoT Edge gateway is now sending simulated telemetry to the remote monitoring solution.</span></span> <span data-ttu-id="bae89-147">Puede verla en el panel de soluciones.</span><span class="sxs-lookup"><span data-stu-id="bae89-147">You can view the telemetry on the solution dashboard.</span></span>

- <span data-ttu-id="bae89-148">Vaya al panel de soluciones.</span><span class="sxs-lookup"><span data-stu-id="bae89-148">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="bae89-149">Seleccione uno de los dos dispositivos que configuró en la puerta de enlace en la lista desplegable **Dispositivo que se visualizará**.</span><span class="sxs-lookup"><span data-stu-id="bae89-149">Select one of the two devices you configured in the gateway in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="bae89-150">La telemetría de los dispositivos de puerta de enlace se muestra en el panel.</span><span class="sxs-lookup"><span data-stu-id="bae89-150">The telemetry from the gateway devices displays on the dashboard.</span></span>

![Mostrar la telemetría de los dispositivos de puerta de enlace simulada][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="bae89-152">Si deja la solución de supervisión remota ejecutándose en su cuenta de Azure, se le cobra por el tiempo que se ejecute.</span><span class="sxs-lookup"><span data-stu-id="bae89-152">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="bae89-153">Para más información sobre cómo reducir el consumo mientras se ejecuta la solución de supervisión remota, consulte [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Configuración de soluciones preconfiguradas del Conjunto de aplicaciones de IoT de Azure para fines de demostración).</span><span class="sxs-lookup"><span data-stu-id="bae89-153">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="bae89-154">Elimine la solución preconfigurada de su cuenta de Azure cuando haya terminado de usarla.</span><span class="sxs-lookup"><span data-stu-id="bae89-154">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bae89-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bae89-155">Next steps</span></span>

<span data-ttu-id="bae89-156">Visite el [Centro para desarrolladores de IoT de Azure](https://azure.microsoft.com/develop/iot/) para obtener más ejemplos y la documentación de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="bae89-156">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started