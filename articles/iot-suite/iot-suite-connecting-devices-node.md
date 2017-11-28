---
title: "Conexión de un dispositivo mediante Node.js | Microsoft Docs"
description: "Se describe cómo conectar un dispositivo a la solución de supervisión remota preconfigurada del Conjunto de IoT de Azure mediante una aplicación creada en Node.js."
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
ms.openlocfilehash: 6459b6196eb7f4a083b67e5a421bcc0d51d39e5c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-nodejs"></a><span data-ttu-id="cae72-103">Conectar el dispositivo a la solución preconfigurada de supervisión remota (Node.js)</span><span class="sxs-lookup"><span data-stu-id="cae72-103">Connect your device to the remote monitoring preconfigured solution (Node.js)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a><span data-ttu-id="cae72-104">Creación de una solución de ejemplo de node.js</span><span class="sxs-lookup"><span data-stu-id="cae72-104">Create a node.js sample solution</span></span>

<span data-ttu-id="cae72-105">Asegúrese de que tiene instalada la versión 0.11.5 o posterior de Node.js en la máquina de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="cae72-105">Ensure that Node.js version 0.11.5 or later is installed on your development machine.</span></span> <span data-ttu-id="cae72-106">Para comprobar la versión, puede ejecutar `node --version` en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="cae72-106">You can run `node --version` at the command line to check the version.</span></span>

1. <span data-ttu-id="cae72-107">Cree una carpeta denominada **RemoteMonitoring** en la máquina de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="cae72-107">Create a folder called **RemoteMonitoring** on your development machine.</span></span> <span data-ttu-id="cae72-108">Vaya a esta carpeta en el entorno de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="cae72-108">Navigate to this folder in your command-line environment.</span></span>

1. <span data-ttu-id="cae72-109">Ejecute los comandos siguientes para descargar e instalar los paquetes que necesita para realizar la aplicación de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cae72-109">Run the following commands to download and install the packages you need to complete the sample app:</span></span>

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="cae72-110">En la carpeta **RemoteMonitoring**, cree un archivo llamado **remote_monitoring.js**.</span><span class="sxs-lookup"><span data-stu-id="cae72-110">In the **RemoteMonitoring** folder, create a file called **remote_monitoring.js**.</span></span> <span data-ttu-id="cae72-111">Abra este archivo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="cae72-111">Open this file in a text editor.</span></span>

1. <span data-ttu-id="cae72-112">En el archivo **remote_monitoring.js**, agregue las siguientes instrucciones `require`:</span><span class="sxs-lookup"><span data-stu-id="cae72-112">In the **remote_monitoring.js** file, add the following `require` statements:</span></span>

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. <span data-ttu-id="cae72-113">Agregue las siguientes declaraciones de variable después de las instrucciones `require` .</span><span class="sxs-lookup"><span data-stu-id="cae72-113">Add the following variable declarations after the `require` statements.</span></span> <span data-ttu-id="cae72-114">Sustituya los valores de marcador de posición [Device Id] y [Device Key] por los valores que anotó para el dispositivo en el panel de la solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="cae72-114">Replace the placeholder values [Device Id] and [Device Key] with values you noted for your device in the remote monitoring solution dashboard.</span></span> <span data-ttu-id="cae72-115">Use el nombre de host de IoT Hub en el panel de la solución para sustituir [IoTHub Name].</span><span class="sxs-lookup"><span data-stu-id="cae72-115">Use the IoT Hub Hostname from the solution dashboard to replace [IoTHub Name].</span></span> <span data-ttu-id="cae72-116">Por ejemplo, si el nombre de host de IoT Hub es **contoso.azure-devices.net**, sustituya [IoTHub Name] por **contoso**:</span><span class="sxs-lookup"><span data-stu-id="cae72-116">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. <span data-ttu-id="cae72-117">Agregue las siguientes variables para definir algunos datos de telemetría de base:</span><span class="sxs-lookup"><span data-stu-id="cae72-117">Add the following variables to define some base telemetry data:</span></span>

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. <span data-ttu-id="cae72-118">Agregue la función auxiliar siguiente para imprimir los resultados de la operación:</span><span class="sxs-lookup"><span data-stu-id="cae72-118">Add the following helper function to print operation results:</span></span>

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. <span data-ttu-id="cae72-119">Agregue la siguiente función auxiliar para aleatorizar los valores de telemetría:</span><span class="sxs-lookup"><span data-stu-id="cae72-119">Add the following helper function to use to randomize the telemetry values:</span></span>

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. <span data-ttu-id="cae72-120">Agregue la siguiente definición para el objeto **DeviceInfo** que envía el dispositivo al inicio:</span><span class="sxs-lookup"><span data-stu-id="cae72-120">Add the following definition for the **DeviceInfo** object the device sends on startup:</span></span>

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

