---
title: "Introducción a la administración de dispositivos de IoT Hub de Azure (:NET y Node) | Microsoft Docs"
description: "Describe cómo usar la administración de dispositivos de IoT Hub de Azure para iniciar un reinicio del dispositivo remoto. Usará el SDK de dispositivo IoT de Azure para Node.js con el fin de implementar una aplicación de dispositivo simulado que incluye un método directo, además del SDK de servicio IoT de Azure para .NET con el objetivo de implementar una aplicación de servicio que invoque el método directo."
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
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: d97fc5493570985f94c23032c870628d6a089dcd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-device-management-netnode"></a><span data-ttu-id="8feda-104">Introducción a la administración de dispositivos (.NET y Node)</span><span class="sxs-lookup"><span data-stu-id="8feda-104">Get started with device management (.NET/Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="8feda-105">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="8feda-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="8feda-106">Usar Azure Portal para un IoT Hub y una identidad de dispositivo en este.</span><span class="sxs-lookup"><span data-stu-id="8feda-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="8feda-107">Crear una aplicación de dispositivo simulado que contiene un método directo que reinicia ese dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8feda-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="8feda-108">Los métodos directos se invocan desde la nube.</span><span class="sxs-lookup"><span data-stu-id="8feda-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="8feda-109">Crear una aplicación de consola de .NET que llame a un método directo de reinicio en la aplicación de dispositivo simulado mediante su centro de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8feda-109">Create a .NET console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="8feda-110">Al final de este tutorial, tendrá una aplicación de dispositivo de consola de Node.js y una aplicación back-end de consola .NET (C#):</span><span class="sxs-lookup"><span data-stu-id="8feda-110">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="8feda-111">**dmpatterns_getstarted_device.js**, que se conecta al IoT Hub con la identidad del dispositivo creada anteriormente, recibe un método directo de reinicio, simula un reinicio físico y notifica la hora del último reinicio.</span><span class="sxs-lookup"><span data-stu-id="8feda-111">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="8feda-112">**TriggerReboot**, que llama a un método directo en la aplicación de dispositivo simulado, muestra la respuesta y muestra las propiedades notificadas actualizadas.</span><span class="sxs-lookup"><span data-stu-id="8feda-112">**TriggerReboot**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="8feda-113">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8feda-113">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="8feda-114">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="8feda-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="8feda-115">Node.js versión 0.12.x o posteriores.</span><span class="sxs-lookup"><span data-stu-id="8feda-115">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="8feda-116">En [Preparación del entorno de desarrollo][lnk-dev-setup] se describe cómo instalar Node.js para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="8feda-116">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="8feda-117">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="8feda-117">An active Azure account.</span></span> <span data-ttu-id="8feda-118">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="8feda-118">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="8feda-119">Desencadenar un reinicio remoto en el dispositivo con un método directo</span><span class="sxs-lookup"><span data-stu-id="8feda-119">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="8feda-120">En esta sección, creará una aplicación de consola de .NET (mediante C#) que inicia una actualización remota en un dispositivo mediante un método directo.</span><span class="sxs-lookup"><span data-stu-id="8feda-120">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="8feda-121">La aplicación usa las consultas gemelas de dispositivo para detectar la hora en que se reinició por última vez el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8feda-121">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="8feda-122">En Visual Studio, agregue un proyecto de escritorio clásico de Windows de Visual C# a una nueva solución mediante la plantilla de proyecto **Aplicación de consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="8feda-122">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="8feda-123">Asegúrese de que la versión de .NET Framework sea 4.5.1 o una posterior.</span><span class="sxs-lookup"><span data-stu-id="8feda-123">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="8feda-124">Asigne al proyecto el nombre **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="8feda-124">Name the project **TriggerReboot**.</span></span>

    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createapp]

2. <span data-ttu-id="8feda-126">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **TriggerReboot** y, luego, haga clic en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="8feda-126">In Solution Explorer, right-click the **TriggerReboot** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="8feda-127">En la ventana **Administrador de paquetes NuGet**, seleccione **Examinar**, busque **microsoft.azure.devices**, seleccione **Instalar** para instalar el paquete **Microsoft.Azure.Devices** y acepte los términos de uso.</span><span class="sxs-lookup"><span data-stu-id="8feda-127">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="8feda-128">Este procedimiento permite descargar, instalar y agregar una referencia al [paquete NuGet del SDK de dispositivo de IoT de Azure][lnk-nuget-service-sdk] y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="8feda-128">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]
4. <span data-ttu-id="8feda-130">Agregue las siguientes instrucciones `using` al principio del archivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="8feda-130">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. <span data-ttu-id="8feda-131">Agregue los campos siguientes a la clase **Program** .</span><span class="sxs-lookup"><span data-stu-id="8feda-131">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="8feda-132">Sustituya el valor de marcador de posición por la cadena de conexión de IoT Hub que creó en la sección anterior y el dispositivo de destino.</span><span class="sxs-lookup"><span data-stu-id="8feda-132">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section and the target device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. <span data-ttu-id="8feda-133">Agregue el método siguiente a la clase **Program**.</span><span class="sxs-lookup"><span data-stu-id="8feda-133">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="8feda-134">Este código obtiene el dispositivo gemelo para el dispositivo de reinicio y genera las propiedades notificadas.</span><span class="sxs-lookup"><span data-stu-id="8feda-134">This code gets the device twin for the rebooting device and outputs the reported properties.</span></span>
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. <span data-ttu-id="8feda-135">Agregue el método siguiente a la clase **Program**.</span><span class="sxs-lookup"><span data-stu-id="8feda-135">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="8feda-136">Este código inicia el reinicio en el dispositivo mediante un método directo.</span><span class="sxs-lookup"><span data-stu-id="8feda-136">This code initiates the reboot on the device using a direct method.</span></span>

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. <span data-ttu-id="8feda-137">Por último, agregue las líneas siguientes al método **Main** :</span><span class="sxs-lookup"><span data-stu-id="8feda-137">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
8. <span data-ttu-id="8feda-138">Compile la solución.</span><span class="sxs-lookup"><span data-stu-id="8feda-138">Build the solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="8feda-139">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="8feda-139">Create a simulated device app</span></span>
<span data-ttu-id="8feda-140">En esta sección:</span><span class="sxs-lookup"><span data-stu-id="8feda-140">In this section, you will</span></span>

