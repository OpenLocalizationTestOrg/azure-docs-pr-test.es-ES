---
title: Uso de las propiedades de dispositivos gemelos de IoT Hub de Azure (.NET y Node) | Microsoft Docs
description: "En este artículo se describe cómo usar los dispositivos gemelos de IoT Hub de Azure para configurar dispositivos. Usará el SDK de dispositivo IoT de Azure para Node.js con el fin de implementar una aplicación de dispositivo simulado, además del SDK de servicio IoT de Azure para .NET con el objetivo de implementar una aplicación de servicio que modifica una configuración de dispositivo que emplea un dispositivo gemelo."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 78b4523fa7d0c056f84214429730a5df1bcdcef7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-desired-properties-to-configure-devices"></a><span data-ttu-id="5cfa9-104">Uso de las propiedades deseadas para configurar dispositivos</span><span class="sxs-lookup"><span data-stu-id="5cfa9-104">Use desired properties to configure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="5cfa9-105">Al final de este tutorial tendrá dos aplicaciones de consola:</span><span class="sxs-lookup"><span data-stu-id="5cfa9-105">At the end of this tutorial, you will have two console apps:</span></span>

* <span data-ttu-id="5cfa9-106">**SimulateDeviceConfiguration.js**, una aplicación de dispositivo simulado que espera por una actualización de la configuración deseada y notifica el estado de un proceso de actualización de configuración simulada.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="5cfa9-107">**SetDesiredConfigurationAndQuery**, una aplicación .NET diseñada para ejecutarse desde el back-end, que establece la configuración deseada en un dispositivo y consulta el proceso de actualización de la configuración.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-107">**SetDesiredConfigurationAndQuery**, a .NET back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="5cfa9-108">En el artículo [SDK de IoT de Azure][lnk-hub-sdks] se proporciona información sobre los SDK que puede usar para crear aplicaciones de dispositivo y de back-end.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="5cfa9-109">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5cfa9-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="5cfa9-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="5cfa9-111">Node.js versión 0.10.x, o posteriores.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="5cfa9-112">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-112">An active Azure account.</span></span> <span data-ttu-id="5cfa9-113">En caso de no tener ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-113">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="5cfa9-114">Si ha seguido el tutorial [Introducción a los dispositivos gemelos][lnk-twin-tutorial], ya tiene una instancia de IoT Hub y una identidad de dispositivo denominada **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-114">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="5cfa9-115">En ese caso, puede ir directamente a la sección [Creación de la aplicación de dispositivo simulado][lnk-how-to-configure-createapp].</span><span class="sxs-lookup"><span data-stu-id="5cfa9-115">In that case, you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-the-simulated-device-app"></a><span data-ttu-id="5cfa9-116">Creación de la aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="5cfa9-116">Create the simulated device app</span></span>
<span data-ttu-id="5cfa9-117">En esta sección, creará una aplicación de consola de Node.js que se conecta a su centro como **myDeviceId**, espera por una actualización de la configuración deseada y, a continuación, informa de las actualizaciones en el proceso de actualización de configuración simulada.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-117">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="5cfa9-118">Cree una nueva carpeta vacía denominada **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-118">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="5cfa9-119">En la carpeta **simulatedeviceconfiguration** , cree un nuevo archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-119">In the **simulatedeviceconfiguration** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="5cfa9-120">Acepte todos los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-120">Accept all the defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="5cfa9-121">En el símbolo del sistema, en la carpeta **simulatedeviceconfiguration**, ejecute el siguiente comando para instalar **azure-iot-device** y los paquetes **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="5cfa9-121">At your command prompt in the **simulatedeviceconfiguration** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="5cfa9-122">Con un editor de texto, cree un nuevo archivo **SimulateDeviceConfiguration.js** en la carpeta **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-122">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in the **simulatedeviceconfiguration** folder.</span></span>
1. <span data-ttu-id="5cfa9-123">Agregue el código siguiente al archivo **SimulateDeviceConfiguration.js** y sustituya el marcador de posición **{device connection string}** con la cadena de conexión del dispositivo que copió al crear la identidad de dispositivo **myDeviceId**:</span><span class="sxs-lookup"><span data-stu-id="5cfa9-123">Add the following code to the **SimulateDeviceConfiguration.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    <span data-ttu-id="5cfa9-124">El objeto **Cliente** expone todos los métodos necesarios para interactuar con dispositivos gemelos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-124">The **Client** object exposes all the methods required to interact with device twins from the device.</span></span> <span data-ttu-id="5cfa9-125">Este código, inicializa el objeto **Cliente**, recupera el dispositivo gemelo de **myDeviceId** y, posteriormente, adjunta un controlador para la actualización en las *propiedades deseadas*.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-125">This code initializes the **Client** object, retrieves the device twin for **myDeviceId**, and then attaches a handler for the update on *desired properties*.</span></span> <span data-ttu-id="5cfa9-126">El controlador comprueba que hay una solicitud real de cambio de la configuración comparando los configId, y a continuación, invoca un método que inicia el cambio de configuración.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-126">The handler verifies that there is an actual configuration change request by comparing the configIds, then invokes a method that starts the configuration change.</span></span>
   
    <span data-ttu-id="5cfa9-127">Tenga en cuenta que, por simplicidad, este código usa un valor predeterminado codificado de forma rígida para la configuración inicial.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-127">Note that for the sake of simplicity, this code uses a hard-coded default for the initial configuration.</span></span> <span data-ttu-id="5cfa9-128">Una aplicación real probablemente cargaría esa configuración desde un almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-128">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="5cfa9-129">Los eventos de cambio de propiedad deseados siempre se emiten una vez en la conexión de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-129">Desired property change events are always emitted once at device connection.</span></span> <span data-ttu-id="5cfa9-130">Asegúrese de comprobar que hay un cambio real en las propiedades deseadas antes de realizar cualquier acción.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-130">Make sure to check that there is an actual change in the desired properties before performing any action.</span></span>
   > 
   > 
