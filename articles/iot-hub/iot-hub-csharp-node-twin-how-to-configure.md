---
title: propiedades de gemelas los dispositivos aaaUse centro de IoT de Azure (nodo/.NET) | Documentos de Microsoft
description: "Cómo los dispositivos del centro de IoT de Azure toouse gemelos tooconfigure dispositivos. Utilice hello servicio IoT de Azure SDK para .NET tooimplement una aplicación de servicio que se modifica una configuración de dispositivo mediante un doble de dispositivo y el dispositivo de hello IoT de Azure SDK para Node.js tooimplement una aplicación de dispositivo simulado."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 840a1b2e45f4763131299577583aa89015dcdd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="7feb1-104">Usar propiedades deseadas tooconfigure dispositivos</span><span class="sxs-lookup"><span data-stu-id="7feb1-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="7feb1-105">Al final de Hola de este tutorial, tendrá dos aplicaciones de consola:</span><span class="sxs-lookup"><span data-stu-id="7feb1-105">At hello end of this tutorial, you will have two console apps:</span></span>

* <span data-ttu-id="7feb1-106">**SimulateDeviceConfiguration.js**, una aplicación de dispositivo simulado que espera una actualización de la configuración deseada e informa del estado de Hola de un proceso de actualización de configuración simulada.</span><span class="sxs-lookup"><span data-stu-id="7feb1-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="7feb1-107">**SetDesiredConfigurationAndQuery**, una aplicación de back-end. NET, que establece Hola la configuración en un dispositivo deseado y consultas Hola el proceso de actualización de configuración.</span><span class="sxs-lookup"><span data-stu-id="7feb1-107">**SetDesiredConfigurationAndQuery**, a .NET back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="7feb1-108">artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que se puede usar toobuild aplicaciones de dispositivo y back-end.</span><span class="sxs-lookup"><span data-stu-id="7feb1-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="7feb1-109">toocomplete este tutorial necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="7feb1-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="7feb1-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="7feb1-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="7feb1-111">Node.js versión 0.10.x, o posteriores.</span><span class="sxs-lookup"><span data-stu-id="7feb1-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="7feb1-112">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="7feb1-112">An active Azure account.</span></span> <span data-ttu-id="7feb1-113">Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="7feb1-113">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="7feb1-114">Si ha seguido hello [empezar a trabajar con: los gemelos de dispositivo] [ lnk-twin-tutorial] tutorial, ya tiene un centro de IoT y una identidad de dispositivo llama **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="7feb1-114">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="7feb1-115">En ese caso, puede omitir toohello [aplicación de dispositivo simulado de hello crear] [ lnk-how-to-configure-createapp] sección.</span><span class="sxs-lookup"><span data-stu-id="7feb1-115">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="7feb1-116">Crear aplicación de dispositivo simulado de hello</span><span class="sxs-lookup"><span data-stu-id="7feb1-116">Create hello simulated device app</span></span>
<span data-ttu-id="7feb1-117">En esta sección, creará una aplicación de consola de Node.js que conecta el concentrador de tooyour como **myDeviceId**, espera a que una actualización de la configuración deseada y, a continuación, informa de las actualizaciones en el proceso de actualización de configuración de Hola simulada.</span><span class="sxs-lookup"><span data-stu-id="7feb1-117">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="7feb1-118">Cree una nueva carpeta vacía denominada **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="7feb1-118">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="7feb1-119">Hola **simulatedeviceconfiguration** carpeta, cree un nuevo archivo package.json mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="7feb1-119">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="7feb1-120">Acepte todos los valores predeterminados de Hola.</span><span class="sxs-lookup"><span data-stu-id="7feb1-120">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="7feb1-121">En el símbolo del sistema en hello **simulatedeviceconfiguration** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure** y **azure iot dispositivo-mqtt**paquetes:</span><span class="sxs-lookup"><span data-stu-id="7feb1-121">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="7feb1-122">Con un editor de texto, cree un nuevo **SimulateDeviceConfiguration.js** archivo Hola **simulatedeviceconfiguration** carpeta.</span><span class="sxs-lookup"><span data-stu-id="7feb1-122">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
1. <span data-ttu-id="7feb1-123">Agregar Hola después código toohello **SimulateDeviceConfiguration.js** archivo y sustituya hello **{cadena de conexión de dispositivo}** marcador de posición con la cadena de conexión de dispositivo Hola copió cuando se crea hello **myDeviceId** identidad del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="7feb1-123">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    <span data-ttu-id="7feb1-124">Hola **cliente** objeto expone métodos toointeract necesarios de hello con: los gemelos de dispositivo del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7feb1-124">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="7feb1-125">Este código inicializa hello **cliente** objeto, recupera Hola gemelas de dispositivo para **myDeviceId**y, a continuación, se adjunta un controlador de actualización de hello en *deseado propiedades*.</span><span class="sxs-lookup"><span data-stu-id="7feb1-125">This code initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and then attaches a handler for hello update on *desired properties*.</span></span> <span data-ttu-id="7feb1-126">controlador de Hello comprueba que hay es una solicitud de cambio de la configuración real mediante la comparación de hello configIds, a continuación, invoca un método que inicia el cambio de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="7feb1-126">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="7feb1-127">Tenga en cuenta que para hello simplificar, este código usa el valor predeterminado codificado de forma rígida para la configuración inicial de Hola.</span><span class="sxs-lookup"><span data-stu-id="7feb1-127">Note that for hello sake of simplicity, this code uses a hard-coded default for hello initial configuration.</span></span> <span data-ttu-id="7feb1-128">Una aplicación real probablemente cargaría esa configuración desde un almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="7feb1-128">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="7feb1-129">Los eventos de cambio de propiedad deseados siempre se emiten una vez en la conexión de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7feb1-129">Desired property change events are always emitted once at device connection.</span></span> <span data-ttu-id="7feb1-130">Asegúrese de que toocheck que hay un cambio real en hello las propiedades adecuadas antes de realizar cualquier acción.</span><span class="sxs-lookup"><span data-stu-id="7feb1-130">Make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
1. <span data-ttu-id="7feb1-131">Agregar Hola siguientes métodos antes de hello `client.open()` invocación:</span><span class="sxs-lookup"><span data-stu-id="7feb1-131">Add hello following methods before hello `client.open()` invocation:</span></span>
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    <span data-ttu-id="7feb1-132">Hola **initConfigChange** método actualizaciones Hola notificado propiedades Hola dispositivo local gemelas objeto con la configuración de hello actualizan solicitud y establece el estado de Hola demasiado**pendiente**, a continuación, Hola de actualizaciones gemelos de dispositivo en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="7feb1-132">hello **initConfigChange** method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="7feb1-133">Después de actualizar correctamente los gemelos de dispositivo de hello, simula un proceso de ejecución prolongada que finaliza en la ejecución de Hola de **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="7feb1-133">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="7feb1-134">Este método actualiza las propiedades del incluido local Hola establecer el estado de hello demasiado**correcto** y quitar hello **pendingConfig** objeto.</span><span class="sxs-lookup"><span data-stu-id="7feb1-134">This method updates hello local reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="7feb1-135">A continuación, actualiza a gemelas de dispositivo de hello en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="7feb1-135">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="7feb1-136">Tenga en cuenta que, ancho de banda toosave, indica que se actualizan propiedades especificando solo Hola propiedades toobe modificado (denominado **revisión** Hola por encima del código), en lugar de reemplazar todo el documento Hola.</span><span class="sxs-lookup"><span data-stu-id="7feb1-136">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7feb1-137">Este tutorial no simula ningún comportamiento de las actualizaciones de configuración simultáneas.</span><span class="sxs-lookup"><span data-stu-id="7feb1-137">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="7feb1-138">Algunos procesos de actualización de la configuración podrían ser capaz de tooaccommodate cambios de configuración de destino mientras se ejecuta la actualización de hello, algunas pueden disponer de tooqueue ellos así como algunos pudieron rechazar ellos con una condición de error.</span><span class="sxs-lookup"><span data-stu-id="7feb1-138">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="7feb1-139">Asegúrese de tooconsider seguro Hola comportamiento deseado para el proceso de configuración específica y cómo agregar lógica adecuada de hello antes de iniciar el cambio de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="7feb1-139">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="7feb1-140">Ejecute la aplicación de dispositivo de hello:</span><span class="sxs-lookup"><span data-stu-id="7feb1-140">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="7feb1-141">Debe aparecer un mensaje Hola `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="7feb1-141">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="7feb1-142">Mantenga la aplicación hello ejecutando.</span><span class="sxs-lookup"><span data-stu-id="7feb1-142">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="7feb1-143">Crear aplicación de servicio de hello</span><span class="sxs-lookup"><span data-stu-id="7feb1-143">Create hello service app</span></span>
<span data-ttu-id="7feb1-144">En esta sección, aprenderá a crear una aplicación de consola .NET que hello las actualizaciones *deseado propiedades* en hello dispositivo gemelas asociada **myDeviceId** con un nuevo objeto de configuración de telemetría.</span><span class="sxs-lookup"><span data-stu-id="7feb1-144">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="7feb1-145">A continuación, consulta: los gemelos de dispositivo de hello almacenados en el centro de IoT de Hola y muestra diferenciar hello en hello deseado y notifica las configuraciones de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7feb1-145">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="7feb1-146">En Visual Studio, agregue una solución actual de toohello de proyectos de Visual C# escritorio clásico de Windows mediante el uso de hello **aplicación de consola** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="7feb1-146">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="7feb1-147">Proyecto de hello Name **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="7feb1-147">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createapp]
1. <span data-ttu-id="7feb1-149">En el Explorador de soluciones, haga clic en hello **SetDesiredConfigurationAndQuery** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="7feb1-149">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="7feb1-150">Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar**, busque **microsoft.azure.devices**, seleccione **instalar** tooinstall Hola **Microsoft.Azure.Devices** empaquetar y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="7feb1-150">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="7feb1-151">Este procedimiento se descarga, se instala y se agrega una referencia toohello [IoT de Azure SDK del servicio] [ lnk-nuget-service-sdk] NuGet paquete y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="7feb1-151">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]
1. <span data-ttu-id="7feb1-153">Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:</span><span class="sxs-lookup"><span data-stu-id="7feb1-153">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="7feb1-154">Agregar Hola después campos toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="7feb1-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="7feb1-155">Sustituya el valor de marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="7feb1-155">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="7feb1-156">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="7feb1-156">Add hello following method toohello **Program** class:</span></span>
   
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
   
            try
            {
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
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
   
    <span data-ttu-id="7feb1-157">Hola **registro** objeto expone métodos toointeract necesarios de hello con: los gemelos de dispositivo del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="7feb1-157">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="7feb1-158">Este código inicializa hello **registro** objeto, recupera Hola gemelas de dispositivo para **myDeviceId**y, a continuación, actualiza sus propiedades deseados con un nuevo objeto de configuración de telemetría.</span><span class="sxs-lookup"><span data-stu-id="7feb1-158">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="7feb1-159">Después de eso, consulta: los gemelos de dispositivo de hello almacenados en el centro de IoT Hola cada 10 segundos y copias fotográficas Hola deseado y notifica las configuraciones de telemetría.</span><span class="sxs-lookup"><span data-stu-id="7feb1-159">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="7feb1-160">Consulte toohello [lenguaje de consultas del centro de IoT] [ lnk-query] toolearn cómo toogenerate enriquecido informes en todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="7feb1-160">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="7feb1-161">Esta aplicación consulta IoT Hub cada 10 segundos con fines ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="7feb1-161">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="7feb1-162">Use consultas toogenerate orientadas al usuario informes a través de varios dispositivos y no toodetect cambios.</span><span class="sxs-lookup"><span data-stu-id="7feb1-162">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="7feb1-163">Si la solución requiere notificaciones en tiempo real de eventos de dispositivo, use [notificaciones gemelas][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="7feb1-163">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="7feb1-164">Por último, agregue Hola después líneas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="7feb1-164">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="7feb1-165">Hola el Explorador de soluciones, abra hello **proyectos de inicio establecido...**  y asegúrese de que hello **acción** para **SetDesiredConfigurationAndQuery** proyecto es **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="7feb1-165">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="7feb1-166">Compile la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="7feb1-166">Build hello solution.</span></span>
1. <span data-ttu-id="7feb1-167">Con **SimulateDeviceConfiguration.js** ejecutando, ejecute la aplicación de .NET de Hola desde Visual Studio mediante **F5** y debería ver Hola notificado configuración cambia de **correcto** demasiado**pendiente** demasiado**correcto** nuevo con activo nuevo Hola enviar frecuencia de cinco minutos en lugar de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="7feb1-167">With **SimulateDeviceConfiguration.js** running, run hello .NET application from Visual Studio using **F5** and you should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Dispositivo configurado correctamente][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="7feb1-169">Hay un retraso de tooa minuto entre la operación de informe de dispositivo de Hola y el resultado de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="7feb1-169">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="7feb1-170">Se trata de tooenable Hola consulta infraestructura toowork a gran escala.</span><span class="sxs-lookup"><span data-stu-id="7feb1-170">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="7feb1-171">tooretrieve vistas coherentes de doble de un único dispositivo usan hello **getDeviceTwin** método Hola **registro** clase.</span><span class="sxs-lookup"><span data-stu-id="7feb1-171">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="7feb1-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7feb1-172">Next steps</span></span>
<span data-ttu-id="7feb1-173">En este tutorial, establezca una configuración deseada como *deseado propiedades* de solución de hello back-end y escribió una toodetect de aplicación de dispositivo que cambian y simular un proceso de actualización de varios pasos reporting su estado a través de hello notificado Propiedades.</span><span class="sxs-lookup"><span data-stu-id="7feb1-173">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="7feb1-174">Hola de uso después cómo toolearn de recursos para:</span><span class="sxs-lookup"><span data-stu-id="7feb1-174">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="7feb1-175">enviar telemetría desde dispositivos con hello [empezar a trabajar con el centro de IoT] [ lnk-iothub-getstarted] tutorial,</span><span class="sxs-lookup"><span data-stu-id="7feb1-175">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="7feb1-176">programar o realizar operaciones en conjuntos grandes de dispositivos Consulte hello [programación y los trabajos de difusión] [ lnk-schedule-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="7feb1-176">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="7feb1-177">controlar los dispositivos de forma interactiva (por ejemplo, al activar un ventilador desde una aplicación controlada por el usuario), con hello [usar métodos directos] [ lnk-methods-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="7feb1-177">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app