* <span data-ttu-id="8feda-141">Creará una aplicación de consola de Node.js que responda a un método directo que se llama desde la nube.</span><span class="sxs-lookup"><span data-stu-id="8feda-141">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="8feda-142">Desencadenará un reinicio del dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="8feda-142">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="8feda-143">Usará las propiedades notificadas para permitir consultas de dispositivo gemelo a fin de identificar los dispositivos y cuándo se reiniciaron por última vez.</span><span class="sxs-lookup"><span data-stu-id="8feda-143">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="8feda-144">Cree una nueva carpeta vacía denominada "**manageddevice**".</span><span class="sxs-lookup"><span data-stu-id="8feda-144">Create a new empty folder called **manageddevice**.</span></span>  <span data-ttu-id="8feda-145">En la carpeta **manageddevice** , cree un archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="8feda-145">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="8feda-146">Acepte todos los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="8feda-146">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="8feda-147">En el símbolo del sistema, en la carpeta **manageddevice**, ejecute el siguiente comando para instalar el paquete del SDK de dispositivo **azure-iot-device** y el paquete **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="8feda-147">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="8feda-148">Con un editor de texto, cree un nuevo archivo **dmpatterns_getstarted_device.js** en la carpeta **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="8feda-148">Using a text editor, create a new **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span></span>
4. <span data-ttu-id="8feda-149">Agregue las siguientes instrucciones "require" al principio del archivo **dmpatterns_getstarted_device.js**:</span><span class="sxs-lookup"><span data-stu-id="8feda-149">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="8feda-150">Agregue una variable **connectionString** y utilícela para crear una instancia de **cliente**.</span><span class="sxs-lookup"><span data-stu-id="8feda-150">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="8feda-151">Reemplace la cadena de conexión por la cadena de conexión del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8feda-151">Replace the connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="8feda-152">Agregue la siguiente función para implementar el método directo en el dispositivo</span><span class="sxs-lookup"><span data-stu-id="8feda-152">Add the following function to implement the direct method on the device</span></span>
   
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
7. <span data-ttu-id="8feda-153">Agregue el siguiente código para abrir la conexión al centro de IoT e iniciar la escucha del método directo:</span><span class="sxs-lookup"><span data-stu-id="8feda-153">Add the following code to open the connection to your IoT hub and start the direct method listener:</span></span>
   
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
8. <span data-ttu-id="8feda-154">Guarde y cierre el archivo **dmpatterns_getstarted_device.js**.</span><span class="sxs-lookup"><span data-stu-id="8feda-154">Save and close the **dmpatterns_getstarted_device.js** file.</span></span>
   
> [!NOTE]
> <span data-ttu-id="8feda-155">Por simplificar, este tutorial no implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="8feda-155">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="8feda-156">En el código de producción, deberá implementar directivas de reintentos (por ejemplo, retroceso exponencial), tal y como se sugiere en el artículo de MSDN [Transient Fault Handling][lnk-transient-faults] (Tratamiento de errores temporales).</span><span class="sxs-lookup"><span data-stu-id="8feda-156">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>


## <a name="run-the-apps"></a><span data-ttu-id="8feda-157">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="8feda-157">Run the apps</span></span>
<span data-ttu-id="8feda-158">Ya está preparado para ejecutar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="8feda-158">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="8feda-159">En el símbolo del sistema dentro de la carpeta **manageddevice**, ejecute el siguiente comando para iniciar la escucha del método directo de reinicio.</span><span class="sxs-lookup"><span data-stu-id="8feda-159">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="8feda-160">Ejecute la aplicación de consola de C# **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="8feda-160">Run the C# console app **TriggerReboot**.</span></span> <span data-ttu-id="8feda-161">Haga clic en el proyecto **TriggerReboot**, seleccione **Depurar** y luego seleccione **Iniciar nueva instancia**.</span><span class="sxs-lookup"><span data-stu-id="8feda-161">Right-click the **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span></span>

3. <span data-ttu-id="8feda-162">Verá la respuesta del dispositivo al método directo en la consola.</span><span class="sxs-lookup"><span data-stu-id="8feda-162">You see the device response to the direct method in the console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/