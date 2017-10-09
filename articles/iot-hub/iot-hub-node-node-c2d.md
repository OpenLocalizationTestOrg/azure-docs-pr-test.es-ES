---
title: mensajes de aaaCloud al dispositivo con el centro de IoT de Azure (nodo) | Documentos de Microsoft
description: "¿Cómo toosend en la nube al dispositivo mensajes tooa del dispositivo de un centro de IoT de Azure con hello Azure IoT SDK para Node.js. Modificar una aplicación de dispositivo simulado tooreceive los mensajes de nube al dispositivo y modificar un mensajes de aplicaciones back-end toosend hello en la nube al dispositivo."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3ca8a78f-ade2-46e8-8a49-d5d599cdf1f1
ms.service: iot-hub
ms.devlang: javascript
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 1ccae0cada52193c2abb91504c086cac226e93da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a>Envío de mensajes de nube a dispositivo con IoT Hub (Node)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>Introducción
IoT Hub de Azure es un servicio totalmente administrado que permite la comunicación bidireccional confiable y segura entre millones de dispositivos y una solución de back-end. Hola [empezar a trabajar con el centro de IoT] tutorial muestra cómo aprovisionar una identidad de dispositivo en el toocreate un centro de IoT y codificar una aplicación de dispositivo simulado que envía mensajes de dispositivo para la nube.

Este tutorial se basa en la [empezar a trabajar con el centro de IoT]. En él se muestra cómo realizar las siguientes acciones:

* Desde el back-end de soluciones, enviar mensajes en la nube al dispositivo tooa dispositivo a través del centro de IoT.
* Reciba mensajes de nube a dispositivo en un dispositivo.
* En el back-end de soluciones, solicitar confirmación de entrega (*comentarios*) para mensajes envían tooa dispositivo desde el centro de IoT.

Puede encontrar más información sobre los mensajes en la nube al dispositivo en hello [Guía del desarrollador de centro de IoT][IoT Hub developer guide - C2D].

Al final de Hola de este tutorial, ejecute dos aplicaciones de consola de Node.js:

* **SimulatedDevice**, una versión modificada de la aplicación hello creado en [empezar a trabajar con el centro de IoT], que se conecta el centro de IoT tooyour y recibe los mensajes de la nube al dispositivo.
* **SendCloudToDeviceMessage**, que envía una aplicación de dispositivo simulado de toohello de mensaje en la nube al dispositivo a través del centro de IoT y, a continuación, recibe la confirmación de entrega.

> [!NOTE]
> El Centro de IoT ofrece compatibilidad con el SDK en muchas plataformas de dispositivos y lenguajes (incluido C, Java y Javascript), mediante los SDK de dispositivos IoT de Azure. Para obtener instrucciones paso a paso sobre cómo tooconnect del su dispositivo toothis tutorial código y generalmente tooAzure centro de IoT, vea hello [Centro para desarrolladores de Azure IoT].
> 
> 

toocomplete este tutorial, necesita Hola siguientes:

* Node.js versión 0.10.x, o posteriores.
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

## <a name="receive-messages-in-hello-simulated-device-app"></a>Recibir mensajes en la aplicación de dispositivo simulado de hello
En esta sección, modificar aplicación de dispositivo simulado de Hola que creó en [empezar a trabajar con el centro de IoT] mensajes de nube al dispositivo tooreceive Hola centro de IoT.

