---
title: "Simulación de un dispositivo con Azure IoT Edge (Linux) | Documentos de Microsoft"
description: "Describe cómo usar Azure IoT Edge en Linux para crear un dispositivo simulado que envíe datos de telemetría a través de una puerta de enlace de IoT Edge a un centro de IoT Hub."
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
ms.openlocfilehash: 5349960373ae6815862c5f79a69dd6d5d9d624ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-to-send-device-to-cloud-messages-with-a-simulated-device-linux"></a><span data-ttu-id="e3ba8-103">Uso de Azure IoT Edge para enviar mensajes de dispositivo a nube con un dispositivo simulado (Linux)</span><span class="sxs-lookup"><span data-stu-id="e3ba8-103">Use Azure IoT Edge to send device-to-cloud messages with a simulated device (Linux)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="e3ba8-104">Ejecución del ejemplo</span><span class="sxs-lookup"><span data-stu-id="e3ba8-104">How to run the sample</span></span>

<span data-ttu-id="e3ba8-105">El script **build.sh** genera su salida en la carpeta **build** de la copia local del repositorio **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-105">The **build.sh** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="e3ba8-106">Esta salida incluye los cuatro módulos de IoT Edge utilizados en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-106">This output includes the four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="e3ba8-107">El script de compilación coloca:</span><span class="sxs-lookup"><span data-stu-id="e3ba8-107">The build script places the:</span></span>

* <span data-ttu-id="e3ba8-108">**liblogger.so** en la carpeta **build/modules/logger**.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-108">**liblogger.so** in the **build/modules/logger** folder.</span></span>
* <span data-ttu-id="e3ba8-109">**libiothub.so** en la carpeta **build/modules/iothub**.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-109">**libiothub.so** in the **build/modules/iothub** folder.</span></span>
* <span data-ttu-id="e3ba8-110">**lib\_identity\_map.so** en la carpeta **build/modules/identitymap**.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-110">**lib\_identity\_map.so** in the **build/modules/identitymap** folder.</span></span>
* <span data-ttu-id="e3ba8-111">**libsimulated\_device.so** en la carpeta **build/modules/simulated\_device**.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-111">**libsimulated\_device.so** in the **build/modules/simulated\_device** folder.</span></span>

<span data-ttu-id="e3ba8-112">Utilice estas rutas de acceso para los valores de **ruta de acceso del módulo**, tal y como se muestra en el archivo de configuración JSON siguiente:</span><span class="sxs-lookup"><span data-stu-id="e3ba8-112">Use these paths for the **module path** values as shown in the following JSON settings file:</span></span>

<span data-ttu-id="e3ba8-113">El proceso de simulated\_device\_cloud\_upload\_sample toma la ruta de acceso a un archivo de configuración JSON como argumento de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-113">The simulated\_device\_cloud\_upload\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="e3ba8-114">El siguiente archivo JSON de ejemplo se proporciona en el repositorio de SDK en **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-114">The following example JSON file is provided in the SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_lin.json**.</span></span> <span data-ttu-id="e3ba8-115">Este archivo de configuración funcionará tal y como está, a menos que se modifique el script de compilación para colocar los módulos de IoT Edge o los ejecutables de ejemplo en ubicaciones que no sean las predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-115">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="e3ba8-116">Las rutas de acceso del módulo son relativas al directorio en donde se inicia el archivo ejecutable simulated\_device\_cloud\_upload\_sample, no al directorio donde se encuentra el archivo ejecutable.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-116">The module paths are relative to the directory from where you run the simulated\_device\_cloud\_upload\_sample executable, not the directory where the executable is located.</span></span> <span data-ttu-id="e3ba8-117">De manera predeterminada, el archivo de configuración JSON de ejemplo escribe en "deviceCloudUploadGatewaylog.log" en el directorio de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-117">The sample JSON configuration file defaults to writing to 'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="e3ba8-118">En un editor de texto, abra el archivo **samples/simulated\_device\_cloud\_upload\_sample/src/simulated\_device\_cloud\_upload\_lin.json** en la copia local del repositorio **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-118">In a text editor, open the file **samples/simulated\_device\_cloud\_upload\_sample/src/simulated\_device\_cloud\_upload\_lin.json** in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="e3ba8-119">Este archivo configura los módulos de IoT Edge en la puerta de enlace de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e3ba8-119">This file configures the IoT Edge modules in the sample gateway:</span></span>

