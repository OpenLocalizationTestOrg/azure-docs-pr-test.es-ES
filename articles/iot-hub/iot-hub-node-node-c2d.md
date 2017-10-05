---
title: Mensajes de nube a dispositivo con IoT Hub de Azure (Node) | Microsoft Docs
description: "Cómo enviar mensajes de nube a un dispositivo de una instancia de IoT Hub de Azure mediante los SDK de IoT de Azure para Node.js. Modifique una aplicación de dispositivo simulado para recibir mensajes de nube a dispositivo y cambie una aplicación de back-end para enviar los mensajes de nube a dispositivo."
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
ms.openlocfilehash: 4580bda5633f84a7c7af0dc85f3cea4951024836
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="13886-104">Envío de mensajes de nube a dispositivo con IoT Hub (Node)</span><span class="sxs-lookup"><span data-stu-id="13886-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="13886-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="13886-105">Introduction</span></span>
<span data-ttu-id="13886-106">IoT Hub de Azure es un servicio totalmente administrado que permite la comunicación bidireccional confiable y segura entre millones de dispositivos y una solución de back-end.</span><span class="sxs-lookup"><span data-stu-id="13886-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="13886-107">El tutorial [Introducción a Iot Hub] muestra cómo crear un centro de IoT, aprovisionar la identidad de un dispositivo en él y codificar una aplicación de dispositivo simulado que envía mensajes de dispositivo a nube.</span><span class="sxs-lookup"><span data-stu-id="13886-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="13886-108">Este tutorial se basa en la [Introducción a Iot Hub].</span><span class="sxs-lookup"><span data-stu-id="13886-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="13886-109">En él se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="13886-109">It shows you how to:</span></span>

