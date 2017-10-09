---
title: aaaSimulate un dispositivo con borde de IoT de Azure (Linux) | Documentos de Microsoft
description: "Cómo toouse borde de IoT de Azure en Linux toocreate un dispositivo simulado que envía telemetría a través de un borde de IoT centro de IoT tooan de puerta de enlace."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 11e7bf28-ee3d-48d6-a386-eb506c7a31cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: 168fb8eda8671d02c63073bdf36dfcd88b397fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-linux"></a><span data-ttu-id="88d2c-103">Usar mensajes de dispositivo a la nube de Azure IoT borde toosend con un dispositivo simulado (Linux)</span><span class="sxs-lookup"><span data-stu-id="88d2c-103">Use Azure IoT Edge toosend device-to-cloud messages with a simulated device (Linux)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="88d2c-104">¿Cómo toorun Hola ejemplo</span><span class="sxs-lookup"><span data-stu-id="88d2c-104">How toorun hello sample</span></span>

<span data-ttu-id="88d2c-105">Hola **build.sh** script genera su resultado en hello **generar** carpeta de la copia local de hello **iot borde** repositorio.</span><span class="sxs-lookup"><span data-stu-id="88d2c-105">hello **build.sh** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="88d2c-106">Este resultado incluye cuatro módulos de borde IoT Hola utilizados en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="88d2c-106">This output includes hello four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="88d2c-107">Hola lugares de la secuencia de comandos de compilación la:</span><span class="sxs-lookup"><span data-stu-id="88d2c-107">hello build script places the:</span></span>

* <span data-ttu-id="88d2c-108">**liblogger.SO** en hello **compilación/módulos/registrador** carpeta.</span><span class="sxs-lookup"><span data-stu-id="88d2c-108">**liblogger.so** in hello **build/modules/logger** folder.</span></span>
* <span data-ttu-id="88d2c-109">**libiothub.SO** en hello **compilación/módulos/el centro de IOT** carpeta.</span><span class="sxs-lookup"><span data-stu-id="88d2c-109">**libiothub.so** in hello **build/modules/iothub** folder.</span></span>
* <span data-ttu-id="88d2c-110">**lib\_identidad\_map.so** en hello **compilación/módulos/identitymap** carpeta.</span><span class="sxs-lookup"><span data-stu-id="88d2c-110">**lib\_identity\_map.so** in hello **build/modules/identitymap** folder.</span></span>
* <span data-ttu-id="88d2c-111">**libsimulated\_device.so** en hello **compilación/módulos/simuladas\_dispositivo** carpeta.</span><span class="sxs-lookup"><span data-stu-id="88d2c-111">**libsimulated\_device.so** in hello **build/modules/simulated\_device** folder.</span></span>

<span data-ttu-id="88d2c-112">Usar estas rutas de acceso para hello **ruta de acceso del módulo** valores tal y como se muestra en el siguiente archivo de configuración de JSON de hello:</span><span class="sxs-lookup"><span data-stu-id="88d2c-112">Use these paths for hello **module path** values as shown in hello following JSON settings file:</span></span>

<span data-ttu-id="88d2c-113">Hola simulado\_dispositivo\_nube\_cargar\_proceso de ejemplo toma el archivo de configuración de hello ruta de acceso tooa JSON como un argumento de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="88d2c-113">hello simulated\_device\_cloud\_upload\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="88d2c-114">siguiente archivo JSON de ejemplo Hola se proporciona una en el repositorio SDK de hello en **ejemplos\\simulada\_dispositivo\_nube\_cargar\_ejemplo\\src\\ simulada\_dispositivo\_nube\_cargar\_ejemplo\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="88d2c-114">hello following example JSON file is provided in hello SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_lin.json**.</span></span> <span data-ttu-id="88d2c-115">Este archivo de configuración funciona tal cual a menos que modifique Hola compilar hello de la secuencia de comandos tooplace IoT borde módulos o archivos ejecutables en ubicaciones no predeterminadas de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="88d2c-115">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="88d2c-116">las rutas de acceso del módulo de Hello son toohello relativa directorio desde donde se ejecuta Hola simulado\_dispositivo\_nube\_cargar\_ejecutable de ejemplo, no es directorio Hola donde se encuentra el ejecutable de Hola.</span><span class="sxs-lookup"><span data-stu-id="88d2c-116">hello module paths are relative toohello directory from where you run hello simulated\_device\_cloud\_upload\_sample executable, not hello directory where hello executable is located.</span></span> <span data-ttu-id="88d2c-117">archivo de configuración de JSON de ejemplo de Hola tiene como valor predeterminado toowriting too'deviceCloudUploadGatewaylog.log' en el directorio de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="88d2c-117">hello sample JSON configuration file defaults toowriting too'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="88d2c-118">En un editor de texto, abra el archivo hello **ejemplos/simuladas\_dispositivo\_nube\_cargar\_ejemplo/src/simuladas\_dispositivo\_nube\_cargar\_lin.json** en su copia local de hello **iot borde** repositorio.</span><span class="sxs-lookup"><span data-stu-id="88d2c-118">In a text editor, open hello file **samples/simulated\_device\_cloud\_upload\_sample/src/simulated\_device\_cloud\_upload\_lin.json** in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="88d2c-119">Este archivo configura los módulos de hello borde IoT de puerta de enlace de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="88d2c-119">This file configures hello IoT Edge modules in hello sample gateway:</span></span>

