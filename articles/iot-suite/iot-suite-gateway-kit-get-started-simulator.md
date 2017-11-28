---
title: un conjunto de IoT mediante un NUC de Intel de puerta de enlace tooAzure aaaConnect | Documentos de Microsoft
description: "Utilice Hola hello y Kit de puerta de enlace de Microsoft IoT comercial remoto preconfigurada solución de supervisión. Hola utilice Azure IoT borde puerta de enlace tooconnect toohello solución de supervisión, enviar telemetría simulada toohello en la nube y responder toomethods invoca desde el panel de la solución de Hola."
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
ms.openlocfilehash: 46b545fc21b054191c8f78ace20fc628f839a819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a><span data-ttu-id="a1fcb-104">Conectar su toohello de puerta de enlace de borde de IoT de Azure remoto solución preconfigurada de supervisión y enviar telemetría simulada</span><span class="sxs-lookup"><span data-stu-id="a1fcb-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send simulated telemetry</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="a1fcb-105">Este tutorial muestra cómo toosimulate temperatura de toouse borde de IoT de Azure y la supervisión remota de humedad datos toosend toohello preconfigurado solución.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-105">This tutorial shows you how toouse Azure IoT Edge toosimulate temperature and humidity data toosend toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="a1fcb-106">tutorial de Hello usa:</span><span class="sxs-lookup"><span data-stu-id="a1fcb-106">hello tutorial uses:</span></span>

- <span data-ttu-id="a1fcb-107">Azure IoT borde tooimplement una puerta de enlace de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-107">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="a1fcb-108">supervisión remota de Hello IoT conjunto había preconfigurado solución como back-end de hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="a1fcb-109">Información general</span><span class="sxs-lookup"><span data-stu-id="a1fcb-109">Overview</span></span>

<span data-ttu-id="a1fcb-110">En este tutorial, se realizará Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a1fcb-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="a1fcb-111">Implemente una instancia de hello remoto supervisión solución preconfigurada tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="a1fcb-112">Este paso implementa y configura varios servicios de Azure automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="a1fcb-113">Configure su toocommunicate de dispositivo de puerta de enlace de Intel NUC con el equipo y la solución de supervisión remota de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-113">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="a1fcb-114">Configurar hello toosend de puerta de enlace de IoT borde simulados telemetría que se puede ver en el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-114">Configure hello IoT Edge gateway toosend simulated telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="a1fcb-115">Hola disposiciones de solución de supervisión remoto un conjunto de servicios de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="a1fcb-116">implementación de Hello refleja una arquitectura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="a1fcb-117">tooavoid cargos de consumo innecesario de Azure, elimine la instancia de la solución de hello preconfigurado en azureiotsuite.com cuando haya terminado con él.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="a1fcb-118">Si necesita hello solución preconfigurada de nuevo, puede crearla fácilmente.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="a1fcb-119">Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="a1fcb-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

<span data-ttu-id="a1fcb-120">Repita Hola anteriores pasos tooadd un segundo dispositivo con un Id. de dispositivo como **device02**.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-120">Repeat hello previous steps tooadd a second device using a Device ID such as **device02**.</span></span> <span data-ttu-id="a1fcb-121">ejemplo de Hola envía datos de dos dispositivos simulados en la solución de supervisión remota toohello Hola puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-121">hello sample sends data from two simulated devices in hello gateway toohello remote monitoring solution.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="a1fcb-122">Crear el módulo personalizado de borde de IoT de Hola</span><span class="sxs-lookup"><span data-stu-id="a1fcb-122">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="a1fcb-123">Ahora puede compilar módulo IoT borde personalizado Hola que permite Hola puerta de enlace toosend mensajes toohello solución de supervisión.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-123">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="a1fcb-124">Para obtener más información sobre cómo configurar una puerta de enlace y los módulos de IoT Edge, consulte [Conceptos de Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="a1fcb-124">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="a1fcb-125">Descargar código de fuente de Hola para módulos personalizados de borde de IoT de Hola desde GitHub con hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a1fcb-125">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="a1fcb-126">Crear el módulo de IoT borde personalizado de hello mediante Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a1fcb-126">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="a1fcb-127">script de compilación de Hello coloca módulo personalizado de borde de IoT de hello libsimulator.so en la carpeta de compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-127">hello build script places hello libsimulator.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="a1fcb-128">Configurar y ejecutar Hola puerta de enlace de borde de IoT</span><span class="sxs-lookup"><span data-stu-id="a1fcb-128">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="a1fcb-129">Ahora puede configurar hello borde IoT puerta de enlace toosend telemetría simulada tooyour remoto panel de supervisión.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-129">You can now configure hello IoT Edge gateway toosend simulated telemetry tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="a1fcb-130">Para obtener más información sobre cómo configurar una puerta de enlace y los módulos de IoT Edge, consulte [Conceptos de Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="a1fcb-130">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="a1fcb-131">En este tutorial, utilice estándar hello `vi` editor de texto en hello NUC de Intel.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-131">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="a1fcb-132">Si no ha usado `vi` antes, debe completar un tutorial introductorio, como [Unix - Hola vi Editor Tutorial] [ lnk-vi-tutorial] toofamiliarize usted mismo con este editor.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-132">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="a1fcb-133">Como alternativa, puede instalar más fácil de usar hello [nano](https://www.nano-editor.org/) editor mediante el comando hello `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-133">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="a1fcb-134">Archivo de configuración de ejemplo de Hola abierto en hello **vi** editor mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a1fcb-134">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

