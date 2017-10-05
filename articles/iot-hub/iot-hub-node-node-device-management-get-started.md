---
title: "Introducción a la administración de dispositivos de IoT Hub de Azure (Node) | Microsoft Docs"
description: "Describe cómo usar la administración de dispositivos de IoT Hub para iniciar un reinicio del dispositivo remoto. Usará los SDK de IoT de Azure para Node.js con el fin de implementar una aplicación de dispositivo simulado que incluye un método directo y un servicio que invoque el método directo."
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
ms.openlocfilehash: 332a3e62cb1ef75e2c6dd5562ee799465c401128
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="2dd38-104">Introducción a la administración de dispositivos (Node)</span><span class="sxs-lookup"><span data-stu-id="2dd38-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="2dd38-105">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="2dd38-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="2dd38-106">Usar Azure Portal para un IoT Hub y una identidad de dispositivo en este.</span><span class="sxs-lookup"><span data-stu-id="2dd38-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="2dd38-107">Crear una aplicación de dispositivo simulado que contiene un método directo que reinicia ese dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2dd38-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="2dd38-108">Los métodos directos se invocan desde la nube.</span><span class="sxs-lookup"><span data-stu-id="2dd38-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="2dd38-109">Crear una aplicación de consola de Node.js que llame a un método directo de reinicio en la aplicación de dispositivo simulado mediante su centro de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2dd38-109">Create a Node.js console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="2dd38-110">Al final de este tutorial tendrá dos aplicaciones de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="2dd38-110">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="2dd38-111">**dmpatterns_getstarted_device.js**, que se conecta al IoT Hub con la identidad del dispositivo creada anteriormente, recibe un método directo de reinicio, simula un reinicio físico y notifica la hora del último reinicio.</span><span class="sxs-lookup"><span data-stu-id="2dd38-111">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="2dd38-112">**dmpatterns_getstarted_service.js**, que llama a un método directo en la aplicación de dispositivo simulado, muestra la respuesta y muestra las propiedades notificadas actualizadas.</span><span class="sxs-lookup"><span data-stu-id="2dd38-112">**dmpatterns_getstarted_service.js**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="2dd38-113">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2dd38-113">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="2dd38-114">Node.js versión 0.12.x o posteriores.</span><span class="sxs-lookup"><span data-stu-id="2dd38-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="2dd38-115">En [Preparación del entorno de desarrollo][lnk-dev-setup] se describe cómo instalar Node.js para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="2dd38-115">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="2dd38-116">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="2dd38-116">An active Azure account.</span></span> <span data-ttu-id="2dd38-117">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="2dd38-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="2dd38-118">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="2dd38-118">Create a simulated device app</span></span>
<span data-ttu-id="2dd38-119">En esta sección:</span><span class="sxs-lookup"><span data-stu-id="2dd38-119">In this section, you will</span></span>