1. Con un editor de texto, abra el archivo SimulatedDevice.js de hello.
2. Modificar hello **connectCallback** función toohandle los mensajes enviados desde el centro de IoT. En este ejemplo, el dispositivo de hello siempre invoca hello **completa** función toonotify centro de IoT que ha procesado el mensaje de bienvenida. La nueva versión de hello **connectCallback** función es parecida Hola siguiente fragmento de código:
   
    ```javascript
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
        client.on('message', function (msg) {
          console.log('Id: ' + msg.messageId + ' Body: ' + msg.data);
          client.complete(msg, printResultFor('completed'));
        });
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
   
   > [!NOTE]
   > Si utiliza HTTP como transporte de hello en lugar de MQTT o AMQP, Hola **DeviceClient** instancia comprueba si hay mensajes de centro de IoT con poca frecuencia (menor que cada 25 minutos). Para obtener más información acerca de las diferencias de hello entre soporte MQTT, AMQP y HTTP y la limitación de centro de IoT, vea hello [Guía del desarrollador de centro de IoT][IoT Hub developer guide - C2D].
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a>Envío de mensajes de nube a dispositivo
En esta sección, creará una aplicación de consola de Node.js que envía mensajes en la nube al dispositivo toohello del dispositivo simulado. Necesita Hola Id. de dispositivo del dispositivo de Hola que agregó en hello [empezar a trabajar con el centro de IoT] tutorial. También necesita Hola cadena de conexión de centro de IoT su base de datos central que se puede encontrar en hello [portal de Azure].

1. Cree una carpeta vacía denominada **sendcloudtodevicemessage**. Hola **sendcloudtodevicemessage** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema. Acepte todos los valores predeterminados de hello:
   
    ```shell
    npm init
    ```
2. En el símbolo del sistema en hello **sendcloudtodevicemessage** carpeta, ejecute hello después comando tooinstall hello **el centro de IOT de azure** paquete:
   
    ```shell
    npm install azure-iothub --save
    ```
3. Con un editor de texto, cree un **SendCloudToDeviceMessage.js** archivo Hola **sendcloudtodevicemessage** carpeta.
4. Agregue Hola siguiente `require` las instrucciones en hello inician de hello **SendCloudToDeviceMessage.js** archivo:
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. Agregar Hola sigue código demasiado**SendCloudToDeviceMessage.js** archivo. Reemplace el valor de marcador de posición de Hola "{iot hub cadena de conexión}" con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en Hola Hola [empezar a trabajar con el centro de IoT] tutorial. Reemplace el marcador de posición de Hola "{Id. de dispositivo}" con Id. de dispositivo de hello de dispositivo de Hola que agregó en hello [empezar a trabajar con el centro de IoT] tutorial:
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. Agregue Hola después de la consola de toohello de función tooprint operación resultados:
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. Agregue Hola después consola toohello de mensajes de comentarios de entrega de función tooprint:
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. Agregue código toosend un dispositivo de tooyour mensaje siguiente de Hola y controlar el mensaje de bienvenida de comentarios al dispositivo Hola confirma el mensaje de saludo en la nube al dispositivo:
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud toodevice message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. Guarde y cierre el archivo **SendCloudToDeviceMessage.js** .

## <a name="run-hello-applications"></a>Ejecutar aplicaciones de Hola
Ya estás listo toorun aplicaciones de Hola.

1. En línea de comandos de Hola Hola **simulateddevice** carpeta, ejecute hello siguiente comando toosend telemetría tooIoT concentrador y toolisten para los mensajes en la nube al dispositivo:
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Ejecutar la aplicación de dispositivo simulado de hello][img-simulated-device]
2. En un símbolo del sistema en hello **sendcloudtodevicemessage** carpeta, ejecute hello después comando toosend un mensaje en la nube al dispositivo y espere para comentarios de Hola confirmación:
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Ejecute el comando en la nube al dispositivo Hola de hello aplicación toosend][img-send-command]
   
   > [!NOTE]
   > Por simplificar, este tutorial no implementa ninguna directiva de reintentos. En el código de producción, debe implementar directivas de reintento (por ejemplo, retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios].
   > 
   > 

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, se habrá aprendido cómo toosend y recibir mensajes en la nube al dispositivo. 

ver ejemplos de toosee de soluciones completas de-to-end que usar el centro de IoT, consulte [Azure IoT Suite].

toolearn más sobre el desarrollo de soluciones con el centro de IoT, vea hello [Guía del desarrollador de centro de IoT].

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

[empezar a trabajar con el centro de IoT]: iot-hub-node-node-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[Guía del desarrollador de centro de IoT]: iot-hub-devguide.md
[Centro para desarrolladores de Azure IoT]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[control de errores transitorios]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[portal de Azure]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