* <span data-ttu-id="88d2c-120">Hola **el centro de IOT** módulo conecta el centro de IoT tooyour.</span><span class="sxs-lookup"><span data-stu-id="88d2c-120">hello **IoTHub** module connects tooyour IoT hub.</span></span> <span data-ttu-id="88d2c-121">Configurar centro de IoT de toosend datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="88d2c-121">You configure it toosend data tooyour IoT hub.</span></span> <span data-ttu-id="88d2c-122">En concreto, un conjunto de hello **IoTHubName** toohello nombre de su centro de IoT de valor y establecer hello **IoTHubSuffix** valor demasiado**devices.net azure**.</span><span class="sxs-lookup"><span data-stu-id="88d2c-122">Specifically, set hello **IoTHubName** value toohello name of your IoT hub and set hello **IoTHubSuffix** value too**azure-devices.net**.</span></span> <span data-ttu-id="88d2c-123">Conjunto hello **transporte** tooone de valor de: **HTTP**, **AMQP**, o **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="88d2c-123">Set hello **Transport** value tooone of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="88d2c-124">Actualmente, solo **HTTP** comparte una conexión TCP para todos los mensajes de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="88d2c-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="88d2c-125">Si establece el valor de hello demasiado**AMQP**, o **MQTT**, puerta de enlace de hello mantiene una tooIoT de conexión TCP concentrador independiente para cada dispositivo.</span><span class="sxs-lookup"><span data-stu-id="88d2c-125">If you set hello value too**AMQP**, or **MQTT**, hello gateway maintains a separate TCP connection tooIoT Hub for each device.</span></span>
* <span data-ttu-id="88d2c-126">Hola **asignación** módulo asigna las direcciones MAC de los identificadores de dispositivo simulado dispositivos tooyour centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="88d2c-126">hello **mapping** module maps hello MAC addresses of your simulated devices tooyour IoT Hub device ids.</span></span> <span data-ttu-id="88d2c-127">Asegúrese de que **deviceId** Hola identificadores de coincidencia de valores de hello dos dispositivos agregados que hello y centro de IoT tooyour **deviceKey** valores contienen las claves de Hola de los dos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="88d2c-127">Make sure that **deviceId** values match hello ids of hello two devices you added tooyour IoT hub, and that hello **deviceKey** values contain hello keys of your two devices.</span></span>
* <span data-ttu-id="88d2c-128">Hola **BLE1** y **BLE2** módulos son dispositivos de hello simulada.</span><span class="sxs-lookup"><span data-stu-id="88d2c-128">hello **BLE1** and **BLE2** modules are hello simulated devices.</span></span> <span data-ttu-id="88d2c-129">Tenga en cuenta cómo su MAC aborda coincidencia Hola direcciones en hello **asignación** módulo.</span><span class="sxs-lookup"><span data-stu-id="88d2c-129">Note how their MAC addresses match hello addresses in hello **mapping** module.</span></span>
* <span data-ttu-id="88d2c-130">Hola **registrador** módulo registra el archivo de tooa de actividad de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="88d2c-130">hello **Logger** module logs your gateway activity tooa file.</span></span>
* <span data-ttu-id="88d2c-131">Hola **ruta de acceso del módulo** valores que se muestran en el ejemplo de Hola supongamos que ejecuta el ejemplo de Hola de hello **generar** carpeta de la copia local de hello **iot borde** repositorio.</span><span class="sxs-lookup"><span data-stu-id="88d2c-131">hello **module path** values shown in hello example assume that you run hello sample from hello **build** folder in your local copy of hello **iot-edge** repository.</span></span>
* <span data-ttu-id="88d2c-132">Hola **vínculos** matriz final Hola de archivo JSON de hello conecta hello **BLE1** y **BLE2** módulos toohello **asignación** hello y módulo **asignación** módulo toohello **el centro de IOT** módulo.</span><span class="sxs-lookup"><span data-stu-id="88d2c-132">hello **links** array at hello bottom of hello JSON file connects hello **BLE1** and **BLE2** modules toohello **mapping** module, and hello **mapping** module toohello **IoTHub** module.</span></span> <span data-ttu-id="88d2c-133">También garantiza que todos los mensajes se registran de forma hello **registrador** módulo.</span><span class="sxs-lookup"><span data-stu-id="88d2c-133">It also ensures that all messages are logged by hello **Logger** module.</span></span>

