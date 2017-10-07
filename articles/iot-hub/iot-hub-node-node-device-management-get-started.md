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
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="2cc2b-104">Introducción a la administración de dispositivos (Node)</span><span class="sxs-lookup"><span data-stu-id="2cc2b-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="2cc2b-105">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="2cc2b-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="2cc2b-106">Usar hello toocreate portal Azure un centro de IoT y cree una identidad de dispositivo en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="2cc2b-107">Crear una aplicación de dispositivo simulado que contiene un método directo que reinicia ese dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="2cc2b-108">Se invocan métodos directos de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="2cc2b-109">Crear una aplicación de consola de Node.js que llama a métodos directas de reinicio de hello en la aplicación de dispositivo simulado de hello a través de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-109">Create a Node.js console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="2cc2b-110">Al final de Hola de este tutorial, tiene dos aplicaciones de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="2cc2b-110">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="2cc2b-111">**dmpatterns_getstarted_device.js**, centro de IoT tooyour que conecta con la identidad del dispositivo Hola creado anteriormente, recibe un método directo de reinicio, simula reiniciar el equipo físico e informa Hola el tiempo de último reinicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="2cc2b-112">**dmpatterns_getstarted_service.js**, que llama a un método directo en la aplicación de dispositivo simulado de hello, muestra la respuesta de Hola y Hola muestra actualizado notificado propiedades.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-112">**dmpatterns_getstarted_service.js**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="2cc2b-113">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="2cc2b-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="2cc2b-114">Node.js versión 0.12.x o posteriores.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="2cc2b-115">[Preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall Node.js para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-115">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="2cc2b-116">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-116">An active Azure account.</span></span> <span data-ttu-id="2cc2b-117">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="2cc2b-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="2cc2b-118">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="2cc2b-118">Create a simulated device app</span></span>
<span data-ttu-id="2cc2b-119">En esta sección:</span><span class="sxs-lookup"><span data-stu-id="2cc2b-119">In this section, you will</span></span>

