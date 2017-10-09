---
title: "aaaUse centro de IoT de Azure dirigir métodos (nodo/.NET) | Documentos de Microsoft"
description: "¿Cómo toouse centro de IoT de Azure dirigir métodos. Usar dispositivos de IoT de Azure de hello SDK para Node.js tooimplement una aplicación de dispositivo simulado que incluye un método directo y el servicio IoT de Azure SDK para .NET tooimplement una aplicación de servicio que invoca el método directo Hola Hola."
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
ms.openlocfilehash: f566f939be840eb308b00ffa4e05c4e5b3fefb39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="c73a3-104">Uso de métodos directos (.NET y Node)</span><span class="sxs-lookup"><span data-stu-id="c73a3-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="c73a3-105">En este tutorial, vamos a toodevelop .NET y una aplicación de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="c73a3-105">In this tutorial, we are going toodevelop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="c73a3-106">**CallMethodOnDevice.sln**, una aplicación de back-end. NET, que llama a un método de aplicación de dispositivo simulado de hello y muestra la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a3-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="c73a3-107">**SimulatedDevice.js**, una aplicación Node.js, que simula un dispositivo que se conecta el centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente y responde método toohello llamado a nube Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a3-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="c73a3-108">artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que puede usar ambos toorun aplicaciones toobuild en dispositivos y el back-end de soluciones.</span><span class="sxs-lookup"><span data-stu-id="c73a3-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="c73a3-109">toocomplete este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="c73a3-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="c73a3-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c73a3-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="c73a3-111">Node.js versión 0.10.x, o posteriores.</span><span class="sxs-lookup"><span data-stu-id="c73a3-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="c73a3-112">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="c73a3-112">An active Azure account.</span></span> <span data-ttu-id="c73a3-113">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="c73a3-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="c73a3-114">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="c73a3-114">Create a simulated device app</span></span>
<span data-ttu-id="c73a3-115">En esta sección, creará una aplicación de consola de Node.js que responde el método tooa llamado a soluciones de hello volver final.</span><span class="sxs-lookup"><span data-stu-id="c73a3-115">In this section, you create a Node.js console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="c73a3-116">Cree una nueva carpeta vacía denominada **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="c73a3-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="c73a3-117">Hola **simulateddevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="c73a3-117">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="c73a3-118">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="c73a3-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="c73a3-119">En el símbolo del sistema en hello **simulateddevice** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure** y **azure-iot-dispositivo-mqtt** paquetes:</span><span class="sxs-lookup"><span data-stu-id="c73a3-119">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="c73a3-120">Con un editor de texto, cree un archivo en hello **simulateddevice** carpeta y asígnele el nombre **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="c73a3-120">Using a text editor, create a file in hello **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="c73a3-121">Agregue Hola siguiente `require` las instrucciones en hello inician de hello **SimulatedDevice.js** archivo:</span><span class="sxs-lookup"><span data-stu-id="c73a3-121">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="c73a3-122">Agregar un **connectionString** variable y utilizar toocreate un **DeviceClient** instancia.</span><span class="sxs-lookup"><span data-stu-id="c73a3-122">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="c73a3-123">Reemplace **{cadena de conexión de dispositivo}** con cadena de conexión de dispositivo de Hola que generó en hello *crear una identidad de dispositivo* sección:</span><span class="sxs-lookup"><span data-stu-id="c73a3-123">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="c73a3-124">Agregue Hola siguiendo métodos directas de función tooimplement hello en dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="c73a3-124">Add hello following function tooimplement hello direct method on hello device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="c73a3-125">Abrir el centro de IoT de hello conexión tooyour e inicializar el agente de escucha de hello método:</span><span class="sxs-lookup"><span data-stu-id="c73a3-125">Open hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
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
8. <span data-ttu-id="c73a3-126">Guarde y cierre hello **SimulatedDevice.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="c73a3-126">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="c73a3-127">tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento.</span><span class="sxs-lookup"><span data-stu-id="c73a3-127">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="c73a3-128">En el código de producción, debe implementar directivas de reintento (por ejemplo, los reintentos de conexión), tal como se sugiere en el artículo MSDN de hello [control de errores transitorios][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="c73a3-128">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="c73a3-129">Llamada a un método directo en un dispositivo</span><span class="sxs-lookup"><span data-stu-id="c73a3-129">Call a direct method on a device</span></span>
<span data-ttu-id="c73a3-130">En esta sección, creará una aplicación de consola .NET que llama a un método de aplicación de dispositivo simulado de hello y, a continuación, muestra la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a3-130">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="c73a3-131">En Visual Studio, agregue una solución actual de toohello de proyectos de Visual C# escritorio clásico de Windows mediante el uso de hello **aplicación de consola** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="c73a3-131">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="c73a3-132">Asegúrese de que la versión de .NET Framework de hello es 4.5.1 o posterior.</span><span class="sxs-lookup"><span data-stu-id="c73a3-132">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="c73a3-133">Proyecto de hello Name **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="c73a3-133">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][10]
2. <span data-ttu-id="c73a3-135">En el Explorador de soluciones, haga clic en hello **CallMethodOnDevice** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="c73a3-135">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="c73a3-136">Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar**, busque **microsoft.azure.devices**, seleccione **instalar** tooinstall Hola **Microsoft.Azure.Devices** empaquetar y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="c73a3-136">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="c73a3-137">Este procedimiento se descarga, se instala y se agrega una referencia toohello [IoT de Azure SDK del servicio] [ lnk-nuget-service-sdk] NuGet paquete y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="c73a3-137">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet][11]