```json
{
    "modules": [
        {
            "name": "IotHub",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/iothub/libiothub.so"
            }
            },
            "args": {
              "IoTHubName": "<<insert here IoTHubName>>",
              "IoTHubSuffix": "<<insert here IoTHubSuffix>>",
              "Transport": "HTTP"
            }
          },
        {
            "name": "mapping",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/identitymap/libidentity_map.so"
            }
            },
            "args": [
              {
                "macAddress": "01:01:01:01:01:01",
                "deviceId": "<<insert here deviceId>>",
                "deviceKey": "<<insert here deviceKey>>"
              },
              {
                "macAddress": "02:02:02:02:02:02",
                "deviceId": "<<insert here deviceId>>",
                "deviceKey": "<<insert here deviceKey>>"
              }
            ]
          },
        {
            "name": "BLE1",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/simulated_device/libsimulated_device.so"
            }
            },
            "args": {
              "macAddress": "01:01:01:01:01:01"
            }
          },
        {
            "name": "BLE2",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/simulated_device/libsimulated_device.so"
            }
            },
            "args": {
              "macAddress": "02:02:02:02:02:02"
            }
          },
        {
            "name": "Logger",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args": {
              "filename": "deviceCloudUploadGatewaylog.log"
            }
          }
    ],
    "links": [
        {
            "source": "*",
            "sink": "Logger"
        },
        {
            "source": "BLE1",
            "sink": "mapping"
        },
        {
            "source": "BLE2",
            "sink": "mapping"
        },
        {
            "source": "mapping",
            "sink": "IotHub"
        }
    ]
}
```

<span data-ttu-id="88d2c-134">Guardar los cambios de hello realiza toohello archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="88d2c-134">Save hello changes you made toohello configuration file.</span></span>

<span data-ttu-id="88d2c-135">ejemplo de Hola a toorun:</span><span class="sxs-lookup"><span data-stu-id="88d2c-135">toorun hello sample:</span></span>

1. <span data-ttu-id="88d2c-136">En el shell, navegue toohello **iot-borde/compilación** carpeta.</span><span class="sxs-lookup"><span data-stu-id="88d2c-136">In your shell, navigate toohello **iot-edge/build** folder.</span></span>
2. <span data-ttu-id="88d2c-137">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="88d2c-137">Run hello following command:</span></span>
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. <span data-ttu-id="88d2c-138">Puede usar hello [explorador del dispositivo] [ lnk-device-explorer] o [el centro de IOT explorador] [ lnk-iothub-explorer] herramienta mensajes de saludo de toomonitor centro de IoT recibe de Hola puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="88d2c-138">You can use hello [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool toomonitor hello messages that IoT hub receives from hello gateway.</span></span> <span data-ttu-id="88d2c-139">Por ejemplo, mediante el centro de IOT explorador puede supervisar mensajes de dispositivo a la nube mediante el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="88d2c-139">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="88d2c-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="88d2c-140">Next steps</span></span>

<span data-ttu-id="88d2c-141">toogain conocimientos avanzados de borde de IoT de Azure y experimento con algunos ejemplos de código, visite siguiente de hello tutoriales de desarrollador y recursos:</span><span class="sxs-lookup"><span data-stu-id="88d2c-141">toogain a more advanced understanding of Azure IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="88d2c-142">[Envío de mensajes de un dispositivo físico a la nube con Azure IoT Edge][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="88d2c-142">[Send device-to-cloud messages from a physical device with Azure IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="88d2c-143">[Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="88d2c-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="88d2c-144">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="88d2c-144">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="88d2c-145">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="88d2c-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="88d2c-146">[Proteger la solución de IoT de hello masa][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="88d2c-146">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
