---
title: "Introducción a Azure IoT Hub (Node) | Microsoft Docs"
description: "Obtenga información sobre cómo enviar mensajes del dispositivo a la nube a una instancia de Azure IoT Hub mediante los SDK de IoT para Node.js. Cree aplicaciones de servicio y de dispositivo simuladas para registrar el dispositivo, enviar mensajes y leerlos en IoT Hub."
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
ms.openlocfilehash: b27a34c0f1f127628912ad68a002e15cc838b4d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-simulated-device-to-your-iot-hub-using-node"></a><span data-ttu-id="ad8c2-104">Conexión del dispositivo simulado en el centro de IoT con Node</span><span class="sxs-lookup"><span data-stu-id="ad8c2-104">Connect your simulated device to your IoT hub using Node</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="ad8c2-105">Al final de este tutorial tendrá tres aplicaciones de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-105">At the end of this tutorial, you have three Node.js console apps:</span></span>

* <span data-ttu-id="ad8c2-106">**CreateDeviceIdentity.js**, que crea una identidad de dispositivo y una clave de seguridad asociada para conectar la aplicación de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="ad8c2-107">**ReadDeviceToCloudMessages.js**, que muestra los datos de telemetría enviados por la aplicación de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-107">**ReadDeviceToCloudMessages.js**, which displays the telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="ad8c2-108">**SimulatedDevice.js**, que se conecta con IoT Hub con la identidad del dispositivo creada anteriormente y envía un mensaje de telemetría cada segundo mediante el protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-108">**SimulatedDevice.js**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="ad8c2-109">En el artículo [Azure Iot SDKs][lnk-hub-sdks] (SDK de IoT de Azure) se proporciona información acerca de los diversos SDK que puede usar para crear ambas aplicaciones para que se ejecuten en dispositivos y en el back-end de la solución.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="ad8c2-110">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="ad8c2-111">Node.js versión 0.10.x, o posteriores.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="ad8c2-112">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-112">An active Azure account.</span></span> <span data-ttu-id="ad8c2-113">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="ad8c2-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="ad8c2-114">Ahora ha creado su Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-114">You have now created your IoT hub.</span></span> <span data-ttu-id="ad8c2-115">Ha creado el nombre de host y la cadena de conexión de IoT Hub que necesita para completar el resto del tutorial.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-115">You have the IoT Hub host name and the IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="ad8c2-116">Creación de una identidad de dispositivo</span><span class="sxs-lookup"><span data-stu-id="ad8c2-116">Create a device identity</span></span>
<span data-ttu-id="ad8c2-117">En esta sección, creará una aplicación de consola de Node.js que crea una identidad de dispositivo en el registro de identidades de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-117">In this section, you create a Node.js console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="ad8c2-118">No se puede conectar a IoT Hub a menos si tiene una entrada en el registro de identidades.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-118">A device can only connect to IoT hub if it has an entry in the identity registry.</span></span> <span data-ttu-id="ad8c2-119">Para más información, consulte la sección sobre el **registro de la identidad** de la [guía para desarrolladores de IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="ad8c2-119">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="ad8c2-120">Cuando ejecuta esta aplicación de consola, se genera una clave y un identificador de dispositivo únicos con el que el dispositivo puede identificarse cuando envía al Centro de IoT mensajes de dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-120">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="ad8c2-121">Cree una nueva carpeta vacía denominada **createdeviceidentity**.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-121">Create a new empty folder called **createdeviceidentity**.</span></span> <span data-ttu-id="ad8c2-122">En la carpeta **createdeviceidentity**, cree un archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-122">In the **createdeviceidentity** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="ad8c2-123">Acepte todos los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-123">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="ad8c2-124">En el símbolo del sistema en la carpeta **createdeviceidentity**, ejecute el siguiente comando para instalar el paquete del SDK del servicio **azure-iothub**:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-124">At your command prompt in the **createdeviceidentity** folder, run the following command to install the **azure-iothub** Service SDK package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="ad8c2-125">Con un editor de texto, cree un archivo **CreateDeviceIdentity.js** en la carpeta **createdeviceidentity**.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-125">Using a text editor, create a **CreateDeviceIdentity.js** file in the **createdeviceidentity** folder.</span></span>
4. <span data-ttu-id="ad8c2-126">Agregue la siguiente instrucción `require` al principio del archivo **CreateDeviceIdentity.js** :</span><span class="sxs-lookup"><span data-stu-id="ad8c2-126">Add the following `require` statement at the start of the **CreateDeviceIdentity.js** file:</span></span>
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. <span data-ttu-id="ad8c2-127">Agregue el siguiente código al archivo **CreateDeviceIdentity.js** y sustituya el valor de marcador de posición por la cadena de conexión de IoT Hub que creó en la sección anterior:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-127">Add the following code to the **CreateDeviceIdentity.js** file and replace the placeholder value with the IoT Hub connection string for the hub you created in the previous section:</span></span> 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="ad8c2-128">Agregue el siguiente código para crear una definición de dispositivo en el registro de identidades en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-128">Add the following code to create a device definition in the identity registry in your IoT hub.</span></span> <span data-ttu-id="ad8c2-129">Este código crea un dispositivo si el identificador de dispositivo no existe en el registro de identidad o, de lo contrario, devuelve la clave del dispositivo existente:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-129">This code creates a device if the device ID does not exist in the identity registry, otherwise it returns the key of the existing device:</span></span>
   
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

7. <span data-ttu-id="ad8c2-130">Guarde y cierre el archivo **CreateDeviceIdentity.js** .</span><span class="sxs-lookup"><span data-stu-id="ad8c2-130">Save and close **CreateDeviceIdentity.js** file.</span></span>
8. <span data-ttu-id="ad8c2-131">Para ejecutar la aplicación **createdeviceidentity**, ejecute el siguiente comando en el símbolo del sistema en la carpeta createdeviceidentity:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-131">To run the **createdeviceidentity** application, execute the following command at the command prompt in the createdeviceidentity folder:</span></span>
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. <span data-ttu-id="ad8c2-132">Anote el **identificador del dispositivo** y la **clave del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-132">Make a note of the **Device ID** and **Device key**.</span></span> <span data-ttu-id="ad8c2-133">Los necesitará más adelante cuando cree una aplicación que se conecta a IoT Hub como un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-133">You need these values later when you create an application that connects to IoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="ad8c2-134">El registro de identidades de IoT Hub solo almacena identidades de dispositivos para permitir el acceso seguro al centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-134">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="ad8c2-135">Almacena las claves y los identificadores de dispositivo para usarlos como credenciales de seguridad, y un indicador de habilitado o deshabilitado que permite deshabilitar el acceso a un dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-135">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="ad8c2-136">Si la aplicación necesita almacenar otros metadatos específicos del dispositivo, debe usar un almacén específico de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-136">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="ad8c2-137">Consulte la [guía para desarrolladores de IoT Hub][lnk-devguide-identity] para más información.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-137">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="ad8c2-138">Recepción de mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="ad8c2-138">Receive device-to-cloud messages</span></span>
<span data-ttu-id="ad8c2-139">En esta sección, creará una aplicación de consola de Node.js que lee los mensajes de dispositivo a nube de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="ad8c2-140">Un centro de IoT expone un punto de conexión compatible con [Event Hubs][lnk-event-hubs-overview] para poder leer los mensajes del dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="ad8c2-141">Para simplificar las cosas, este tutorial crea un lector básico que no es apto para una implementación de alta capacidad de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-141">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="ad8c2-142">El [tutorial: procesamiento de mensajes de dispositivo a la nube][lnk-process-d2c-tutorial] muestra cómo procesar mensajes de dispositivo a la nube a escala.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-142">The [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how to process device-to-cloud messages at scale.</span></span> <span data-ttu-id="ad8c2-143">En el tutorial [Introducción a Event Hubs][lnk-eventhubs-tutorial] se proporciona información adicional acerca de cómo procesar los mensajes desde Event Hubs. Dicha información se puede aplicar a los puntos de conexión de IoT Hub compatibles con Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-143">The [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how to process messages from Event Hubs and is applicable to the IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="ad8c2-144">El punto de conexión compatible con Event Hubs para leer mensajes de dispositivo a la nube siempre usa el protocolo AMQP.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-144">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="ad8c2-145">Cree una carpeta vacía denominada **readdevicetocloudmessages**.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-145">Create an empty folder called **readdevicetocloudmessages**.</span></span> <span data-ttu-id="ad8c2-146">En la carpeta **readdevicetocloudmessages**, cree un archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-146">In the **readdevicetocloudmessages** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="ad8c2-147">Acepte todos los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-147">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="ad8c2-148">En el símbolo del sistema, en la carpeta **readdevicetocloudmessages**, ejecute el siguiente comando para instalar el paquete **azure-event-hubs**:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-148">At your command prompt in the **readdevicetocloudmessages** folder, run the following command to install the **azure-event-hubs** package:</span></span>
   
    ```
    npm install azure-event-hubs --save
    ```
3. <span data-ttu-id="ad8c2-149">Con un editor de texto, cree un archivo **ReadDeviceToCloudMessages.js** en la carpeta **readdevicetocloudmessages**.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in the **readdevicetocloudmessages** folder.</span></span>
4. <span data-ttu-id="ad8c2-150">Agregue las siguientes instrucciones `require` al principio del archivo **ReadDeviceToCloudMessages.js** :</span><span class="sxs-lookup"><span data-stu-id="ad8c2-150">Add the following `require` statements at the start of the **ReadDeviceToCloudMessages.js** file:</span></span>
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. <span data-ttu-id="ad8c2-151">Agregue la siguiente declaración de variable y sustituya el valor de marcador de posición por la cadena de conexión de IoT Hub para su centro:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-151">Add the following variable declaration and replace the placeholder value with the IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. <span data-ttu-id="ad8c2-152">Agregue las siguientes dos funciones que imprimen la salida en la consola:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-152">Add the following two functions that print output to the console:</span></span>
   
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
7. <span data-ttu-id="ad8c2-153">Agregue el siguiente código para crear **EventHubClient**, abra la conexión a IoT Hub y cree un receptor para cada partición.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-153">Add the following code to create the **EventHubClient**, open the connection to your IoT Hub, and create a receiver for each partition.</span></span> <span data-ttu-id="ad8c2-154">Esta aplicación utiliza un filtro cuando crea el receptor para que este solo lea los mensajes enviados al Centro de IoT después de que el receptor comience a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-154">This application uses a filter when it creates a receiver so that the receiver only reads messages sent to IoT Hub after the receiver starts running.</span></span> <span data-ttu-id="ad8c2-155">Este filtro es útil en un entorno de prueba, porque puede ver solo el conjunto actual de mensajes.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-155">This filter is useful in a test environment so you see just the current set of messages.</span></span> <span data-ttu-id="ad8c2-156">En un entorno de producción, el código debe asegurarse de que este procesa todos los mensajes.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-156">In a production environment, your code should make sure that it processes all the messages.</span></span> <span data-ttu-id="ad8c2-157">Para más información, consulte el [Tutorial: procesamiento de mensajes de dispositivo a la nube de IoT Hub][lnk-process-d2c-tutorial]:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-157">For more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span></span>
   
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
8. <span data-ttu-id="ad8c2-158">Guarde y cierre el archivo **ReadDeviceToCloudMessages.js** .</span><span class="sxs-lookup"><span data-stu-id="ad8c2-158">Save and close the **ReadDeviceToCloudMessages.js** file.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="ad8c2-159">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="ad8c2-159">Create a simulated device app</span></span>
<span data-ttu-id="ad8c2-160">En esta sección, creará una aplicación de consola de Node.js que simula un dispositivo que envía mensajes de dispositivo a nube a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="ad8c2-161">Cree una carpeta vacía denominada **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-161">Create an empty folder called **simulateddevice**.</span></span> <span data-ttu-id="ad8c2-162">En la carpeta **simulateddevice**, cree un archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-162">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="ad8c2-163">Acepte todos los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-163">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="ad8c2-164">En el símbolo del sistema, en la carpeta **simulateddevice**, ejecute el siguiente comando para instalar el paquete del SDK de dispositivo **azure-iot-device** y el paquete **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-164">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="ad8c2-165">Con un editor de texto, cree un archivo **SimulatedDevice.js** en la carpeta **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-165">Using a text editor, create a **SimulatedDevice.js** file in the **simulateddevice** folder.</span></span>
4. <span data-ttu-id="ad8c2-166">Agregue las siguientes instrucciones `require` al principio del archivo **SimulatedDevice.js** :</span><span class="sxs-lookup"><span data-stu-id="ad8c2-166">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. <span data-ttu-id="ad8c2-167">Agregue una variable **connectionString** y utilícela para crear una instancia de **cliente**.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-167">Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="ad8c2-168">Reemplace **{nombreDeHostDeIoT}** por el nombre del centro de IoT que creó en la sección *Creación de un centro de IoT* .</span><span class="sxs-lookup"><span data-stu-id="ad8c2-168">Replace **{youriothostname}** with the name of the IoT hub you created the *Create an IoT Hub* section.</span></span> <span data-ttu-id="ad8c2-169">Reemplace **{nombreDeClaveDeDispositivo}** por el valor de la clave del dispositivo que ha generado en la sección *Creación de una identidad de dispositivo* :</span><span class="sxs-lookup"><span data-stu-id="ad8c2-169">Replace **{yourdevicekey}** with the device key value you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. <span data-ttu-id="ad8c2-170">Agregue la siguiente función para mostrar la salida de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-170">Add the following function to display output from the application:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="ad8c2-171">Cree una devolución de llamada y utilice la función **setInterval** para enviar un mensaje a IoT Hub cada segundo:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-171">Create a callback and use the **setInterval** function to send a message to your IoT hub every second:</span></span>
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
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
8. <span data-ttu-id="ad8c2-172">Abra la conexión al su Centro de IoT y empiece a enviar mensajes:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-172">Open the connection to your IoT Hub and start sending messages:</span></span>
   
    ```
    client.open(connectCallback);
    ```
9. <span data-ttu-id="ad8c2-173">Guarde el archivo **SimulatedDevice.js** y ciérrelo.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-173">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="ad8c2-174">Por simplificar, este tutorial no implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-174">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="ad8c2-175">En el código de producción, deberá implementar directivas de reintentos (por ejemplo, retroceso exponencial), tal y como se sugiere en el artículo de MSDN [Transient Fault Handling][lnk-transient-faults] (Tratamiento de errores temporales).</span><span class="sxs-lookup"><span data-stu-id="ad8c2-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-the-apps"></a><span data-ttu-id="ad8c2-176">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ad8c2-176">Run the apps</span></span>
<span data-ttu-id="ad8c2-177">Ya está preparado para ejecutar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-177">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="ad8c2-178">En un símbolo del sistema, en la carpeta **readdevicetocloudmessages** , ejecute el siguiente comando para empezar la supervisión de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-178">At a command prompt in the **readdevicetocloudmessages** folder, run the following command to begin monitoring your IoT hub:</span></span>
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Aplicación de servicio de IoT Hub de Node.js para supervisar mensajes del dispositivo a la nube][7]
2. <span data-ttu-id="ad8c2-180">En un símbolo del sistema, en la carpeta **simulateddevice**, ejecute el siguiente comando para empezar el envío de datos de telemetría a IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-180">At a command prompt in the **simulateddevice** folder, run the following command to begin sending telemetry data to your IoT hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Aplicación de dispositivo de IoT Hub de Node.js para enviar mensajes del dispositivo a la nube][8]
3. <span data-ttu-id="ad8c2-182">El icono **Uso** de [Azure Portal][lnk-portal] muestra el número de mensajes enviados al centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-182">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>
   
    ![Icono Uso de Azure Portal que muestra el número de mensajes enviados a IoT Hub][43]

## <a name="next-steps"></a><span data-ttu-id="ad8c2-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ad8c2-184">Next steps</span></span>
<span data-ttu-id="ad8c2-185">En este tutorial, configuró una nueva instancia de IoT Hub en Azure Portal y, después, creó una identidad de dispositivo en el registro de identidades de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-185">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="ad8c2-186">Usó esta identidad de dispositivo para habilitar la aplicación del dispositivo simulado para enviar a IoT Hub los mensajes del dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-186">You used this device identity to enable the simulated device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="ad8c2-187">También creó otra aplicación que muestra los mensajes recibidos por el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ad8c2-187">You also created an app that displays the messages received by the IoT hub.</span></span> 

<span data-ttu-id="ad8c2-188">Para continuar la introducción a IoT Hub y explorar otros escenarios de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="ad8c2-188">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="ad8c2-189">[Conexión del dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="ad8c2-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="ad8c2-190">[Introducción a la administración de dispositivos][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="ad8c2-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="ad8c2-191">[Introducción a Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="ad8c2-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="ad8c2-192">Para aprender a ampliar su solución IoT y cómo procesar mensajes de dispositivo a la nube a escala, consulte [Tutorial: procesamiento de mensajes de dispositivo a la nube][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="ad8c2-192">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
