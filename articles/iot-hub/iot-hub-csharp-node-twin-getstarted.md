---
title: "Introducción a los dispositivos gemelos de IoT Hub de Azure (.NET y Node) | Microsoft Docs"
description: "Describe cómo usar dispositivos gemelos de IoT Hub de Azure para agregar etiquetas y, luego, usar una consulta de IoT Hub. Usará el SDK de dispositivo IoT de Azure para Node.js con el fin de implementar una aplicación de dispositivo simulado, además del SDK de servicio IoT de Azure para .NET con el objetivo de implementar una aplicación de servicio que agrega las etiquetas y ejecuta la consulta de IoT Hub."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: elioda
ms.openlocfilehash: 07797b9159c9b926e9eb47d8864c63048951931a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="19506-104">Introducción a los dispositivos gemelos (.NET y Node)</span><span class="sxs-lookup"><span data-stu-id="19506-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="19506-105">Al final de este tutorial tendrá una aplicación de consola Node.js y .NET:</span><span class="sxs-lookup"><span data-stu-id="19506-105">At the end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="19506-106">**AddTagsAndQuery.js**, una aplicación de .NET de back-end diseñada para ejecutarse desde el back-end, que agrega etiquetas y consulta dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="19506-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="19506-107">**TwinSimulatedDevice.js**, una aplicación de Node.js que simula un dispositivo que se conecta a su centro de IoT con la identidad del dispositivo creada anteriormente e informa de su estado de conectividad.</span><span class="sxs-lookup"><span data-stu-id="19506-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="19506-108">En el artículo [SDK de IoT de Azure][lnk-hub-sdks] se proporciona información sobre los SDK que puede usar para crear aplicaciones de dispositivo y de back-end.</span><span class="sxs-lookup"><span data-stu-id="19506-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="19506-109">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="19506-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="19506-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="19506-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="19506-111">Node.js versión 0.10.x, o posteriores.</span><span class="sxs-lookup"><span data-stu-id="19506-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="19506-112">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="19506-112">An active Azure account.</span></span> <span data-ttu-id="19506-113">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="19506-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="19506-114">Creación de la aplicación de servicio</span><span class="sxs-lookup"><span data-stu-id="19506-114">Create the service app</span></span>
<span data-ttu-id="19506-115">En esta sección, creará una aplicación de consola de .NET (que usa C#) que agrega metadatos de ubicación al dispositivo gemelo asociado con **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="19506-115">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="19506-116">A continuación, consulta los dispositivos gemelos almacenados en IoT Hub seleccionando los dispositivos ubicados en Estados Unidos y, después, los que informan de una conexión de red de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="19506-116">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="19506-117">En Visual Studio, agregue un proyecto de escritorio clásico de Windows de Visual C# a la solución actual mediante la plantilla de proyecto **Aplicación de consola** .</span><span class="sxs-lookup"><span data-stu-id="19506-117">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="19506-118">Asigne el nombre **AddTagsAndQuery** al proyecto.</span><span class="sxs-lookup"><span data-stu-id="19506-118">Name the project **AddTagsAndQuery**.</span></span>
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createapp]
1. <span data-ttu-id="19506-120">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **AddTagsAndQuery** y luego seleccione **Administrar paquetes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="19506-120">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="19506-121">En la ventana **Administrador de paquetes NuGet**, seleccione **Examinar** y busque **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="19506-121">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="19506-122">Seleccione **Instalar** para instalar el paquete **Microsoft.Azure.Devices** y acepte las condiciones de uso.</span><span class="sxs-lookup"><span data-stu-id="19506-122">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="19506-123">Este procedimiento permite descargar, instalar y agregar una referencia al [paquete NuGet del SDK de dispositivo de IoT de Azure][lnk-nuget-service-sdk] y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="19506-123">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]
1. <span data-ttu-id="19506-125">Agregue las siguientes instrucciones `using` al principio del archivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="19506-125">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="19506-126">Agregue los campos siguientes a la clase **Program** .</span><span class="sxs-lookup"><span data-stu-id="19506-126">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="19506-127">Sustituya el valor de marcador de posición por la cadena de conexión de IoT Hub para el centro que creó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="19506-127">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="19506-128">Agregue el método siguiente a la clase **Program** :</span><span class="sxs-lookup"><span data-stu-id="19506-128">Add the following method to the **Program** class:</span></span>
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    <span data-ttu-id="19506-129">La clase **RegistryManager** expone todos los métodos necesarios para interactuar con dispositivos gemelos del servicio.</span><span class="sxs-lookup"><span data-stu-id="19506-129">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="19506-130">El código anterior inicializa primero el objeto **registryManager**, luego recupera el dispositivo gemelo de **myDeviceId** y, por último, actualiza sus etiquetas con la información de la ubicación deseada.</span><span class="sxs-lookup"><span data-stu-id="19506-130">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="19506-131">Después de la actualización, ejecuta dos consultas: la primera selecciona solo los dispositivos gemelos que se encuentran en la planta **Redmond43** y la segunda mejora la consulta para seleccionar solo los dispositivos que están también conectados a través de la red de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="19506-131">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="19506-132">Tenga en cuenta que el código anterior, cuando crea el objeto de **consulta**, especifica un número máximo de documentos devueltos.</span><span class="sxs-lookup"><span data-stu-id="19506-132">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="19506-133">El objeto **consulta** contiene una propiedad booleana **HasMoreResults** que puede utilizar para invocar a los métodos **GetNextAsTwinAsync** varias veces para recuperar todos los resultados.</span><span class="sxs-lookup"><span data-stu-id="19506-133">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="19506-134">Un método llamado **GetNextAsJson** está disponible para los resultados que no son dispositivos gemelos, por ejemplo, los resultados de consultas de agregación.</span><span class="sxs-lookup"><span data-stu-id="19506-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="19506-135">Por último, agregue las líneas siguientes al método **Main** :</span><span class="sxs-lookup"><span data-stu-id="19506-135">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="19506-136">En el Explorador de soluciones, abra **Establecer proyectos de inicio...** y asegúrese de que la **acción** de **AddTagsAndQuery** sea **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="19506-136">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="19506-137">Compile la solución.</span><span class="sxs-lookup"><span data-stu-id="19506-137">Build the solution.</span></span>
1. <span data-ttu-id="19506-138">Ejecute esta aplicación haciendo clic con el botón derecho en el proyecto **AddTagsAndQuery** y seleccionando **Depurar**, seguido de **Iniciar nueva instancia**.</span><span class="sxs-lookup"><span data-stu-id="19506-138">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="19506-139">Debería ver un dispositivo en los resultados de la consulta que pregunta por todos los dispositivos que se encuentran en **Redmond43** y ninguno para la consulta que restringe los resultados a los dispositivos que utilizan una red de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="19506-139">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![Resultados de consulta en ventana][img-addtagapp]