<span data-ttu-id="a1fcb-135">Busque Hola siguiendo las líneas en la configuración de hello para el módulo de hello el centro de IOT:</span><span class="sxs-lookup"><span data-stu-id="a1fcb-135">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="a1fcb-136">Reemplace el marcador de posición de hello valores con información de centro de IoT creado y guardado en Hola Hola inicio de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-136">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="a1fcb-137">valor de Hola para IoTHubName es similar a **yourrmsolution37e08**, y valor hello IoTSuffix es normalmente **devices.net azure**.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-137">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="a1fcb-138">Busque Hola siguiendo las líneas en la configuración de hello para el módulo de asignación de hello:</span><span class="sxs-lookup"><span data-stu-id="a1fcb-138">Locate hello following lines in hello configuration for hello mapping module:</span></span>

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

<span data-ttu-id="a1fcb-139">Reemplace hello **deviceID** y **deviceKey** marcadores de posición con identificadores de Hola y claves para dispositivos de hello dos que se creó anteriormente en la solución de supervisión remota Hola.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-139">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="a1fcb-140">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-140">Save your changes.</span></span>

<span data-ttu-id="a1fcb-141">Ahora puede ejecutar Hola comandos de puerta de enlace de IoT borde con hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="a1fcb-141">You can now run hello IoT Edge gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

<span data-ttu-id="a1fcb-142">puerta de enlace de Hello comienza en hello NUC de Intel y envía la solución de supervisión remota de telemetría simulada toohello:</span><span class="sxs-lookup"><span data-stu-id="a1fcb-142">hello gateway starts on hello Intel NUC and sends simulated telemetry toohello remote monitoring solution:</span></span>

![La puerta de enlace de IoT Edge genera telemetría simulada.][img-simulated telemetry]

<span data-ttu-id="a1fcb-144">Presione **Ctrl-C** programa Hola de tooexit en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-144">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="a1fcb-145">Vista Hola telemetría</span><span class="sxs-lookup"><span data-stu-id="a1fcb-145">View hello telemetry</span></span>

<span data-ttu-id="a1fcb-146">Hola puerta de enlace de IoT borde ahora está enviando telemetría simulada toohello solución de supervisión remoto.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-146">hello IoT Edge gateway is now sending simulated telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="a1fcb-147">Puede ver la telemetría de hello en el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-147">You can view hello telemetry on hello solution dashboard.</span></span>

- <span data-ttu-id="a1fcb-148">Vaya a Panel de solución toohello.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-148">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="a1fcb-149">Seleccione uno de los dispositivos de hello dos que configuró en la puerta de enlace de Hola Hola **tooView dispositivo** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-149">Select one of hello two devices you configured in hello gateway in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="a1fcb-150">telemetría Hola desde dispositivos de puerta de enlace de Hola se muestra en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-150">hello telemetry from hello gateway devices displays on hello dashboard.</span></span>

![Mostrar la telemetría de dispositivos de puerta de enlace de hello simulada][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="a1fcb-152">Si deja Hola supervisión de solución que se ejecuta en su cuenta de Azure remota, se le facturará por vez Hola que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-152">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="a1fcb-153">Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="a1fcb-153">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="a1fcb-154">Eliminar soluciones Hola preconfigurado de su cuenta de Azure cuando termine de usarlo.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-154">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1fcb-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a1fcb-155">Next steps</span></span>

<span data-ttu-id="a1fcb-156">Visite hello [centro de desarrollo de Azure IoT](https://azure.microsoft.com/develop/iot/) para obtener más ejemplos y documentación sobre IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-156">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started