---
title: "actualización de firmware de aaaDevice con el centro de IoT de Azure (nodo/.NET) | Documentos de Microsoft"
description: "Cómo actualizar toouse la administración de dispositivos en el centro de IoT de Azure tooinitiate un firmware del dispositivo. Utilice hello servicio IoT de Azure SDK para .NET tooimplement una aplicación de servicio que desencadena la actualización de firmware de Hola y dispositivo de hello IoT de Azure SDK para Node.js tooimplement una aplicación de dispositivo simulado."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: d48899651bcd5d67e577c971be0f9453c8f21592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a><span data-ttu-id="80b0e-104">Use Administración de dispositivo tooinitiate una actualización de firmware del dispositivo (o nodo de. NET)</span><span class="sxs-lookup"><span data-stu-id="80b0e-104">Use device management tooinitiate a device firmware update (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="80b0e-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="80b0e-105">Introduction</span></span>
<span data-ttu-id="80b0e-106">Hola [empezar a trabajar con la administración de dispositivos] [ lnk-dm-getstarted] tutorial, ha visto cómo hello toouse [gemelas dispositivo] [ lnk-devtwin] y [directo métodos] [ lnk-c2dmethod] tooremotely primitivas reiniciar un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="80b0e-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="80b0e-107">Este tutorial se utiliza Hola mismos tipos primitivos de centro de IoT y muestra cómo toodo un extremo a otro simula la actualización de firmware.</span><span class="sxs-lookup"><span data-stu-id="80b0e-107">This tutorial uses hello same IoT Hub primitives and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="80b0e-108">Este patrón se utiliza en la implementación de actualización de firmware de Hola para hello [ejemplo de implementación de dispositivo de frambuesa Pi][lnk-rpi-implementation].</span><span class="sxs-lookup"><span data-stu-id="80b0e-108">This pattern is used in hello firmware update implementation for hello [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span></span>

<span data-ttu-id="80b0e-109">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="80b0e-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="80b0e-110">Crear una aplicación de consola .NET que llama a métodos directas de hello firmwareUpdate en aplicación del dispositivo simulado de hello a través de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="80b0e-110">Create a .NET console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="80b0e-111">Cree una aplicación de dispositivo simulado que implemente un método directo **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="80b0e-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="80b0e-112">Este método inicia un proceso de varias fase que espera a que la imagen de firmware de hello toodownload, descarga la imagen de firmware de Hola y por último, se aplica la imagen de firmware Hola.</span><span class="sxs-lookup"><span data-stu-id="80b0e-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="80b0e-113">Durante cada fase de actualización de hello, Hola dispositivo usa Hola notifica propiedades tooreport en progreso.</span><span class="sxs-lookup"><span data-stu-id="80b0e-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="80b0e-114">Al final de Hola de este tutorial, tendrá una aplicación de dispositivo de consola de Node.js y una aplicación de back-end de consola .NET (C#):</span><span class="sxs-lookup"><span data-stu-id="80b0e-114">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="80b0e-115">**dmpatterns_fwupdate_service.js**, que llama a un método directo en la aplicación de dispositivo simulado de hello, muestra la respuesta de Hola y periódicamente (cada 500 ms) hello muestra actualizado notificado propiedades.</span><span class="sxs-lookup"><span data-stu-id="80b0e-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="80b0e-116">**TriggerFWUpdate**, centro de IoT tooyour que conecta con la identidad del dispositivo Hola creado anteriormente, recibe un método directo firmwareUpdate, se ejecuta a través de un proceso de varios Estados toosimulate un incluidos de actualización de firmware: espera de descarga de la imagen de hello, Descargar la nueva imagen de Hola y finalmente Aplicar imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="80b0e-116">**TriggerFWUpdate**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="80b0e-117">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="80b0e-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="80b0e-118">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="80b0e-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="80b0e-119">Node.js versión 0.12.x o posteriores.</span><span class="sxs-lookup"><span data-stu-id="80b0e-119">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="80b0e-120">[Preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall Node.js para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="80b0e-120">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="80b0e-121">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="80b0e-121">An active Azure account.</span></span> <span data-ttu-id="80b0e-122">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="80b0e-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="80b0e-123">Siga hello [empezar a trabajar con la administración de dispositivos](iot-hub-csharp-node-device-management-get-started.md) artículo toocreate su centro de IoT y obtener la cadena de conexión de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="80b0e-123">Follow hello [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="80b0e-124">Desencadenar una actualización de firmware remoto en dispositivo Hola utilizando un método directo</span><span class="sxs-lookup"><span data-stu-id="80b0e-124">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="80b0e-125">En esta sección, creará una aplicación de consola de .NET (mediante C#) que inicia una actualización de firmware remota en un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="80b0e-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="80b0e-126">aplicación Hello usa una actualización de hello tooinitiate método directo y usa dispositivos gemelas consultas tooperiodically obtener estado de Hola de actualización de firmware active Hola.</span><span class="sxs-lookup"><span data-stu-id="80b0e-126">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="80b0e-127">En Visual Studio, agregue una solución actual de toohello de proyectos de Visual C# escritorio clásico de Windows mediante el uso de hello **aplicación de consola** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="80b0e-127">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="80b0e-128">Proyecto de hello Name **TriggerFWUpdate**.</span><span class="sxs-lookup"><span data-stu-id="80b0e-128">Name hello project **TriggerFWUpdate**.</span></span>

    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createapp]

1. <span data-ttu-id="80b0e-130">En el Explorador de soluciones, haga clic en hello **TriggerFWUpdate** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="80b0e-130">In Solution Explorer, right-click hello **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="80b0e-131">Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar**, busque **microsoft.azure.devices**, seleccione **instalar** tooinstall Hola **Microsoft.Azure.Devices** empaquetar y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="80b0e-131">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="80b0e-132">Este procedimiento se descarga, se instala y se agrega una referencia toohello [IoT de Azure SDK del servicio] [ lnk-nuget-service-sdk] NuGet paquete y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="80b0e-132">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]
1. <span data-ttu-id="80b0e-134">Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:</span><span class="sxs-lookup"><span data-stu-id="80b0e-134">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. <span data-ttu-id="80b0e-135">Agregar Hola después campos toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="80b0e-135">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="80b0e-136">Reemplace Hola Hola de varios valores de marcador de posición con cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola y Hola Id. del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="80b0e-136">Replace hello multiple placeholder values with hello IoT Hub connection string for hello hub that you created in hello previous section and hello Id of your device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. <span data-ttu-id="80b0e-137">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="80b0e-137">Add hello following method toohello **Program** class:</span></span>
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. <span data-ttu-id="80b0e-138">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="80b0e-138">Add hello following method toohello **Program** class:</span></span>

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. <span data-ttu-id="80b0e-139">Por último, agregue Hola después líneas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="80b0e-139">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. <span data-ttu-id="80b0e-140">Hola el Explorador de soluciones, abra hello **proyectos de inicio establecido...**  y asegúrese de que hello **acción** para **TriggerFWUpdate** proyecto es **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="80b0e-140">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **TriggerFWUpdate** project is **Start**.</span></span>

