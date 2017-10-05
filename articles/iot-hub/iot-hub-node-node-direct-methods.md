---
title: "Métodos directos de IoT Hub de Azure (Node) | Microsoft Docs"
description: "Describe cómo usar los métodos directos de IoT Hub de Azure. Usará los SDK de IoT de Azure para Node.js con el fin de implementar una aplicación de dispositivo simulado que incluye un método directo y un servicio que invoque el método directo."
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
ms.openlocfilehash: 83725c3ae3fd3807f2469be888e270ba078a8972
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="0ecd0-104">Uso de métodos directos en el dispositivo IoT con Node.js</span><span class="sxs-lookup"><span data-stu-id="0ecd0-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="0ecd0-105">Al final de este tutorial tendrá dos aplicaciones de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="0ecd0-105">At the end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="0ecd0-106">**CallMethodOnDevice.js**, que llama a un método de la aplicación de dispositivo simulado y muestra la respuesta.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-106">**CallMethodOnDevice.js**, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="0ecd0-107">**SimulatedDevice.js**, que se conecta al centro de IoT con la identidad del dispositivo creada anteriormente y responde al método llamado desde la nube.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-107">**SimulatedDevice.js**, which connects to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="0ecd0-108">En el artículo [Azure Iot SDKs][lnk-hub-sdks] (SDK de IoT de Azure) se proporciona información acerca de los diversos SDK que puede usar para crear ambas aplicaciones para que se ejecuten en dispositivos y en el back-end de la solución.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="0ecd0-109">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0ecd0-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="0ecd0-110">Node.js versión 0.10.x, o posteriores.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="0ecd0-111">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-111">An active Azure account.</span></span> <span data-ttu-id="0ecd0-112">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="0ecd0-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="0ecd0-113">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="0ecd0-113">Create a simulated device app</span></span>
<span data-ttu-id="0ecd0-114">En esta sección, creará una aplicación de consola de Node.js que responda a un método que llama desde la nube.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-114">In this section, you create a Node.js console app that responds to a method called by the cloud.</span></span>