1. <span data-ttu-id="5cfa9-131">Agregue los métodos siguientes antes de la invocación `client.open()`:</span><span class="sxs-lookup"><span data-stu-id="5cfa9-131">Add the following methods before the `client.open()` invocation:</span></span>
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    <span data-ttu-id="5cfa9-132">El método **initConfigChange** actualiza propiedades notificadas en el objeto del dispositivo gemelo local con la solicitud de actualización de la configuración y establece el estado en **Pendiente**, a continuación, actualiza el dispositivo gemelo en el servicio.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-132">The **initConfigChange** method updates the reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="5cfa9-133">Después de actualizar correctamente el dispositivo gemelo, simula un proceso de ejecución prolongada que finaliza en la ejecución de **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-133">After successfully updating the device twin, it simulates a long running process that terminates in the execution of **completeConfigChange**.</span></span> <span data-ttu-id="5cfa9-134">Este método actualiza las propiedades notificadas locales estableciendo el estado en **Correcto** y eliminado el objeto **pendingConfig**.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-134">This method updates the local reported properties setting the status to **Success** and removing the **pendingConfig** object.</span></span> <span data-ttu-id="5cfa9-135">A continuación, actualiza el dispositivo gemelo en el servicio.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-135">It then updates the device twin on the service.</span></span>
   
    <span data-ttu-id="5cfa9-136">Tenga en cuenta que, para ahorrar ancho de banda, las propiedades notificadas se actualizan especificando solo las propiedades que se van a modificar (denominadas **revisión** en el código anterior), en lugar de reemplazar el documento completo.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-136">Note that, to save bandwidth, reported properties are updated by specifying only the properties to be modified (named **patch** in the above code), instead of replacing the whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5cfa9-137">Este tutorial no simula ningún comportamiento de las actualizaciones de configuración simultáneas.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-137">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="5cfa9-138">Algunos procesos de actualización de configuración pueden dar cabida a cambios de configuración de destino mientras se está ejecutando la actualización, otros tiene que ponerlos en cola, y otros podría rechazarlos con una condición de error.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-138">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, some might have to queue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="5cfa9-139">Asegúrese de que considera el comportamiento deseado para el proceso de configuración específica y agregue la lógica adecuada antes de iniciar el cambio de configuración.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-139">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="5cfa9-140">Ejecute la aplicación del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="5cfa9-140">Run the device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="5cfa9-141">Verá el mensaje `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-141">You should see the message `retrieved device twin`.</span></span> <span data-ttu-id="5cfa9-142">Mantenga la aplicación en ejecución.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-142">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="5cfa9-143">Creación de la aplicación de servicio</span><span class="sxs-lookup"><span data-stu-id="5cfa9-143">Create the service app</span></span>