4. <span data-ttu-id="c73a3-139">Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:</span><span class="sxs-lookup"><span data-stu-id="c73a3-139">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="c73a3-140">Agregar Hola después campos toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="c73a3-140">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="c73a3-141">Sustituya el valor de marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a3-141">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="c73a3-142">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="c73a3-142">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="c73a3-143">Este método invoca un método directo con el nombre `writeLine` en hello `myDeviceId` dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c73a3-143">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="c73a3-144">A continuación, escribe respuesta Hola proporcionada por dispositivo de hello en la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a3-144">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="c73a3-145">Tenga en cuenta cómo es posible toospecify un valor de tiempo de espera para hello dispositivo toorespond.</span><span class="sxs-lookup"><span data-stu-id="c73a3-145">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="c73a3-146">Por último, agregue Hola después líneas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="c73a3-146">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

## <a name="run-hello-applications"></a><span data-ttu-id="c73a3-147">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="c73a3-147">Run hello applications</span></span>
<span data-ttu-id="c73a3-148">Ya estás listo toorun aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a3-148">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="c73a3-149">Hola Visual Studio Solution Explorer, haga clic en la solución y, a continuación, haga clic en **Establecer proyectos de inicio...** . Seleccione **proyecto de inicio único**y, a continuación, seleccione hello **CallMethodOnDevice** proyecto en el menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a3-149">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

2. <span data-ttu-id="c73a3-150">En un símbolo del sistema en hello **simulateddevice** carpeta, ejecute hello después de realizar escuchas para las llamadas de método desde el centro de IoT de toostart de comando:</span><span class="sxs-lookup"><span data-stu-id="c73a3-150">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="c73a3-151">Espere Hola simulada dispositivos tooopen:![][7]</span><span class="sxs-lookup"><span data-stu-id="c73a3-151">Wait for hello simulated device tooopen:  ![][7]</span></span>
3. <span data-ttu-id="c73a3-152">Ahora está conectado a ese dispositivo hello y espera para las invocaciones de método, ejecute hello .NET **CallMethodOnDevice** el método de aplicación tooinvoke hello en la aplicación de dispositivo simulado de hello.</span><span class="sxs-lookup"><span data-stu-id="c73a3-152">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="c73a3-153">Debería ver la respuesta del dispositivo Hola escrito en la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a3-153">You should see hello device response written in hello console.</span></span>
   
    ![][8]
4. <span data-ttu-id="c73a3-154">dispositivo de Hello, a continuación, reacciona toohello método imprimiendo este mensaje:</span><span class="sxs-lookup"><span data-stu-id="c73a3-154">hello device then reacts toohello method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="c73a3-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c73a3-155">Next steps</span></span>
<span data-ttu-id="c73a3-156">En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a3-156">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="c73a3-157">Utiliza este toomethods dispositivo identidad tooenable Hola simulada dispositivos aplicación tooreact invocado por la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a3-157">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="c73a3-158">También crea una aplicación que invoca los métodos en el dispositivo de Hola y muestra la respuesta de hello de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c73a3-158">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="c73a3-159">toocontinue introducción con el centro de IoT y tooexplore otros escenarios de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="c73a3-159">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="c73a3-160">[Introducción al Centro de IoT]</span><span class="sxs-lookup"><span data-stu-id="c73a3-160">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="c73a3-161">[Programación de trabajos en varios dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="c73a3-161">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="c73a3-162">toolearn cómo tooextend llama a su método de programación y de solución de IoT en varios dispositivos, vea hello [programación y los trabajos de difusión] [ lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="c73a3-162">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
[Introducción al Centro de IoT]: iot-hub-node-node-getstarted.md