* <span data-ttu-id="13886-110">Desde el back-end de la nube de la aplicación, envíe mensajes de nube a dispositivo en un único dispositivo a través de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="13886-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="13886-111">Reciba mensajes de nube a dispositivo en un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="13886-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="13886-112">Desde el back-end de la nube de la aplicación, solicite confirmación de entrega (*comentarios*) para los mensajes enviados a un dispositivo desde IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="13886-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="13886-113">Encontrará más información sobre los mensajes de nube a dispositivo en la [Guía para desarrolladores de IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="13886-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="13886-114">Al final de este tutorial, ejecutará dos aplicaciones de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="13886-114">At the end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="13886-115">**SimulatedDevice**, versión modificada de la aplicación creada en [Introducción a Iot Hub], que se conecta al Centro de IoT y recibe mensajes de nube a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="13886-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="13886-116">**SendCloudToDeviceMessage**, que envía un mensaje de la nube a la aplicación de dispositivo simulado mediante IoT Hub y, luego, recibe su confirmación de entrega.</span><span class="sxs-lookup"><span data-stu-id="13886-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="13886-117">El Centro de IoT ofrece compatibilidad con el SDK en muchas plataformas de dispositivos y lenguajes (incluido C, Java y Javascript), mediante los SDK de dispositivos IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="13886-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="13886-118">Visite el [Centro para desarrolladores de IoT de Azure]para obtener instrucciones paso a paso sobre cómo conectar el dispositivo al código de este tutorial y, en general, al Centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="13886-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="13886-119">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="13886-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="13886-120">Node.js versión 0.10.x, o posteriores.</span><span class="sxs-lookup"><span data-stu-id="13886-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="13886-121">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="13886-121">An active Azure account.</span></span> <span data-ttu-id="13886-122">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="13886-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="13886-123">Recepción de mensajes en la aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="13886-123">Receive messages in the simulated device app</span></span>
<span data-ttu-id="13886-124">En esta sección, modificará la aplicación de dispositivo simulado que creó en el tutorial [Introducción a Iot Hub] para recibir mensajes de nube a dispositivo desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="13886-124">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="13886-125">Con un editor de texto, abra el archivo SimulatedDevice.js.</span><span class="sxs-lookup"><span data-stu-id="13886-125">Using a text editor, open the SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="13886-126">Modifique la función **connectCallback** para controlar los mensajes enviados desde Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="13886-126">Modify the **connectCallback** function to handle messages sent from IoT Hub.</span></span> <span data-ttu-id="13886-127">En este ejemplo, el dispositivo siempre invoca la función **complete** para notificar al Centro de IoT que ha procesado el mensaje.</span><span class="sxs-lookup"><span data-stu-id="13886-127">In this example, the device always invokes the **complete** function to notify IoT Hub that it has processed the message.</span></span> <span data-ttu-id="13886-128">La nueva versión de la función **connectCallback** tiene un aspecto similar al fragmento siguiente:</span><span class="sxs-lookup"><span data-stu-id="13886-128">Your new version of the **connectCallback** function looks like the following snippet:</span></span>
   
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
        // Create a message and send it to the IoT Hub every second
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
   > <span data-ttu-id="13886-129">Si usa HTTP en lugar de MQTT o AMQP como transporte, la instancia de **DeviceClient** busca mensajes del IoT Hub con menos frecuencia (menos de 25 minutos).</span><span class="sxs-lookup"><span data-stu-id="13886-129">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="13886-130">Para obtener más información sobre las diferencias entre la compatibilidad con MQTT, AMQP y HTTP, y la limitación de IoT Hub, consulte la [Guía del desarrollador de IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="13886-130">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="13886-131">Envío de mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="13886-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="13886-132">En esta sección, usted crea una aplicación de consola de Node.js que envía mensajes de nube a dispositivo a la aplicación del dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="13886-132">In this section, you create a Node.js console app that sends cloud-to-device messages to the simulated device app.</span></span> <span data-ttu-id="13886-133">Necesita el identificador de dispositivo que agregó en el tutorial de [Introducción a Iot Hub].</span><span class="sxs-lookup"><span data-stu-id="13886-133">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="13886-134">También necesita la cadena de conexión para IoT Hub que encontrará en [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="13886-134">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span></span>

1. <span data-ttu-id="13886-135">Cree una carpeta vacía denominada **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="13886-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="13886-136">En la carpeta **sendcloudtodevicemessage** , cree un archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="13886-136">In the **sendcloudtodevicemessage** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="13886-137">Acepte todos los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="13886-137">Accept all the defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="13886-138">En el símbolo del sistema en la carpeta **sendcloudtodevicemessage**, ejecute el siguiente comando para instalar el paquete **azure-iothub**:</span><span class="sxs-lookup"><span data-stu-id="13886-138">At your command prompt in the **sendcloudtodevicemessage** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="13886-139">Con un editor de texto, cree un archivo **SendCloudToDeviceMessage.js** en la carpeta **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="13886-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in the **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="13886-140">Agregue las siguientes instrucciones `require` al principio del archivo **SendCloudToDeviceMessage.js** :</span><span class="sxs-lookup"><span data-stu-id="13886-140">Add the following `require` statements at the start of the **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="13886-141">Agregue el código siguiente al archivo **SendCloudToDeviceMessage.js** .</span><span class="sxs-lookup"><span data-stu-id="13886-141">Add the following code to **SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="13886-142">Sustituya el valor de marcador de posición "{iot hub connection string}" por la cadena de conexión de IoT Hub que creó en el tutorial [Introducción a Iot Hub].</span><span class="sxs-lookup"><span data-stu-id="13886-142">Replace the "{iot hub connection string}" placeholder value with the IoT Hub connection string for the hub you created in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="13886-143">Sustituya el marcador de posición "{device id}" por el identificador del dispositivo que agregó en el tutorial [Introducción a Iot Hub]:</span><span class="sxs-lookup"><span data-stu-id="13886-143">Replace the "{device id}" placeholder with the device ID of the device you added in the [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="13886-144">Agregue la función siguiente para imprimir los resultados de la operación en la consola:</span><span class="sxs-lookup"><span data-stu-id="13886-144">Add the following function to print operation results to the console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="13886-145">Agregue la función siguiente para imprimir mensajes de comentarios de entrega en la consola:</span><span class="sxs-lookup"><span data-stu-id="13886-145">Add the following function to print delivery feedback messages to the console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="13886-146">Agregue el código siguiente para enviar un mensaje a su dispositivo y procesar el mensaje de comentarios cuando el dispositivo reconozca el mensaje de la nube al dispositivo:</span><span class="sxs-lookup"><span data-stu-id="13886-146">Add the following code to send a message to your device and handle the feedback message when the device acknowledges the cloud-to-device message:</span></span>
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud to device message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. <span data-ttu-id="13886-147">Guarde y cierre el archivo **SendCloudToDeviceMessage.js** .</span><span class="sxs-lookup"><span data-stu-id="13886-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="13886-148">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="13886-148">Run the applications</span></span>
<span data-ttu-id="13886-149">Ahora está preparado para ejecutar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="13886-149">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="13886-150">En el símbolo del sistema de la carpeta **simulateddevice** , ejecute el comando siguiente para enviar la telemetría al centro de IoT Hub y escuchar mensajes de nube al dispositivo:</span><span class="sxs-lookup"><span data-stu-id="13886-150">At the command prompt in the **simulateddevice** folder, run the following command to send telemetry to IoT Hub and to listen for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Ejecución de una aplicación de dispositivo simulada][img-simulated-device]
2. <span data-ttu-id="13886-152">En un símbolo del sistema de la carpeta **sendcloudtodevicemessage** , ejecute el comando siguiente para enviar un mensaje de nube al dispositivo y espere el comentario de confirmación:</span><span class="sxs-lookup"><span data-stu-id="13886-152">At a command prompt in the **sendcloudtodevicemessage** folder, run the following command to send a cloud-to-device message and wait for the acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Ejecución de la aplicación para enviar el comando de nube a dispositivo][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="13886-154">Por simplificar, este tutorial no implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="13886-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="13886-155">En el código de producción, deberá implementar directivas de reintentos (por ejemplo, retroceso exponencial), tal y como se sugiere en el artículo de MSDN [Transient Fault Handling](Control de errores transitorios).</span><span class="sxs-lookup"><span data-stu-id="13886-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="13886-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="13886-156">Next steps</span></span>
<span data-ttu-id="13886-157">En este tutorial, aprendió a enviar y recibir mensajes de nube a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="13886-157">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="13886-158">Para ver ejemplos de soluciones completas de un extremo a otro que usen el Centro de IoT, consulte [Documentación del Conjunto de aplicaciones de IoT].</span><span class="sxs-lookup"><span data-stu-id="13886-158">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="13886-159">Para obtener más información sobre cómo desarrollar soluciones con IoT Hub, consulte la [Guía del desarrollador de IoTHub de Azure].</span><span class="sxs-lookup"><span data-stu-id="13886-159">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

<span data-ttu-id="13886-160">[Introducción a Iot Hub]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="13886-160">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
<span data-ttu-id="13886-161">[Guía del desarrollador de IoTHub de Azure]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="13886-161">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="13886-162">[Centro para desarrolladores de IoT de Azure]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="13886-162">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
<span data-ttu-id="13886-163">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="13886-163">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="13886-164">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="13886-164">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="13886-165">[Documentación del Conjunto de aplicaciones de IoT]: https://azure.microsoft.com/documentation/suites/iot-suite/</span><span class="sxs-lookup"><span data-stu-id="13886-165">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span></span>
