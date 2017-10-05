---
title: "Introducción a los dispositivos gemelos de Azure IoT Hub (.NET/.NET) | Microsoft Docs"
description: "Describe cómo usar dispositivos gemelos de IoT Hub de Azure para agregar etiquetas y, luego, usar una consulta de IoT Hub. Usará el SDK de dispositivo Azure IoT para .NET con el fin de implementar una aplicación para dispositivo simulado, además del SDK de servicios Azure IoT para .NET con el objetivo de implementar una aplicación de servicio que agrega las etiquetas y ejecuta la consulta de IoT Hub."
services: iot-hub
documentationcenter: node
author: dsk-2015
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: dkshir
ms.openlocfilehash: 6073d594117e69676b753a1e3af25fffa3583a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="59458-104">Introducción a los dispositivos gemelos (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="59458-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="59458-105">Al final de este tutorial, tendrá dos aplicaciones de consola de .NET:</span><span class="sxs-lookup"><span data-stu-id="59458-105">At the end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="59458-106">**CreateDeviceIdentity**, una aplicación .NET que crea una identidad de dispositivo y una clave de seguridad asociada para conectar la aplicación para dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="59458-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="59458-107">**AddTagsAndQuery**, una aplicación .NET de back-end diseñada para ejecutarse desde el back-end, que agrega etiquetas y consulta dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="59458-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>
* <span data-ttu-id="59458-108">**ReportConnectivity**, una aplicación .NET para dispositivo que simula un dispositivo que se conecta a su centro de IoT con la identidad del dispositivo creada anteriormente e informa de su estado de conectividad.</span><span class="sxs-lookup"><span data-stu-id="59458-108">**ReportConnectivity**, a .NET device app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="59458-109">En el artículo [SDK de IoT de Azure][lnk-hub-sdks] se proporciona información sobre los SDK que puede usar para crear aplicaciones de dispositivo y de back-end.</span><span class="sxs-lookup"><span data-stu-id="59458-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="59458-110">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="59458-110">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="59458-111">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="59458-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="59458-112">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="59458-112">An active Azure account.</span></span> <span data-ttu-id="59458-113">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="59458-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="59458-114">Si, por el contrario, desea crear la identidad del dispositivo mediante programación, lea la sección correspondiente en el artículo [Conexión del dispositivo simulado en el centro de IoT con .NET][lnk-device-identity-csharp].</span><span class="sxs-lookup"><span data-stu-id="59458-114">If you want to create the device identity programmatically instead, read the corresponding section in the [Connect your simulated device to your IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="59458-115">Creación de la aplicación de servicio</span><span class="sxs-lookup"><span data-stu-id="59458-115">Create the service app</span></span>
<span data-ttu-id="59458-116">En esta sección, creará una aplicación de consola de .NET (que usa C#) que agrega metadatos de ubicación al dispositivo gemelo asociado con **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="59458-116">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="59458-117">A continuación, consulta los dispositivos gemelos almacenados en IoT Hub seleccionando los dispositivos ubicados en Estados Unidos y, después, los que informan de una conexión de red de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="59458-117">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="59458-118">En Visual Studio, agregue un proyecto de escritorio clásico de Windows de Visual C# a la solución actual mediante la plantilla de proyecto **Aplicación de consola** .</span><span class="sxs-lookup"><span data-stu-id="59458-118">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="59458-119">Asigne el nombre **AddTagsAndQuery** al proyecto.</span><span class="sxs-lookup"><span data-stu-id="59458-119">Name the project **AddTagsAndQuery**.</span></span>
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createapp]
1. <span data-ttu-id="59458-121">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **AddTagsAndQuery** y luego seleccione **Administrar paquetes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="59458-121">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="59458-122">En la ventana **Administrador de paquetes NuGet**, seleccione **Examinar** y busque **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="59458-122">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="59458-123">Seleccione **Instalar** para instalar el paquete **Microsoft.Azure.Devices** y acepte las condiciones de uso.</span><span class="sxs-lookup"><span data-stu-id="59458-123">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="59458-124">Este procedimiento permite descargar, instalar y agregar una referencia al [paquete NuGet del SDK de dispositivo de IoT de Azure][lnk-nuget-service-sdk] y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="59458-124">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]
1. <span data-ttu-id="59458-126">Agregue las siguientes instrucciones `using` al principio del archivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="59458-126">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="59458-127">Agregue los campos siguientes a la clase **Program** .</span><span class="sxs-lookup"><span data-stu-id="59458-127">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="59458-128">Sustituya el valor de marcador de posición por la cadena de conexión de IoT Hub para el centro que creó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="59458-128">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="59458-129">Agregue el método siguiente a la clase **Program** :</span><span class="sxs-lookup"><span data-stu-id="59458-129">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="59458-130">La clase **RegistryManager** expone todos los métodos necesarios para interactuar con dispositivos gemelos del servicio.</span><span class="sxs-lookup"><span data-stu-id="59458-130">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="59458-131">El código anterior inicializa primero el objeto **registryManager**, luego recupera el dispositivo gemelo de **myDeviceId** y, por último, actualiza sus etiquetas con la información de la ubicación deseada.</span><span class="sxs-lookup"><span data-stu-id="59458-131">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="59458-132">Después de la actualización, ejecuta dos consultas: la primera selecciona solo los dispositivos gemelos que se encuentran en la planta **Redmond43** y la segunda mejora la consulta para seleccionar solo los dispositivos que están también conectados a través de la red de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="59458-132">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="59458-133">Tenga en cuenta que el código anterior, cuando crea el objeto de **consulta**, especifica un número máximo de documentos devueltos.</span><span class="sxs-lookup"><span data-stu-id="59458-133">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="59458-134">El objeto **consulta** contiene una propiedad booleana **HasMoreResults** que puede utilizar para invocar a los métodos **GetNextAsTwinAsync** varias veces para recuperar todos los resultados.</span><span class="sxs-lookup"><span data-stu-id="59458-134">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="59458-135">Un método llamado **GetNextAsJson** está disponible para los resultados que no son dispositivos gemelos, por ejemplo, los resultados de consultas de agregación.</span><span class="sxs-lookup"><span data-stu-id="59458-135">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="59458-136">Por último, agregue las líneas siguientes al método **Main** :</span><span class="sxs-lookup"><span data-stu-id="59458-136">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="59458-137">En el Explorador de soluciones, abra **Establecer proyectos de inicio...** y asegúrese de que la **acción** de **AddTagsAndQuery** sea **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="59458-137">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="59458-138">Compile la solución.</span><span class="sxs-lookup"><span data-stu-id="59458-138">Build the solution.</span></span>
1. <span data-ttu-id="59458-139">Ejecute esta aplicación haciendo clic con el botón derecho en el proyecto **AddTagsAndQuery** y seleccionando **Depurar**, seguido de **Iniciar nueva instancia**.</span><span class="sxs-lookup"><span data-stu-id="59458-139">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="59458-140">Debería ver un dispositivo en los resultados de la consulta que pregunta por todos los dispositivos que se encuentran en **Redmond43** y ninguno para la consulta que restringe los resultados a los dispositivos que utilizan una red de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="59458-140">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![Resultados de consulta en ventana][img-addtagapp]

