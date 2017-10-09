---
title: aaaGet a trabajar con el centro de IoT de Azure (nodo) | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosend dispositivo a la nube mensajes tooAzure centro de IoT con IoT SDK para Node.js. Crear dispositivo simulado y tooregister de aplicaciones de servicio, el dispositivo, enviar mensajes y leer los mensajes de centro de IoT."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0747895365f2359a9c38ea1e85a5881d6efec0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a>Conectar el centro de IoT de tooyour dispositivo simulado mediante el nodo
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Al final de Hola de este tutorial, tendrá tres aplicaciones de consola de Node.js:

* **CreateDeviceIdentity.js**, que crea una identidad de dispositivo y la clave de seguridad asociadas tooconnect la aplicación de dispositivo simulado.
* **ReadDeviceToCloudMessages.js**, que muestra la telemetría de hello enviado por la aplicación de dispositivo simulado.
* **SimulatedDevice.js**, que se conecta el centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente y envía un mensaje de telemetría cada segundo mediante Hola protocolo MQTT.

> [!NOTE]
> artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que puede usar ambos toorun aplicaciones toobuild en dispositivos y el back-end de soluciones.
> 
> 

toocomplete este tutorial, necesita Hola siguientes:

* Node.js versión 0.10.x, o posteriores.
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Ahora ha creado su instancia de IoT Hub. Dispone de nombre de host del centro de IoT de Hola y Hola cadena de conexión de centro de IoT que necesite que el resto de hello toocomplete de este tutorial.

## <a name="create-a-device-identity"></a>Creación de una identidad de dispositivo
En esta sección, creará una aplicación de consola de Node.js que crea una identidad de dispositivo en el registro de la identidad de hello en el centro de IoT. Un dispositivo solo puede conectarse tooIoT concentrador, si existe una entrada en el registro de la identidad de Hola. Para obtener más información, vea hello **del registro de identidad** sección de hello [Guía del desarrollador de centro de IoT][lnk-devguide-identity]. Al ejecutar esta aplicación de consola, se generará un identificador de dispositivo único y clave que el dispositivo pueda usar tooidentify propio cuando el dispositivo a la nube sitio envía mensajes tooIoT concentrador.

1. Cree una nueva carpeta vacía denominada **createdeviceidentity**. Hola **createdeviceidentity** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema. Acepte todos los valores predeterminados de hello:
   
    ```
    npm init
    ```
2. En el símbolo del sistema en hello **createdeviceidentity** carpeta, ejecute hello después comando tooinstall hello **el centro de IOT de azure** paquete SDK del servicio:
   
    ```
    npm install azure-iothub --save
    ```
