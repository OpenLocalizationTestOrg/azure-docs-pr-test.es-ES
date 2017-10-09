---
title: trabajos de aaaSchedule con el centro de IoT de Azure (nodo/.NET) | Documentos de Microsoft
description: "¿Cómo tooschedule un centro de IoT de Azure trabajo tooinvoke un método directo en varios dispositivos. Usar dispositivos de IoT de Azure de hello SDK para hello servicio IoT de Azure SDK para .NET tooimplement un trabajo de servicio aplicación toorun hello y aplicaciones para dispositivos Node.js tooimplement Hola simulada."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: juanpere
ms.openlocfilehash: f6148b67129dde4580bfe9ccceafd6400fbc5976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a><span data-ttu-id="d7686-104">Programación y difusión de trabajos (.NET/Node.js)</span><span class="sxs-lookup"><span data-stu-id="d7686-104">Schedule and broadcast jobs (.NET/Node.js)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="d7686-105">Utilice los trabajos de tooschedule y realizar un seguimiento de centro de IoT de Azure que actualizan millones de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d7686-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="d7686-106">Use los trabajos para:</span><span class="sxs-lookup"><span data-stu-id="d7686-106">Use jobs to:</span></span>

* <span data-ttu-id="d7686-107">Actualizar las propiedades deseadas</span><span class="sxs-lookup"><span data-stu-id="d7686-107">Update desired properties</span></span>
* <span data-ttu-id="d7686-108">Actualizar etiquetas</span><span class="sxs-lookup"><span data-stu-id="d7686-108">Update tags</span></span>
* <span data-ttu-id="d7686-109">Invocar métodos directos</span><span class="sxs-lookup"><span data-stu-id="d7686-109">Invoke direct methods</span></span>