1. <span data-ttu-id="cae72-121">Agregue la siguiente definición para los valores notificados por el dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="cae72-121">Add the following definition for the device twin reported values.</span></span> <span data-ttu-id="cae72-122">Esta definición incluye descripciones de los métodos directos que admite el dispositivo:</span><span class="sxs-lookup"><span data-stu-id="cae72-122">This definition includes descriptions of the direct methods the device supports:</span></span>

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
            "Reboot": "Reboot the device",
            "InitiateFirmwareUpdate--FwPackageURI-string": "Updates device Firmware. Use parameter FwPackageURI to specifiy the URI of the firmware file"
        },
    }
    ```

1. <span data-ttu-id="cae72-123">Agregue la siguiente función para controlar la llamada al método directo **Reboot**:</span><span class="sxs-lookup"><span data-stu-id="cae72-123">Add the following function to handle the **Reboot** direct method call:</span></span>

    ```nodejs
    function onReboot(request, response) {
        // Implement actual logic here.
        console.log('Simulated reboot...');

        // Complete the response
        response.send(200, "Rebooting device", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```

1. <span data-ttu-id="cae72-124">Agregue la siguiente función para controlar la llamada al método directo **InitiateFirmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="cae72-124">Add the following function to handle the **InitiateFirmwareUpdate** direct method call.</span></span> <span data-ttu-id="cae72-125">Este método directo usa un parámetro para especificar la ubicación de la imagen de firmware que se va a descargar e inicia la actualización de firmware en el dispositivo de forma asincrónica:</span><span class="sxs-lookup"><span data-stu-id="cae72-125">This direct method uses a parameter to specify the location of the firmware image to download, and initiates the firmware update on the device asynchronously:</span></span>

    ```nodejs
    function onInitiateFirmwareUpdate(request, response) {
        console.log('Simulated firmware update initiated, using: ' + request.payload.FwPackageURI);

        // Complete the response
        response.send(200, "Firmware update initiated", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });

        // Add logic here to perform the firmware update asynchronously
    }
    ```

1. <span data-ttu-id="cae72-126">Agregue el código siguiente para crear una instancia de cliente:</span><span class="sxs-lookup"><span data-stu-id="cae72-126">Add the following code to create a client instance:</span></span>

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="cae72-127">Agregue el siguiente código para:</span><span class="sxs-lookup"><span data-stu-id="cae72-127">Add the following code to:</span></span>

    * <span data-ttu-id="cae72-128">Abrir la conexión.</span><span class="sxs-lookup"><span data-stu-id="cae72-128">Open the connection.</span></span>
    * <span data-ttu-id="cae72-129">Enviar el objeto **DeviceInfo**.</span><span class="sxs-lookup"><span data-stu-id="cae72-129">Send the **DeviceInfo** object.</span></span>
    * <span data-ttu-id="cae72-130">Configurar un controlador para propiedades deseadas.</span><span class="sxs-lookup"><span data-stu-id="cae72-130">Set up a handler for desired properties.</span></span>
    * <span data-ttu-id="cae72-131">Enviar propiedades notificadas.</span><span class="sxs-lookup"><span data-stu-id="cae72-131">Send reported properties.</span></span>
    * <span data-ttu-id="cae72-132">Registrar controladores para métodos directos.</span><span class="sxs-lookup"><span data-stu-id="cae72-132">Register handlers for the direct methods.</span></span>
    * <span data-ttu-id="cae72-133">Empezar a enviar telemetría.</span><span class="sxs-lookup"><span data-stu-id="cae72-133">Start sending telemetry.</span></span>

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

1. <span data-ttu-id="cae72-134">Guarde los cambios al archivo **remote_monitoring.js**.</span><span class="sxs-lookup"><span data-stu-id="cae72-134">Save the changes to the **remote_monitoring.js** file.</span></span>

1. <span data-ttu-id="cae72-135">Ejecute el siguiente comando en un símbolo del sistema para iniciar la aplicación de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cae72-135">Run the following command at a command prompt to launch the sample application:</span></span>
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