<span data-ttu-id="19506-141">En la siguiente sección, creará una aplicación de dispositivo que notifica la información de conectividad y cambia el resultado de la consulta en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="19506-141">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="19506-142">Creación de la aplicación del dispositivo</span><span class="sxs-lookup"><span data-stu-id="19506-142">Create the device app</span></span>
<span data-ttu-id="19506-143">En esta sección, creará una aplicación de consola de Node.js que se conecta al centro como **myDeviceId**, y luego actualiza las propiedades notificadas para contener la información que está conectada mediante una red de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="19506-143">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="19506-144">Cree una nueva carpeta vacía denominada **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="19506-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="19506-145">En la carpeta **reportconnectivity** , cree un nuevo archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="19506-145">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="19506-146">Acepte todos los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="19506-146">Accept all the defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="19506-147">En el símbolo del sistema, en la carpeta **reportconnectivity**, ejecute el siguiente comando para instalar **azure-iot-device** y el paquete **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="19506-147">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="19506-148">Con un editor de texto, cree un nuevo archivo **ReportConnectivity.js** en la carpeta **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="19506-148">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="19506-149">Agregue el código siguiente al archivo **ReportConnectivity.js** y sustituya el marcador de posición de la cadena de conexión del dispositivo por la cadena que copió al crear la identidad de dispositivo **myDeviceId**:</span><span class="sxs-lookup"><span data-stu-id="19506-149">Add the following code to the **ReportConnectivity.js** file, and substitute the placeholder for device connection string with the one you copied when you created the **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    <span data-ttu-id="19506-150">El objeto **Cliente** expone todos los métodos necesarios para interactuar con dispositivos gemelos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="19506-150">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="19506-151">El código anterior, una vez que inicialice el objeto **Cliente**, recupera el dispositivo gemelo de **myDeviceId**, y actualiza su propiedad notificada con la información de conectividad.</span><span class="sxs-lookup"><span data-stu-id="19506-151">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
1. <span data-ttu-id="19506-152">Ejecute la aplicación del dispositivo</span><span class="sxs-lookup"><span data-stu-id="19506-152">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="19506-153">Verá el mensaje `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="19506-153">You should see the message `twin state reported`.</span></span>
1. <span data-ttu-id="19506-154">Ahora que el dispositivo ha informado sobre su información de conectividad, debe aparecer en ambas consultas.</span><span class="sxs-lookup"><span data-stu-id="19506-154">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="19506-155">Ejecute la aplicación **AddTagsAndQuery** .NET para volver a ejecutar las consultas.</span><span class="sxs-lookup"><span data-stu-id="19506-155">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="19506-156">Esta vez **myDeviceId** debe aparecer en los resultados de ambas consulta.</span><span class="sxs-lookup"><span data-stu-id="19506-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="19506-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="19506-157">Next steps</span></span>
<span data-ttu-id="19506-158">En este tutorial, configuró un centro de IoT nuevo en Azure Portal y, después, creó una identidad de dispositivo en el registro de identidades del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="19506-158">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="19506-159">Ha agregado metadatos de dispositivo como etiquetas desde una aplicación back-end y ha escrito una aplicación de dispositivo simulado para notificar la información de conectividad de dispositivos en el dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="19506-159">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="19506-160">También ha aprendido cómo consultar esta información mediante el lenguaje de consulta de IoT Hub de tipo SQL.</span><span class="sxs-lookup"><span data-stu-id="19506-160">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="19506-161">Use los siguientes recursos para obtener información sobre cómo:</span><span class="sxs-lookup"><span data-stu-id="19506-161">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="19506-162">enviar telemetría desde dispositivos con el tutorial [Introducción a IoT Hub][lnk-iothub-getstarted];</span><span class="sxs-lookup"><span data-stu-id="19506-162">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="19506-163">configurar dispositivos mediante las propiedades deseadas del dispositivo gemelo con el tutorial [Uso de las propiedades deseadas para configurar dispositivos][lnk-twin-how-to-configure];</span><span class="sxs-lookup"><span data-stu-id="19506-163">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="19506-164">controlar los dispositivos de forma interactiva (por ejemplo, encender un ventilador desde una aplicación controlada por el usuario), con el tutorial [Use direct methods][lnk-methods-tutorial] (Uso de métodos directos).</span><span class="sxs-lookup"><span data-stu-id="19506-164">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-node-twin-getstarted/addtagapp.png
[img-addtagapp2]: media/iot-hub-csharp-node-twin-getstarted/addtagapp2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