<span data-ttu-id="d7686-110">Un trabajo encapsula una de estas acciones y pistas Hola ejecución con un conjunto de dispositivos que se define mediante una consulta de gemelas de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d7686-110">A job wraps one of these actions and tracks hello execution against a set of devices that is defined by a device twin query.</span></span> <span data-ttu-id="d7686-111">Por ejemplo, una aplicación de back-end puede usar un tooinvoke de trabajo un método directo en 10.000 dispositivos que reinicia dispositivos Hola.</span><span class="sxs-lookup"><span data-stu-id="d7686-111">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="d7686-112">Especifique el conjunto de Hola de dispositivos con una consulta de gemelas de dispositivo y programar toorun de trabajo de hello en el futuro.</span><span class="sxs-lookup"><span data-stu-id="d7686-112">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="d7686-113">progreso de realiza un seguimiento del trabajo de Hello como cada uno de los dispositivos de Hola recibir y ejecutar el método directo de reinicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7686-113">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="d7686-114">toolearn más información acerca de cada una de estas funciones, vea:</span><span class="sxs-lookup"><span data-stu-id="d7686-114">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="d7686-115">Gemelos de dispositivo y propiedades: [empezar a trabajar con: los gemelos de dispositivo] [ lnk-get-started-twin] y [Tutorial: cómo toouse dispositivo dos propiedades][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="d7686-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="d7686-116">Métodos directos: [Guía del desarrollador de IoT Hub: métodos directos][lnk-dev-methods] y [Tutorial: Uso de métodos directos][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="d7686-116">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: Use direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="d7686-117">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="d7686-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="d7686-118">Crear una aplicación de dispositivo que implementa un método directo denominado **lockDoor** que puede llamarse mediante aplicaciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7686-118">Create a device app that implements a direct method called **lockDoor** that can be called by hello back-end app.</span></span> <span data-ttu-id="d7686-119">aplicación de dispositivo de Hello también recibe cambios de la propiedad deseada desde aplicaciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7686-119">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="d7686-120">Crear una aplicación de back-end que crea un Hola de trabajo toocall **lockDoor** método directo en varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d7686-120">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="d7686-121">Otro trabajo envía la propiedad deseada actualiza toomultiple dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d7686-121">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="d7686-122">Al final de Hola de este tutorial, tendrá una aplicación de dispositivo de consola de Node.js y una aplicación de back-end de consola .NET (C#):</span><span class="sxs-lookup"><span data-stu-id="d7686-122">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="d7686-123">**simDevice.js** que se conecta el centro de IoT tooyour, implementa hello **lockDoor** dirigir deseado de método y controla los cambios de propiedad.</span><span class="sxs-lookup"><span data-stu-id="d7686-123">**simDevice.js** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="d7686-124">**ScheduleJob** que usa Hola de trabajos toocall **lockDoor** directo gemelas del dispositivo de hello método y actualizar las propiedades en varios dispositivos adecuadas.</span><span class="sxs-lookup"><span data-stu-id="d7686-124">**ScheduleJob** that uses jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

<span data-ttu-id="d7686-125">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="d7686-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d7686-126">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d7686-126">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="d7686-127">Node.js versión 0.12.x o posteriores.</span><span class="sxs-lookup"><span data-stu-id="d7686-127">Node.js version 0.12.x or later.</span></span> <span data-ttu-id="d7686-128">artículo de Hello [preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall Node.js para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="d7686-128">hello article [Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="d7686-129">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="d7686-129">An active Azure account.</span></span> <span data-ttu-id="d7686-130">En caso de no tener ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="d7686-130">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a><span data-ttu-id="d7686-131">Programación de trabajos para llamar a un método directo y envío de actualizaciones de dispositivo gemelo</span><span class="sxs-lookup"><span data-stu-id="d7686-131">Schedule jobs for calling a direct method and sending device twin updates</span></span>

<span data-ttu-id="d7686-132">En esta sección, creará una aplicación de consola de .NET (mediante C#) que usa Hola de toocall trabajos **lockDoor** método directo y enviar la propiedad deseada actualiza toomultiple dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d7686-132">In this section, you create a .NET console app (using C#) that uses jobs toocall hello **lockDoor** direct method and send desired property updates toomultiple devices.</span></span>

1. <span data-ttu-id="d7686-133">En Visual Studio, agregue una solución actual de toohello de proyectos de Visual C# escritorio clásico de Windows mediante el uso de hello **aplicación de consola** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="d7686-133">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="d7686-134">Proyecto de hello Name **ScheduleJob**.</span><span class="sxs-lookup"><span data-stu-id="d7686-134">Name hello project **ScheduleJob**.</span></span>

    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createapp]

1. <span data-ttu-id="d7686-136">En el Explorador de soluciones, haga clic en hello **ScheduleJob** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="d7686-136">In Solution Explorer, right-click hello **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="d7686-137">Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar**, busque **microsoft.azure.devices**, seleccione **instalar** tooinstall Hola **Microsoft.Azure.Devices** empaquetar y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="d7686-137">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="d7686-138">Este paso descarga, se instala y se agrega una referencia toohello [IoT de Azure SDK del servicio] [ lnk-nuget-service-sdk] NuGet paquete y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="d7686-138">This step downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]
1. <span data-ttu-id="d7686-140">Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:</span><span class="sxs-lookup"><span data-stu-id="d7686-140">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. <span data-ttu-id="d7686-141">Agregue los siguiente hello `using` instrucción si no están ya presentes en las instrucciones de Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d7686-141">Add hello following `using` statement if not already present in hello default statements.</span></span>

    ```csharp
    using System.Threading.Tasks;
    ```

1. <span data-ttu-id="d7686-142">Agregar Hola después campos toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="d7686-142">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="d7686-143">Reemplace el marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="d7686-143">Replace hello placeholder with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. <span data-ttu-id="d7686-144">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="d7686-144">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
    }
    ```

1. <span data-ttu-id="d7686-145">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="d7686-145">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            "deviceId='myDeviceId'",
            directMethod,
            DateTime.Now,
            10);

        Console.WriteLine("Started Method Job");
    }
    ```

1. <span data-ttu-id="d7686-146">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="d7686-146">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        var twin = new Twin();
        twin.Properties.Desired["Building"] = "43";
        twin.Properties.Desired["Floor"] = "3";
        twin.ETag = "*";

        JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
            "deviceId='myDeviceId'",
            twin,
            DateTime.Now,
            10);

        Console.WriteLine("Started Twin Update Job");
    }
    ```

1. <span data-ttu-id="d7686-147">Por último, agregue Hola después líneas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="d7686-147">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER toorun hello next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER tooexit.");
    Console.ReadLine();
    ```

1. <span data-ttu-id="d7686-148">Hola el Explorador de soluciones, abra hello **proyectos de inicio establecido...**  y asegúrese de que hello **acción** para **ScheduleJob** proyecto es **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="d7686-148">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **ScheduleJob** project is **Start**.</span></span> <span data-ttu-id="d7686-149">Compile la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7686-149">Build hello solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="d7686-150">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="d7686-150">Create a simulated device app</span></span>

