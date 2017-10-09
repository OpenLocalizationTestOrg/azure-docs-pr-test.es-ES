---
title: aaaConnect un dispositivo con Node.js | Documentos de Microsoft
description: "Describe cómo tooconnect una toohello dispositivo Azure IoT conjunto preconfigurado solución de supervisión remota con una aplicación escrita en Node.js."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: fc50a33f-9fb9-42d7-b1b8-eb5cff19335e
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 80bf2b70f15f539bfce4f135d533c46dd2b3f5a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a><span data-ttu-id="6ab34-103">Conectar su toohello de dispositivo remoto de supervisión de solución preconfigurada (Node.js)</span><span class="sxs-lookup"><span data-stu-id="6ab34-103">Connect your device toohello remote monitoring preconfigured solution (Node.js)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a><span data-ttu-id="6ab34-104">Creación de una solución de ejemplo de node.js</span><span class="sxs-lookup"><span data-stu-id="6ab34-104">Create a node.js sample solution</span></span>

<span data-ttu-id="6ab34-105">Asegúrese de que tiene instalada la versión 0.11.5 o posterior de Node.js en la máquina de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="6ab34-105">Ensure that Node.js version 0.11.5 or later is installed on your development machine.</span></span> <span data-ttu-id="6ab34-106">Puede ejecutar `node --version` en la versión de Hola de toocheck de línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6ab34-106">You can run `node --version` at hello command line toocheck hello version.</span></span>

1. <span data-ttu-id="6ab34-107">Cree una carpeta denominada **RemoteMonitoring** en la máquina de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="6ab34-107">Create a folder called **RemoteMonitoring** on your development machine.</span></span> <span data-ttu-id="6ab34-108">Desplazarse por las carpetas de toothis en su entorno de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="6ab34-108">Navigate toothis folder in your command-line environment.</span></span>

1. <span data-ttu-id="6ab34-109">Hola ejecución sigue comandos toodownload e instalar paquetes de hello necesita la aplicación de ejemplo de Hola toocomplete:</span><span class="sxs-lookup"><span data-stu-id="6ab34-109">Run hello following commands toodownload and install hello packages you need toocomplete hello sample app:</span></span>

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="6ab34-110">Hola **RemoteMonitoring** carpeta, cree un archivo denominado **remote_monitoring.js**.</span><span class="sxs-lookup"><span data-stu-id="6ab34-110">In hello **RemoteMonitoring** folder, create a file called **remote_monitoring.js**.</span></span> <span data-ttu-id="6ab34-111">Abra este archivo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="6ab34-111">Open this file in a text editor.</span></span>

1. <span data-ttu-id="6ab34-112">Hola **remote_monitoring.js** , agregue la siguiente hello `require` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="6ab34-112">In hello **remote_monitoring.js** file, add hello following `require` statements:</span></span>

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. <span data-ttu-id="6ab34-113">Agregar Hola siguiendo las declaraciones de variable después de hello `require` instrucciones.</span><span class="sxs-lookup"><span data-stu-id="6ab34-113">Add hello following variable declarations after hello `require` statements.</span></span> <span data-ttu-id="6ab34-114">Reemplace los valores de marcador de posición de hello [Id. de dispositivo] y [clave de dispositivo] con los valores indicados para el dispositivo en el panel de solución de supervisión remota de Hola.</span><span class="sxs-lookup"><span data-stu-id="6ab34-114">Replace hello placeholder values [Device Id] and [Device Key] with values you noted for your device in hello remote monitoring solution dashboard.</span></span> <span data-ttu-id="6ab34-115">Usar hello Hostname del centro de IoT de hello solución panel tooreplace [el centro de IOT Name].</span><span class="sxs-lookup"><span data-stu-id="6ab34-115">Use hello IoT Hub Hostname from hello solution dashboard tooreplace [IoTHub Name].</span></span> <span data-ttu-id="6ab34-116">Por ejemplo, si el nombre de host de IoT Hub es **contoso.azure-devices.net**, sustituya [IoTHub Name] por **contoso**:</span><span class="sxs-lookup"><span data-stu-id="6ab34-116">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. <span data-ttu-id="6ab34-117">Agregue Hola siguientes variables toodefine algunos datos de telemetría de base:</span><span class="sxs-lookup"><span data-stu-id="6ab34-117">Add hello following variables toodefine some base telemetry data:</span></span>

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. <span data-ttu-id="6ab34-118">Agregue Hola siguiendo los resultados de la operación de la función auxiliar tooprint:</span><span class="sxs-lookup"><span data-stu-id="6ab34-118">Add hello following helper function tooprint operation results:</span></span>

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. <span data-ttu-id="6ab34-119">Agregue Hola después de valores de telemetría de aplicación auxiliar para la función toouse toorandomize hello:</span><span class="sxs-lookup"><span data-stu-id="6ab34-119">Add hello following helper function toouse toorandomize hello telemetry values:</span></span>

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. <span data-ttu-id="6ab34-120">Agregar Hola después de la definición de hello **DeviceInfo** dispositivo Hola de objeto se envía en el inicio:</span><span class="sxs-lookup"><span data-stu-id="6ab34-120">Add hello following definition for hello **DeviceInfo** object hello device sends on startup:</span></span>

    ```nodejs
    var deviceMetaData = {
        'ObjectType': 'DeviceInfo',
        'IsSimulatedDevice': 0,
        'Version': '1.0',
        'DeviceProperties': {
            'DeviceID': deviceId,
            'HubEnabledState': 1
        }
    };
    ```

