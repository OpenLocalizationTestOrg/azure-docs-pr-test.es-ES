---
title: Uso de las propiedades de dispositivo gemelo de Azure IoT Hub (.NET/.NET) | Microsoft Docs
description: "En este artículo se describe cómo usar los dispositivos gemelos de IoT Hub de Azure para configurar dispositivos. Usará el SDK de dispositivo IoT de Azure para .NET con el fin de implementar una aplicación de dispositivo simulado, además del SDK del servicio IoT de Azure para .NET para implementar una aplicación de servicio que modifica una configuración de dispositivo que emplea un dispositivo gemelo."
services: iot-hub
documentationcenter: .net
author: dsk-2015
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dkshir
ms.openlocfilehash: 679cda28bf3ce9fb207fe3693a3453b355f1de15
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="use-desired-properties-to-configure-devices"></a><span data-ttu-id="5f74f-104">Uso de las propiedades deseadas para configurar dispositivos</span><span class="sxs-lookup"><span data-stu-id="5f74f-104">Use desired properties to configure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="5f74f-105">Al final de este tutorial tendrá dos aplicaciones de consola de .NET:</span><span class="sxs-lookup"><span data-stu-id="5f74f-105">At the end of this tutorial, you will have two .NET console apps:</span></span>

* <span data-ttu-id="5f74f-106">**SimulateDeviceConfiguration**, una aplicación de dispositivo simulado que espera una actualización de la configuración deseada y notifica el estado de un proceso de actualización de configuración simulada.</span><span class="sxs-lookup"><span data-stu-id="5f74f-106">**SimulateDeviceConfiguration**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="5f74f-107">**SetDesiredConfigurationAndQuery**, una aplicación de back-end que establece la configuración deseada en un dispositivo y consulta el proceso de actualización de la configuración.</span><span class="sxs-lookup"><span data-stu-id="5f74f-107">**SetDesiredConfigurationAndQuery**, a back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="5f74f-108">En el artículo [SDK de IoT de Azure][lnk-hub-sdks] se proporciona información sobre los SDK que puede usar para crear aplicaciones de dispositivo y de back-end.</span><span class="sxs-lookup"><span data-stu-id="5f74f-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="5f74f-109">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5f74f-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="5f74f-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="5f74f-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="5f74f-111">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="5f74f-111">An active Azure account.</span></span> <span data-ttu-id="5f74f-112">En caso de no tener ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="5f74f-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="5f74f-113">Si ha seguido el tutorial [Introducción a los dispositivos gemelos][lnk-twin-tutorial], ya tiene una instancia de IoT Hub y una identidad de dispositivo denominada **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="5f74f-113">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="5f74f-114">En ese caso, puede ir directamente a la sección [Creación de la aplicación de dispositivo simulado][lnk-how-to-configure-createapp].</span><span class="sxs-lookup"><span data-stu-id="5f74f-114">In that case, you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-the-simulated-device-app"></a><span data-ttu-id="5f74f-115">Creación de la aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="5f74f-115">Create the simulated device app</span></span>
<span data-ttu-id="5f74f-116">En esta sección, creará una aplicación de consola de .NET que se conecta a su centro como **myDeviceId**, espera una actualización de la configuración deseada e informa de las actualizaciones en el proceso de actualización de la configuración simulada.</span><span class="sxs-lookup"><span data-stu-id="5f74f-116">In this section, you create a .NET console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="5f74f-117">En Visual Studio, cree un proyecto de escritorio clásico de Windows de Visual C# con la plantilla de proyecto de **aplicación de consola**.</span><span class="sxs-lookup"><span data-stu-id="5f74f-117">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using the **Console Application** project template.</span></span> <span data-ttu-id="5f74f-118">Asigne al proyecto el nombre **SimulateDeviceConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="5f74f-118">Name the project **SimulateDeviceConfiguration**.</span></span>
   
    ![Nueva aplicación para dispositivo de Windows clásico de Visual C#][img-createdeviceapp]

1. <span data-ttu-id="5f74f-120">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **SimulateDeviceConfiguration** y seleccione **Administrar paquetes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="5f74f-120">In Solution Explorer, right-click the **SimulateDeviceConfiguration** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="5f74f-121">En la ventana **Administrador de paquetes NuGet**, seleccione **Examinar** y busque **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="5f74f-121">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="5f74f-122">Seleccione **Instalar** para instalar el paquete **Microsoft.Azure.Devices.Client** y acepte las condiciones de uso.</span><span class="sxs-lookup"><span data-stu-id="5f74f-122">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="5f74f-123">Este procedimiento permite descargar, instalar y agregar una referencia al paquete NuGet del [SDK de dispositivo Azure IoT][lnk-nuget-client-sdk] y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="5f74f-123">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet: aplicación cliente][img-clientnuget]
1. <span data-ttu-id="5f74f-125">Agregue las siguientes instrucciones `using` al principio del archivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="5f74f-125">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="5f74f-126">Agregue los campos siguientes a la clase **Program** .</span><span class="sxs-lookup"><span data-stu-id="5f74f-126">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="5f74f-127">Sustituya el valor de marcador de posición por la cadena de conexión del dispositivo del anotó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="5f74f-127">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. <span data-ttu-id="5f74f-128">Agregue el método siguiente a la clase **Program** :</span><span class="sxs-lookup"><span data-stu-id="5f74f-128">Add the following method to the **Program** class:</span></span>
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting to hub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    <span data-ttu-id="5f74f-129">El objeto **Cliente** expone todos los métodos necesarios para interactuar con dispositivos gemelos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5f74f-129">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="5f74f-130">El código mostrado anteriormente, inicializa el objeto **Client** y, luego, recupera el dispositivo gemelo para **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="5f74f-130">The code shown above, initializes the **Client** object, and then retrieves the device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="5f74f-131">Agregue el método siguiente a la clase **Program**.</span><span class="sxs-lookup"><span data-stu-id="5f74f-131">Add the following method to the **Program** class.</span></span> <span data-ttu-id="5f74f-132">Este método establece los valores iniciales de telemetría en el dispositivo local y actualiza el dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="5f74f-132">This method sets the initial values of telemetry on the local device and then updates the device twin.</span></span>

        public static async void InitTelemetry()
        {
            try
            {
                Console.WriteLine("Report initial telemetry config:");
                TwinCollection telemetryConfig = new TwinCollection();
                
                telemetryConfig["configId"] = "0";
                telemetryConfig["sendFrequency"] = "24h";
                reportedProperties["telemetryConfig"] = telemetryConfig;
                Console.WriteLine(JsonConvert.SerializeObject(reportedProperties));

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="5f74f-133">Agregue el método siguiente a la clase **Program**.</span><span class="sxs-lookup"><span data-stu-id="5f74f-133">Add the following method to the **Program** class.</span></span> <span data-ttu-id="5f74f-134">Se trata de una devolución de llamada que detecta un cambio en las *propiedades pertinentes* del dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="5f74f-134">This is a callback which will detect a change in *desired properties* in the device twin.</span></span>

        private static async Task OnDesiredPropertyChanged(TwinCollection desiredProperties, object userContext)
        {
            try
            {
                Console.WriteLine("Desired property change:");
                Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));

                var currentTelemetryConfig = reportedProperties["telemetryConfig"];
                var desiredTelemetryConfig = desiredProperties["telemetryConfig"];

                if ((desiredTelemetryConfig != null) && (desiredTelemetryConfig["configId"] != currentTelemetryConfig["configId"]))
                {
                    Console.WriteLine("\nInitiating config change");
                    currentTelemetryConfig["status"] = "Pending";
                    currentTelemetryConfig["pendingConfig"] = desiredTelemetryConfig;

                    await Client.UpdateReportedPropertiesAsync(reportedProperties);

                    CompleteConfigChange();
                }
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="5f74f-135">Este método actualiza las propiedades notificadas en el objeto del dispositivo gemelo local con la solicitud de actualización de la configuración y establece el estado en **Pendiente**; a continuación, actualiza el dispositivo gemelo en el servicio.</span><span class="sxs-lookup"><span data-stu-id="5f74f-135">This method updates the reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="5f74f-136">Después de actualizar correctamente el dispositivo gemelo, se completa el cambio de configuración llamando al método `CompleteConfigChange` que se describe en el siguiente punto.</span><span class="sxs-lookup"><span data-stu-id="5f74f-136">After successfully updating the device twin, it completes the config change by calling the method `CompleteConfigChange` described in the next point.</span></span>

1. <span data-ttu-id="5f74f-137">Agregue el método siguiente a la clase **Program**.</span><span class="sxs-lookup"><span data-stu-id="5f74f-137">Add the following method to the **Program** class.</span></span> <span data-ttu-id="5f74f-138">Este método simula un restablecimiento de dispositivo, actualiza las propiedades notificadas locales al establecer el estado en **Correcto** y elimina el elemento **pendingConfig**.</span><span class="sxs-lookup"><span data-stu-id="5f74f-138">This method simulates a device reset, then updates the local reported properties setting the status to **Success** and removes the **pendingConfig** element.</span></span> <span data-ttu-id="5f74f-139">A continuación, actualiza el dispositivo gemelo en el servicio.</span><span class="sxs-lookup"><span data-stu-id="5f74f-139">It then updates the device twin on the service.</span></span> 

        public static async void CompleteConfigChange()
        {
            try
            {
                var currentTelemetryConfig = reportedProperties["telemetryConfig"];

                Console.WriteLine("\nSimulating device reset");
                await Task.Delay(30000); 

                Console.WriteLine("\nCompleting config change");
                currentTelemetryConfig["configId"] = currentTelemetryConfig["pendingConfig"]["configId"];
                currentTelemetryConfig["sendFrequency"] = currentTelemetryConfig["pendingConfig"]["sendFrequency"];
                currentTelemetryConfig["status"] = "Success";
                currentTelemetryConfig["pendingConfig"] = null;

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
                Console.WriteLine("Config change complete \nPress any key to exit.");
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="5f74f-140">Por último, agregue las líneas siguientes al método **Main**:</span><span class="sxs-lookup"><span data-stu-id="5f74f-140">Finally add the following lines to the **Main** method:</span></span>

        try
        {
            InitClient();
            InitTelemetry();

            Console.WriteLine("Wait for desired telemetry...");
            Client.SetDesiredPropertyUpdateCallback(OnDesiredPropertyChanged, null).Wait();
            Console.ReadKey();
        }
        catch (AggregateException ex)
        {
            foreach (Exception exception in ex.InnerExceptions)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", exception);
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }

   > [!NOTE]
   > <span data-ttu-id="5f74f-141">Este tutorial no simula ningún comportamiento de las actualizaciones de configuración simultáneas.</span><span class="sxs-lookup"><span data-stu-id="5f74f-141">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="5f74f-142">Algunos procesos de actualización de configuración pueden dar cabida a cambios de configuración de destino mientras se está ejecutando la actualización, otros tiene que ponerlos en cola, y otros podría rechazarlos con una condición de error.</span><span class="sxs-lookup"><span data-stu-id="5f74f-142">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, some might have to queue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="5f74f-143">Asegúrese de que considera el comportamiento deseado para el proceso de configuración específica y agregue la lógica adecuada antes de iniciar el cambio de configuración.</span><span class="sxs-lookup"><span data-stu-id="5f74f-143">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="5f74f-144">Compile la solución y ejecute la aplicación de dispositivo desde Visual Studio al hacer clic en **F5**.</span><span class="sxs-lookup"><span data-stu-id="5f74f-144">Build the solution and then run the device app from Visual Studio by clicking **F5**.</span></span> <span data-ttu-id="5f74f-145">En la consola de salida, debería ver los mensajes que indican que el dispositivo simulado está recuperando el dispositivo gemelo, configurando la telemetría y esperando al cambio de la propiedad deseada.</span><span class="sxs-lookup"><span data-stu-id="5f74f-145">On the output console, you should see the messages indicating that your simulated device is retrieving the device twin, setting up the telemetry, and waiting for desired property change.</span></span> <span data-ttu-id="5f74f-146">Mantenga la aplicación en ejecución.</span><span class="sxs-lookup"><span data-stu-id="5f74f-146">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="5f74f-147">Creación de la aplicación de servicio</span><span class="sxs-lookup"><span data-stu-id="5f74f-147">Create the service app</span></span>
<span data-ttu-id="5f74f-148">En esta sección, creará una aplicación de consola .NET que actualiza las *propiedades deseadas* en el dispositivo gemelo asociado con **myDeviceId** con un nuevo objeto de configuración de telemetría.</span><span class="sxs-lookup"><span data-stu-id="5f74f-148">In this section, you will create a .NET console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="5f74f-149">A continuación, consulta los dispositivos gemelos almacenados en IoT Hub y muestra la diferencia entre las configuraciones deseada y notificada del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5f74f-149">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="5f74f-150">En Visual Studio, agregue un proyecto de escritorio clásico de Windows de Visual C# a la solución actual mediante la plantilla de proyecto **Aplicación de consola** .</span><span class="sxs-lookup"><span data-stu-id="5f74f-150">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="5f74f-151">Asigne el nombre **SetDesiredConfigurationAndQuery** al proyecto.</span><span class="sxs-lookup"><span data-stu-id="5f74f-151">Name the project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createapp]
1. <span data-ttu-id="5f74f-153">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **SetDesiredConfigurationAndQuery** y luego seleccione **Administrar paquetes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="5f74f-153">In Solution Explorer, right-click the **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="5f74f-154">En la ventana **Administrador de paquetes NuGet**, seleccione **Examinar**, busque **microsoft.azure.devices**, seleccione **Instalar** para instalar el paquete **Microsoft.Azure.Devices** y acepte los términos de uso.</span><span class="sxs-lookup"><span data-stu-id="5f74f-154">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="5f74f-155">Este procedimiento permite descargar, instalar y agregar una referencia al [paquete NuGet del SDK de dispositivo de IoT de Azure][lnk-nuget-service-sdk] y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="5f74f-155">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]
1. <span data-ttu-id="5f74f-157">Agregue las siguientes instrucciones `using` al principio del archivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="5f74f-157">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="5f74f-158">Agregue los campos siguientes a la clase **Program** .</span><span class="sxs-lookup"><span data-stu-id="5f74f-158">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="5f74f-159">Sustituya el valor de marcador de posición por la cadena de conexión de IoT Hub para el centro que creó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="5f74f-159">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="5f74f-160">Agregue el método siguiente a la clase **Program** :</span><span class="sxs-lookup"><span data-stu-id="5f74f-160">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="5f74f-161">El objeto **Registro** expone todos los métodos necesarios para interactuar con dispositivos gemelos del servicio.</span><span class="sxs-lookup"><span data-stu-id="5f74f-161">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="5f74f-162">Este código inicializa el objeto **Registro**, recupera el dispositivo gemelo de **myDeviceId** y actualiza sus propiedades deseadas con un nuevo objeto de configuración de telemetría.</span><span class="sxs-lookup"><span data-stu-id="5f74f-162">This code initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="5f74f-163">Después, cada 10 segundos, consulta los dispositivos gemelos almacenados en IoT Hub e imprime las configuraciones de telemetría deseadas y notificadas.</span><span class="sxs-lookup"><span data-stu-id="5f74f-163">After that, it queries the device twins stored in the IoT hub every 10 seconds, and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="5f74f-164">Consulte el [lenguaje de consulta de IoT Hub][lnk-query] para obtener información sobre cómo generar informes completos en todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="5f74f-164">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="5f74f-165">Esta aplicación consulta IoT Hub cada 10 segundos con fines ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="5f74f-165">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="5f74f-166">Use consultas para generar informes de cara al usuario en muchos dispositivos y no para detectar cambios.</span><span class="sxs-lookup"><span data-stu-id="5f74f-166">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="5f74f-167">Si la solución requiere notificaciones en tiempo real de eventos de dispositivo, use [notificaciones gemelas][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="5f74f-167">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="5f74f-168">Por último, agregue las líneas siguientes al método **Main** :</span><span class="sxs-lookup"><span data-stu-id="5f74f-168">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key to quit.");
        Console.ReadLine();
1. <span data-ttu-id="5f74f-169">En el Explorador de soluciones, abra **Establecer proyectos de inicio...** y asegúrese de que la **acción** de **SetDesiredConfigurationAndQuery** sea **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="5f74f-169">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="5f74f-170">Compile la solución.</span><span class="sxs-lookup"><span data-stu-id="5f74f-170">Build the solution.</span></span>
1. <span data-ttu-id="5f74f-171">Con la aplicación de dispositivo **SimulateDeviceConfiguration** en ejecución, ejecute la aplicación de servicio desde Visual Studio mediante **F5**.</span><span class="sxs-lookup"><span data-stu-id="5f74f-171">With **SimulateDeviceConfiguration** device app running, run the service app from Visual Studio using **F5**.</span></span> <span data-ttu-id="5f74f-172">Debería ver cómo la configuración notificada cambia de **Pendiente** a **Correcto** con la nueva frecuencia de envío de cinco minutos activa en lugar de la de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="5f74f-172">You should see the reported configuration change from **Pending** to **Success** with the new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Dispositivo configurado correctamente][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="5f74f-174">Hay un retraso de hasta un minuto entre la operación de informe de dispositivo y el resultado de la consulta.</span><span class="sxs-lookup"><span data-stu-id="5f74f-174">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="5f74f-175">Esto es para habilitar la infraestructura de consulta para que funcione a gran escala.</span><span class="sxs-lookup"><span data-stu-id="5f74f-175">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="5f74f-176">Para recuperar vistas coherentes de un único dispositivo gemelo, use el método **getDeviceTwin** en la clase **Registro**.</span><span class="sxs-lookup"><span data-stu-id="5f74f-176">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="5f74f-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5f74f-177">Next steps</span></span>
<span data-ttu-id="5f74f-178">En este tutorial, ha establecido una configuración deseada como *propiedades deseadas* desde el back-end de solución, y ha escrito una aplicación de dispositivo para detectar ese cambio y simular un proceso de actualización de varios pasos que informe de su estado mediante las propiedades notificadas.</span><span class="sxs-lookup"><span data-stu-id="5f74f-178">In this tutorial, you set a desired configuration as *desired properties* from the solution back end, and wrote a device app to detect that change and simulate a multi-step update process reporting its status through the reported properties.</span></span>

<span data-ttu-id="5f74f-179">Use los siguientes recursos para obtener información sobre cómo:</span><span class="sxs-lookup"><span data-stu-id="5f74f-179">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="5f74f-180">enviar telemetría desde dispositivos con el tutorial [Introducción a IoT Hub][lnk-iothub-getstarted];</span><span class="sxs-lookup"><span data-stu-id="5f74f-180">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="5f74f-181">programar o realizar operaciones en grandes conjuntos de dispositivos (consulte el tutorial [Schedule and broadcast jobs][lnk-schedule-jobs] [Programación y difusión de trabajos]);</span><span class="sxs-lookup"><span data-stu-id="5f74f-181">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="5f74f-182">controlar los dispositivos de forma interactiva (por ejemplo, encender un ventilador desde una aplicación controlada por el usuario), con el tutorial [Uso de métodos directos][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="5f74f-182">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/devicesdknuget.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png


<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-twin-tutorial]: iot-hub-csharp-csharp-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-how-to-configure-createapp]: iot-hub-csharp-csharp-twin-how-to-configure.md#create-the-simulated-device-app