<span data-ttu-id="d7686-151">En esta sección, creará una aplicación de consola de Node.js que responde tooa método directo llamado a la nube de hello, lo que desencadena un reinicio del dispositivo simulado y utiliza Hola notificado propiedades tooenable dispositivos gemelas consultas tooidentify dispositivos y cuando reinició por última vez.</span><span class="sxs-lookup"><span data-stu-id="d7686-151">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="d7686-152">Cree una nueva carpeta vacía denominada **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="d7686-152">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="d7686-153">Hola **simDevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="d7686-153">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="d7686-154">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="d7686-154">Accept all hello defaults:</span></span>

    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="d7686-155">En el símbolo del sistema en hello **simDevice** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure** y **azure-iot-dispositivo-mqtt** paquetes:</span><span class="sxs-lookup"><span data-stu-id="d7686-155">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="d7686-156">Con un editor de texto, cree un nuevo **simDevice.js** archivo Hola **simDevice** carpeta.</span><span class="sxs-lookup"><span data-stu-id="d7686-156">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>

1. <span data-ttu-id="d7686-157">Agregar siguiente hello 'requiere' instrucciones al principio de Hola de hello **simDevice.js** archivo:</span><span class="sxs-lookup"><span data-stu-id="d7686-157">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. <span data-ttu-id="d7686-158">Agregar un **connectionString** variable y utilizar toocreate un **cliente** instancia.</span><span class="sxs-lookup"><span data-stu-id="d7686-158">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="d7686-159">Asegúrese de los marcadores de posición hello tooreplace seguro con el programa de instalación de valores tooyour adecuado.</span><span class="sxs-lookup"><span data-stu-id="d7686-159">Make sure tooreplace hello placeholders with values appropriate tooyour setup.</span></span>

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="d7686-160">Agregar Hola después Hola de función toohandle **lockDoor** método.</span><span class="sxs-lookup"><span data-stu-id="d7686-160">Add hello following function toohandle hello **lockDoor** method.</span></span>

    ```nodejs
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```

1. <span data-ttu-id="d7686-161">Agregar Hola siguiente controlador de hello tooregister de código de hello **lockDoor** método.</span><span class="sxs-lookup"><span data-stu-id="d7686-161">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. <span data-ttu-id="d7686-162">Guarde y cierre hello **simDevice.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="d7686-162">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="d7686-163">tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento.</span><span class="sxs-lookup"><span data-stu-id="d7686-163">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d7686-164">En el código de producción, debe implementar directivas de reintento (por ejemplo, un retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="d7686-164">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="d7686-165">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="d7686-165">Run hello apps</span></span>

<span data-ttu-id="d7686-166">Ya estás listo toorun Hola aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d7686-166">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="d7686-167">En línea de comandos de Hola Hola **simDevice** carpeta, ejecute hello después toobegin comando realizar escuchas de método directo de reinicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7686-167">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>

    ```cmd/sh
    node simDevice.js
    ```

1. <span data-ttu-id="d7686-168">Aplicación de consola de hello ejecución C# **ScheduleJob** con el botón secundario en hello **ScheduleJob** proyecto, a continuación, seleccione **depurar** y **Iniciar nueva instancia**.</span><span class="sxs-lookup"><span data-stu-id="d7686-168">Run hello C# console app **ScheduleJob** by right-clicking on hello **ScheduleJob** project, then selecting **Debug** and **Start new instance**.</span></span>

1. <span data-ttu-id="d7686-169">Consulte la salida de hello de dispositivo y aplicaciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="d7686-169">You see hello output from both device and back-end apps.</span></span>

    ![Ejecutar aplicaciones de hello tooschedule trabajos][img-schedulejobs]

## <a name="next-steps"></a><span data-ttu-id="d7686-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d7686-171">Next steps</span></span>

<span data-ttu-id="d7686-172">En este tutorial, ha utilizado un trabajo tooschedule un dispositivo de tooa método directo y actualización de Hola de las propiedades del doble del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7686-172">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="d7686-173">toocontinue introducción con patrones de la administración de centro de IoT y el dispositivo como el remoto a través de la actualización de firmware de aire hello, leer [Tutorial: cómo toodo un firmware actualizar][lnk-fwupdate].</span><span class="sxs-lookup"><span data-stu-id="d7686-173">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, read [Tutorial: How toodo a firmware update][lnk-fwupdate].</span></span>

<span data-ttu-id="d7686-174">toocontinue Introducción a centro de IoT, consulte [introducción con borde IoT][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="d7686-174">toocontinue getting started with IoT Hub, see [Getting started with IoT Edge][lnk-iot-edge].</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