<span data-ttu-id="59458-142">En la siguiente sección, creará una aplicación de dispositivo que notifica la información de conectividad y cambia el resultado de la consulta en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="59458-142">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="59458-143">Creación de la aplicación del dispositivo</span><span class="sxs-lookup"><span data-stu-id="59458-143">Create the device app</span></span>
<span data-ttu-id="59458-144">En esta sección, creará una aplicación de consola de .NET que se conecta al centro como **myDeviceId** y, luego, actualiza las propiedades notificadas para contener la información que indica que está conectado mediante una red de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="59458-144">In this section, you create a .NET console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="59458-145">En Visual Studio, agregue un proyecto de escritorio clásico de Windows de Visual C# a la solución actual mediante la plantilla de proyecto **Aplicación de consola** .</span><span class="sxs-lookup"><span data-stu-id="59458-145">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="59458-146">Denomine el proyecto **ReportConnectivity**.</span><span class="sxs-lookup"><span data-stu-id="59458-146">Name the project **ReportConnectivity**.</span></span>
   
    ![Nueva aplicación para dispositivo de Windows clásico de Visual C#][img-createdeviceapp]
    
1. <span data-ttu-id="59458-148">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **ReportConnectivity** y, luego, seleccione **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="59458-148">In Solution Explorer, right-click the **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="59458-149">En la ventana **Administrador de paquetes NuGet**, seleccione **Examinar** y busque **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="59458-149">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="59458-150">Seleccione **Instalar** para instalar el paquete **Microsoft.Azure.Devices.Client** y acepte las condiciones de uso.</span><span class="sxs-lookup"><span data-stu-id="59458-150">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="59458-151">Este procedimiento permite descargar, instalar y agregar una referencia al paquete NuGet del [SDK de dispositivo Azure IoT][lnk-nuget-client-sdk] y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="59458-151">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet: aplicación cliente][img-clientnuget]
1. <span data-ttu-id="59458-153">Agregue las siguientes instrucciones `using` al principio del archivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="59458-153">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="59458-154">Agregue los campos siguientes a la clase **Program** .</span><span class="sxs-lookup"><span data-stu-id="59458-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="59458-155">Sustituya el valor de marcador de posición por la cadena de conexión del dispositivo del anotó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="59458-155">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="59458-156">Agregue el método siguiente a la clase **Program** :</span><span class="sxs-lookup"><span data-stu-id="59458-156">Add the following method to the **Program** class:</span></span>

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting to hub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
                Console.WriteLine("Retrieving twin");
                await Client.GetTwinAsync();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="59458-157">El objeto **Cliente** expone todos los métodos necesarios para interactuar con dispositivos gemelos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="59458-157">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="59458-158">El código mostrado anteriormente, inicializa el objeto **Client** y, luego, recupera el dispositivo gemelo para **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="59458-158">The code shown above, initializes the **Client** object, and then retrieves the device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="59458-159">Agregue el método siguiente a la clase **Program** :</span><span class="sxs-lookup"><span data-stu-id="59458-159">Add the following method to the **Program** class:</span></span>
   
        public static async void ReportConnectivity()
        {
            try
            {
                Console.WriteLine("Sending connectivity data as reported property");
                
                TwinCollection reportedProperties, connectivity;
                reportedProperties = new TwinCollection();
                connectivity = new TwinCollection();
                connectivity["type"] = "cellular";
                reportedProperties["connectivity"] = connectivity;
                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

   <span data-ttu-id="59458-160">El código anterior actualiza la propiedad notificada de **myDeviceId** con la información de conectividad.</span><span class="sxs-lookup"><span data-stu-id="59458-160">The code above updates **myDeviceId**'s reported property with the connectivity information.</span></span>

1. <span data-ttu-id="59458-161">Por último, agregue las líneas siguientes al método **Main** :</span><span class="sxs-lookup"><span data-stu-id="59458-161">Finally, add the following lines to the **Main** method:</span></span>
   
       try
       {
            InitClient();
            ReportConnectivity();
       }
       catch (Exception ex)
       {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
       }
       Console.WriteLine("Press Enter to exit.");
       Console.ReadLine();

1. <span data-ttu-id="59458-162">En el Explorador de soluciones, abra **Establecer proyectos de inicio** y asegúrese de que la **acción** de **ReportConnectivity** sea **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="59458-162">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="59458-163">Compile la solución.</span><span class="sxs-lookup"><span data-stu-id="59458-163">Build the solution.</span></span>
1. <span data-ttu-id="59458-164">Ejecute esta aplicación haciendo clic con el botón derecho en el proyecto **ReportConnectivity** y seleccionando **Depurar**, seguido de **Iniciar nueva instancia**.</span><span class="sxs-lookup"><span data-stu-id="59458-164">Run this application by right-clicking on the **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="59458-165">Debería ver cómo obtiene la información del gemelo y, luego, envía la conectividad como una *propiedad notificada*.</span><span class="sxs-lookup"><span data-stu-id="59458-165">You should see it getting the twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![Ejecución la aplicación para dispositivo para notificar sobre la conectividad][img-rundeviceapp]
    
    
1. <span data-ttu-id="59458-167">Ahora que el dispositivo ha informado sobre su información de conectividad, debe aparecer en ambas consultas.</span><span class="sxs-lookup"><span data-stu-id="59458-167">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="59458-168">Ejecute la aplicación **AddTagsAndQuery** .NET para volver a ejecutar las consultas.</span><span class="sxs-lookup"><span data-stu-id="59458-168">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="59458-169">Esta vez **myDeviceId** debe aparecer en los resultados de ambas consulta.</span><span class="sxs-lookup"><span data-stu-id="59458-169">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![Conectividad de dispositivo notificada correctamente][img-tagappsuccess]

## <a name="next-steps"></a><span data-ttu-id="59458-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="59458-171">Next steps</span></span>
<span data-ttu-id="59458-172">En este tutorial, configuró un centro de IoT nuevo en Azure Portal y, después, creó una identidad de dispositivo en el registro de identidades del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="59458-172">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="59458-173">Ha agregado metadatos de dispositivo como etiquetas desde una aplicación back-end y ha escrito una aplicación de dispositivo simulado para notificar la información de conectividad de dispositivos en el dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="59458-173">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="59458-174">También ha aprendido cómo consultar esta información mediante el lenguaje de consulta de IoT Hub de tipo SQL.</span><span class="sxs-lookup"><span data-stu-id="59458-174">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="59458-175">Use los siguientes recursos para obtener información sobre cómo:</span><span class="sxs-lookup"><span data-stu-id="59458-175">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="59458-176">enviar telemetría desde dispositivos con el tutorial [Introducción a IoT Hub][lnk-iothub-getstarted];</span><span class="sxs-lookup"><span data-stu-id="59458-176">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="59458-177">configurar dispositivos mediante las propiedades deseadas del dispositivo gemelo con el tutorial [Uso de las propiedades deseadas para configurar dispositivos][lnk-twin-how-to-configure];</span><span class="sxs-lookup"><span data-stu-id="59458-177">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="59458-178">controlar los dispositivos de forma interactiva (por ejemplo, encender un ventilador desde una aplicación controlada por el usuario), con el tutorial [Use direct methods][lnk-methods-tutorial] (Uso de métodos directos).</span><span class="sxs-lookup"><span data-stu-id="59458-178">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-csharp-twin-getstarted/addtagapp.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-getstarted/clientsdknuget.png
[img-rundeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/rundeviceapp.png
[img-tagappsuccess]: media/iot-hub-csharp-csharp-twin-getstarted/tagappsuccess.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

