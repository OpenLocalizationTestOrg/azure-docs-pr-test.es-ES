---
title: "Uso de los métodos directos de Azure IoT Hub (.NET/.NET) | Microsoft Docs"
description: "Describe cómo usar los métodos directos de IoT Hub de Azure. Usará el SDK de dispositivo IoT de Azure para .NET con el fin de implementar una aplicación de dispositivo simulado que incluye un método directo, además del SDK de servicio IoT de Azure para .NET con el objetivo de implementar una aplicación de servicio que invoque el método directo."
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
ms.openlocfilehash: 9ce1fbebb6417c10618aa182e3c1d9ddf8132fb6
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="use-direct-methods-netnet"></a><span data-ttu-id="2b540-104">Uso de métodos directos (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="2b540-104">Use direct methods (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="2b540-105">En este tutorial, vamos a desarrollar dos aplicaciones de consola de .NET:</span><span class="sxs-lookup"><span data-stu-id="2b540-105">In this tutorial, we are going to develop two .NET console apps:</span></span>

* <span data-ttu-id="2b540-106">**CallMethodOnDevice**, una aplicación de back-end, que llama a un método de la aplicación de dispositivo simulado y muestra la respuesta.</span><span class="sxs-lookup"><span data-stu-id="2b540-106">**CallMethodOnDevice**, a back-end app, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="2b540-107">**SimulateDeviceMethods**, una aplicación de consola que simula un dispositivo que se conecta a su IoT Hub con la identidad del dispositivo creada anteriormente y responde al método llamado por la nube.</span><span class="sxs-lookup"><span data-stu-id="2b540-107">**SimulateDeviceMethods**, a console app which simulates a device connecting to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="2b540-108">En el artículo [Azure Iot SDKs][lnk-hub-sdks] (SDK de IoT de Azure) se proporciona información acerca de los diversos SDK que puede usar para crear ambas aplicaciones para que se ejecuten en dispositivos y en el back-end de la solución.</span><span class="sxs-lookup"><span data-stu-id="2b540-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="2b540-109">Para completar este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="2b540-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="2b540-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2b540-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="2b540-111">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="2b540-111">An active Azure account.</span></span> <span data-ttu-id="2b540-112">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="2b540-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="2b540-113">Si, por el contrario, desea crear la identidad del dispositivo mediante programación, lea la sección correspondiente en el artículo [Conexión del dispositivo simulado en el centro de IoT con .NET][lnk-device-identity-csharp].</span><span class="sxs-lookup"><span data-stu-id="2b540-113">If you want to create the device identity programmatically instead, read the corresponding section in the [Connect your simulated device to your IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="2b540-114">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="2b540-114">Create a simulated device app</span></span>
<span data-ttu-id="2b540-115">En esta sección, creará una aplicación de consola de .NET que responderá a un método llamado por el back-end de solución.</span><span class="sxs-lookup"><span data-stu-id="2b540-115">In this section, you create a .NET console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="2b540-116">En Visual Studio, agregue un proyecto de escritorio clásico de Windows de Visual C# a la solución actual mediante la plantilla de proyecto **Aplicación de consola** .</span><span class="sxs-lookup"><span data-stu-id="2b540-116">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="2b540-117">Asigne al proyecto el nombre **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="2b540-117">Name the project **SimulateDeviceMethods**.</span></span>
   
    ![Nueva aplicación para dispositivo de Windows clásico de Visual C#][img-createdeviceapp]
    
1. <span data-ttu-id="2b540-119">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **SimulateDeviceMethods** y luego haga clic en **Administrar paquetes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="2b540-119">In Solution Explorer, right-click the **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="2b540-120">En la ventana **Administrador de paquetes NuGet**, seleccione **Examinar** y busque **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="2b540-120">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="2b540-121">Seleccione **Instalar** para instalar el paquete **Microsoft.Azure.Devices.Client** y acepte las condiciones de uso.</span><span class="sxs-lookup"><span data-stu-id="2b540-121">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="2b540-122">Este procedimiento permite descargar, instalar y agregar una referencia al paquete NuGet del [SDK de dispositivo Azure IoT][lnk-nuget-client-sdk] y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="2b540-122">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet: aplicación cliente][img-clientnuget]
1. <span data-ttu-id="2b540-124">Agregue las siguientes instrucciones `using` al principio del archivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="2b540-124">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="2b540-125">Agregue los campos siguientes a la clase **Program** .</span><span class="sxs-lookup"><span data-stu-id="2b540-125">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="2b540-126">Sustituya el valor de marcador de posición por la cadena de conexión del dispositivo del anotó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="2b540-126">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="2b540-127">Agregue lo siguiente para implementar el método directo en el dispositivo:</span><span class="sxs-lookup"><span data-stu-id="2b540-127">Add the following to implement the direct method on the device:</span></span>

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written to log.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. <span data-ttu-id="2b540-128">Finalmente, agregue el código siguiente al método **Main** para abrir la conexión a su IoT Hub e inicializar la escucha del método directo:</span><span class="sxs-lookup"><span data-stu-id="2b540-128">Finally, add the following code to the **Main** method to open the connection to your IoT hub and initialize the method listener:</span></span>
   
        try
        {
            Console.WriteLine("Connecting to hub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter to exit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove the "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. <span data-ttu-id="2b540-129">En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en la solución y seleccione **Establecer proyectos de inicio...**.</span><span class="sxs-lookup"><span data-stu-id="2b540-129">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="2b540-130">Seleccione **Proyecto de inicio único** y luego seleccione el proyecto **SimulateDeviceMethods** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="2b540-130">Select **Single startup project**, and then select the **SimulateDeviceMethods** project in the dropdown menu.</span></span>        

> [!NOTE]
> <span data-ttu-id="2b540-131">Por simplificar, este tutorial no implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="2b540-131">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="2b540-132">En el código de producción, debe implementar directivas de reintento (por ejemplo, reintento de conexión), tal y como se sugiere en el artículo de MSDN [Transient Fault Handling][lnk-transient-faults] (Control de errores temporales).</span><span class="sxs-lookup"><span data-stu-id="2b540-132">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="2b540-133">Llamada a un método directo en un dispositivo</span><span class="sxs-lookup"><span data-stu-id="2b540-133">Call a direct method on a device</span></span>
<span data-ttu-id="2b540-134">En esta sección, creará una aplicación de consola de .NET que llame a un método en la aplicación de dispositivo simulado y muestre la respuesta.</span><span class="sxs-lookup"><span data-stu-id="2b540-134">In this section, you create a .NET console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="2b540-135">En Visual Studio, agregue un proyecto de escritorio clásico de Windows de Visual C# a la solución actual mediante la plantilla de proyecto **Aplicación de consola** .</span><span class="sxs-lookup"><span data-stu-id="2b540-135">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="2b540-136">Asegúrese de que la versión de .NET Framework sea 4.5.1 o una posterior.</span><span class="sxs-lookup"><span data-stu-id="2b540-136">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="2b540-137">Asigne al proyecto el nombre **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="2b540-137">Name the project **CallMethodOnDevice**.</span></span>
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createserviceapp]
2. <span data-ttu-id="2b540-139">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **CallMethodOnDevice** y luego seleccione **Administrar paquetes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="2b540-139">In Solution Explorer, right-click the **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="2b540-140">En la ventana **Administrador de paquetes NuGet**, seleccione **Examinar**, busque **microsoft.azure.devices**, seleccione **Instalar** para instalar el paquete **Microsoft.Azure.Devices** y acepte los términos de uso.</span><span class="sxs-lookup"><span data-stu-id="2b540-140">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="2b540-141">Este procedimiento permite descargar, instalar y agregar una referencia al [paquete NuGet del SDK de dispositivo de IoT de Azure][lnk-nuget-service-sdk] y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="2b540-141">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]

4. <span data-ttu-id="2b540-143">Agregue las siguientes instrucciones `using` al principio del archivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="2b540-143">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="2b540-144">Agregue los campos siguientes a la clase **Program** .</span><span class="sxs-lookup"><span data-stu-id="2b540-144">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="2b540-145">Sustituya el valor de marcador de posición por la cadena de conexión de IoT Hub para el centro que creó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="2b540-145">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="2b540-146">Agregue el método siguiente a la clase **Program** :</span><span class="sxs-lookup"><span data-stu-id="2b540-146">Add the following method to the **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line to be written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="2b540-147">Este método invoca un método directo con el nombre `writeLine` en el dispositivo `myDeviceId`.</span><span class="sxs-lookup"><span data-stu-id="2b540-147">This method invokes a direct method with name `writeLine` on the `myDeviceId` device.</span></span> <span data-ttu-id="2b540-148">A continuación, escribe la respuesta proporcionada por el dispositivo en la consola.</span><span class="sxs-lookup"><span data-stu-id="2b540-148">Then, it writes the response provided by the device on the console.</span></span> <span data-ttu-id="2b540-149">Observe cómo es posible especificar un valor de tiempo de espera de respuesta para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2b540-149">Note how it is possible to specify a timeout value for the device to respond.</span></span>
7. <span data-ttu-id="2b540-150">Por último, agregue las líneas siguientes al método **Main** :</span><span class="sxs-lookup"><span data-stu-id="2b540-150">Finally, add the following lines to the **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="2b540-151">En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en la solución y seleccione **Establecer proyectos de inicio...**.</span><span class="sxs-lookup"><span data-stu-id="2b540-151">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="2b540-152">Seleccione **Proyecto de inicio único**y, a continuación, seleccione el proyecto **CallMethodOnDevice** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="2b540-152">Select **Single startup project**, and then select the **CallMethodOnDevice** project in the dropdown menu.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="2b540-153">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="2b540-153">Run the applications</span></span>
<span data-ttu-id="2b540-154">Ahora está preparado para ejecutar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2b540-154">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="2b540-155">Ejecute la aplicación de dispositivos .NET **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="2b540-155">Run the .NET device app **SimulateDeviceMethods**.</span></span> <span data-ttu-id="2b540-156">Debería empezar a escuchar llamadas de método desde IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="2b540-156">It should start listening for method calls from your IoT Hub:</span></span> 

    ![Ejecución de la aplicación de dispositivo][img-deviceapprun]
1. <span data-ttu-id="2b540-158">Ahora que el dispositivo está conectado y esperando invocaciones del método, ejecute la aplicación **CallMethodOnDevice** de .NET para invocar el método en la aplicación de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="2b540-158">Now that the device is connected and waiting for method invocations, run the .NET **CallMethodOnDevice** app to invoke the method in the simulated device app.</span></span> <span data-ttu-id="2b540-159">Debería ver la respuesta del dispositivo escrita en la consola.</span><span class="sxs-lookup"><span data-stu-id="2b540-159">You should see the device response written in the console.</span></span>
   
    ![Ejecución de la aplicación de servicio][img-serviceapprun]
1. <span data-ttu-id="2b540-161">El dispositivo, a continuación, responde al método imprimiendo este mensaje:</span><span class="sxs-lookup"><span data-stu-id="2b540-161">The device then reacts to the method by printing this message:</span></span>
   
    ![Método directo que se invoca en el dispositivo][img-directmethodinvoked]

## <a name="next-steps"></a><span data-ttu-id="2b540-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2b540-163">Next steps</span></span>
<span data-ttu-id="2b540-164">En este tutorial, configuró un centro de IoT nuevo en Azure Portal y, después, creó una identidad de dispositivo en el registro de identidades del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="2b540-164">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="2b540-165">Usó esta identidad de dispositivo para que la aplicación del dispositivo simulado reaccionara a los métodos que se invoquen desde la nube.</span><span class="sxs-lookup"><span data-stu-id="2b540-165">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="2b540-166">También creó una aplicación que invoca métodos en el dispositivo y muestra la respuesta del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2b540-166">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="2b540-167">Para continuar la introducción a IoT Hub y explorar otros escenarios de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="2b540-167">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="2b540-168">[Introducción a Iot Hub]</span><span class="sxs-lookup"><span data-stu-id="2b540-168">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="2b540-169">[Programación de trabajos en varios dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="2b540-169">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="2b540-170">Para información sobre cómo ampliar la solución de IoT y programar llamadas de método en varios dispositivos, consulte el tutorial [Programación de trabajos en varios dispositivos][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="2b540-170">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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

<span data-ttu-id="2b540-171">[Introducción a Iot Hub]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="2b540-171">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