<span data-ttu-id="5cfa9-144">En esta sección, creará una aplicación de consola .NET que actualiza las *propiedades deseadas* en el dispositivo gemelo asociado con **myDeviceId** con un nuevo objeto de configuración de telemetría.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-144">In this section, you will create a .NET console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="5cfa9-145">A continuación, consulta los dispositivos gemelos almacenados en IoT Hub y muestra la diferencia entre las configuraciones deseada y notificada del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-145">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="5cfa9-146">En Visual Studio, agregue un proyecto de escritorio clásico de Windows de Visual C# a la solución actual mediante la plantilla de proyecto **Aplicación de consola** .</span><span class="sxs-lookup"><span data-stu-id="5cfa9-146">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="5cfa9-147">Asigne el nombre **SetDesiredConfigurationAndQuery** al proyecto.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-147">Name the project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createapp]
1. <span data-ttu-id="5cfa9-149">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **SetDesiredConfigurationAndQuery** y luego seleccione **Administrar paquetes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-149">In Solution Explorer, right-click the **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="5cfa9-150">En la ventana **Administrador de paquetes NuGet**, seleccione **Examinar**, busque **microsoft.azure.devices**, seleccione **Instalar** para instalar el paquete **Microsoft.Azure.Devices** y acepte los términos de uso.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-150">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="5cfa9-151">Este procedimiento permite descargar, instalar y agregar una referencia al [paquete NuGet del SDK de dispositivo de IoT de Azure][lnk-nuget-service-sdk] y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-151">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]
1. <span data-ttu-id="5cfa9-153">Agregue las siguientes instrucciones `using` al principio del archivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="5cfa9-153">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="5cfa9-154">Agregue los campos siguientes a la clase **Program** .</span><span class="sxs-lookup"><span data-stu-id="5cfa9-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="5cfa9-155">Sustituya el valor de marcador de posición por la cadena de conexión de IoT Hub para el centro que creó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-155">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="5cfa9-156">Agregue el método siguiente a la clase **Program** :</span><span class="sxs-lookup"><span data-stu-id="5cfa9-156">Add the following method to the **Program** class:</span></span>
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            try
            {
                while (true)
                {
                    var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                    var results = await query.GetNextAsTwinAsync();
                    foreach (var result in results)
                    {
                        Console.WriteLine("Config report for: {0}", result.DeviceId);
                        Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine();
                    }
                    Thread.Sleep(10000);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
   
    <span data-ttu-id="5cfa9-157">El objeto **Registro** expone todos los métodos necesarios para interactuar con dispositivos gemelos del servicio.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-157">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="5cfa9-158">Este código inicializa el objeto **Registro**, recupera el dispositivo gemelo de **myDeviceId** y actualiza sus propiedades deseadas con un nuevo objeto de configuración de telemetría.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-158">This code initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="5cfa9-159">Después, cada 10 segundos, consulta los dispositivos gemelos almacenados en IoT Hub e imprime las configuraciones de telemetría deseadas y notificadas.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-159">After that, it queries the device twins stored in the IoT hub every 10 seconds, and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="5cfa9-160">Consulte el [lenguaje de consulta de IoT Hub][lnk-query] para obtener información sobre cómo generar informes completos en todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-160">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="5cfa9-161">Esta aplicación consulta IoT Hub cada 10 segundos con fines ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-161">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="5cfa9-162">Use consultas para generar informes de cara al usuario en muchos dispositivos y no para detectar cambios.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-162">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="5cfa9-163">Si la solución requiere notificaciones en tiempo real de eventos de dispositivo, use [notificaciones gemelas][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="5cfa9-163">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="5cfa9-164">Por último, agregue las líneas siguientes al método **Main** :</span><span class="sxs-lookup"><span data-stu-id="5cfa9-164">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key to quit.");
        Console.ReadLine();
1. <span data-ttu-id="5cfa9-165">En el Explorador de soluciones, abra **Establecer proyectos de inicio...** y asegúrese de que la **acción** de **SetDesiredConfigurationAndQuery** sea **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-165">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="5cfa9-166">Compile la solución.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-166">Build the solution.</span></span>
1. <span data-ttu-id="5cfa9-167">Con **SimulateDeviceConfiguration.js** ejecutándose, ejecute la aplicación .NET desde Visual Studio mediante **F5** y debería ver cómo la configuración notificada cambia de **Correcto** a **Pendiente** a **Correcto** de nuevo con la nueva frecuencia de envío activa de cinco minutos en lugar de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-167">With **SimulateDeviceConfiguration.js** running, run the .NET application from Visual Studio using **F5** and you should see the reported configuration change from **Success** to **Pending** to **Success** again with the new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Dispositivo configurado correctamente][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="5cfa9-169">Hay un retraso de hasta un minuto entre la operación de informe de dispositivo y el resultado de la consulta.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-169">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="5cfa9-170">Esto es para habilitar la infraestructura de consulta para que funcione a gran escala.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-170">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="5cfa9-171">Para recuperar vistas coherentes de un único dispositivo gemelo, use el método **getDeviceTwin** en la clase **Registro**.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-171">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="5cfa9-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5cfa9-172">Next steps</span></span>
<span data-ttu-id="5cfa9-173">En este tutorial, ha establecido una configuración deseada como *propiedades deseadas* desde el back-end de solución, y ha escrito una aplicación de dispositivo para detectar ese cambio y simular un proceso de actualización de varios pasos que informe de su estado mediante las propiedades notificadas.</span><span class="sxs-lookup"><span data-stu-id="5cfa9-173">In this tutorial, you set a desired configuration as *desired properties* from the solution back end, and wrote a device app to detect that change and simulate a multi-step update process reporting its status through the reported properties.</span></span>

<span data-ttu-id="5cfa9-174">Use los siguientes recursos para obtener información sobre cómo:</span><span class="sxs-lookup"><span data-stu-id="5cfa9-174">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="5cfa9-175">enviar telemetría desde dispositivos con el tutorial [Introducción a IoT Hub][lnk-iothub-getstarted];</span><span class="sxs-lookup"><span data-stu-id="5cfa9-175">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="5cfa9-176">programar o realizar operaciones en grandes conjuntos de dispositivos (consulte el tutorial [Schedule and broadcast jobs][lnk-schedule-jobs] [Programación y difusión de trabajos]);</span><span class="sxs-lookup"><span data-stu-id="5cfa9-176">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="5cfa9-177">controlar los dispositivos de forma interactiva (por ejemplo, encender un ventilador desde una aplicación controlada por el usuario), con el tutorial [Uso de métodos directos][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="5cfa9-177">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app
