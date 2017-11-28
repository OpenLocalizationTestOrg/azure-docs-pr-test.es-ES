---
title: propiedades de gemelas del dispositivo de Azure IoT Hub aaaUse (.NET/.NET) | Documentos de Microsoft
description: "Cómo los dispositivos del centro de IoT de Azure toouse gemelos tooconfigure dispositivos. Utilice hello servicio IoT de Azure SDK para .NET tooimplement una aplicación de servicio que se modifica una configuración de dispositivo mediante un doble de dispositivo y el dispositivo de hello IoT de Azure SDK para .NET tooimplement una aplicación de dispositivo simulado."
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
ms.openlocfilehash: 486436d29abfd5158c253adc5abf5935e0e1fdba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="071dd-104">Usar propiedades deseadas tooconfigure dispositivos</span><span class="sxs-lookup"><span data-stu-id="071dd-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="071dd-105">Al final de Hola de este tutorial, tendrá dos aplicaciones de consola. NET:</span><span class="sxs-lookup"><span data-stu-id="071dd-105">At hello end of this tutorial, you will have two .NET console apps:</span></span>

* <span data-ttu-id="071dd-106">**SimulateDeviceConfiguration**, una aplicación de dispositivo simulado que espera una actualización de la configuración deseada e informa del estado de Hola de un proceso de actualización de configuración simulada.</span><span class="sxs-lookup"><span data-stu-id="071dd-106">**SimulateDeviceConfiguration**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="071dd-107">**SetDesiredConfigurationAndQuery**, una aplicación back-end, que establece Hola la configuración en un dispositivo deseado y consultas Hola el proceso de actualización de configuración.</span><span class="sxs-lookup"><span data-stu-id="071dd-107">**SetDesiredConfigurationAndQuery**, a back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="071dd-108">artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que se puede usar toobuild aplicaciones de dispositivo y back-end.</span><span class="sxs-lookup"><span data-stu-id="071dd-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="071dd-109">toocomplete este tutorial necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="071dd-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="071dd-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="071dd-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="071dd-111">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="071dd-111">An active Azure account.</span></span> <span data-ttu-id="071dd-112">Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="071dd-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="071dd-113">Si ha seguido hello [empezar a trabajar con: los gemelos de dispositivo] [ lnk-twin-tutorial] tutorial, ya tiene un centro de IoT y una identidad de dispositivo llama **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="071dd-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="071dd-114">En ese caso, puede omitir toohello [aplicación de dispositivo simulado de hello crear] [ lnk-how-to-configure-createapp] sección.</span><span class="sxs-lookup"><span data-stu-id="071dd-114">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="071dd-115">Crear aplicación de dispositivo simulado de hello</span><span class="sxs-lookup"><span data-stu-id="071dd-115">Create hello simulated device app</span></span>
<span data-ttu-id="071dd-116">En esta sección, creará una aplicación de consola .NET que se conecta el concentrador de tooyour como **myDeviceId**, espera a que una actualización de la configuración deseada y, a continuación, informa de las actualizaciones en el proceso de actualización de configuración de Hola simulada.</span><span class="sxs-lookup"><span data-stu-id="071dd-116">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="071dd-117">En Visual Studio, cree un nuevo proyecto de Visual C# escritorio clásico de Windows mediante el uso de hello **aplicación de consola** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="071dd-117">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using hello **Console Application** project template.</span></span> <span data-ttu-id="071dd-118">Proyecto de hello Name **SimulateDeviceConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="071dd-118">Name hello project **SimulateDeviceConfiguration**.</span></span>
   
    ![Nueva aplicación para dispositivo de Windows clásico de Visual C#][img-createdeviceapp]

1. <span data-ttu-id="071dd-120">En el Explorador de soluciones, haga clic en hello **SimulateDeviceConfiguration** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="071dd-120">In Solution Explorer, right-click hello **SimulateDeviceConfiguration** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="071dd-121">Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar** y busque **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="071dd-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="071dd-122">Seleccione **instalar** tooinstall hello **Microsoft.Azure.Devices.Client** empaquetar y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="071dd-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="071dd-123">Este procedimiento se descarga, se instala y se agrega una referencia toohello [dispositivos de IoT de Azure SDK] [ lnk-nuget-client-sdk] NuGet paquete y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="071dd-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet: aplicación cliente][img-clientnuget]
1. <span data-ttu-id="071dd-125">Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:</span><span class="sxs-lookup"><span data-stu-id="071dd-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="071dd-126">Agregar Hola después campos toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="071dd-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="071dd-127">Reemplace el valor de marcador de posición de hello con cadena de conexión de dispositivo de Hola que anotó en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="071dd-127">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. <span data-ttu-id="071dd-128">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="071dd-128">Add hello following method toohello **Program** class:</span></span>
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    <span data-ttu-id="071dd-129">Hola **cliente** objeto expone todos los métodos de hello requieren toointeract con: los gemelos de dispositivo del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="071dd-129">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="071dd-130">Hola mostrado anteriormente, el código inicializa hello **cliente** objeto y, a continuación, recupera Hola dispositivo gemelas para **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="071dd-130">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="071dd-131">Agregar Hola siguiendo el método toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="071dd-131">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="071dd-132">Este método establece valores iniciales de Hola de telemetría en dispositivo local hello y, a continuación, las actualizaciones de Hola a gemelas de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="071dd-132">This method sets hello initial values of telemetry on hello local device and then updates hello device twin.</span></span>

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

1. <span data-ttu-id="071dd-133">Agregar Hola siguiendo el método toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="071dd-133">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="071dd-134">Se trata de una devolución de llamada que se detecte un cambio en *las propiedades adecuadas* en gemelas de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="071dd-134">This is a callback which will detect a change in *desired properties* in hello device twin.</span></span>

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

    <span data-ttu-id="071dd-135">Este Hola de actualizaciones de método notifica propiedades Hola dispositivo local gemelas objeto con la configuración de hello actualizan solicitud y establece el estado de Hola demasiado**pendiente**, a continuación, las actualizaciones de Hola gemelas de dispositivo en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="071dd-135">This method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="071dd-136">Después de actualizar correctamente los gemelos de dispositivo de hello, se completa Hola de cambios de configuración mediante una llamada a método hello `CompleteConfigChange` descrita en el siguiente punto de Hola.</span><span class="sxs-lookup"><span data-stu-id="071dd-136">After successfully updating hello device twin, it completes hello config change by calling hello method `CompleteConfigChange` described in hello next point.</span></span>

1. <span data-ttu-id="071dd-137">Agregar Hola siguiendo el método toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="071dd-137">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="071dd-138">Este método simula un restablecimiento del dispositivo, a continuación, las actualizaciones de Hola locales propiedades notificados establecer el estado de hello demasiado**correcto** quita hello y **pendingConfig** elemento.</span><span class="sxs-lookup"><span data-stu-id="071dd-138">This method simulates a device reset, then updates hello local reported properties setting hello status too**Success** and removes hello **pendingConfig** element.</span></span> <span data-ttu-id="071dd-139">A continuación, actualiza a gemelas de dispositivo de hello en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="071dd-139">It then updates hello device twin on hello service.</span></span> 

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
                Console.WriteLine("Config change complete \nPress any key tooexit.");
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

1. <span data-ttu-id="071dd-140">Finalmente agregue Hola después líneas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="071dd-140">Finally add hello following lines toohello **Main** method:</span></span>

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
   > <span data-ttu-id="071dd-141">Este tutorial no simula ningún comportamiento de las actualizaciones de configuración simultáneas.</span><span class="sxs-lookup"><span data-stu-id="071dd-141">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="071dd-142">Algunos procesos de actualización de la configuración podrían ser capaz de tooaccommodate cambios de configuración de destino mientras se ejecuta la actualización de hello, algunas pueden disponer de tooqueue ellos así como algunos pudieron rechazar ellos con una condición de error.</span><span class="sxs-lookup"><span data-stu-id="071dd-142">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="071dd-143">Asegúrese de tooconsider seguro Hola comportamiento deseado para el proceso de configuración específica y cómo agregar lógica adecuada de hello antes de iniciar el cambio de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="071dd-143">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="071dd-144">Compilar soluciones de hello y, a continuación, ejecutar la aplicación de dispositivo de hello desde Visual Studio haciendo clic en **F5**.</span><span class="sxs-lookup"><span data-stu-id="071dd-144">Build hello solution and then run hello device app from Visual Studio by clicking **F5**.</span></span> <span data-ttu-id="071dd-145">En la consola de salida de hello, debería ver mensajes de Hola que indica que el dispositivo simulado es recuperar a gemelas de dispositivo de Hola, configuración de telemetría de Hola y espera para que el cambio de propiedad deseada.</span><span class="sxs-lookup"><span data-stu-id="071dd-145">On hello output console, you should see hello messages indicating that your simulated device is retrieving hello device twin, setting up hello telemetry, and waiting for desired property change.</span></span> <span data-ttu-id="071dd-146">Mantenga la aplicación hello ejecutando.</span><span class="sxs-lookup"><span data-stu-id="071dd-146">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="071dd-147">Crear aplicación de servicio de hello</span><span class="sxs-lookup"><span data-stu-id="071dd-147">Create hello service app</span></span>
<span data-ttu-id="071dd-148">En esta sección, aprenderá a crear una aplicación de consola .NET que hello las actualizaciones *deseado propiedades* en hello dispositivo gemelas asociada **myDeviceId** con un nuevo objeto de configuración de telemetría.</span><span class="sxs-lookup"><span data-stu-id="071dd-148">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="071dd-149">A continuación, consulta: los gemelos de dispositivo de hello almacenados en el centro de IoT de Hola y muestra diferenciar hello en hello deseado y notifica las configuraciones de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="071dd-149">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="071dd-150">En Visual Studio, agregue una solución actual de toohello de proyectos de Visual C# escritorio clásico de Windows mediante el uso de hello **aplicación de consola** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="071dd-150">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="071dd-151">Proyecto de hello Name **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="071dd-151">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createapp]
1. <span data-ttu-id="071dd-153">En el Explorador de soluciones, haga clic en hello **SetDesiredConfigurationAndQuery** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="071dd-153">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="071dd-154">Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar**, busque **microsoft.azure.devices**, seleccione **instalar** tooinstall Hola **Microsoft.Azure.Devices** empaquetar y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="071dd-154">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="071dd-155">Este procedimiento se descarga, se instala y se agrega una referencia toohello [IoT de Azure SDK del servicio] [ lnk-nuget-service-sdk] NuGet paquete y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="071dd-155">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]
1. <span data-ttu-id="071dd-157">Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:</span><span class="sxs-lookup"><span data-stu-id="071dd-157">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="071dd-158">Agregar Hola después campos toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="071dd-158">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="071dd-159">Sustituya el valor de marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="071dd-159">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="071dd-160">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="071dd-160">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="071dd-161">Hola **registro** objeto expone métodos toointeract necesarios de hello con: los gemelos de dispositivo del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="071dd-161">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="071dd-162">Este código inicializa hello **registro** objeto, recupera Hola gemelas de dispositivo para **myDeviceId**y, a continuación, actualiza sus propiedades deseados con un nuevo objeto de configuración de telemetría.</span><span class="sxs-lookup"><span data-stu-id="071dd-162">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="071dd-163">Después de eso, consulta: los gemelos de dispositivo de hello almacenados en el centro de IoT Hola cada 10 segundos y copias fotográficas Hola deseado y notifica las configuraciones de telemetría.</span><span class="sxs-lookup"><span data-stu-id="071dd-163">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="071dd-164">Consulte toohello [lenguaje de consultas del centro de IoT] [ lnk-query] toolearn cómo toogenerate enriquecido informes en todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="071dd-164">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="071dd-165">Esta aplicación consulta IoT Hub cada 10 segundos con fines ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="071dd-165">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="071dd-166">Use consultas toogenerate orientadas al usuario informes a través de varios dispositivos y no toodetect cambios.</span><span class="sxs-lookup"><span data-stu-id="071dd-166">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="071dd-167">Si la solución requiere notificaciones en tiempo real de eventos de dispositivo, use [notificaciones gemelas][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="071dd-167">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="071dd-168">Por último, agregue Hola después líneas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="071dd-168">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="071dd-169">Hola el Explorador de soluciones, abra hello **proyectos de inicio establecido...**  y asegúrese de que hello **acción** para **SetDesiredConfigurationAndQuery** proyecto es **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="071dd-169">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="071dd-170">Compile la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="071dd-170">Build hello solution.</span></span>
1. <span data-ttu-id="071dd-171">Con **SimulateDeviceConfiguration** dispositivo que ejecuta aplicaciones, aplicación de servicio de ejecución hello desde Visual Studio mediante **F5**.</span><span class="sxs-lookup"><span data-stu-id="071dd-171">With **SimulateDeviceConfiguration** device app running, run hello service app from Visual Studio using **F5**.</span></span> <span data-ttu-id="071dd-172">Debería ver Hola notificado configuración cambia de **pendiente** demasiado**correcto** con activo nuevo Hola enviar frecuencia de cinco minutos en lugar de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="071dd-172">You should see hello reported configuration change from **Pending** too**Success** with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Dispositivo configurado correctamente][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="071dd-174">Hay un retraso de tooa minuto entre la operación de informe de dispositivo de Hola y el resultado de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="071dd-174">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="071dd-175">Se trata de tooenable Hola consulta infraestructura toowork a gran escala.</span><span class="sxs-lookup"><span data-stu-id="071dd-175">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="071dd-176">tooretrieve vistas coherentes de doble de un único dispositivo usan hello **getDeviceTwin** método Hola **registro** clase.</span><span class="sxs-lookup"><span data-stu-id="071dd-176">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="071dd-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="071dd-177">Next steps</span></span>
<span data-ttu-id="071dd-178">En este tutorial, establezca una configuración deseada como *deseado propiedades* de solución de hello back-end y escribió una toodetect de aplicación de dispositivo que cambian y simular un proceso de actualización de varios pasos reporting su estado a través de hello notificado Propiedades.</span><span class="sxs-lookup"><span data-stu-id="071dd-178">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="071dd-179">Hola de uso después cómo toolearn de recursos para:</span><span class="sxs-lookup"><span data-stu-id="071dd-179">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="071dd-180">enviar telemetría desde dispositivos con hello [empezar a trabajar con el centro de IoT] [ lnk-iothub-getstarted] tutorial,</span><span class="sxs-lookup"><span data-stu-id="071dd-180">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="071dd-181">programar o realizar operaciones en conjuntos grandes de dispositivos Consulte hello [programación y los trabajos de difusión] [ lnk-schedule-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="071dd-181">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="071dd-182">controlar los dispositivos de forma interactiva (por ejemplo, al activar un ventilador desde una aplicación controlada por el usuario), con hello [usar métodos directos] [ lnk-methods-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="071dd-182">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