1. <span data-ttu-id="6ab34-121">Agregue los siguiente Hola definición doble de dispositivo de hello notificado valores.</span><span class="sxs-lookup"><span data-stu-id="6ab34-121">Add hello following definition for hello device twin reported values.</span></span> <span data-ttu-id="6ab34-122">Esta definición incluye descripciones de los métodos directos Hola Hola dispositivo admite:</span><span class="sxs-lookup"><span data-stu-id="6ab34-122">This definition includes descriptions of hello direct methods hello device supports:</span></span>

    ```nodejs
    var reportedProperties = {
        "Device": {
            "DeviceState": "normal",
            "Location": {
                "Latitude": 47.642877,
                "Longitude": -122.125497
            }
        },
        "Config": {
            "TemperatureMeanValue": 56.7,
            "TelemetryInterval": 45
        },
        "System": {
            "Manufacturer": "Contoso Inc.",
            "FirmwareVersion": "2.22",
            "InstalledRAM": "8 MB",
            "ModelNumber": "DB-14",
            "Platform": "Plat 9.75",
            "Processor": "i3-9",
            "SerialNumber": "SER99"
        },
        "Location": {
            "Latitude": 47.642877,
            "Longitude": -122.125497
        },
        "SupportedMethods": {
            "Reboot": "Reboot hello device",
            "InitiateFirmwareUpdate--FwPackageURI-string": "Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file"
        },
    }
    ```

1. <span data-ttu-id="6ab34-123">Agregar Hola después Hola de función toohandle **reiniciar** dirigir la llamada al método:</span><span class="sxs-lookup"><span data-stu-id="6ab34-123">Add hello following function toohandle hello **Reboot** direct method call:</span></span>

    ```nodejs
    function onReboot(request, response) {
        // Implement actual logic here.
        console.log('Simulated reboot...');

        // Complete hello response
        response.send(200, "Rebooting device", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```

1. <span data-ttu-id="6ab34-124">Agregar Hola después Hola de función toohandle **InitiateFirmwareUpdate** dirigir la llamada al método.</span><span class="sxs-lookup"><span data-stu-id="6ab34-124">Add hello following function toohandle hello **InitiateFirmwareUpdate** direct method call.</span></span> <span data-ttu-id="6ab34-125">Este método directo utiliza una ubicación de Hola de parámetro toospecify de toodownload de imagen de firmware de Hola e inicia Hola actualización de firmware en el dispositivo de Hola de forma asincrónica:</span><span class="sxs-lookup"><span data-stu-id="6ab34-125">This direct method uses a parameter toospecify hello location of hello firmware image toodownload, and initiates hello firmware update on hello device asynchronously:</span></span>

    ```nodejs
    function onInitiateFirmwareUpdate(request, response) {
        console.log('Simulated firmware update initiated, using: ' + request.payload.FwPackageURI);

        // Complete hello response
        response.send(200, "Firmware update initiated", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });

        // Add logic here tooperform hello firmware update asynchronously
    }
    ```