1. <span data-ttu-id="80b0e-141">Compile la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="80b0e-141">Build hello solution.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="80b0e-142">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="80b0e-142">Run hello apps</span></span>
<span data-ttu-id="80b0e-143">Ya estás listo toorun Hola aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="80b0e-143">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="80b0e-144">En línea de comandos de Hola Hola **manageddevice** carpeta, ejecute hello después toobegin comando realizar escuchas de método directo de reinicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="80b0e-144">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="80b0e-145">En Visual Studio, haga doble clic en hello **TriggerFWUpdate** aplicación de consola de toohello C# projectRun, seleccione **depurar** y **Iniciar nueva instancia**.</span><span class="sxs-lookup"><span data-stu-id="80b0e-145">In Visual Studio, right-click on hello **TriggerFWUpdate** projectRun toohello C# console app, select **Debug** and **Start new instance**.</span></span>

3. <span data-ttu-id="80b0e-146">Consulte dispositivo respuesta toohello directo método hello en la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="80b0e-146">You see hello device response toohello direct method in hello console.</span></span>

    ![Firmware actualizado correctamente][img-fwupdate]

## <a name="next-steps"></a><span data-ttu-id="80b0e-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="80b0e-148">Next steps</span></span>
<span data-ttu-id="80b0e-149">En este tutorial, ha utilizado un tootrigger método directo un control remoto actualización de firmware en un dispositivo y Hola usado informó sobre el progreso de hello toofollow de propiedades de actualización de firmware de Hola.</span><span class="sxs-lookup"><span data-stu-id="80b0e-149">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="80b0e-150">toolearn cómo tooextend llama a su método de programación y de solución de IoT en varios dispositivos, vea hello [programación y los trabajos de difusión] [ lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="80b0e-150">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/