* <span data-ttu-id="2dd38-120">Creará una aplicación de consola de Node.js que responda a un método directo que se llama desde la nube.</span><span class="sxs-lookup"><span data-stu-id="2dd38-120">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="2dd38-121">Desencadenará un reinicio del dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="2dd38-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="2dd38-122">Usará las propiedades notificadas para permitir consultas de dispositivo gemelo a fin de identificar los dispositivos y cuándo se reiniciaron por última vez.</span><span class="sxs-lookup"><span data-stu-id="2dd38-122">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="2dd38-123">Cree una nueva carpeta vacía denominada **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="2dd38-124">En la carpeta **manageddevice** , cree un archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="2dd38-124">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="2dd38-125">Acepte todos los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="2dd38-125">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="2dd38-126">En el símbolo del sistema, en la carpeta **manageddevice**, ejecute el siguiente comando para instalar el paquete del SDK de dispositivo **azure-iot-device** y el paquete **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="2dd38-126">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="2dd38-127">Con un editor de texto, cree un archivo **dmpatterns_getstarted_device.js** en la carpeta **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span></span>
4. <span data-ttu-id="2dd38-128">Agregue las siguientes instrucciones "require" al principio del archivo **dmpatterns_getstarted_device.js**:</span><span class="sxs-lookup"><span data-stu-id="2dd38-128">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="2dd38-129">Agregue una variable **connectionString** y utilícela para crear una instancia de **cliente**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-129">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="2dd38-130">Reemplace la cadena de conexión por la cadena de conexión del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2dd38-130">Replace the connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="2dd38-131">Agregue la siguiente función para implementar el método directo en el dispositivo</span><span class="sxs-lookup"><span data-stu-id="2dd38-131">Add the following function to implement the direct method on the device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report the reboot before the physical restart
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
7. <span data-ttu-id="2dd38-132">Abra la conexión al IoT Hub e inicie la escucha del método directo:</span><span class="sxs-lookup"><span data-stu-id="2dd38-132">Open the connection to your IoT hub and start the direct method listener:</span></span>
   
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
8. <span data-ttu-id="2dd38-133">Guarde y cierre el archivo **dmpatterns_getstarted_device.js**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-133">Save and close the **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="2dd38-134">Por simplificar, este tutorial no implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="2dd38-134">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="2dd38-135">En el código de producción, deberá implementar directivas de reintentos (por ejemplo, retroceso exponencial), tal y como se sugiere en el artículo de MSDN [Transient Fault Handling][lnk-transient-faults] (Tratamiento de errores temporales).</span><span class="sxs-lookup"><span data-stu-id="2dd38-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="2dd38-136">Desencadenar un reinicio remoto en el dispositivo con un método directo</span><span class="sxs-lookup"><span data-stu-id="2dd38-136">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="2dd38-137">En esta sección, creará una aplicación de consola de Node.js que inicia un reinicio remoto en un dispositivo mediante un método directo.</span><span class="sxs-lookup"><span data-stu-id="2dd38-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="2dd38-138">La aplicación usa las consultas gemelas de dispositivo para detectar la hora en que se reinició por última vez el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2dd38-138">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="2dd38-139">Cree una carpeta vacía denominada **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="2dd38-140">En la carpeta **triggerrebootondevice**, cree un archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="2dd38-140">In the **triggerrebootondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="2dd38-141">Acepte todos los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="2dd38-141">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="2dd38-142">En el símbolo del sistema, en la carpeta **triggerrebootondevice**, ejecute el siguiente comando para instalar el paquete del SDK de dispositivo **azure-iothub** y el paquete **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="2dd38-142">At your command prompt in the **triggerrebootondevice** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="2dd38-143">Con un editor de texto, cree un archivo **dmpatterns_getstarted_service.js** en la carpeta **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="2dd38-144">Agregue las siguientes instrucciones "require" al principio del archivo **dmpatterns_getstarted_service.js**:</span><span class="sxs-lookup"><span data-stu-id="2dd38-144">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="2dd38-145">Agregue las siguientes declaraciones de variable y reemplace los valores de marcador de posición:</span><span class="sxs-lookup"><span data-stu-id="2dd38-145">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="2dd38-146">Agregue la siguiente función para invocar el método del dispositivo con el fin de reiniciar el dispositivo de destino:</span><span class="sxs-lookup"><span data-stu-id="2dd38-146">Add the following function to invoke the device method to reboot the target device:</span></span>
   
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
                console.log("Successfully invoked the device to reboot.");  
            }
        });
    };
    ```
7. <span data-ttu-id="2dd38-147">Agregue la siguiente función para consultar el dispositivo y obtener la última hora de reinicio:</span><span class="sxs-lookup"><span data-stu-id="2dd38-147">Add the following function to query for the device and get the last reboot time:</span></span>
   
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
                console.log('Waiting for device to report last reboot time.');
        });
    };
    ```
8. <span data-ttu-id="2dd38-148">Agregue el siguiente código para llamar a las funciones que desencadenan el método directo de reinicio y la consulta de última hora de reinicio:</span><span class="sxs-lookup"><span data-stu-id="2dd38-148">Add the following code to call the functions that trigger the reboot direct method and query for the last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="2dd38-149">Guarde y cierre el archivo **dmpatterns_getstarted_service.js**.</span><span class="sxs-lookup"><span data-stu-id="2dd38-149">Save and close the **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="2dd38-150">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="2dd38-150">Run the apps</span></span>
<span data-ttu-id="2dd38-151">Ya está preparado para ejecutar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2dd38-151">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="2dd38-152">En el símbolo del sistema dentro de la carpeta **manageddevice**, ejecute el siguiente comando para iniciar la escucha del método directo de reinicio.</span><span class="sxs-lookup"><span data-stu-id="2dd38-152">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="2dd38-153">En el símbolo del sistema dentro de la carpeta **triggerrebootondevice**, ejecute el siguiente comando para desencadenar el reinicio remoto y la consulta en el dispositivo gemelo para buscar la hora del último reinicio.</span><span class="sxs-lookup"><span data-stu-id="2dd38-153">At the command prompt in the **triggerrebootondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="2dd38-154">Verá la respuesta del dispositivo al método directo en la consola.</span><span class="sxs-lookup"><span data-stu-id="2dd38-154">You see the device response to the direct method in the console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