1. <span data-ttu-id="6ab34-126">Agregue Hola después código toocreate una instancia de cliente:</span><span class="sxs-lookup"><span data-stu-id="6ab34-126">Add hello following code toocreate a client instance:</span></span>

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="6ab34-127">Agregue Hola siguiente de código:</span><span class="sxs-lookup"><span data-stu-id="6ab34-127">Add hello following code to:</span></span>

    * <span data-ttu-id="6ab34-128">Abrir conexión Hola.</span><span class="sxs-lookup"><span data-stu-id="6ab34-128">Open hello connection.</span></span>
    * <span data-ttu-id="6ab34-129">Enviar hello **DeviceInfo** objeto.</span><span class="sxs-lookup"><span data-stu-id="6ab34-129">Send hello **DeviceInfo** object.</span></span>
    * <span data-ttu-id="6ab34-130">Configurar un controlador para propiedades deseadas.</span><span class="sxs-lookup"><span data-stu-id="6ab34-130">Set up a handler for desired properties.</span></span>
    * <span data-ttu-id="6ab34-131">Enviar propiedades notificadas.</span><span class="sxs-lookup"><span data-stu-id="6ab34-131">Send reported properties.</span></span>
    * <span data-ttu-id="6ab34-132">Registrar los controladores para los métodos de hello directa.</span><span class="sxs-lookup"><span data-stu-id="6ab34-132">Register handlers for hello direct methods.</span></span>
    * <span data-ttu-id="6ab34-133">Empezar a enviar telemetría.</span><span class="sxs-lookup"><span data-stu-id="6ab34-133">Start sending telemetry.</span></span>

    ```nodejs
    client.open(function (err) {
        if (err) {
            printErrorFor('open')(err);
        } else {
            console.log('Sending device metadata:\n' + JSON.stringify(deviceMetaData));
            client.sendEvent(new Message(JSON.stringify(deviceMetaData)), printErrorFor('send metadata'));

            // Create device twin
            client.getTwin(function(err, twin) {
                if (err) {
                    console.error('Could not get device twin');
                } else {
                    console.log('Device twin created');

                    twin.on('properties.desired', function(delta) {
                        console.log('Received new desired properties:');
                        console.log(JSON.stringify(delta));
                    });

                    // Send reported properties
                    twin.properties.reported.update(reportedProperties, function(err) {
                        if (err) throw err;
                        console.log('twin state reported');
                    });

                    // Register handlers for direct methods
                    client.onDeviceMethod('Reboot', onReboot);
                    client.onDeviceMethod('InitiateFirmwareUpdate', onInitiateFirmwareUpdate);
                }
            });

            // Start sending telemetry
            var sendInterval = setInterval(function () {
                temperature += generateRandomIncrement();
                externalTemperature += generateRandomIncrement();
                humidity += generateRandomIncrement();

                var data = JSON.stringify({
                    'DeviceID': deviceId,
                    'Temperature': temperature,
                    'Humidity': humidity,
                    'ExternalTemperature': externalTemperature
                });

                console.log('Sending device event data:\n' + data);
                client.sendEvent(new Message(data), printErrorFor('send event'));
            }, 5000);

            client.on('error', function (err) {
                printErrorFor('client')(err);
                if (sendInterval) clearInterval(sendInterval);
                client.close(printErrorFor('client.close'));
            });
        }
    });
    ```

1. <span data-ttu-id="6ab34-134">Guardar Hola cambios toohello **remote_monitoring.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="6ab34-134">Save hello changes toohello **remote_monitoring.js** file.</span></span>

1. <span data-ttu-id="6ab34-135">Ejecute hello siguiente comando en una aplicación de ejemplo de Hola de toolaunch de símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="6ab34-135">Run hello following command at a command prompt toolaunch hello sample application:</span></span>
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
