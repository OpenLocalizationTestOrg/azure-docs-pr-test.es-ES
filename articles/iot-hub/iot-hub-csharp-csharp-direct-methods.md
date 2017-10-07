---
title: "Centro de IoT de Azure aaaUse dirigir métodos (.NET/.NET) | Documentos de Microsoft"
description: "¿Cómo toouse centro de IoT de Azure dirigir métodos. Usar dispositivos de IoT de Azure de hello SDK para .NET tooimplement una aplicación de dispositivo simulado que incluye un método directo y el servicio IoT de Azure SDK para .NET tooimplement una aplicación de servicio que invoca el método directo Hola Hola."
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a><span data-ttu-id="f55b3-104">Uso de métodos directos (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="f55b3-104">Use direct methods (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="f55b3-105">En este tutorial, estamos continuo toodevelop aplicaciones de consola de .NET dos:</span><span class="sxs-lookup"><span data-stu-id="f55b3-105">In this tutorial, we are going toodevelop two .NET console apps:</span></span>

* <span data-ttu-id="f55b3-106">**CallMethodOnDevice**, una aplicación back-end, que llama a un método de aplicación de dispositivo simulado de hello y muestra la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="f55b3-106">**CallMethodOnDevice**, a back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="f55b3-107">**SimulateDeviceMethods**, una aplicación de consola que simula un dispositivo que se conecta el centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente y responde método toohello llamado a nube Hola.</span><span class="sxs-lookup"><span data-stu-id="f55b3-107">**SimulateDeviceMethods**, a console app which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="f55b3-108">artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que puede usar ambos toorun aplicaciones toobuild en dispositivos y el back-end de soluciones.</span><span class="sxs-lookup"><span data-stu-id="f55b3-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="f55b3-109">toocomplete este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="f55b3-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="f55b3-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="f55b3-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="f55b3-111">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="f55b3-111">An active Azure account.</span></span> <span data-ttu-id="f55b3-112">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="f55b3-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="f55b3-113">Si desea identidad del dispositivo toocreate hello mediante programación en su lugar, lea las secciones correspondientes de Hola Hola [conectar el centro de IoT de tooyour dispositivo simulado mediante .NET] [ lnk-device-identity-csharp] artículo.</span><span class="sxs-lookup"><span data-stu-id="f55b3-113">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="f55b3-114">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="f55b3-114">Create a simulated device app</span></span>
<span data-ttu-id="f55b3-115">En esta sección, creará una aplicación de consola .NET que responde el método tooa llamado a soluciones de hello volver final.</span><span class="sxs-lookup"><span data-stu-id="f55b3-115">In this section, you create a .NET console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="f55b3-116">En Visual Studio, agregue una solución actual de toohello de proyectos de Visual C# escritorio clásico de Windows mediante el uso de hello **aplicación de consola** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="f55b3-116">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="f55b3-117">Proyecto de hello Name **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="f55b3-117">Name hello project **SimulateDeviceMethods**.</span></span>
   
    ![Nueva aplicación para dispositivo de Windows clásico de Visual C#][img-createdeviceapp]
    
1. <span data-ttu-id="f55b3-119">En el Explorador de soluciones, haga clic en hello **SimulateDeviceMethods** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="f55b3-119">In Solution Explorer, right-click hello **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="f55b3-120">Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar** y busque **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="f55b3-120">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="f55b3-121">Seleccione **instalar** tooinstall hello **Microsoft.Azure.Devices.Client** empaquetar y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="f55b3-121">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="f55b3-122">Este procedimiento se descarga, se instala y se agrega una referencia toohello [dispositivos de IoT de Azure SDK] [ lnk-nuget-client-sdk] NuGet paquete y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="f55b3-122">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet: aplicación cliente][img-clientnuget]
1. <span data-ttu-id="f55b3-124">Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:</span><span class="sxs-lookup"><span data-stu-id="f55b3-124">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="f55b3-125">Agregar Hola después campos toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="f55b3-125">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="f55b3-126">Reemplace el valor de marcador de posición de hello con cadena de conexión de dispositivo de Hola que anotó en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="f55b3-126">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="f55b3-127">Agregue Hola siguiendo métodos directas de tooimplement hello en dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="f55b3-127">Add hello following tooimplement hello direct method on hello device:</span></span>

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. <span data-ttu-id="f55b3-128">Por último, agregue Hola después código toohello **Main** método tooopen Hola conexión tooyour IoT hub- and initialize Hola método agente de escucha:</span><span class="sxs-lookup"><span data-stu-id="f55b3-128">Finally, add hello following code toohello **Main** method tooopen hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. <span data-ttu-id="f55b3-129">Hola Visual Studio Solution Explorer, haga clic en la solución y, a continuación, haga clic en **Establecer proyectos de inicio...** . Seleccione **proyecto de inicio único**y, a continuación, seleccione hello **SimulateDeviceMethods** proyecto en el menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="f55b3-129">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **SimulateDeviceMethods** project in hello dropdown menu.</span></span>        

> [!NOTE]
> <span data-ttu-id="f55b3-130">tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento.</span><span class="sxs-lookup"><span data-stu-id="f55b3-130">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="f55b3-131">En el código de producción, debe implementar directivas de reintento (por ejemplo, los reintentos de conexión), tal como se sugiere en el artículo MSDN de hello [control de errores transitorios][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="f55b3-131">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="f55b3-132">Llamada a un método directo en un dispositivo</span><span class="sxs-lookup"><span data-stu-id="f55b3-132">Call a direct method on a device</span></span>
<span data-ttu-id="f55b3-133">En esta sección, creará una aplicación de consola .NET que llama a un método de aplicación de dispositivo simulado de hello y, a continuación, muestra la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="f55b3-133">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="f55b3-134">En Visual Studio, agregue una solución actual de toohello de proyectos de Visual C# escritorio clásico de Windows mediante el uso de hello **aplicación de consola** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="f55b3-134">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="f55b3-135">Asegúrese de que la versión de .NET Framework de hello es 4.5.1 o posterior.</span><span class="sxs-lookup"><span data-stu-id="f55b3-135">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="f55b3-136">Proyecto de hello Name **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="f55b3-136">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createserviceapp]
2. <span data-ttu-id="f55b3-138">En el Explorador de soluciones, haga clic en hello **CallMethodOnDevice** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="f55b3-138">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="f55b3-139">Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar**, busque **microsoft.azure.devices**, seleccione **instalar** tooinstall Hola **Microsoft.Azure.Devices** empaquetar y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="f55b3-139">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="f55b3-140">Este procedimiento se descarga, se instala y se agrega una referencia toohello [IoT de Azure SDK del servicio] [ lnk-nuget-service-sdk] NuGet paquete y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="f55b3-140">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]

4. <span data-ttu-id="f55b3-142">Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:</span><span class="sxs-lookup"><span data-stu-id="f55b3-142">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="f55b3-143">Agregar Hola después campos toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="f55b3-143">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="f55b3-144">Sustituya el valor de marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="f55b3-144">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="f55b3-145">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="f55b3-145">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="f55b3-146">Este método invoca un método directo con el nombre `writeLine` en hello `myDeviceId` dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f55b3-146">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="f55b3-147">A continuación, escribe respuesta Hola proporcionada por dispositivo de hello en la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="f55b3-147">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="f55b3-148">Tenga en cuenta cómo es posible toospecify un valor de tiempo de espera para hello dispositivo toorespond.</span><span class="sxs-lookup"><span data-stu-id="f55b3-148">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="f55b3-149">Por último, agregue Hola después líneas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="f55b3-149">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="f55b3-150">Hola Visual Studio Solution Explorer, haga clic en la solución y, a continuación, haga clic en **Establecer proyectos de inicio...** . Seleccione **proyecto de inicio único**y, a continuación, seleccione hello **CallMethodOnDevice** proyecto en el menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="f55b3-150">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="f55b3-151">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="f55b3-151">Run hello applications</span></span>
<span data-ttu-id="f55b3-152">Ya estás listo toorun aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="f55b3-152">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="f55b3-153">Ejecutar la aplicación de dispositivo de hello .NET **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="f55b3-153">Run hello .NET device app **SimulateDeviceMethods**.</span></span> <span data-ttu-id="f55b3-154">Debería empezar a escuchar llamadas de método desde IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="f55b3-154">It should start listening for method calls from your IoT Hub:</span></span> 

    ![Ejecución de la aplicación de dispositivo][img-deviceapprun]
1. <span data-ttu-id="f55b3-156">Ahora está conectado a ese dispositivo hello y espera para las invocaciones de método, ejecute hello .NET **CallMethodOnDevice** el método de aplicación tooinvoke hello en la aplicación de dispositivo simulado de hello.</span><span class="sxs-lookup"><span data-stu-id="f55b3-156">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="f55b3-157">Debería ver la respuesta del dispositivo Hola escrito en la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="f55b3-157">You should see hello device response written in hello console.</span></span>
   
    ![Ejecución de la aplicación de servicio][img-serviceapprun]
1. <span data-ttu-id="f55b3-159">dispositivo de Hello, a continuación, reacciona toohello método imprimiendo este mensaje:</span><span class="sxs-lookup"><span data-stu-id="f55b3-159">hello device then reacts toohello method by printing this message:</span></span>
   
    ![Método directo que se invoca en el dispositivo de Hola][img-directmethodinvoked]

## <a name="next-steps"></a><span data-ttu-id="f55b3-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f55b3-161">Next steps</span></span>
<span data-ttu-id="f55b3-162">En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="f55b3-162">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="f55b3-163">Utiliza este toomethods dispositivo identidad tooenable Hola simulada dispositivos aplicación tooreact invocado por la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="f55b3-163">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="f55b3-164">También crea una aplicación que invoca los métodos en el dispositivo de Hola y muestra la respuesta de hello de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f55b3-164">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="f55b3-165">toocontinue introducción con el centro de IoT y tooexplore otros escenarios de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="f55b3-165">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="f55b3-166">[Introducción al Centro de IoT]</span><span class="sxs-lookup"><span data-stu-id="f55b3-166">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="f55b3-167">[Programación de trabajos en varios dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="f55b3-167">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="f55b3-168">toolearn cómo tooextend llama a su método de programación y de solución de IoT en varios dispositivos, vea hello [programación y los trabajos de difusión] [ lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="f55b3-168">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[Introducción al Centro de IoT]: iot-hub-node-node-getstarted.md
