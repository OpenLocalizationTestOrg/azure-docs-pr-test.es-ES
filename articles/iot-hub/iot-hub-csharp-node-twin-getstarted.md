---
title: "aaaGet partió gemelos de dispositivo del centro de IoT de Azure (nodo/.NET) | Documentos de Microsoft"
description: "¿Cómo toouse centro de IoT de Azure dispositivo: los gemelos tooadd etiquetas y, a continuación, utilice una consulta de centro de IoT. Usar dispositivos de IoT de Azure de hello SDK para hello servicio IoT de Azure SDK para .NET tooimplement una aplicación de servicio que agrega etiquetas de Hola y ejecuta consultas del centro de IoT hello y aplicación de Node.js tooimplement hello dispositivo simulado."
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
ms.openlocfilehash: 1cec082ebddc19c9b87998a5fd0159d32b07acd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="c3b5a-104">Introducción a los dispositivos gemelos (.NET y Node)</span><span class="sxs-lookup"><span data-stu-id="c3b5a-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="c3b5a-105">Al final de Hola de este tutorial, dispondrá de .NET y una aplicación de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="c3b5a-105">At hello end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="c3b5a-106">**AddTagsAndQuery.js**, una aplicación de .NET de back-end diseñada para ejecutarse desde el back-end, que agrega etiquetas y consulta dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="c3b5a-107">**TwinSimulatedDevice.js**, una aplicación Node.js que simula un dispositivo que conecta el centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente e informa acerca de su condición de conectividad.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="c3b5a-108">artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que se puede usar toobuild aplicaciones de dispositivo y back-end.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="c3b5a-109">toocomplete este tutorial necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="c3b5a-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="c3b5a-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="c3b5a-111">Node.js versión 0.10.x, o posteriores.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="c3b5a-112">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-112">An active Azure account.</span></span> <span data-ttu-id="c3b5a-113">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="c3b5a-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="c3b5a-114">Crear aplicación de servicio de hello</span><span class="sxs-lookup"><span data-stu-id="c3b5a-114">Create hello service app</span></span>
<span data-ttu-id="c3b5a-115">En esta sección, creará una aplicación de consola de .NET (mediante C#) que agrega gemelas de dispositivo de toohello ubicación metadatos asociados a **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-115">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="c3b5a-116">A continuación, consulta: los gemelos de hello dispositivo almacenan en el centro de IoT Hola seleccionar dispositivos de hello ubicados en hello nos y los que informó de una conexión de telefonía móvil Hola, a continuación.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-116">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="c3b5a-117">En Visual Studio, agregue una solución actual de toohello de proyectos de Visual C# escritorio clásico de Windows mediante el uso de hello **aplicación de consola** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-117">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="c3b5a-118">Proyecto de hello Name **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-118">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createapp]
1. <span data-ttu-id="c3b5a-120">En el Explorador de soluciones, haga clic en hello **AddTagsAndQuery** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="c3b5a-120">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="c3b5a-121">Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar** y busque **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="c3b5a-122">Seleccione **instalar** tooinstall hello **Microsoft.Azure.Devices** empaquetar y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="c3b5a-123">Este procedimiento se descarga, se instala y se agrega una referencia toohello [IoT de Azure SDK del servicio] [ lnk-nuget-service-sdk] NuGet paquete y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]
1. <span data-ttu-id="c3b5a-125">Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:</span><span class="sxs-lookup"><span data-stu-id="c3b5a-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="c3b5a-126">Agregar Hola después campos toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="c3b5a-127">Sustituya el valor de marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-127">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="c3b5a-128">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="c3b5a-128">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="c3b5a-129">Hola **RegistryManager** clase expone métodos toointeract necesarios de hello con: los gemelos de dispositivo del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-129">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="c3b5a-130">código anterior Hola inicializa por primera vez hello **registryManager** objeto, a continuación, recupera Hola gemelas de dispositivo para **myDeviceId**y por último actualiza sus etiquetas con información de ubicación de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-130">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="c3b5a-131">Después de actualizar, se ejecutan dos consultas: Hola primero selecciona solo Hola dispositivo: los gemelos de dispositivos que se encuentran en hello **Redmond43** planta Hola segundo perfecciona Hola consulta tooselect solo Hola dispositivos y que también están conectados a través de red de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-131">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="c3b5a-132">Tenga en cuenta ese código Hola anterior, cuando crea hello **consulta** de objetos, especifica un número máximo de documentos devueltos.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-132">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="c3b5a-133">Hola **consulta** objeto contiene un **HasMoreResults** propiedad booleana que se puede usar hello tooinvoke **GetNextAsTwinAsync** métodos varias veces tooretrieve todos los resultados.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-133">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="c3b5a-134">Un método llamado **GetNextAsJson** está disponible para los resultados que no son dispositivos gemelos, por ejemplo, los resultados de consultas de agregación.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="c3b5a-135">Por último, agregue Hola después líneas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="c3b5a-135">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="c3b5a-136">Hola el Explorador de soluciones, abra hello **proyectos de inicio establecido...**  y asegúrese de que hello **acción** para **AddTagsAndQuery** proyecto es **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-136">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="c3b5a-137">Compile la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-137">Build hello solution.</span></span>
1. <span data-ttu-id="c3b5a-138">Ejecutar esta aplicación con el botón secundario en hello **AddTagsAndQuery** proyecto y seleccione **depurar**, seguido de **Iniciar nueva instancia**.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-138">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="c3b5a-139">Debería ver un dispositivo en los resultados de Hola para hello formular de consulta para todos los dispositivos ubicados en **Redmond43** y ninguno para consulta de Hola que restringe Hola resultados toodevices que usan una red móvil.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-139">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![Resultados de consulta en ventana][img-addtagapp]

