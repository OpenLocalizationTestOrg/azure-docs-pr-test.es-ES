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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a>Conectar su toohello de dispositivo remoto de supervisión de solución preconfigurada (Node.js)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a>Creación de una solución de ejemplo de node.js

Asegúrese de que tiene instalada la versión 0.11.5 o posterior de Node.js en la máquina de desarrollo. Puede ejecutar `node --version` en la versión de Hola de toocheck de línea de comandos de Hola.

1. Cree una carpeta denominada **RemoteMonitoring** en la máquina de desarrollo. Desplazarse por las carpetas de toothis en su entorno de línea de comandos.

1. Hola ejecución sigue comandos toodownload e instalar paquetes de hello necesita la aplicación de ejemplo de Hola toocomplete:

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. Hola **RemoteMonitoring** carpeta, cree un archivo denominado **remote_monitoring.js**. Abra este archivo en un editor de texto.

1. Hola **remote_monitoring.js** , agregue la siguiente hello `require` instrucciones:

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. Agregar Hola siguiendo las declaraciones de variable después de hello `require` instrucciones. Reemplace los valores de marcador de posición de hello [Id. de dispositivo] y [clave de dispositivo] con los valores indicados para el dispositivo en el panel de solución de supervisión remota de Hola. Usar hello Hostname del centro de IoT de hello solución panel tooreplace [el centro de IOT Name]. Por ejemplo, si el nombre de host de IoT Hub es **contoso.azure-devices.net**, sustituya [IoTHub Name] por **contoso**:

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. Agregue Hola siguientes variables toodefine algunos datos de telemetría de base:

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. Agregue Hola siguiendo los resultados de la operación de la función auxiliar tooprint:

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. Agregue Hola después de valores de telemetría de aplicación auxiliar para la función toouse toorandomize hello:

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. Agregar Hola después de la definición de hello **DeviceInfo** dispositivo Hola de objeto se envía en el inicio:

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

1. Agregue los siguiente Hola definición doble de dispositivo de hello notificado valores. Esta definición incluye descripciones de los métodos directos Hola Hola dispositivo admite:

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

1. Agregar Hola después Hola de función toohandle **reiniciar** dirigir la llamada al método:

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

1. Agregar Hola después Hola de función toohandle **InitiateFirmwareUpdate** dirigir la llamada al método. Este método directo utiliza una ubicación de Hola de parámetro toospecify de toodownload de imagen de firmware de Hola e inicia Hola actualización de firmware en el dispositivo de Hola de forma asincrónica:

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

1. Agregue Hola después código toocreate una instancia de cliente:

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. Agregue Hola siguiente de código:

    * Abrir conexión Hola.
    * Enviar hello **DeviceInfo** objeto.
    * Configurar un controlador para propiedades deseadas.
    * Enviar propiedades notificadas.
    * Registrar los controladores para los métodos de hello directa.
    * Empezar a enviar telemetría.

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

1. Guardar Hola cambios toohello **remote_monitoring.js** archivo.

1. Ejecute hello siguiente comando en una aplicación de ejemplo de Hola de toolaunch de símbolo del sistema:
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
