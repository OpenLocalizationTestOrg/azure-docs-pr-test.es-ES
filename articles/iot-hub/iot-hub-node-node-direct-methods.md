---
title: "Centro de IoT aaaAzure dirigir métodos (nodo) | Documentos de Microsoft"
description: "¿Cómo toouse centro de IoT de Azure dirigir métodos. Utilice hello Azure IoT SDK para Node.js tooimplement una aplicación de dispositivo simulado que incluye un método directo y una aplicación de servicio que invoca el método directo Hola."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ea9c73ca-7778-4e38-a8f1-0bee9d142f04
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12300ba451816fec1f80163b633f6b6e411d9e5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a>Uso de métodos directos en el dispositivo IoT con Node.js
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

Al final de Hola de este tutorial, tiene dos aplicaciones de consola de Node.js:

* **CallMethodOnDevice.js**, que llama a un método de aplicación de dispositivo simulado de hello y se muestra la respuesta de Hola.
* **SimulatedDevice.js**, que se conecta el centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente y responde método toohello llamado a nube Hola.

> [!NOTE]
> artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que puede usar ambos toorun aplicaciones toobuild en dispositivos y el back-end de soluciones.
> 
> 

toocomplete este tutorial, necesita Hola siguientes:

* Node.js versión 0.10.x, o posteriores.
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Creación de una aplicación de dispositivo simulado
En esta sección, creará una aplicación de consola de Node.js que responde el método tooa llamado a nube Hola.

1. Cree una nueva carpeta vacía denominada **simulateddevice**. Hola **simulateddevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema. Acepte todos los valores predeterminados de hello:
   
    ```
    npm init
    ```
2. En el símbolo del sistema en hello **simulateddevice** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure** paquete del SDK de dispositivo y **azure iot dispositivo-mqtt**paquete:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Con un editor de texto, cree un nuevo **SimulatedDevice.js** archivo Hola **simulateddevice** carpeta.
4. Agregue Hola siguiente `require` las instrucciones en hello inician de hello **SimulatedDevice.js** archivo:
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. Agregar un **connectionString** variable y utilizar toocreate un **DeviceClient** instancia. Reemplace **{cadena de conexión de dispositivo}** con cadena de conexión de dispositivo de Hola que generó en hello *crear una identidad de dispositivo* sección:
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. Agregue Hola después de método de función tooimplement hello en dispositivo hello:
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Abrir el centro de IoT de hello conexión tooyour e iniciar el agente de escucha de inicializar Hola método:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. Guarde y cierre hello **SimulatedDevice.js** archivo.

> [!NOTE]
> tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento. En el código de producción, debe implementar directivas de reintento (por ejemplo, los reintentos de conexión), tal como se sugiere en el artículo MSDN de hello [control de errores transitorios][lnk-transient-faults].
> 
> 

## <a name="call-a-method-on-a-device"></a>Llamada a un método de un dispositivo
En esta sección, creará una aplicación de consola de Node.js que llama a un método de aplicación de dispositivo simulado de hello y, a continuación, muestra la respuesta de Hola.

1. Cree una nueva carpeta vacía denominada **callmethodondevice**. Hola **callmethodondevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema. Acepte todos los valores predeterminados de hello:
   
    ```
    npm init
    ```
2. En el símbolo del sistema en hello **callmethodondevice** carpeta, ejecute hello después comando tooinstall hello **el centro de IOT de azure** paquete:
   
    ```
    npm install azure-iothub --save
    ```
3. Con un editor de texto, cree un **CallMethodOnDevice.js** archivo Hola **callmethodondevice** carpeta.
4. Agregue Hola siguiente `require` las instrucciones en hello inician de hello **CallMethodOnDevice.js** archivo:
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. Agregue Hola después de la declaración de variable y reemplace el valor de marcador de posición de hello con hello cadena de conexión de centro de IoT para el centro de:
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. Crear centro de IoT tooyour de hello cliente tooopen Hola conexión.
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. Agregue Hola después de la función tooinvoke Hola método e impresión Hola dispositivo respuesta toohello consola del dispositivo:
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed tooinvoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. Guarde y cierre hello **CallMethodOnDevice.js** archivo.

## <a name="run-hello-apps"></a>Ejecutar aplicaciones de Hola
Ya estás listo toorun Hola aplicaciones.

1. En un símbolo del sistema en hello **simulateddevice** carpeta, ejecute hello después de realizar escuchas para las llamadas de método desde el centro de IoT de toostart de comando:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. En un símbolo del sistema en hello **callmethodondevice** carpeta, ejecute hello después toobegin de comando su centro de IoT de supervisión:
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. Podrá ver Hola dispositivo reaccionar toohello método por aplicación hello denominadas respuesta de hello método mostrar hello de dispositivo de Hola y el mensaje de bienvenida de la impresión:
   
    ![][9]

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola. Utiliza este toomethods dispositivo identidad tooenable Hola simulada dispositivos aplicación tooreact invocado por la nube de Hola. También crea una aplicación que invoca los métodos en el dispositivo de Hola y muestra la respuesta de hello de dispositivo de Hola. 

toocontinue introducción con el centro de IoT y tooexplore otros escenarios de IoT, vea:

* [Introducción al Centro de IoT]
* [Programación de trabajos en varios dispositivos][lnk-devguide-jobs]

toolearn cómo tooextend llama a su método de programación y de solución de IoT en varios dispositivos, vea hello [programación y los trabajos de difusión] [ lnk-tutorial-jobs] tutorial.

<!-- Images. -->
[7]: ./media/iot-hub-node-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-node-node-direct-methods/run-callmethodondevice.png
[9]: ./media/iot-hub-node-node-direct-methods/methods-output.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Introducción al Centro de IoT]: iot-hub-node-node-getstarted.md
