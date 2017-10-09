---
title: un conjunto de IoT mediante un NUC de Intel de puerta de enlace tooAzure aaaConnect | Documentos de Microsoft
description: "Utilice Hola hello y Kit de puerta de enlace de Microsoft IoT comercial remoto preconfigurada solución de supervisión. Usar una solución de supervisión remota de toohello de tooconnect de dispositivo de SensorTag de tooenable de puerta de enlace de borde de IoT de Azure de hello, enviar en la nube toohello telemetría y responder toomethods invocado desde el panel de la solución de Hola."
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
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 6f98ee3c1e2311a8644da9d72d40e671e7cbcf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="9085a-104">Conectar su toohello de puerta de enlace de borde de IoT de Azure remoto solución preconfigurada de supervisión y enviar telemetría desde un SensorTag</span><span class="sxs-lookup"><span data-stu-id="9085a-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="9085a-105">Este tutorial muestra cómo toouse los datos de temperatura y humedad de toosend borde de IoT de Azure de supervisión remota de SensorTag dispositivo toohello había preconfigurado solución.</span><span class="sxs-lookup"><span data-stu-id="9085a-105">This tutorial shows you how toouse Azure IoT Edge toosend temperature and humidity data from SensorTag device toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="9085a-106">Hola SensorTag conecta la puerta de enlace de toohello NUC de Intel con Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="9085a-106">hello SensorTag connects toohello Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="9085a-107">tutorial de Hello usa:</span><span class="sxs-lookup"><span data-stu-id="9085a-107">hello tutorial uses:</span></span>

- <span data-ttu-id="9085a-108">Azure IoT borde tooimplement una puerta de enlace de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9085a-108">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="9085a-109">supervisión remota de Hello IoT conjunto había preconfigurado solución como back-end de hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="9085a-109">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="9085a-110">Información general</span><span class="sxs-lookup"><span data-stu-id="9085a-110">Overview</span></span>

<span data-ttu-id="9085a-111">En este tutorial, se realizará Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9085a-111">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="9085a-112">Implemente una instancia de hello remoto supervisión solución preconfigurada tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9085a-112">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="9085a-113">Este paso implementa y configura varios servicios de Azure automáticamente.</span><span class="sxs-lookup"><span data-stu-id="9085a-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="9085a-114">Configure su toocommunicate de dispositivo de puerta de enlace de Intel NUC con el equipo y la solución de supervisión remota de Hola.</span><span class="sxs-lookup"><span data-stu-id="9085a-114">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="9085a-115">Configurar la telemetría de tooreceive de puerta de enlace de Intel NUC desde un dispositivo de SensorTag y envíelo toohello panel de supervisión remoto.</span><span class="sxs-lookup"><span data-stu-id="9085a-115">Set up your Intel NUC gateway tooreceive telemetry from a SensorTag device and send it toohello remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="9085a-116">[SensorTag de Texas Instruments BLE][lnk-sensortag].</span><span class="sxs-lookup"><span data-stu-id="9085a-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="9085a-117">Este tutorial recupera los datos de telemetría a través de Bluetooth del dispositivo de SensorTag Hola.</span><span class="sxs-lookup"><span data-stu-id="9085a-117">This tutorial retrieves telemetry data over Bluetooth from hello SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="9085a-118">Hola disposiciones de solución de supervisión remoto un conjunto de servicios de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9085a-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="9085a-119">implementación de Hello refleja una arquitectura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="9085a-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="9085a-120">tooavoid cargos de consumo innecesario de Azure, elimine la instancia de la solución de hello preconfigurado en azureiotsuite.com cuando haya terminado con él.</span><span class="sxs-lookup"><span data-stu-id="9085a-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="9085a-121">Si necesita hello solución preconfigurada de nuevo, puede crearla fácilmente.</span><span class="sxs-lookup"><span data-stu-id="9085a-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="9085a-122">Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="9085a-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="9085a-123">Configurar la conectividad de Bluetooth</span><span class="sxs-lookup"><span data-stu-id="9085a-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="9085a-124">Configurar el Bluetooth en hello NUC Intel tooenable hello SensorTag dispositivo tooconnect y enviar telemetría.</span><span class="sxs-lookup"><span data-stu-id="9085a-124">Configure Bluetooth on hello Intel NUC tooenable hello SensorTag device tooconnect and send telemetry.</span></span>

### <a name="find-hello-mac-address-of-hello-sensortag"></a><span data-ttu-id="9085a-125">Buscar la dirección MAC de Hola de hello SensorTag</span><span class="sxs-lookup"><span data-stu-id="9085a-125">Find hello MAC address of hello SensorTag</span></span>

