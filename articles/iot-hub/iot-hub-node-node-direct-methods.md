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
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="e6544-104">Uso de métodos directos en el dispositivo IoT con Node.js</span><span class="sxs-lookup"><span data-stu-id="e6544-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="e6544-105">Al final de Hola de este tutorial, tiene dos aplicaciones de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="e6544-105">At hello end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="e6544-106">**CallMethodOnDevice.js**, que llama a un método de aplicación de dispositivo simulado de hello y se muestra la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6544-106">**CallMethodOnDevice.js**, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="e6544-107">**SimulatedDevice.js**, que se conecta el centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente y responde método toohello llamado a nube Hola.</span><span class="sxs-lookup"><span data-stu-id="e6544-107">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="e6544-108">artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que puede usar ambos toorun aplicaciones toobuild en dispositivos y el back-end de soluciones.</span><span class="sxs-lookup"><span data-stu-id="e6544-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="e6544-109">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e6544-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="e6544-110">Node.js versión 0.10.x, o posteriores.</span><span class="sxs-lookup"><span data-stu-id="e6544-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="e6544-111">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="e6544-111">An active Azure account.</span></span> <span data-ttu-id="e6544-112">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="e6544-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="e6544-113">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="e6544-113">Create a simulated device app</span></span>
<span data-ttu-id="e6544-114">En esta sección, creará una aplicación de consola de Node.js que responde el método tooa llamado a nube Hola.</span><span class="sxs-lookup"><span data-stu-id="e6544-114">In this section, you create a Node.js console app that responds tooa method called by hello cloud.</span></span>