* <span data-ttu-id="e3ba8-120">El módulo **IoTHub** conecta con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-120">The **IoTHub** module connects to your IoT hub.</span></span> <span data-ttu-id="e3ba8-121">Debe configurarlo para enviar datos a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-121">You configure it to send data to your IoT hub.</span></span> <span data-ttu-id="e3ba8-122">En concreto, establezca el valor **IoTHubName** en el nombre de IoT Hub y el valor **IoTHubSuffix** en **azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-122">Specifically, set the **IoTHubName** value to the name of your IoT hub and set the **IoTHubSuffix** value to **azure-devices.net**.</span></span> <span data-ttu-id="e3ba8-123">Establezca el valor **Transport** en uno de los siguientes: **HTTP**, **AMQP** o **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-123">Set the **Transport** value to one of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="e3ba8-124">Actualmente, solo **HTTP** comparte una conexión TCP para todos los mensajes de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="e3ba8-125">Si establece el valor en **AMQP** o **MQTT**, la puerta de enlace mantendrá una conexión TCP independiente con IoT Hub para cada dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-125">If you set the value to **AMQP**, or **MQTT**, the gateway maintains a separate TCP connection to IoT Hub for each device.</span></span>
* <span data-ttu-id="e3ba8-126">El módulo **mapping** asigna las direcciones MAC de los dispositivos simulados a los identificadores de dispositivo de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-126">The **mapping** module maps the MAC addresses of your simulated devices to your IoT Hub device ids.</span></span> <span data-ttu-id="e3ba8-127">Asegúrese de que los valores **deviceId** coincidan con los identificadores de los dos dispositivos agregados a su centro de IoT y que los valores **deviceKey** contengan las claves de los dos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-127">Make sure that **deviceId** values match the ids of the two devices you added to your IoT hub, and that the **deviceKey** values contain the keys of your two devices.</span></span>
* <span data-ttu-id="e3ba8-128">Los módulos **BLE1** y **BLE2** son los dispositivos simulados.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-128">The **BLE1** and **BLE2** modules are the simulated devices.</span></span> <span data-ttu-id="e3ba8-129">Observe cómo las direcciones MAC coinciden con las del módulo de **asignación**.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-129">Note how their MAC addresses match the addresses in the **mapping** module.</span></span>
* <span data-ttu-id="e3ba8-130">El módulo **Registrador** registra la actividad de puerta de enlace en un archivo.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-130">The **Logger** module logs your gateway activity to a file.</span></span>
* <span data-ttu-id="e3ba8-131">Los valores de **ruta de acceso del módulo** que se muestran en el ejemplo dan por hecho que ejecuta el ejemplo desde la carpeta **build** de la copia local del repositorio **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-131">The **module path** values shown in the example assume that you run the sample from the **build** folder in your local copy of the **iot-edge** repository.</span></span>
* <span data-ttu-id="e3ba8-132">La matriz **links** de la parte inferior del archivo JSON conecta los módulos **BLE1** y **BLE2** al módulo de **asignación** y el módulo de **asignación** al módulo **IoTHub**.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-132">The **links** array at the bottom of the JSON file connects the **BLE1** and **BLE2** modules to the **mapping** module, and the **mapping** module to the **IoTHub** module.</span></span> <span data-ttu-id="e3ba8-133">También garantiza que el módulo **Registrador** registre todos los mensajes.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-133">It also ensures that all messages are logged by the **Logger** module.</span></span>

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

<span data-ttu-id="e3ba8-134">Guarde los cambios realizados en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-134">Save the changes you made to the configuration file.</span></span>

<span data-ttu-id="e3ba8-135">Para ejecutar el ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e3ba8-135">To run the sample:</span></span>

1. <span data-ttu-id="e3ba8-136">En el shell, vaya a la carpeta **iot-edge/build**.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-136">In your shell, navigate to the **iot-edge/build** folder.</span></span>
2. <span data-ttu-id="e3ba8-137">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e3ba8-137">Run the following command:</span></span>
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. <span data-ttu-id="e3ba8-138">Puede usar la herramienta [Explorador de dispositivos][lnk-device-explorer] o [iothub-explorer][lnk-iothub-explorer] para supervisar los mensajes que la instancia de IoT Hub recibe de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="e3ba8-138">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to monitor the messages that IoT hub receives from the gateway.</span></span> <span data-ttu-id="e3ba8-139">Por ejemplo, mediante iothub-explorer, puede supervisar los mensajes del dispositivo a la nube con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="e3ba8-139">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="e3ba8-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e3ba8-140">Next steps</span></span>

<span data-ttu-id="e3ba8-141">Para obtener una descripción más avanzada de Azure IoT Edge y experimentar con algunos ejemplos de código, consulte los siguientes tutoriales y recursos para desarrolladores:</span><span class="sxs-lookup"><span data-stu-id="e3ba8-141">To gain a more advanced understanding of Azure IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="e3ba8-142">[Envío de mensajes de un dispositivo físico a la nube con Azure IoT Edge][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="e3ba8-142">[Send device-to-cloud messages from a physical device with Azure IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="e3ba8-143">[Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="e3ba8-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="e3ba8-144">Para explorar aún más las funcionalidades de IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="e3ba8-144">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="e3ba8-145">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="e3ba8-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="e3ba8-146">[Protección total de la solución de IoT][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="e3ba8-146">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
