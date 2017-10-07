---
title: "aaaGet comenzar con la administración de dispositivos del centro de IoT de Azure (nodo) | Documentos de Microsoft"
description: "Cómo toouse tooinitiate de administración de dispositivos de centro de IoT reiniciar un dispositivo remoto. Usar hello IoT de Azure SDK para Node.js tooimplement una aplicación de dispositivo simulado que incluye un método directo y una aplicación de servicio que invoca el método directo Hola."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: juanpere
ms.openlocfilehash: 5dd1878e71231850fb95f4170b823f1e86c3ee83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-node"></a>Introducción a la administración de dispositivos (Node)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

En este tutorial se muestra cómo realizar las siguientes acciones:

* Usar hello toocreate portal Azure un centro de IoT y cree una identidad de dispositivo en el centro de IoT.
* Crear una aplicación de dispositivo simulado que contiene un método directo que reinicia ese dispositivo. Se invocan métodos directos de nube de Hola.
* Crear una aplicación de consola de Node.js que llama a métodos directas de reinicio de hello en la aplicación de dispositivo simulado de hello a través de su centro de IoT.

Al final de Hola de este tutorial, tiene dos aplicaciones de consola de Node.js:

**dmpatterns_getstarted_device.js**, centro de IoT tooyour que conecta con la identidad del dispositivo Hola creado anteriormente, recibe un método directo de reinicio, simula reiniciar el equipo físico e informa Hola el tiempo de último reinicio de Hola.

**dmpatterns_getstarted_service.js**, que llama a un método directo en la aplicación de dispositivo simulado de hello, muestra la respuesta de Hola y Hola muestra actualizado notificado propiedades.

toocomplete este tutorial, necesita Hola siguientes:

* Node.js versión 0.12.x o posteriores. <br/>  [Preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall Node.js para este tutorial en Windows o Linux.
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Creación de una aplicación de dispositivo simulado
En esta sección:

* Crear una aplicación de consola de Node.js que responde tooa método directo llamado en la nube Hola
* Desencadenará un reinicio del dispositivo simulado.
* Hola uso notificado propiedades tooenable dispositivos gemelas consultas tooidentify dispositivos y cuándo reinició por última vez

1. Cree una nueva carpeta vacía denominada **manageddevice**.  Hola **manageddevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.  Acepte todos los valores predeterminados de hello:
   
    ```
    npm init
    ```
2. En el símbolo del sistema en hello **manageddevice** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure** paquete del SDK de dispositivo y **azure iot dispositivo-mqtt**paquete:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Con un editor de texto, cree un **dmpatterns_getstarted_device.js** archivo Hola **manageddevice** carpeta.
4. Agregar siguiente hello 'requiere' instrucciones al principio de Hola de hello **dmpatterns_getstarted_device.js** archivo:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Agregar un **connectionString** variable y utilizar toocreate un **cliente** instancia.  Reemplace la cadena de conexión de hello con la cadena de conexión del dispositivo.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Agregar Hola siguiendo métodos directas de función tooimplement hello en dispositivo Hola
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. Abrir el centro de IoT de hello conexión tooyour e iniciar el agente de escucha de hello método directo:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. Guarde y cierre hello **dmpatterns_getstarted_device.js** archivo.

> [!NOTE]
> tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento. En el código de producción, debe implementar directivas de reintento (por ejemplo, un retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios][lnk-transient-faults].

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Desencadenar un reinicio remoto en dispositivo Hola utilizando un método directo
En esta sección, creará una aplicación de consola de Node.js que inicia un reinicio remoto en un dispositivo mediante un método directo. aplicación Hello usa Hola de toodiscover de consultas última hora de reinicio de dispositivo gemelas para dicho dispositivo.

1. Cree una carpeta vacía denominada **triggerrebootondevice**.  Hola **triggerrebootondevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.  Acepte todos los valores predeterminados de hello:
   
    ```
    npm init
    ```
2. En el símbolo del sistema en hello **triggerrebootondevice** carpeta, ejecute hello después comando tooinstall hello **el centro de IOT de azure** paquete del SDK de dispositivo y **azure iot dispositivo-mqtt** paquete:
   
    ```
    npm install azure-iothub --save
    ```
3. Con un editor de texto, cree un **dmpatterns_getstarted_service.js** archivo Hola **triggerrebootondevice** carpeta.
4. Agregar siguiente hello 'requiere' instrucciones al principio de Hola de hello **dmpatterns_getstarted_service.js** archivo:
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. Agregue Hola siguiendo las declaraciones de variable y reemplace los valores de marcador de posición de hello:
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. Agregue Hola después de la función tooinvoke Hola dispositivo método tooreboot Hola dispositivo de destino:
   
    ```
    var startRebootDevice = function(twin) {
   
        var methodName = "reboot";
   
        var methodParams = {
            methodName: methodName,
            payload: null,
            timeoutInSeconds: 30
        };
   
        client.invokeDeviceMethod(deviceToReboot, methodParams, function(err, result) {
            if (err) { 
                console.error("Direct method error: "+err.message);
            } else {
                console.log("Successfully invoked hello device tooreboot.");  
            }
        });
    };
    ```
7. Agregar siguiente Hola función tooquery para dispositivo hello y obtener Hola última hora de reinicio:
   
    ```
    var queryTwinLastReboot = function() {
   
        registry.getTwin(deviceToReboot, function(err, twin){
   
            if (twin.properties.reported.iothubDM != null)
            {
                if (err) {
                    console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
                } else {
                    var lastRebootTime = twin.properties.reported.iothubDM.reboot.lastReboot;
                    console.log('Last reboot time: ' + JSON.stringify(lastRebootTime, null, 2));
                }
            } else 
                console.log('Waiting for device tooreport last reboot time.');
        });
    };
    ```
8. Agregue Hola siguiendo las funciones de código toocall Hola que desencadenan Hola reinicie método directo y consultar Hola reiniciar última hora:
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. Guarde y cierre hello **dmpatterns_getstarted_service.js** archivo.

## <a name="run-hello-apps"></a>Ejecutar aplicaciones de Hola
Ya estás listo toorun Hola aplicaciones.

1. En línea de comandos de Hola Hola **manageddevice** carpeta, ejecute hello después toobegin comando realizar escuchas de método directo de reinicio de Hola.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. En línea de comandos de Hola Hola **triggerrebootondevice** carpeta, ejecute hello después comando tootrigger Hola remoto de reinicio y de consulta de Hola de hello dispositivo gemelas toofind reiniciar última hora.
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. Consulte dispositivo respuesta toohello directo método hello en la consola de Hola.

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
