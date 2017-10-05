---
title: "Actualización de firmware de dispositivos con IoT Hub de Azure | Microsoft Docs"
description: "Describe cómo usar la administración de dispositivos en IoT Hub de Azure para iniciar una actualización de firmware del dispositivo. Usará el SDK de dispositivo IoT de Azure para Node.js con el fin de implementar una aplicación de dispositivo simulado, además del SDK de servicio IoT de Azure para .NET con el objetivo de implementar una aplicación de servicio que desencadena la actualización el firmware."
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
ms.openlocfilehash: c2192328a152e955d182c4a07b391c98a5960964
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-netnode"></a><span data-ttu-id="d14e6-104">Use la administración de dispositivos para iniciar una actualización de firmware del dispositivo (. NET y Node)</span><span class="sxs-lookup"><span data-stu-id="d14e6-104">Use device management to initiate a device firmware update (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="d14e6-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="d14e6-105">Introduction</span></span>
<span data-ttu-id="d14e6-106">En el tutorial de [Introducción a la administración de dispositivos][lnk-dm-getstarted], vimos cómo usar los primitivos de [dispositivo gemelo][lnk-devtwin] y [métodos directos][lnk-c2dmethod] para reiniciar de forma remota un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d14e6-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="d14e6-107">Este tutorial emplea los mismos tipos primitivos de IoT Hub. Además, proporciona orientación y muestra cómo realizar una actualización de firmware simulada de extremo a extremo.</span><span class="sxs-lookup"><span data-stu-id="d14e6-107">This tutorial uses the same IoT Hub primitives and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="d14e6-108">Este patrón se usa en la implementación de actualizaciones de firmware del [ejemplo de implementación de dispositivos Raspberry Pi][lnk-rpi-implementation].</span><span class="sxs-lookup"><span data-stu-id="d14e6-108">This pattern is used in the firmware update implementation for the [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span></span>

<span data-ttu-id="d14e6-109">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="d14e6-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="d14e6-110">Crear una aplicación de consola de .NET que llame al método directo firmwareUpdate en la aplicación de dispositivo simulado a través de su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d14e6-110">Create a .NET console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="d14e6-111">Cree una aplicación de dispositivo simulado que implemente un método directo **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="d14e6-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="d14e6-112">Este método inicia un proceso de varias fases que espera para descargar la imagen de firmware, la descarga y, por último, la aplica.</span><span class="sxs-lookup"><span data-stu-id="d14e6-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="d14e6-113">Durante cada fase de la actualización, el dispositivo usa las propiedades notificadas para informar sobre el progreso.</span><span class="sxs-lookup"><span data-stu-id="d14e6-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="d14e6-114">Al final de este tutorial, tendrá una aplicación de dispositivo de consola de Node.js y una aplicación back-end de consola .NET (C#):</span><span class="sxs-lookup"><span data-stu-id="d14e6-114">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="d14e6-115">**dmpatterns_fwupdate_service.js**, que llama a un método directo en la aplicación de dispositivo simulado, muestra la respuesta y muestra periódicamente (cada 500 ms) las propiedades notificadas actualizadas.</span><span class="sxs-lookup"><span data-stu-id="d14e6-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="d14e6-116">**TriggerFWUpdate**, que se conecta a IoT Hub con la identidad del dispositivo creada anteriormente, recibe un método directo firmwareUpdate y se ejecuta mediante un proceso de varios estados para simular una actualización de firmware; entre ellas, la espera para la descarga de imágenes, la descarga de la nueva imagen y, finalmente, la aplicación de dicha imagen.</span><span class="sxs-lookup"><span data-stu-id="d14e6-116">**TriggerFWUpdate**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="d14e6-117">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d14e6-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="d14e6-118">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d14e6-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="d14e6-119">Node.js versión 0.12.x o posteriores.</span><span class="sxs-lookup"><span data-stu-id="d14e6-119">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="d14e6-120">En [Preparación del entorno de desarrollo][lnk-dev-setup] se describe cómo instalar Node.js para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="d14e6-120">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="d14e6-121">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="d14e6-121">An active Azure account.</span></span> <span data-ttu-id="d14e6-122">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="d14e6-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="d14e6-123">Siga los pasos del artículo de [introducción a la administración de dispositivos](iot-hub-csharp-node-device-management-get-started.md) para crear su instancia de IoT Hub y obtener la cadena de conexión de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d14e6-123">Follow the [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="d14e6-124">Desencadenamiento de una actualización de firmware remota en el dispositivo con un método directo</span><span class="sxs-lookup"><span data-stu-id="d14e6-124">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="d14e6-125">En esta sección, creará una aplicación de consola de .NET (mediante C#) que inicia una actualización de firmware remota en un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d14e6-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="d14e6-126">La aplicación usa un método directo para iniciar la actualización y utiliza consultas de dispositivos gemelos para obtener periódicamente el estado de la actualización del firmware activa.</span><span class="sxs-lookup"><span data-stu-id="d14e6-126">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="d14e6-127">En Visual Studio, agregue un proyecto de escritorio clásico de Windows de Visual C# a la solución actual mediante la plantilla de proyecto **Aplicación de consola** .</span><span class="sxs-lookup"><span data-stu-id="d14e6-127">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="d14e6-128">Asigne al proyecto el nombre **TriggerFWUpdate**.</span><span class="sxs-lookup"><span data-stu-id="d14e6-128">Name the project **TriggerFWUpdate**.</span></span>

    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createapp]

1. <span data-ttu-id="d14e6-130">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **TriggerFWUpdate** y luego seleccione **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d14e6-130">In Solution Explorer, right-click the **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="d14e6-131">En la ventana **Administrador de paquetes NuGet**, seleccione **Examinar**, busque **microsoft.azure.devices**, seleccione **Instalar** para instalar el paquete **Microsoft.Azure.Devices** y acepte los términos de uso.</span><span class="sxs-lookup"><span data-stu-id="d14e6-131">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="d14e6-132">Este procedimiento permite descargar, instalar y agregar una referencia al [paquete NuGet del SDK de dispositivo de IoT de Azure][lnk-nuget-service-sdk] y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="d14e6-132">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]
1. <span data-ttu-id="d14e6-134">Agregue las siguientes instrucciones `using` al principio del archivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="d14e6-134">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. <span data-ttu-id="d14e6-135">Agregue los campos siguientes a la clase **Program** .</span><span class="sxs-lookup"><span data-stu-id="d14e6-135">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="d14e6-136">Sustituya los valores de varios marcadores de posición por la cadena de conexión de IoT Hub que creó en la sección anterior y por el identificador del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d14e6-136">Replace the multiple placeholder values with the IoT Hub connection string for the hub that you created in the previous section and the Id of your device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. <span data-ttu-id="d14e6-137">Agregue el método siguiente a la clase **Program** :</span><span class="sxs-lookup"><span data-stu-id="d14e6-137">Add the following method to the **Program** class:</span></span>
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. <span data-ttu-id="d14e6-138">Agregue el método siguiente a la clase **Program** :</span><span class="sxs-lookup"><span data-stu-id="d14e6-138">Add the following method to the **Program** class:</span></span>

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

1. <span data-ttu-id="d14e6-139">Por último, agregue las líneas siguientes al método **Main** :</span><span class="sxs-lookup"><span data-stu-id="d14e6-139">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
1. <span data-ttu-id="d14e6-140">En el Explorador de soluciones, abra **Establecer proyectos de inicio...** y asegúrese de que la **acción** de **TriggerFWUpdate** sea **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="d14e6-140">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **TriggerFWUpdate** project is **Start**.</span></span>

1. <span data-ttu-id="d14e6-141">Compile la solución.</span><span class="sxs-lookup"><span data-stu-id="d14e6-141">Build the solution.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="d14e6-142">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d14e6-142">Run the apps</span></span>
<span data-ttu-id="d14e6-143">Ya está preparado para ejecutar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d14e6-143">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="d14e6-144">En el símbolo del sistema dentro de la carpeta **manageddevice**, ejecute el siguiente comando para iniciar la escucha del método directo de reinicio.</span><span class="sxs-lookup"><span data-stu-id="d14e6-144">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="d14e6-145">En Visual Studio, haga clic con el botón derecho en el proyecto **TriggerFWUpdate**, ejecute la aplicación de consola de C# y seleccione **Depurar** e **Iniciar nueva instancia**.</span><span class="sxs-lookup"><span data-stu-id="d14e6-145">In Visual Studio, right-click on the **TriggerFWUpdate** projectRun to the C# console app, select **Debug** and **Start new instance**.</span></span>

3. <span data-ttu-id="d14e6-146">Verá la respuesta del dispositivo al método directo en la consola.</span><span class="sxs-lookup"><span data-stu-id="d14e6-146">You see the device response to the direct method in the console.</span></span>

    ![Firmware actualizado correctamente][img-fwupdate]

## <a name="next-steps"></a><span data-ttu-id="d14e6-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d14e6-148">Next steps</span></span>
<span data-ttu-id="d14e6-149">En este tutorial, ha usado un método directo para desencadenar una actualización de firmware remota en un dispositivo y ha utilizado las propiedades notificadas para entender el progreso del proceso de actualización del firmware.</span><span class="sxs-lookup"><span data-stu-id="d14e6-149">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="d14e6-150">Para información sobre cómo ampliar la solución de IoT y programar llamadas de método en varios dispositivos, consulte el tutorial [Programación de trabajos en varios dispositivos][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="d14e6-150">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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