3. Con un editor de texto, cree un **CreateDeviceIdentity.js** archivo Hola **createdeviceidentity** carpeta.
4. Agregue los siguiente hello `require` instrucción al principio de Hola de hello **CreateDeviceIdentity.js** archivo:
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. Agregar Hola después código toohello **CreateDeviceIdentity.js** archivo y reemplace el valor de marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola Hola: 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. Agregar Hola después código toocreate una definición de dispositivo en el registro de la identidad de hello en el centro de IoT. Este código crea un dispositivo si Hola Id. de dispositivo no existe en el registro de la identidad de hello, en caso contrario, devuelve clave hello de dispositivo de hello existente:
   
    ```
    var device = {
      deviceId: 'myFirstNodeDevice'
    }
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

7. Guarde y cierre el archivo **CreateDeviceIdentity.js** .
8. Hola toorun **createdeviceidentity** aplicación, ejecutar el siguiente comando en línea de comandos de hello en la carpeta de createdeviceidentity Hola de Hola:
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. Tome nota de hello **Id. de dispositivo** y **clave de dispositivo**. Necesita estos valores más tarde cuando se crea una aplicación que se conecta tooIoT concentrador como un dispositivo.

> [!NOTE]
> Hola del registro de identidad de centro de IoT solo almacena centro de IoT toohello de dispositivo identidades tooenable un acceso seguro. Toouse de identificadores y las claves de dispositivo almacena como credenciales de seguridad y una marca de habilitado/deshabilitado que puede usar acceso toodisable para un dispositivo individual. Si la aplicación necesita toostore otros metadatos específicos del dispositivo, debe usar un almacén específico de la aplicación. Para obtener más información, vea hello [Guía del desarrollador de centro de IoT][lnk-devguide-identity].
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a>Recepción de mensajes de dispositivo a nube
En esta sección, creará una aplicación de consola de Node.js que lee los mensajes de dispositivo a nube de IoT Hub. Un centro de IoT expone un [centros de eventos][lnk-event-hubs-overview]-extremo compatible tooenable tooread mensajes de dispositivo a la nube. tookeep cosas simples, en este tutorial se crea un lector básico que no es adecuado para una implementación de alto rendimiento. Hola [procesar mensajes del dispositivo a la nube] [ lnk-process-d2c-tutorial] tutorial muestra cómo los mensajes tooprocess dispositivo a la nube a escala. Hola [empezar a trabajar con concentradores de eventos] [ lnk-eventhubs-tutorial] tutorial proporciona información adicional acerca de cómo tooprocess mensajes desde los centros de eventos y es aplicable toohello los puntos de conexión compatibles con eventos de centro de IoT Hub.

> [!NOTE]
> Hola extremo compatible de concentrador de eventos para leer mensajes de dispositivo para la nube siempre utiliza Hola protocolo AMQP.
> 
> 

1. Cree una carpeta vacía denominada **readdevicetocloudmessages**. Hola **readdevicetocloudmessages** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema. Acepte todos los valores predeterminados de hello:
   
    ```
    npm init
    ```
2. En el símbolo del sistema en hello **readdevicetocloudmessages** carpeta, ejecute hello después comando tooinstall hello **centros de eventos de azure** paquete:
   
    ```
    npm install azure-event-hubs --save
    ```
3. Con un editor de texto, cree un **ReadDeviceToCloudMessages.js** archivo Hola **readdevicetocloudmessages** carpeta.
4. Agregue Hola siguiente `require` las instrucciones en hello inician de hello **ReadDeviceToCloudMessages.js** archivo:
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. Agregue Hola después de la declaración de variable y reemplace el valor de marcador de posición de hello con hello cadena de conexión de centro de IoT para el centro de:
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. Agregue Hola siguiendo dos funciones que la consola de toohello de salida de impresión:
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. Agregar Hola después Hola de código toocreate **EventHubClient**, abra Hola conexión tooyour centro de IoT y crear un receptor para cada partición. Esta aplicación utiliza un filtro cuando crea un receptor de modo que hello receptor solo lee los mensajes enviados tooIoT concentrador después de receptor de hello empieza a ejecutarse. Este filtro es útil en un entorno de prueba para ver solo Hola conjunto actual de mensajes. En un entorno de producción, el código debe asegurarse de que procesa todos los mensajes de saludo. Para obtener más información, vea hello [cómo tooprocess mensajes del dispositivo a la nube de centro de IoT] [ lnk-process-d2c-tutorial] tutorial:
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. Guarde y cierre hello **ReadDeviceToCloudMessages.js** archivo.

## <a name="create-a-simulated-device-app"></a>Creación de una aplicación de dispositivo simulado
En esta sección, creará una aplicación de consola de Node.js que simula un dispositivo que envía el centro de IoT tooan de mensajes del dispositivo a la nube.

1. Cree una carpeta vacía denominada **simulateddevice**. Hola **simulateddevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema. Acepte todos los valores predeterminados de hello:
   
    ```
    npm init
    ```
2. En el símbolo del sistema en hello **simulateddevice** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure** paquete del SDK de dispositivo y **azure iot dispositivo-mqtt**paquete:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Con un editor de texto, cree un **SimulatedDevice.js** archivo Hola **simulateddevice** carpeta.
4. Agregue Hola siguiente `require` las instrucciones en hello inician de hello **SimulatedDevice.js** archivo:
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. Agregar un **connectionString** variable y utilizar toocreate un **cliente** instancia. Reemplace **{youriothostname}** por nombre de hello del centro de IoT Hola creaste hello *crear un centro de IoT* sección. Reemplace **{yourdevicekey}** con hello dispositivo clave-valor que generó en hello *crear una identidad de dispositivo* sección:
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. Agregue Hola siguientes salida toodisplay de función de la aplicación hello:
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. Crear una devolución de llamada y usar hello **setInterval** función toosend un centro de IoT de mensaje tooyour cada segundo:
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
        // Create a message and send it toohello IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
8. Abra Hola conexión tooyour centro de IoT y empezar a enviar mensajes:
   
    ```
    client.open(connectCallback);
    ```
9. Guarde y cierre hello **SimulatedDevice.js** archivo.

> [!NOTE]
> tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento. En el código de producción, debe implementar directivas de reintento (por ejemplo, un retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios][lnk-transient-faults].
> 
> 

## <a name="run-hello-apps"></a>Ejecutar aplicaciones de Hola
Ya estás listo toorun Hola aplicaciones.

1. En un símbolo del sistema en hello **readdevicetocloudmessages** carpeta, ejecute hello después toobegin de comando su centro de IoT de supervisión:
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Mensajes dispositivo a la nube de toomonitor de aplicación de servicio de Node.js centro de IoT][7]
2. En un símbolo del sistema en hello **simulateddevice** carpeta, ejecute hello después toobegin comando Enviar centro de IoT de tooyour de datos de telemetría:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Mensajes de dispositivo para la nube de toosend aplicación de dispositivo de Node.js centro de IoT][8]
3. Hola **uso** el icono Servicios hello [portal de Azure] [ lnk-portal] muestra Hola número de mensajes enviados toohello centro de IoT:
   
    ![Azure portal uso icono que muestra el número de mensajes enviados tooIoT concentrador][43]

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola. Usar este dispositivo identidad tooenable Hola simulada dispositivos aplicación toosend mensajes del dispositivo a la nube toohello centro de IoT. También crea una aplicación que muestra los mensajes de saludo recibidos por centro de IoT Hola. 

toocontinue introducción con el centro de IoT y tooexplore otros escenarios de IoT, vea:

* [Conexión del dispositivo][lnk-connect-device]
* [Introducción a la administración de dispositivos][lnk-device-management]
* [Introducción a Azure IoT Edge][lnk-iot-edge]

toolearn tooextend mensajes de dispositivo a la nube de su solución y proceso de IoT a escala, vea hello [procesar mensajes del dispositivo a la nube] [ lnk-process-d2c-tutorial] tutorial.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]


<!-- Images. -->
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
