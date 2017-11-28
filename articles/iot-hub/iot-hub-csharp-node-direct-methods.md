---
title: "Uso de los métodos directos de IoT Hub de Azure (.NET y Node) | Microsoft Docs"
description: "Describe cómo usar los métodos directos de IoT Hub de Azure. Usará el SDK de dispositivo IoT de Azure para Node.js con el fin de implementar una aplicación de dispositivo simulado que incluye un método directo, además del SDK de servicio IoT de Azure para .NET con el objetivo de implementar una aplicación de servicio que invoque el método directo."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: ad705789a153381e21b2ccb05d4e0c17f78671fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="66ec9-104">Uso de métodos directos (.NET y Node)</span><span class="sxs-lookup"><span data-stu-id="66ec9-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="66ec9-105">En este tutorial, vamos a desarrollar una aplicación de consola de Node.js y de .NET:</span><span class="sxs-lookup"><span data-stu-id="66ec9-105">In this tutorial, we are going to develop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="66ec9-106">**CallMethodOnDevice.js**, una aplicación de back-end de .NET, que llama a un método de la aplicación de dispositivo simulado y muestra la respuesta.</span><span class="sxs-lookup"><span data-stu-id="66ec9-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="66ec9-107">**SimulatedDevice.js**, una aplicación de Node.js que simula un dispositivo que se conecta a su centro de IoT con la identidad del dispositivo creada anteriormente y responde al método llamado por la nube.</span><span class="sxs-lookup"><span data-stu-id="66ec9-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="66ec9-108">En el artículo [Azure Iot SDKs][lnk-hub-sdks] (SDK de IoT de Azure) se proporciona información acerca de los diversos SDK que puede usar para crear ambas aplicaciones para que se ejecuten en dispositivos y en el back-end de la solución.</span><span class="sxs-lookup"><span data-stu-id="66ec9-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="66ec9-109">Para completar este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="66ec9-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="66ec9-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="66ec9-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="66ec9-111">Node.js versión 0.10.x, o posteriores.</span><span class="sxs-lookup"><span data-stu-id="66ec9-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="66ec9-112">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="66ec9-112">An active Azure account.</span></span> <span data-ttu-id="66ec9-113">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="66ec9-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="66ec9-114">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="66ec9-114">Create a simulated device app</span></span>
<span data-ttu-id="66ec9-115">En esta sección, creará una aplicación de consola de Node.js que responda a un método llamado por el back-end de solución.</span><span class="sxs-lookup"><span data-stu-id="66ec9-115">In this section, you create a Node.js console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="66ec9-116">Cree una nueva carpeta vacía denominada **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="66ec9-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="66ec9-117">En la carpeta **simulateddevice**, cree un archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="66ec9-117">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="66ec9-118">Acepte todos los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="66ec9-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="66ec9-119">En el símbolo del sistema, en la carpeta **simulateddevice**, ejecute el siguiente comando para instalar los paquetes **azure-iot-device** y **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="66ec9-119">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="66ec9-120">Con un editor de texto, cree un archivo en la carpeta **simulateddevice** y asígnele el nombre **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="66ec9-120">Using a text editor, create a file in the **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="66ec9-121">Agregue las siguientes instrucciones `require` al principio del archivo **SimulatedDevice.js** :</span><span class="sxs-lookup"><span data-stu-id="66ec9-121">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="66ec9-122">Agregue una variable **connectionString** y utilícela para crear una instancia de **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="66ec9-122">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="66ec9-123">Reemplace **{device connection string}** por la cadena conexión de dispositivo que generó en la sección sobre cómo *crear una identidad de dispositivo*:</span><span class="sxs-lookup"><span data-stu-id="66ec9-123">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="66ec9-124">Agregue la siguiente función para implementar el método directo en el dispositivo:</span><span class="sxs-lookup"><span data-stu-id="66ec9-124">Add the following function to implement the direct method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="66ec9-125">Abra la conexión al centro de IoT y e inicialice la escucha del método:</span><span class="sxs-lookup"><span data-stu-id="66ec9-125">Open the connection to your IoT hub and initialize the method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. <span data-ttu-id="66ec9-126">Guarde el archivo **SimulatedDevice.js** y ciérrelo.</span><span class="sxs-lookup"><span data-stu-id="66ec9-126">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="66ec9-127">Por simplificar, este tutorial no implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="66ec9-127">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="66ec9-128">En el código de producción, debe implementar directivas de reintento (por ejemplo, reintento de conexión), tal y como se sugiere en el artículo de MSDN [Transient Fault Handling][lnk-transient-faults] (Control de errores temporales).</span><span class="sxs-lookup"><span data-stu-id="66ec9-128">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="66ec9-129">Llamada a un método directo en un dispositivo</span><span class="sxs-lookup"><span data-stu-id="66ec9-129">Call a direct method on a device</span></span>
<span data-ttu-id="66ec9-130">En esta sección, creará una aplicación de consola de .NET que llame a un método en la aplicación de dispositivo simulado y muestre la respuesta.</span><span class="sxs-lookup"><span data-stu-id="66ec9-130">In this section, you create a .NET console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="66ec9-131">En Visual Studio, agregue un proyecto de escritorio clásico de Windows de Visual C# a la solución actual mediante la plantilla de proyecto **Aplicación de consola** .</span><span class="sxs-lookup"><span data-stu-id="66ec9-131">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="66ec9-132">Asegúrese de que la versión de .NET Framework sea 4.5.1 o una posterior.</span><span class="sxs-lookup"><span data-stu-id="66ec9-132">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="66ec9-133">Asigne al proyecto el nombre **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="66ec9-133">Name the project **CallMethodOnDevice**.</span></span>
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][10]
2. <span data-ttu-id="66ec9-135">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **CallMethodOnDevice** y luego seleccione **Administrar paquetes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="66ec9-135">In Solution Explorer, right-click the **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="66ec9-136">En la ventana **Administrador de paquetes NuGet**, seleccione **Examinar**, busque **microsoft.azure.devices**, seleccione **Instalar** para instalar el paquete **Microsoft.Azure.Devices** y acepte los términos de uso.</span><span class="sxs-lookup"><span data-stu-id="66ec9-136">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="66ec9-137">Este procedimiento permite descargar, instalar y agregar una referencia al [paquete NuGet del SDK de dispositivo de IoT de Azure][lnk-nuget-service-sdk] y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="66ec9-137">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet][11]