1. <span data-ttu-id="9085a-126">En el shell de hello en hello NUC de Intel, ejecute hello después de comando toounblock Hola Bluetooth servicio:</span><span class="sxs-lookup"><span data-stu-id="9085a-126">In hello shell on hello Intel NUC, run hello following command toounblock hello Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="9085a-127">Siguiente ejecución Hola comandos del servicio de Bluetooth toostart hello en hello NUC de Intel y escriba shell de hello Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="9085a-127">Run hello following commands toostart hello Bluetooth service on hello Intel NUC and enter hello Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="9085a-128">Ejecute hello después toopower de comando en el controlador de hello Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="9085a-128">Run hello following command toopower on hello Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="9085a-129">Cuando el controlador de hello está activada, verá un mensaje **cambiar power en se realizó correctamente**.</span><span class="sxs-lookup"><span data-stu-id="9085a-129">When hello controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="9085a-130">Ejecute hello después tooscan de comando para dispositivos Bluetooth cercanos:</span><span class="sxs-lookup"><span data-stu-id="9085a-130">Run hello following command tooscan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="9085a-131">Presione Hola del botón de encendido en hello SensorTag toomake se puede detectar.</span><span class="sxs-lookup"><span data-stu-id="9085a-131">Press hello power button on hello SensorTag toomake it discoverable.</span></span> <span data-ttu-id="9085a-132">Hola verde LED parpadea.</span><span class="sxs-lookup"><span data-stu-id="9085a-132">hello green LED flashes.</span></span>

1. <span data-ttu-id="9085a-133">Cuando vea un mensaje en el shell de hello ese controlador Hola descubrió hello SensorTag, tome nota de la dirección MAC del dispositivo de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="9085a-133">When you see a message in hello shell that hello controller has discovered hello SensorTag, make a note of hello MAC address of hello device.</span></span> <span data-ttu-id="9085a-134">Hola dirección MAC es similar a **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="9085a-134">hello MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="9085a-135">Necesita dirección MAC de hello más adelante en el tutorial Hola al configurar la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="9085a-135">You need hello MAC address later in hello tutorial when you configure hello gateway.</span></span>

1. <span data-ttu-id="9085a-136">Ejecute hello después tooturn comando desactivado el análisis de Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="9085a-136">Run hello following command tooturn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="9085a-137">Ejecute hello después tooverify de comandos que puede conectarse toohello SensorTag dispositivo:</span><span class="sxs-lookup"><span data-stu-id="9085a-137">Run hello following command tooverify that you can connect toohello SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="9085a-138">Si se conecta correctamente, el shell de hello muestra mensajes de bienvenida **conexión correcta** y se imprime información acerca del dispositivo de SensorTag Hola.</span><span class="sxs-lookup"><span data-stu-id="9085a-138">If you connect successfully, hello shell shows hello message **Connection successful** and prints information about hello SensorTag device.</span></span> <span data-ttu-id="9085a-139">Si no puede conectarse, compruebe hello que sensortag todavía está encendida.</span><span class="sxs-lookup"><span data-stu-id="9085a-139">If you cannot connect, check hello SensorTag is still powered on.</span></span>