<span data-ttu-id="c3b5a-141">En la siguiente sección hello, crear una aplicación de dispositivo que contiene información de conectividad de Hola y cambios Hola resultado de consulta de hello en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-141">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="c3b5a-142">Crear aplicación de dispositivo de hello</span><span class="sxs-lookup"><span data-stu-id="c3b5a-142">Create hello device app</span></span>
<span data-ttu-id="c3b5a-143">En esta sección, creará una aplicación de consola de Node.js que conecta el concentrador de tooyour como **myDeviceId**y, a continuación, actualiza su información de Hola de toocontain propiedades notificado que está conectado mediante una red de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-143">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="c3b5a-144">Cree una nueva carpeta vacía denominada **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="c3b5a-145">Hola **reportconnectivity** carpeta, cree un nuevo archivo package.json mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-145">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="c3b5a-146">Acepte todos los valores predeterminados de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-146">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="c3b5a-147">En el símbolo del sistema en hello **reportconnectivity** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure**, y **azure-iot-dispositivo-mqtt** paquete :</span><span class="sxs-lookup"><span data-stu-id="c3b5a-147">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="c3b5a-148">Con un editor de texto, cree un nuevo **ReportConnectivity.js** archivo Hola **reportconnectivity** carpeta.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-148">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="c3b5a-149">Agregar Hola después código toohello **ReportConnectivity.js** archivo y sustituya el marcador de posición de hello para la cadena de conexión de dispositivo con hello uno que copió al crear hello **myDeviceId** dispositivo identidad:</span><span class="sxs-lookup"><span data-stu-id="c3b5a-149">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello placeholder for device connection string with hello one you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="c3b5a-150">Hola **cliente** objeto expone todos los métodos de hello requieren toointeract con: los gemelos de dispositivo del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-150">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="c3b5a-151">Hola código anterior, una vez que inicialice hello **cliente** objeto, recupera Hola gemelas de dispositivo para **myDeviceId** y actualiza su propiedad incluido con información de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-151">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
1. <span data-ttu-id="c3b5a-152">Ejecutar la aplicación de dispositivo de hello</span><span class="sxs-lookup"><span data-stu-id="c3b5a-152">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="c3b5a-153">Debe aparecer un mensaje Hola `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-153">You should see hello message `twin state reported`.</span></span>
1. <span data-ttu-id="c3b5a-154">Ahora que hello dispositivo había notificado su información de conectividad, debe aparecer en las dos consultas.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-154">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="c3b5a-155">Ejecute hello .NET **AddTagsAndQuery** Hola de toorun aplicación consulta de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-155">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="c3b5a-156">Esta vez **myDeviceId** debe aparecer en los resultados de ambas consulta.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="c3b5a-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c3b5a-157">Next steps</span></span>
<span data-ttu-id="c3b5a-158">En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-158">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="c3b5a-159">Agrega los metadatos del dispositivo como etiquetas desde una aplicación de back-end y una información de conectividad del dispositivo de tooreport de aplicación de dispositivo simulado se escribió en gemelas de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-159">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="c3b5a-160">También habrá aprendido cómo tooquery esta información mediante el lenguaje de consulta de hello centro de IoT similar a SQL.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-160">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="c3b5a-161">Hola de uso después cómo toolearn de recursos para:</span><span class="sxs-lookup"><span data-stu-id="c3b5a-161">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="c3b5a-162">enviar telemetría desde dispositivos con hello [empezar a trabajar con el centro de IoT] [ lnk-iothub-getstarted] tutorial,</span><span class="sxs-lookup"><span data-stu-id="c3b5a-162">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="c3b5a-163">configurar dispositivos mediante propiedades que desee del doble del dispositivo con hello [uso deseado propiedades de dispositivos con tooconfigure] [ lnk-twin-how-to-configure] tutorial,</span><span class="sxs-lookup"><span data-stu-id="c3b5a-163">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="c3b5a-164">controlar los dispositivos de forma interactiva (por ejemplo, al activar un ventilador desde una aplicación controlada por el usuario) con hello [usar métodos directos] [ lnk-methods-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="c3b5a-164">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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