4. <span data-ttu-id="66ec9-139">Agregue las siguientes instrucciones `using` al principio del archivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="66ec9-139">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="66ec9-140">Agregue los campos siguientes a la clase **Program** .</span><span class="sxs-lookup"><span data-stu-id="66ec9-140">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="66ec9-141">Sustituya el valor de marcador de posición por la cadena de conexión de IoT Hub para el centro que creó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="66ec9-141">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="66ec9-142">Agregue el método siguiente a la clase **Program** :</span><span class="sxs-lookup"><span data-stu-id="66ec9-142">Add the following method to the **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line to be written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="66ec9-143">Este método invoca un método directo con el nombre `writeLine` en el dispositivo `myDeviceId`.</span><span class="sxs-lookup"><span data-stu-id="66ec9-143">This method invokes a direct method with name `writeLine` on the `myDeviceId` device.</span></span> <span data-ttu-id="66ec9-144">A continuación, escribe la respuesta proporcionada por el dispositivo en la consola.</span><span class="sxs-lookup"><span data-stu-id="66ec9-144">Then, it writes the response provided by the device on the console.</span></span> <span data-ttu-id="66ec9-145">Observe cómo es posible especificar un valor de tiempo de espera de respuesta para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="66ec9-145">Note how it is possible to specify a timeout value for the device to respond.</span></span>
7. <span data-ttu-id="66ec9-146">Por último, agregue las líneas siguientes al método **Main** :</span><span class="sxs-lookup"><span data-stu-id="66ec9-146">Finally, add the following lines to the **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

## <a name="run-the-applications"></a><span data-ttu-id="66ec9-147">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="66ec9-147">Run the applications</span></span>
<span data-ttu-id="66ec9-148">Ahora está preparado para ejecutar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="66ec9-148">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="66ec9-149">En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en la solución y seleccione **Establecer proyectos de inicio...**.</span><span class="sxs-lookup"><span data-stu-id="66ec9-149">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="66ec9-150">Seleccione **Proyecto de inicio único**y, a continuación, seleccione el proyecto **CallMethodOnDevice** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="66ec9-150">Select **Single startup project**, and then select the **CallMethodOnDevice** project in the dropdown menu.</span></span>

2. <span data-ttu-id="66ec9-151">En un símbolo del sistema, en la carpeta **simulateddevice** , ejecute el siguiente comando para empezar la escucha de llamadas de método desde IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="66ec9-151">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="66ec9-152">Espere a que se abra el dispositivo simulado: ![][7]</span><span class="sxs-lookup"><span data-stu-id="66ec9-152">Wait for the simulated device to open:  ![][7]</span></span>
3. <span data-ttu-id="66ec9-153">Ahora que el dispositivo está conectado y esperando invocaciones del método, ejecute la aplicación **CallMethodOnDevice** de .NET para invocar el método en la aplicación de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="66ec9-153">Now that the device is connected and waiting for method invocations, run the .NET **CallMethodOnDevice** app to invoke the method in the simulated device app.</span></span> <span data-ttu-id="66ec9-154">Debería ver la respuesta del dispositivo escrita en la consola.</span><span class="sxs-lookup"><span data-stu-id="66ec9-154">You should see the device response written in the console.</span></span>
   
    ![][8]
4. <span data-ttu-id="66ec9-155">El dispositivo, a continuación, responde al método imprimiendo este mensaje:</span><span class="sxs-lookup"><span data-stu-id="66ec9-155">The device then reacts to the method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="66ec9-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="66ec9-156">Next steps</span></span>
<span data-ttu-id="66ec9-157">En este tutorial, configuró un centro de IoT nuevo en Azure Portal y, después, creó una identidad de dispositivo en el registro de identidades del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="66ec9-157">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="66ec9-158">Usó esta identidad de dispositivo para que la aplicación del dispositivo simulado reaccionara a los métodos que se invoquen desde la nube.</span><span class="sxs-lookup"><span data-stu-id="66ec9-158">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="66ec9-159">También creó una aplicación que invoca métodos en el dispositivo y muestra la respuesta del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="66ec9-159">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="66ec9-160">Para continuar la introducción a IoT Hub y explorar otros escenarios de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="66ec9-160">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="66ec9-161">[Introducción a Iot Hub]</span><span class="sxs-lookup"><span data-stu-id="66ec9-161">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="66ec9-162">[Programación de trabajos en varios dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="66ec9-162">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="66ec9-163">Para información sobre cómo ampliar la solución de IoT y programar llamadas de método en varios dispositivos, consulte el tutorial [Programación de trabajos en varios dispositivos][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="66ec9-163">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: ./media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
<span data-ttu-id="66ec9-164">[Introducción a Iot Hub]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="66ec9-164">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