1. <span data-ttu-id="9085a-140">Ahora puede desconectarse de hello SensorTag y ejecutar salir del shell de Bluetooth Hola Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="9085a-140">You can now disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="9085a-141">Crear el módulo personalizado de borde de IoT de Hola</span><span class="sxs-lookup"><span data-stu-id="9085a-141">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="9085a-142">Ahora puede compilar módulo IoT borde personalizado Hola que permite Hola puerta de enlace toosend mensajes toohello solución de supervisión.</span><span class="sxs-lookup"><span data-stu-id="9085a-142">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="9085a-143">Para obtener más información sobre cómo configurar una puerta de enlace y los módulos de IoT Edge, consulte [Conceptos de Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="9085a-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="9085a-144">Descargar código de fuente de Hola para módulos personalizados de borde de IoT de Hola desde GitHub con hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="9085a-144">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="9085a-145">Crear el módulo de IoT borde personalizado de hello mediante Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="9085a-145">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="9085a-146">script de compilación de Hello coloca módulo personalizado de borde de IoT de hello libsensor2remotemonitoring.so en la carpeta de compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9085a-146">hello build script places hello libsensor2remotemonitoring.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="9085a-147">Configurar y ejecutar Hola puerta de enlace de borde de IoT</span><span class="sxs-lookup"><span data-stu-id="9085a-147">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="9085a-148">Ahora puede configurar Hola telemetría de toosend de puerta de enlace de IoT borde de su tooyour de dispositivo SensorTag panel de supervisión remoto.</span><span class="sxs-lookup"><span data-stu-id="9085a-148">You can now configure hello IoT Edge gateway toosend telemetry from your SensorTag device tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="9085a-149">Para obtener más información sobre cómo configurar una puerta de enlace y los módulos de IoT Edge, consulte [Conceptos de Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="9085a-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="9085a-150">En este tutorial, utilice estándar hello `vi` editor de texto en hello NUC de Intel.</span><span class="sxs-lookup"><span data-stu-id="9085a-150">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="9085a-151">Si no ha usado `vi` antes, debe completar un tutorial introductorio, como [Unix - Hola vi Editor Tutorial] [ lnk-vi-tutorial] toofamiliarize usted mismo con este editor.</span><span class="sxs-lookup"><span data-stu-id="9085a-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="9085a-152">Como alternativa, puede instalar más fácil de usar hello [nano](https://www.nano-editor.org/) editor mediante el comando hello `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="9085a-152">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="9085a-153">Archivo de configuración de ejemplo de Hola abierto en hello **vi** editor mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="9085a-153">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="9085a-154">Busque Hola siguiendo las líneas en la configuración de hello para el módulo de hello el centro de IOT:</span><span class="sxs-lookup"><span data-stu-id="9085a-154">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="9085a-155">Reemplace el marcador de posición de hello valores con información de centro de IoT creado y guardado en Hola Hola inicio de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9085a-155">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="9085a-156">valor de Hola para IoTHubName es similar a **yourrmsolution37e08**, y valor hello IoTSuffix es normalmente **devices.net azure**.</span><span class="sxs-lookup"><span data-stu-id="9085a-156">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="9085a-157">Busque Hola siguiendo las líneas en la configuración de hello para el módulo de asignación de hello:</span><span class="sxs-lookup"><span data-stu-id="9085a-157">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="9085a-158">Reemplace hello **macAddress** marcador de posición con hello dirección MAC de su SensorTag se ha indicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9085a-158">Replace hello **macAddress** placeholder with hello MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="9085a-159">Reemplace hello **deviceID** y **deviceKey** marcadores de posición con identificadores de Hola y claves para dispositivos de hello dos que se creó anteriormente en la solución de supervisión remota Hola.</span><span class="sxs-lookup"><span data-stu-id="9085a-159">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="9085a-160">Busque Hola siguiendo las líneas en la configuración de hello para el módulo de Hola SensorTag:</span><span class="sxs-lookup"><span data-stu-id="9085a-160">Locate hello following lines in hello configuration for hello SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="9085a-161">Reemplace hello **dispositivo\_mac\_dirección** marcador de posición con hello dirección MAC de su SensorTag se ha indicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9085a-161">Replace hello **device\_mac\_address** placeholder  with hello MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="9085a-162">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="9085a-162">Save your changes.</span></span>

<span data-ttu-id="9085a-163">Ahora puede ejecutar la puerta de enlace de hello con hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="9085a-163">You can now run hello gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="9085a-164">Hola puerta de enlace de IoT borde comienza en hello NUC de Intel y envía la telemetría de hello SensorTag toohello solución de supervisión remota:</span><span class="sxs-lookup"><span data-stu-id="9085a-164">hello IoT Edge gateway starts on hello Intel NUC and sends telemetry from hello SensorTag toohello remote monitoring solution:</span></span>

![Puerta de enlace de IoT borde envía telemetría de hello SensorTag][img-telemetry]

<span data-ttu-id="9085a-166">Presione **Ctrl-C** programa Hola de tooexit en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="9085a-166">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="9085a-167">Vista Hola telemetría</span><span class="sxs-lookup"><span data-stu-id="9085a-167">View hello telemetry</span></span>

<span data-ttu-id="9085a-168">puerta de enlace de Hello ahora está enviando telemetría de hello SensorTag dispositivo toohello solución de supervisión.</span><span class="sxs-lookup"><span data-stu-id="9085a-168">hello gateway is now sending telemetry from hello SensorTag device toohello remote monitoring solution.</span></span> <span data-ttu-id="9085a-169">Puede ver la telemetría de hello en el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="9085a-169">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="9085a-170">También puede enviar el dispositivo de SensorTag tooyour de comandos a través de puerta de enlace de Hola desde el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="9085a-170">You can also send commands tooyour SensorTag device through hello gateway from hello solution dashboard.</span></span>

- <span data-ttu-id="9085a-171">Vaya a Panel de solución toohello.</span><span class="sxs-lookup"><span data-stu-id="9085a-171">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="9085a-172">Dispositivo Hola SELECT que configuró en la puerta de enlace de Hola que representa hello SensorTag Hola **tooView dispositivo** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="9085a-172">Select hello device you configured in hello gateway that represents hello SensorTag in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="9085a-173">telemetría Hello de dispositivo de SensorTag Hola se muestra en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="9085a-173">hello telemetry from hello SensorTag device displays on hello dashboard.</span></span>

![Mostrar la telemetría de hello SensorTag dispositivos][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="9085a-175">Si deja Hola supervisión de solución que se ejecuta en su cuenta de Azure remota, se le facturará por vez Hola que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="9085a-175">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="9085a-176">Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="9085a-176">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="9085a-177">Eliminar soluciones Hola preconfigurado de su cuenta de Azure cuando termine de usarlo.</span><span class="sxs-lookup"><span data-stu-id="9085a-177">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9085a-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9085a-178">Next steps</span></span>

<span data-ttu-id="9085a-179">Visite hello [centro de desarrollo de Azure IoT](https://azure.microsoft.com/develop/iot/) para obtener más ejemplos y documentación sobre IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="9085a-179">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started