* <span data-ttu-id="2cc2b-120">Crear una aplicación de consola de Node.js que responde tooa método directo llamado en la nube Hola</span><span class="sxs-lookup"><span data-stu-id="2cc2b-120">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="2cc2b-121">Desencadenará un reinicio del dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="2cc2b-122">Hola uso notificado propiedades tooenable dispositivos gemelas consultas tooidentify dispositivos y cuándo reinició por última vez</span><span class="sxs-lookup"><span data-stu-id="2cc2b-122">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="2cc2b-123">Cree una nueva carpeta vacía denominada **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="2cc2b-124">Hola **manageddevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-124">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="2cc2b-125">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="2cc2b-125">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="2cc2b-126">En el símbolo del sistema en hello **manageddevice** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure** paquete del SDK de dispositivo y **azure iot dispositivo-mqtt**paquete:</span><span class="sxs-lookup"><span data-stu-id="2cc2b-126">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="2cc2b-127">Con un editor de texto, cree un **dmpatterns_getstarted_device.js** archivo Hola **manageddevice** carpeta.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="2cc2b-128">Agregar siguiente hello 'requiere' instrucciones al principio de Hola de hello **dmpatterns_getstarted_device.js** archivo:</span><span class="sxs-lookup"><span data-stu-id="2cc2b-128">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="2cc2b-129">Agregar un **connectionString** variable y utilizar toocreate un **cliente** instancia.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-129">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="2cc2b-130">Reemplace la cadena de conexión de hello con la cadena de conexión del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-130">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="2cc2b-131">Agregar Hola siguiendo métodos directas de función tooimplement hello en dispositivo Hola</span><span class="sxs-lookup"><span data-stu-id="2cc2b-131">Add hello following function tooimplement hello direct method on hello device</span></span>
   
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
7. <span data-ttu-id="2cc2b-132">Abrir el centro de IoT de hello conexión tooyour e iniciar el agente de escucha de hello método directo:</span><span class="sxs-lookup"><span data-stu-id="2cc2b-132">Open hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
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
8. <span data-ttu-id="2cc2b-133">Guarde y cierre hello **dmpatterns_getstarted_device.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-133">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="2cc2b-134">tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-134">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="2cc2b-135">En el código de producción, debe implementar directivas de reintento (por ejemplo, un retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="2cc2b-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="2cc2b-136">Desencadenar un reinicio remoto en dispositivo Hola utilizando un método directo</span><span class="sxs-lookup"><span data-stu-id="2cc2b-136">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="2cc2b-137">En esta sección, creará una aplicación de consola de Node.js que inicia un reinicio remoto en un dispositivo mediante un método directo.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="2cc2b-138">aplicación Hello usa Hola de toodiscover de consultas última hora de reinicio de dispositivo gemelas para dicho dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-138">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="2cc2b-139">Cree una carpeta vacía denominada **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="2cc2b-140">Hola **triggerrebootondevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-140">In hello **triggerrebootondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="2cc2b-141">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="2cc2b-141">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="2cc2b-142">En el símbolo del sistema en hello **triggerrebootondevice** carpeta, ejecute hello después comando tooinstall hello **el centro de IOT de azure** paquete del SDK de dispositivo y **azure iot dispositivo-mqtt** paquete:</span><span class="sxs-lookup"><span data-stu-id="2cc2b-142">At your command prompt in hello **triggerrebootondevice** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="2cc2b-143">Con un editor de texto, cree un **dmpatterns_getstarted_service.js** archivo Hola **triggerrebootondevice** carpeta.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="2cc2b-144">Agregar siguiente hello 'requiere' instrucciones al principio de Hola de hello **dmpatterns_getstarted_service.js** archivo:</span><span class="sxs-lookup"><span data-stu-id="2cc2b-144">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="2cc2b-145">Agregue Hola siguiendo las declaraciones de variable y reemplace los valores de marcador de posición de hello:</span><span class="sxs-lookup"><span data-stu-id="2cc2b-145">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="2cc2b-146">Agregue Hola después de la función tooinvoke Hola dispositivo método tooreboot Hola dispositivo de destino:</span><span class="sxs-lookup"><span data-stu-id="2cc2b-146">Add hello following function tooinvoke hello device method tooreboot hello target device:</span></span>
   
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
7. <span data-ttu-id="2cc2b-147">Agregar siguiente Hola función tooquery para dispositivo hello y obtener Hola última hora de reinicio:</span><span class="sxs-lookup"><span data-stu-id="2cc2b-147">Add hello following function tooquery for hello device and get hello last reboot time:</span></span>
   
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
8. <span data-ttu-id="2cc2b-148">Agregue Hola siguiendo las funciones de código toocall Hola que desencadenan Hola reinicie método directo y consultar Hola reiniciar última hora:</span><span class="sxs-lookup"><span data-stu-id="2cc2b-148">Add hello following code toocall hello functions that trigger hello reboot direct method and query for hello last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="2cc2b-149">Guarde y cierre hello **dmpatterns_getstarted_service.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-149">Save and close hello **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="2cc2b-150">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="2cc2b-150">Run hello apps</span></span>
<span data-ttu-id="2cc2b-151">Ya estás listo toorun Hola aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-151">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="2cc2b-152">En línea de comandos de Hola Hola **manageddevice** carpeta, ejecute hello después toobegin comando realizar escuchas de método directo de reinicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-152">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="2cc2b-153">En línea de comandos de Hola Hola **triggerrebootondevice** carpeta, ejecute hello después comando tootrigger Hola remoto de reinicio y de consulta de Hola de hello dispositivo gemelas toofind reiniciar última hora.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-153">At hello command prompt in hello **triggerrebootondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="2cc2b-154">Consulte dispositivo respuesta toohello directo método hello en la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="2cc2b-154">You see hello device response toohello direct method in hello console.</span></span>

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
