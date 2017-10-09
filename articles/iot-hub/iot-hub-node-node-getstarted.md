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
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a><span data-ttu-id="b78d9-104">Conectar el centro de IoT de tooyour dispositivo simulado mediante el nodo</span><span class="sxs-lookup"><span data-stu-id="b78d9-104">Connect your simulated device tooyour IoT hub using Node</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="b78d9-105">Al final de Hola de este tutorial, tendrá tres aplicaciones de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="b78d9-105">At hello end of this tutorial, you have three Node.js console apps:</span></span>

* <span data-ttu-id="b78d9-106">**CreateDeviceIdentity.js**, que crea una identidad de dispositivo y la clave de seguridad asociadas tooconnect la aplicación de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="b78d9-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="b78d9-107">**ReadDeviceToCloudMessages.js**, que muestra la telemetría de hello enviado por la aplicación de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="b78d9-107">**ReadDeviceToCloudMessages.js**, which displays hello telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="b78d9-108">**SimulatedDevice.js**, que se conecta el centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente y envía un mensaje de telemetría cada segundo mediante Hola protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="b78d9-108">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="b78d9-109">artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que puede usar ambos toorun aplicaciones toobuild en dispositivos y el back-end de soluciones.</span><span class="sxs-lookup"><span data-stu-id="b78d9-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="b78d9-110">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b78d9-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="b78d9-111">Node.js versión 0.10.x, o posteriores.</span><span class="sxs-lookup"><span data-stu-id="b78d9-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="b78d9-112">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="b78d9-112">An active Azure account.</span></span> <span data-ttu-id="b78d9-113">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="b78d9-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="b78d9-114">Ahora ha creado su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b78d9-114">You have now created your IoT hub.</span></span> <span data-ttu-id="b78d9-115">Dispone de nombre de host del centro de IoT de Hola y Hola cadena de conexión de centro de IoT que necesite que el resto de hello toocomplete de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b78d9-115">You have hello IoT Hub host name and hello IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="b78d9-116">Creación de una identidad de dispositivo</span><span class="sxs-lookup"><span data-stu-id="b78d9-116">Create a device identity</span></span>
<span data-ttu-id="b78d9-117">En esta sección, creará una aplicación de consola de Node.js que crea una identidad de dispositivo en el registro de la identidad de hello en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="b78d9-117">In this section, you create a Node.js console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="b78d9-118">Un dispositivo solo puede conectarse tooIoT concentrador, si existe una entrada en el registro de la identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="b78d9-118">A device can only connect tooIoT hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="b78d9-119">Para obtener más información, vea hello **del registro de identidad** sección de hello [Guía del desarrollador de centro de IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="b78d9-119">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="b78d9-120">Al ejecutar esta aplicación de consola, se generará un identificador de dispositivo único y clave que el dispositivo pueda usar tooidentify propio cuando el dispositivo a la nube sitio envía mensajes tooIoT concentrador.</span><span class="sxs-lookup"><span data-stu-id="b78d9-120">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="b78d9-121">Cree una nueva carpeta vacía denominada **createdeviceidentity**.</span><span class="sxs-lookup"><span data-stu-id="b78d9-121">Create a new empty folder called **createdeviceidentity**.</span></span> <span data-ttu-id="b78d9-122">Hola **createdeviceidentity** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="b78d9-122">In hello **createdeviceidentity** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="b78d9-123">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="b78d9-123">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b78d9-124">En el símbolo del sistema en hello **createdeviceidentity** carpeta, ejecute hello después comando tooinstall hello **el centro de IOT de azure** paquete SDK del servicio:</span><span class="sxs-lookup"><span data-stu-id="b78d9-124">At your command prompt in hello **createdeviceidentity** folder, run hello following command tooinstall hello **azure-iothub** Service SDK package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="b78d9-125">Con un editor de texto, cree un **CreateDeviceIdentity.js** archivo Hola **createdeviceidentity** carpeta.</span><span class="sxs-lookup"><span data-stu-id="b78d9-125">Using a text editor, create a **CreateDeviceIdentity.js** file in hello **createdeviceidentity** folder.</span></span>
4. <span data-ttu-id="b78d9-126">Agregue los siguiente hello `require` instrucción al principio de Hola de hello **CreateDeviceIdentity.js** archivo:</span><span class="sxs-lookup"><span data-stu-id="b78d9-126">Add hello following `require` statement at hello start of hello **CreateDeviceIdentity.js** file:</span></span>
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. <span data-ttu-id="b78d9-127">Agregar Hola después código toohello **CreateDeviceIdentity.js** archivo y reemplace el valor de marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola Hola:</span><span class="sxs-lookup"><span data-stu-id="b78d9-127">Add hello following code toohello **CreateDeviceIdentity.js** file and replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello previous section:</span></span> 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="b78d9-128">Agregar Hola después código toocreate una definición de dispositivo en el registro de la identidad de hello en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="b78d9-128">Add hello following code toocreate a device definition in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="b78d9-129">Este código crea un dispositivo si Hola Id. de dispositivo no existe en el registro de la identidad de hello, en caso contrario, devuelve clave hello de dispositivo de hello existente:</span><span class="sxs-lookup"><span data-stu-id="b78d9-129">This code creates a device if hello device ID does not exist in hello identity registry, otherwise it returns hello key of hello existing device:</span></span>
   
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

7. <span data-ttu-id="b78d9-130">Guarde y cierre el archivo **CreateDeviceIdentity.js** .</span><span class="sxs-lookup"><span data-stu-id="b78d9-130">Save and close **CreateDeviceIdentity.js** file.</span></span>
8. <span data-ttu-id="b78d9-131">Hola toorun **createdeviceidentity** aplicación, ejecutar el siguiente comando en línea de comandos de hello en la carpeta de createdeviceidentity Hola de Hola:</span><span class="sxs-lookup"><span data-stu-id="b78d9-131">toorun hello **createdeviceidentity** application, execute hello following command at hello command prompt in hello createdeviceidentity folder:</span></span>
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. <span data-ttu-id="b78d9-132">Tome nota de hello **Id. de dispositivo** y **clave de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="b78d9-132">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="b78d9-133">Necesita estos valores más tarde cuando se crea una aplicación que se conecta tooIoT concentrador como un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b78d9-133">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="b78d9-134">Hola del registro de identidad de centro de IoT solo almacena centro de IoT toohello de dispositivo identidades tooenable un acceso seguro.</span><span class="sxs-lookup"><span data-stu-id="b78d9-134">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="b78d9-135">Toouse de identificadores y las claves de dispositivo almacena como credenciales de seguridad y una marca de habilitado/deshabilitado que puede usar acceso toodisable para un dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="b78d9-135">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="b78d9-136">Si la aplicación necesita toostore otros metadatos específicos del dispositivo, debe usar un almacén específico de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b78d9-136">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="b78d9-137">Para obtener más información, vea hello [Guía del desarrollador de centro de IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="b78d9-137">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="b78d9-138">Recepción de mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="b78d9-138">Receive device-to-cloud messages</span></span>
<span data-ttu-id="b78d9-139">En esta sección, creará una aplicación de consola de Node.js que lee los mensajes de dispositivo a nube de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b78d9-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="b78d9-140">Un centro de IoT expone un [centros de eventos][lnk-event-hubs-overview]-extremo compatible tooenable tooread mensajes de dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="b78d9-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="b78d9-141">tookeep cosas simples, en este tutorial se crea un lector básico que no es adecuado para una implementación de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="b78d9-141">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="b78d9-142">Hola [procesar mensajes del dispositivo a la nube] [ lnk-process-d2c-tutorial] tutorial muestra cómo los mensajes tooprocess dispositivo a la nube a escala.</span><span class="sxs-lookup"><span data-stu-id="b78d9-142">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="b78d9-143">Hola [empezar a trabajar con concentradores de eventos] [ lnk-eventhubs-tutorial] tutorial proporciona información adicional acerca de cómo tooprocess mensajes desde los centros de eventos y es aplicable toohello los puntos de conexión compatibles con eventos de centro de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b78d9-143">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="b78d9-144">Hola extremo compatible de concentrador de eventos para leer mensajes de dispositivo para la nube siempre utiliza Hola protocolo AMQP.</span><span class="sxs-lookup"><span data-stu-id="b78d9-144">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="b78d9-145">Cree una carpeta vacía denominada **readdevicetocloudmessages**.</span><span class="sxs-lookup"><span data-stu-id="b78d9-145">Create an empty folder called **readdevicetocloudmessages**.</span></span> <span data-ttu-id="b78d9-146">Hola **readdevicetocloudmessages** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="b78d9-146">In hello **readdevicetocloudmessages** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="b78d9-147">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="b78d9-147">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b78d9-148">En el símbolo del sistema en hello **readdevicetocloudmessages** carpeta, ejecute hello después comando tooinstall hello **centros de eventos de azure** paquete:</span><span class="sxs-lookup"><span data-stu-id="b78d9-148">At your command prompt in hello **readdevicetocloudmessages** folder, run hello following command tooinstall hello **azure-event-hubs** package:</span></span>
   
    ```
    npm install azure-event-hubs --save
    ```
3. <span data-ttu-id="b78d9-149">Con un editor de texto, cree un **ReadDeviceToCloudMessages.js** archivo Hola **readdevicetocloudmessages** carpeta.</span><span class="sxs-lookup"><span data-stu-id="b78d9-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in hello **readdevicetocloudmessages** folder.</span></span>
4. <span data-ttu-id="b78d9-150">Agregue Hola siguiente `require` las instrucciones en hello inician de hello **ReadDeviceToCloudMessages.js** archivo:</span><span class="sxs-lookup"><span data-stu-id="b78d9-150">Add hello following `require` statements at hello start of hello **ReadDeviceToCloudMessages.js** file:</span></span>
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. <span data-ttu-id="b78d9-151">Agregue Hola después de la declaración de variable y reemplace el valor de marcador de posición de hello con hello cadena de conexión de centro de IoT para el centro de:</span><span class="sxs-lookup"><span data-stu-id="b78d9-151">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. <span data-ttu-id="b78d9-152">Agregue Hola siguiendo dos funciones que la consola de toohello de salida de impresión:</span><span class="sxs-lookup"><span data-stu-id="b78d9-152">Add hello following two functions that print output toohello console:</span></span>
   
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
7. <span data-ttu-id="b78d9-153">Agregar Hola después Hola de código toocreate **EventHubClient**, abra Hola conexión tooyour centro de IoT y crear un receptor para cada partición.</span><span class="sxs-lookup"><span data-stu-id="b78d9-153">Add hello following code toocreate hello **EventHubClient**, open hello connection tooyour IoT Hub, and create a receiver for each partition.</span></span> <span data-ttu-id="b78d9-154">Esta aplicación utiliza un filtro cuando crea un receptor de modo que hello receptor solo lee los mensajes enviados tooIoT concentrador después de receptor de hello empieza a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="b78d9-154">This application uses a filter when it creates a receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="b78d9-155">Este filtro es útil en un entorno de prueba para ver solo Hola conjunto actual de mensajes.</span><span class="sxs-lookup"><span data-stu-id="b78d9-155">This filter is useful in a test environment so you see just hello current set of messages.</span></span> <span data-ttu-id="b78d9-156">En un entorno de producción, el código debe asegurarse de que procesa todos los mensajes de saludo.</span><span class="sxs-lookup"><span data-stu-id="b78d9-156">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="b78d9-157">Para obtener más información, vea hello [cómo tooprocess mensajes del dispositivo a la nube de centro de IoT] [ lnk-process-d2c-tutorial] tutorial:</span><span class="sxs-lookup"><span data-stu-id="b78d9-157">For more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span></span>
   
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
8. <span data-ttu-id="b78d9-158">Guarde y cierre hello **ReadDeviceToCloudMessages.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="b78d9-158">Save and close hello **ReadDeviceToCloudMessages.js** file.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="b78d9-159">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="b78d9-159">Create a simulated device app</span></span>
<span data-ttu-id="b78d9-160">En esta sección, creará una aplicación de consola de Node.js que simula un dispositivo que envía el centro de IoT tooan de mensajes del dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="b78d9-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="b78d9-161">Cree una carpeta vacía denominada **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="b78d9-161">Create an empty folder called **simulateddevice**.</span></span> <span data-ttu-id="b78d9-162">Hola **simulateddevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="b78d9-162">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="b78d9-163">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="b78d9-163">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b78d9-164">En el símbolo del sistema en hello **simulateddevice** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure** paquete del SDK de dispositivo y **azure iot dispositivo-mqtt**paquete:</span><span class="sxs-lookup"><span data-stu-id="b78d9-164">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="b78d9-165">Con un editor de texto, cree un **SimulatedDevice.js** archivo Hola **simulateddevice** carpeta.</span><span class="sxs-lookup"><span data-stu-id="b78d9-165">Using a text editor, create a **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="b78d9-166">Agregue Hola siguiente `require` las instrucciones en hello inician de hello **SimulatedDevice.js** archivo:</span><span class="sxs-lookup"><span data-stu-id="b78d9-166">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. <span data-ttu-id="b78d9-167">Agregar un **connectionString** variable y utilizar toocreate un **cliente** instancia.</span><span class="sxs-lookup"><span data-stu-id="b78d9-167">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="b78d9-168">Reemplace **{youriothostname}** por nombre de hello del centro de IoT Hola creaste hello *crear un centro de IoT* sección.</span><span class="sxs-lookup"><span data-stu-id="b78d9-168">Replace **{youriothostname}** with hello name of hello IoT hub you created hello *Create an IoT Hub* section.</span></span> <span data-ttu-id="b78d9-169">Reemplace **{yourdevicekey}** con hello dispositivo clave-valor que generó en hello *crear una identidad de dispositivo* sección:</span><span class="sxs-lookup"><span data-stu-id="b78d9-169">Replace **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. <span data-ttu-id="b78d9-170">Agregue Hola siguientes salida toodisplay de función de la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="b78d9-170">Add hello following function toodisplay output from hello application:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="b78d9-171">Crear una devolución de llamada y usar hello **setInterval** función toosend un centro de IoT de mensaje tooyour cada segundo:</span><span class="sxs-lookup"><span data-stu-id="b78d9-171">Create a callback and use hello **setInterval** function toosend a message tooyour IoT hub every second:</span></span>
   
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
8. <span data-ttu-id="b78d9-172">Abra Hola conexión tooyour centro de IoT y empezar a enviar mensajes:</span><span class="sxs-lookup"><span data-stu-id="b78d9-172">Open hello connection tooyour IoT Hub and start sending messages:</span></span>
   
    ```
    client.open(connectCallback);
    ```
9. <span data-ttu-id="b78d9-173">Guarde y cierre hello **SimulatedDevice.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="b78d9-173">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="b78d9-174">tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento.</span><span class="sxs-lookup"><span data-stu-id="b78d9-174">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b78d9-175">En el código de producción, debe implementar directivas de reintento (por ejemplo, un retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="b78d9-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-hello-apps"></a><span data-ttu-id="b78d9-176">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="b78d9-176">Run hello apps</span></span>
<span data-ttu-id="b78d9-177">Ya estás listo toorun Hola aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b78d9-177">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="b78d9-178">En un símbolo del sistema en hello **readdevicetocloudmessages** carpeta, ejecute hello después toobegin de comando su centro de IoT de supervisión:</span><span class="sxs-lookup"><span data-stu-id="b78d9-178">At a command prompt in hello **readdevicetocloudmessages** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Mensajes dispositivo a la nube de toomonitor de aplicación de servicio de Node.js centro de IoT][7]
2. <span data-ttu-id="b78d9-180">En un símbolo del sistema en hello **simulateddevice** carpeta, ejecute hello después toobegin comando Enviar centro de IoT de tooyour de datos de telemetría:</span><span class="sxs-lookup"><span data-stu-id="b78d9-180">At a command prompt in hello **simulateddevice** folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Mensajes de dispositivo para la nube de toosend aplicación de dispositivo de Node.js centro de IoT][8]
3. <span data-ttu-id="b78d9-182">Hola **uso** el icono Servicios hello [portal de Azure] [ lnk-portal] muestra Hola número de mensajes enviados toohello centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="b78d9-182">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>
   
    ![Azure portal uso icono que muestra el número de mensajes enviados tooIoT concentrador][43]

## <a name="next-steps"></a><span data-ttu-id="b78d9-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b78d9-184">Next steps</span></span>
<span data-ttu-id="b78d9-185">En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="b78d9-185">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="b78d9-186">Usar este dispositivo identidad tooenable Hola simulada dispositivos aplicación toosend mensajes del dispositivo a la nube toohello centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="b78d9-186">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="b78d9-187">También crea una aplicación que muestra los mensajes de saludo recibidos por centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="b78d9-187">You also created an app that displays hello messages received by hello IoT hub.</span></span> 

<span data-ttu-id="b78d9-188">toocontinue introducción con el centro de IoT y tooexplore otros escenarios de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="b78d9-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="b78d9-189">[Conexión del dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="b78d9-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="b78d9-190">[Introducción a la administración de dispositivos][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="b78d9-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="b78d9-191">[Introducción a Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="b78d9-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="b78d9-192">toolearn tooextend mensajes de dispositivo a la nube de su solución y proceso de IoT a escala, vea hello [procesar mensajes del dispositivo a la nube] [ lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="b78d9-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