1. <span data-ttu-id="e6544-115">Cree una nueva carpeta vacía denominada **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="e6544-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="e6544-116">Hola **simulateddevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="e6544-116">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="e6544-117">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="e6544-117">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="e6544-118">En el símbolo del sistema en hello **simulateddevice** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure** paquete del SDK de dispositivo y **azure iot dispositivo-mqtt**paquete:</span><span class="sxs-lookup"><span data-stu-id="e6544-118">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="e6544-119">Con un editor de texto, cree un nuevo **SimulatedDevice.js** archivo Hola **simulateddevice** carpeta.</span><span class="sxs-lookup"><span data-stu-id="e6544-119">Using a text editor, create a new **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="e6544-120">Agregue Hola siguiente `require` las instrucciones en hello inician de hello **SimulatedDevice.js** archivo:</span><span class="sxs-lookup"><span data-stu-id="e6544-120">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="e6544-121">Agregar un **connectionString** variable y utilizar toocreate un **DeviceClient** instancia.</span><span class="sxs-lookup"><span data-stu-id="e6544-121">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="e6544-122">Reemplace **{cadena de conexión de dispositivo}** con cadena de conexión de dispositivo de Hola que generó en hello *crear una identidad de dispositivo* sección:</span><span class="sxs-lookup"><span data-stu-id="e6544-122">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="e6544-123">Agregue Hola después de método de función tooimplement hello en dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="e6544-123">Add hello following function tooimplement hello method on hello device:</span></span>
   
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
7. <span data-ttu-id="e6544-124">Abrir el centro de IoT de hello conexión tooyour e iniciar el agente de escucha de inicializar Hola método:</span><span class="sxs-lookup"><span data-stu-id="e6544-124">Open hello connection tooyour IoT hub and start initialize hello method listener:</span></span>
   
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
8. <span data-ttu-id="e6544-125">Guarde y cierre hello **SimulatedDevice.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="e6544-125">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="e6544-126">tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento.</span><span class="sxs-lookup"><span data-stu-id="e6544-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="e6544-127">En el código de producción, debe implementar directivas de reintento (por ejemplo, los reintentos de conexión), tal como se sugiere en el artículo MSDN de hello [control de errores transitorios][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="e6544-127">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="e6544-128">Llamada a un método de un dispositivo</span><span class="sxs-lookup"><span data-stu-id="e6544-128">Call a method on a device</span></span>
<span data-ttu-id="e6544-129">En esta sección, creará una aplicación de consola de Node.js que llama a un método de aplicación de dispositivo simulado de hello y, a continuación, muestra la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6544-129">In this section, you create a Node.js console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="e6544-130">Cree una nueva carpeta vacía denominada **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="e6544-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="e6544-131">Hola **callmethodondevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="e6544-131">In hello **callmethodondevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="e6544-132">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="e6544-132">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="e6544-133">En el símbolo del sistema en hello **callmethodondevice** carpeta, ejecute hello después comando tooinstall hello **el centro de IOT de azure** paquete:</span><span class="sxs-lookup"><span data-stu-id="e6544-133">At your command prompt in hello **callmethodondevice** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="e6544-134">Con un editor de texto, cree un **CallMethodOnDevice.js** archivo Hola **callmethodondevice** carpeta.</span><span class="sxs-lookup"><span data-stu-id="e6544-134">Using a text editor, create a **CallMethodOnDevice.js** file in hello **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="e6544-135">Agregue Hola siguiente `require` las instrucciones en hello inician de hello **CallMethodOnDevice.js** archivo:</span><span class="sxs-lookup"><span data-stu-id="e6544-135">Add hello following `require` statements at hello start of hello **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="e6544-136">Agregue Hola después de la declaración de variable y reemplace el valor de marcador de posición de hello con hello cadena de conexión de centro de IoT para el centro de:</span><span class="sxs-lookup"><span data-stu-id="e6544-136">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="e6544-137">Crear centro de IoT tooyour de hello cliente tooopen Hola conexión.</span><span class="sxs-lookup"><span data-stu-id="e6544-137">Create hello client tooopen hello connection tooyour IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="e6544-138">Agregue Hola después de la función tooinvoke Hola método e impresión Hola dispositivo respuesta toohello consola del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="e6544-138">Add hello following function tooinvoke hello device method and print hello device response toohello console:</span></span>
   
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
8. <span data-ttu-id="e6544-139">Guarde y cierre hello **CallMethodOnDevice.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="e6544-139">Save and close hello **CallMethodOnDevice.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="e6544-140">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="e6544-140">Run hello apps</span></span>
<span data-ttu-id="e6544-141">Ya estás listo toorun Hola aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e6544-141">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="e6544-142">En un símbolo del sistema en hello **simulateddevice** carpeta, ejecute hello después de realizar escuchas para las llamadas de método desde el centro de IoT de toostart de comando:</span><span class="sxs-lookup"><span data-stu-id="e6544-142">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="e6544-143">En un símbolo del sistema en hello **callmethodondevice** carpeta, ejecute hello después toobegin de comando su centro de IoT de supervisión:</span><span class="sxs-lookup"><span data-stu-id="e6544-143">At a command prompt in hello **callmethodondevice** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="e6544-144">Podrá ver Hola dispositivo reaccionar toohello método por aplicación hello denominadas respuesta de hello método mostrar hello de dispositivo de Hola y el mensaje de bienvenida de la impresión:</span><span class="sxs-lookup"><span data-stu-id="e6544-144">You will see hello device react toohello method by printing out hello message and hello application which called hello method display hello response from hello device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="e6544-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e6544-145">Next steps</span></span>
<span data-ttu-id="e6544-146">En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="e6544-146">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="e6544-147">Utiliza este toomethods dispositivo identidad tooenable Hola simulada dispositivos aplicación tooreact invocado por la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6544-147">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="e6544-148">También crea una aplicación que invoca los métodos en el dispositivo de Hola y muestra la respuesta de hello de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6544-148">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="e6544-149">toocontinue introducción con el centro de IoT y tooexplore otros escenarios de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="e6544-149">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="e6544-150">[Introducción al Centro de IoT]</span><span class="sxs-lookup"><span data-stu-id="e6544-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="e6544-151">[Programación de trabajos en varios dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="e6544-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="e6544-152">toolearn cómo tooextend llama a su método de programación y de solución de IoT en varios dispositivos, vea hello [programación y los trabajos de difusión] [ lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="e6544-152">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