1. <span data-ttu-id="0ecd0-115">Cree una nueva carpeta vacía denominada **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="0ecd0-116">En la carpeta **simulateddevice**, cree un archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-116">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="0ecd0-117">Acepte todos los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="0ecd0-117">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="0ecd0-118">En el símbolo del sistema, en la carpeta **simulateddevice**, ejecute el siguiente comando para instalar el paquete del SDK de dispositivo **azure-iot-device** y el paquete **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="0ecd0-118">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="0ecd0-119">Con un editor de texto, cree un nuevo archivo **SimulatedDevice.js** en la carpeta **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-119">Using a text editor, create a new **SimulatedDevice.js** file in the **simulateddevice** folder.</span></span>
4. <span data-ttu-id="0ecd0-120">Agregue las siguientes instrucciones `require` al principio del archivo **SimulatedDevice.js** :</span><span class="sxs-lookup"><span data-stu-id="0ecd0-120">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="0ecd0-121">Agregue una variable **connectionString** y utilícela para crear una instancia de **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-121">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="0ecd0-122">Reemplace **{device connection string}** por la cadena conexión de dispositivo que generó en la sección sobre cómo *crear una identidad de dispositivo*:</span><span class="sxs-lookup"><span data-stu-id="0ecd0-122">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="0ecd0-123">Agregue la siguiente función para implementar el método en el dispositivo:</span><span class="sxs-lookup"><span data-stu-id="0ecd0-123">Add the following function to implement the method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="0ecd0-124">Abra la conexión al centro de IoT y empiece a por inicializar la escucha del método:</span><span class="sxs-lookup"><span data-stu-id="0ecd0-124">Open the connection to your IoT hub and start initialize the method listener:</span></span>
   
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
8. <span data-ttu-id="0ecd0-125">Guarde el archivo **SimulatedDevice.js** y ciérrelo.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-125">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="0ecd0-126">Por simplificar, este tutorial no implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-126">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="0ecd0-127">En el código de producción, deberá implementar directivas de reintento (por ejemplo, reintento de conexión), tal y como se sugiere en el artículo de MSDN [Transient Fault Handling][lnk-transient-faults] (Control de errores temporales).</span><span class="sxs-lookup"><span data-stu-id="0ecd0-127">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="0ecd0-128">Llamada a un método de un dispositivo</span><span class="sxs-lookup"><span data-stu-id="0ecd0-128">Call a method on a device</span></span>
<span data-ttu-id="0ecd0-129">En esta sección, creará una aplicación de consola de Node.js que llame a un método de la aplicación de dispositivo simulado y muestre la respuesta.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-129">In this section, you create a Node.js console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="0ecd0-130">Cree una nueva carpeta vacía denominada **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="0ecd0-131">En la carpeta **callmethodondevice** , cree un archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-131">In the **callmethodondevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="0ecd0-132">Acepte todos los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="0ecd0-132">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="0ecd0-133">En el símbolo del sistema, en la carpeta **createdeviceidentity**, ejecute el siguiente comando para instalar el paquete **azure-iothub**:</span><span class="sxs-lookup"><span data-stu-id="0ecd0-133">At your command prompt in the **callmethodondevice** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="0ecd0-134">Con un editor de texto, cree un archivo **CallMethodOnDevice.js** en la carpeta **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-134">Using a text editor, create a **CallMethodOnDevice.js** file in the **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="0ecd0-135">Agregue las siguientes instrucciones `require` al principio del archivo **CallMethodOnDevice.js**:</span><span class="sxs-lookup"><span data-stu-id="0ecd0-135">Add the following `require` statements at the start of the **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="0ecd0-136">Agregue la siguiente declaración de variable y sustituya el valor de marcador de posición por la cadena de conexión de IoT Hub para su centro:</span><span class="sxs-lookup"><span data-stu-id="0ecd0-136">Add the following variable declaration and replace the placeholder value with the IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="0ecd0-137">Cree el cliente para abrir la conexión al centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-137">Create the client to open the connection to your IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="0ecd0-138">Agregue la siguiente función para invocar el método de dispositivo e imprimir la respuesta del dispositivo en la consola:</span><span class="sxs-lookup"><span data-stu-id="0ecd0-138">Add the following function to invoke the device method and print the device response to the console:</span></span>
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed to invoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. <span data-ttu-id="0ecd0-139">Guarde y cierre el archivo **CallMethodOnDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-139">Save and close the **CallMethodOnDevice.js** file.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="0ecd0-140">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="0ecd0-140">Run the apps</span></span>
<span data-ttu-id="0ecd0-141">Ya está preparado para ejecutar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-141">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="0ecd0-142">En un símbolo del sistema, en la carpeta **simulateddevice** , ejecute el siguiente comando para empezar la escucha de llamadas de método desde IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="0ecd0-142">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="0ecd0-143">En un símbolo del sistema, en la carpeta **callmethodondevice**, ejecute el siguiente comando para empezar la supervisión del centro de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="0ecd0-143">At a command prompt in the **callmethodondevice** folder, run the following command to begin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="0ecd0-144">Verá cómo el dispositivo reacciona al método imprimiendo el mensaje y cómo la aplicación que llamó al método muestra la respuesta del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="0ecd0-144">You will see the device react to the method by printing out the message and the application which called the method display the response from the device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="0ecd0-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0ecd0-145">Next steps</span></span>
<span data-ttu-id="0ecd0-146">En este tutorial, configuró un centro de IoT nuevo en Azure Portal y, después, creó una identidad de dispositivo en el registro de identidades del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-146">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="0ecd0-147">Usó esta identidad de dispositivo para que la aplicación del dispositivo simulado reaccionara a los métodos que se invoquen desde la nube.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-147">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="0ecd0-148">También creó una aplicación que invoca métodos en el dispositivo y muestra la respuesta del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0ecd0-148">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="0ecd0-149">Para continuar la introducción a IoT Hub y explorar otros escenarios de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="0ecd0-149">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="0ecd0-150">[Introducción a Iot Hub]</span><span class="sxs-lookup"><span data-stu-id="0ecd0-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="0ecd0-151">[Programación de trabajos en varios dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="0ecd0-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="0ecd0-152">Para información sobre cómo ampliar la solución de IoT y programar llamadas de método en varios dispositivos, consulte el tutorial [Programación de trabajos en varios dispositivos][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="0ecd0-152">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
[Introducción a Iot Hub]: iot-hub-node-node-getstarted.md
