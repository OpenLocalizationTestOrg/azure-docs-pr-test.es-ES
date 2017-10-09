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
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="674e0-104">Envío de mensajes de nube a dispositivo con IoT Hub (Node)</span><span class="sxs-lookup"><span data-stu-id="674e0-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="674e0-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="674e0-105">Introduction</span></span>
<span data-ttu-id="674e0-106">IoT Hub de Azure es un servicio totalmente administrado que permite la comunicación bidireccional confiable y segura entre millones de dispositivos y una solución de back-end.</span><span class="sxs-lookup"><span data-stu-id="674e0-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="674e0-107">Hola [empezar a trabajar con el centro de IoT] tutorial muestra cómo aprovisionar una identidad de dispositivo en el toocreate un centro de IoT y codificar una aplicación de dispositivo simulado que envía mensajes de dispositivo para la nube.</span><span class="sxs-lookup"><span data-stu-id="674e0-107">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="674e0-108">Este tutorial se basa en la [empezar a trabajar con el centro de IoT].</span><span class="sxs-lookup"><span data-stu-id="674e0-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="674e0-109">En él se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="674e0-109">It shows you how to:</span></span>

* <span data-ttu-id="674e0-110">Desde el back-end de soluciones, enviar mensajes en la nube al dispositivo tooa dispositivo a través del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="674e0-110">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="674e0-111">Reciba mensajes de nube a dispositivo en un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="674e0-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="674e0-112">En el back-end de soluciones, solicitar confirmación de entrega (*comentarios*) para mensajes envían tooa dispositivo desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="674e0-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="674e0-113">Puede encontrar más información sobre los mensajes en la nube al dispositivo en hello [Guía del desarrollador de centro de IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="674e0-113">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="674e0-114">Al final de Hola de este tutorial, ejecute dos aplicaciones de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="674e0-114">At hello end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="674e0-115">**SimulatedDevice**, una versión modificada de la aplicación hello creado en [empezar a trabajar con el centro de IoT], que se conecta el centro de IoT tooyour y recibe los mensajes de la nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="674e0-115">**SimulatedDevice**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="674e0-116">**SendCloudToDeviceMessage**, que envía una aplicación de dispositivo simulado de toohello de mensaje en la nube al dispositivo a través del centro de IoT y, a continuación, recibe la confirmación de entrega.</span><span class="sxs-lookup"><span data-stu-id="674e0-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="674e0-117">El Centro de IoT ofrece compatibilidad con el SDK en muchas plataformas de dispositivos y lenguajes (incluido C, Java y Javascript), mediante los SDK de dispositivos IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="674e0-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="674e0-118">Para obtener instrucciones paso a paso sobre cómo tooconnect del su dispositivo toothis tutorial código y generalmente tooAzure centro de IoT, vea hello [Centro para desarrolladores de Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="674e0-118">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="674e0-119">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="674e0-119">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="674e0-120">Node.js versión 0.10.x, o posteriores.</span><span class="sxs-lookup"><span data-stu-id="674e0-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="674e0-121">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="674e0-121">An active Azure account.</span></span> <span data-ttu-id="674e0-122">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="674e0-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="674e0-123">Recibir mensajes en la aplicación de dispositivo simulado de hello</span><span class="sxs-lookup"><span data-stu-id="674e0-123">Receive messages in hello simulated device app</span></span>
<span data-ttu-id="674e0-124">En esta sección, modificar aplicación de dispositivo simulado de Hola que creó en [empezar a trabajar con el centro de IoT] mensajes de nube al dispositivo tooreceive Hola centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="674e0-124">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="674e0-125">Con un editor de texto, abra el archivo SimulatedDevice.js de hello.</span><span class="sxs-lookup"><span data-stu-id="674e0-125">Using a text editor, open hello SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="674e0-126">Modificar hello **connectCallback** función toohandle los mensajes enviados desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="674e0-126">Modify hello **connectCallback** function toohandle messages sent from IoT Hub.</span></span> <span data-ttu-id="674e0-127">En este ejemplo, el dispositivo de hello siempre invoca hello **completa** función toonotify centro de IoT que ha procesado el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="674e0-127">In this example, hello device always invokes hello **complete** function toonotify IoT Hub that it has processed hello message.</span></span> <span data-ttu-id="674e0-128">La nueva versión de hello **connectCallback** función es parecida Hola siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="674e0-128">Your new version of hello **connectCallback** function looks like hello following snippet:</span></span>
   
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
   > <span data-ttu-id="674e0-129">Si utiliza HTTP como transporte de hello en lugar de MQTT o AMQP, Hola **DeviceClient** instancia comprueba si hay mensajes de centro de IoT con poca frecuencia (menor que cada 25 minutos).</span><span class="sxs-lookup"><span data-stu-id="674e0-129">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="674e0-130">Para obtener más información acerca de las diferencias de hello entre soporte MQTT, AMQP y HTTP y la limitación de centro de IoT, vea hello [Guía del desarrollador de centro de IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="674e0-130">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="674e0-131">Envío de mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="674e0-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="674e0-132">En esta sección, creará una aplicación de consola de Node.js que envía mensajes en la nube al dispositivo toohello del dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="674e0-132">In this section, you create a Node.js console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="674e0-133">Necesita Hola Id. de dispositivo del dispositivo de Hola que agregó en hello [empezar a trabajar con el centro de IoT] tutorial.</span><span class="sxs-lookup"><span data-stu-id="674e0-133">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="674e0-134">También necesita Hola cadena de conexión de centro de IoT su base de datos central que se puede encontrar en hello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="674e0-134">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="674e0-135">Cree una carpeta vacía denominada **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="674e0-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="674e0-136">Hola **sendcloudtodevicemessage** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="674e0-136">In hello **sendcloudtodevicemessage** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="674e0-137">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="674e0-137">Accept all hello defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="674e0-138">En el símbolo del sistema en hello **sendcloudtodevicemessage** carpeta, ejecute hello después comando tooinstall hello **el centro de IOT de azure** paquete:</span><span class="sxs-lookup"><span data-stu-id="674e0-138">At your command prompt in hello **sendcloudtodevicemessage** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="674e0-139">Con un editor de texto, cree un **SendCloudToDeviceMessage.js** archivo Hola **sendcloudtodevicemessage** carpeta.</span><span class="sxs-lookup"><span data-stu-id="674e0-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in hello **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="674e0-140">Agregue Hola siguiente `require` las instrucciones en hello inician de hello **SendCloudToDeviceMessage.js** archivo:</span><span class="sxs-lookup"><span data-stu-id="674e0-140">Add hello following `require` statements at hello start of hello **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="674e0-141">Agregar Hola sigue código demasiado**SendCloudToDeviceMessage.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="674e0-141">Add hello following code too**SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="674e0-142">Reemplace el valor de marcador de posición de Hola "{iot hub cadena de conexión}" con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en Hola Hola [empezar a trabajar con el centro de IoT] tutorial.</span><span class="sxs-lookup"><span data-stu-id="674e0-142">Replace hello "{iot hub connection string}" placeholder value with hello IoT Hub connection string for hello hub you created in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="674e0-143">Reemplace el marcador de posición de Hola "{Id. de dispositivo}" con Id. de dispositivo de hello de dispositivo de Hola que agregó en hello [empezar a trabajar con el centro de IoT] tutorial:</span><span class="sxs-lookup"><span data-stu-id="674e0-143">Replace hello "{device id}" placeholder with hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="674e0-144">Agregue Hola después de la consola de toohello de función tooprint operación resultados:</span><span class="sxs-lookup"><span data-stu-id="674e0-144">Add hello following function tooprint operation results toohello console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="674e0-145">Agregue Hola después consola toohello de mensajes de comentarios de entrega de función tooprint:</span><span class="sxs-lookup"><span data-stu-id="674e0-145">Add hello following function tooprint delivery feedback messages toohello console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="674e0-146">Agregue código toosend un dispositivo de tooyour mensaje siguiente de Hola y controlar el mensaje de bienvenida de comentarios al dispositivo Hola confirma el mensaje de saludo en la nube al dispositivo:</span><span class="sxs-lookup"><span data-stu-id="674e0-146">Add hello following code toosend a message tooyour device and handle hello feedback message when hello device acknowledges hello cloud-to-device message:</span></span>
   
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
9. <span data-ttu-id="674e0-147">Guarde y cierre el archivo **SendCloudToDeviceMessage.js** .</span><span class="sxs-lookup"><span data-stu-id="674e0-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="674e0-148">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="674e0-148">Run hello applications</span></span>
<span data-ttu-id="674e0-149">Ya estás listo toorun aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="674e0-149">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="674e0-150">En línea de comandos de Hola Hola **simulateddevice** carpeta, ejecute hello siguiente comando toosend telemetría tooIoT concentrador y toolisten para los mensajes en la nube al dispositivo:</span><span class="sxs-lookup"><span data-stu-id="674e0-150">At hello command prompt in hello **simulateddevice** folder, run hello following command toosend telemetry tooIoT Hub and toolisten for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Ejecutar la aplicación de dispositivo simulado de hello][img-simulated-device]
2. <span data-ttu-id="674e0-152">En un símbolo del sistema en hello **sendcloudtodevicemessage** carpeta, ejecute hello después comando toosend un mensaje en la nube al dispositivo y espere para comentarios de Hola confirmación:</span><span class="sxs-lookup"><span data-stu-id="674e0-152">At a command prompt in hello **sendcloudtodevicemessage** folder, run hello following command toosend a cloud-to-device message and wait for hello acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Ejecute el comando en la nube al dispositivo Hola de hello aplicación toosend][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="674e0-154">Por simplificar, este tutorial no implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="674e0-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="674e0-155">En el código de producción, debe implementar directivas de reintento (por ejemplo, retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios].</span><span class="sxs-lookup"><span data-stu-id="674e0-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="674e0-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="674e0-156">Next steps</span></span>
<span data-ttu-id="674e0-157">En este tutorial, se habrá aprendido cómo toosend y recibir mensajes en la nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="674e0-157">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="674e0-158">ver ejemplos de toosee de soluciones completas de-to-end que usar el centro de IoT, consulte [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="674e0-158">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="674e0-159">toolearn más sobre el desarrollo de soluciones con el centro de IoT, vea hello [Guía del desarrollador de centro de IoT].</span><span class="sxs-lookup"><span data-stu-id="674e0-159">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

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
