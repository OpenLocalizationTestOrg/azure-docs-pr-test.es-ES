---
title: Uso de las propiedades de dispositivos gemelos de IoT Hub de Azure | Microsoft Docs
description: "En este artículo se describe cómo usar los dispositivos gemelos de IoT Hub de Azure para configurar dispositivos. Los SDK de IoT de Azure para Node.js se utilizan para implementar una aplicación de dispositivo simulado y una aplicación de servicio que modifica una configuración de dispositivo mediante un dispositivo gemelo."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 771106ce7b00a5231d9929e4b5ea34aefe693597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-desired-properties-to-configure-devices-node"></a><span data-ttu-id="cd6a2-104">Uso de las propiedades deseadas para configurar dispositivos (Node)</span><span class="sxs-lookup"><span data-stu-id="cd6a2-104">Use desired properties to configure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="cd6a2-105">Al final de este tutorial tendrá dos aplicaciones de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="cd6a2-105">At the end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="cd6a2-106">**SimulateDeviceConfiguration.js**, una aplicación de dispositivo simulado que espera por una actualización de la configuración deseada y notifica el estado de un proceso de actualización de configuración simulada.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="cd6a2-107">**SetDesiredConfigurationAndQuery.js**, una aplicación Node.js diseñada para ejecutarse desde el back-end, que establece la configuración deseada en un dispositivo y consulta el proceso de actualización de la configuración.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="cd6a2-108">En el artículo [SDK de IoT de Azure][lnk-hub-sdks] se proporciona información sobre los SDK que puede usar para crear aplicaciones de dispositivo y de back-end.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="cd6a2-109">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cd6a2-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="cd6a2-110">Node.js versión 0.10.x o posteriores.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="cd6a2-111">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-111">An active Azure account.</span></span> <span data-ttu-id="cd6a2-112">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="cd6a2-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="cd6a2-113">Si ha seguido el tutorial [Introducción a los dispositivos gemelos][lnk-twin-tutorial], ya tiene un centro de IoT y una identidad de dispositivo denominada **myDeviceId**; y puede ir directamente a la sección [Creación de la aplicación de dispositivo simulado][lnk-how-to-configure-createapp] .</span><span class="sxs-lookup"><span data-stu-id="cd6a2-113">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-simulated-device-app"></a><span data-ttu-id="cd6a2-114">Creación de la aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="cd6a2-114">Create the simulated device app</span></span>
<span data-ttu-id="cd6a2-115">En esta sección, creará una aplicación de consola de Node.js que se conecta a su centro como **myDeviceId**, espera por una actualización de la configuración deseada y, a continuación, informa de las actualizaciones en el proceso de actualización de configuración simulada.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-115">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="cd6a2-116">Cree una nueva carpeta vacía denominada **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="cd6a2-117">En la carpeta **simulatedeviceconfiguration** , cree un nuevo archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-117">In the **simulatedeviceconfiguration** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="cd6a2-118">Acepte todos los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="cd6a2-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="cd6a2-119">En el símbolo del sistema, en la carpeta **simulatedeviceconfiguration**, ejecute el siguiente comando para instalar **azure-iot-device** y el paquete **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="cd6a2-119">At your command prompt in the **simulatedeviceconfiguration** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="cd6a2-120">Con un editor de texto, cree un nuevo archivo **SimulateDeviceConfiguration.js** en la carpeta **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in the **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="cd6a2-121">Agregue el código siguiente al archivo **SimulateDeviceConfiguration.js** y sustituya el marcador de posición **{device connection string}** con la cadena de conexión del dispositivo que copió al crear la identidad de dispositivo **myDeviceId**:</span><span class="sxs-lookup"><span data-stu-id="cd6a2-121">Add the following code to the **SimulateDeviceConfiguration.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="cd6a2-122">El objeto **Cliente** expone todos los métodos necesarios para interactuar con dispositivos gemelos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-122">The **Client** object exposes all the methods required to interact with device twins from the device.</span></span> <span data-ttu-id="cd6a2-123">El código anterior, una vez que inicialice el objeto **Cliente**, recupera el dispositivo gemelo de **myDeviceId**, y adjunta un controlador para la actualización en las propiedades deseadas.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-123">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId**, and attaches a handler for the update on desired properties.</span></span> <span data-ttu-id="cd6a2-124">El controlador comprueba que hay una solicitud real de cambio de la configuración comparando los configId, y a continuación, invoca un método que inicia el cambio de configuración.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-124">The handler verifies that there is an actual configuration change request by comparing the configIds, then invokes a method that starts the configuration change.</span></span>
   
    <span data-ttu-id="cd6a2-125">Tenga en cuenta que, por simplicidad, el código anterior usa un valor predeterminado codificado de forma rígida para la configuración inicial.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-125">Note that for the sake of simplicity, the previous code uses a hard-coded default for the inital configuration.</span></span> <span data-ttu-id="cd6a2-126">Una aplicación real probablemente cargaría esa configuración desde un almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="cd6a2-127">Los eventos de cambio de propiedad deseados siempre se emiten una vez en la conexión del dispositivo, no olvide comprobar que hay un cambio real en las propiedades deseadas antes de realizar cualquier acción.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-127">Desired property change events are always emitted once at device connection, make sure to check that there is an actual change in the desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="cd6a2-128">Agregue los métodos siguientes antes de la invocación `client.open()`:</span><span class="sxs-lookup"><span data-stu-id="cd6a2-128">Add the following methods before the `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="cd6a2-129">El método **initConfigChange** actualiza propiedades notificadas en el objeto del dispositivo gemelo local con la solicitud de actualización de la configuración y establece el estado en **Pendiente**, a continuación, actualiza el dispositivo gemelo en el servicio.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-129">The **initConfigChange** method updates reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="cd6a2-130">Después de actualizar correctamente el dispositivo gemelo, simula un proceso de ejecución prolongada que finaliza en la ejecución de **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-130">After successfully updating the device twin, it simulates a long running process that terminates in the execution of **completeConfigChange**.</span></span> <span data-ttu-id="cd6a2-131">Este método actualiza las propiedades notificadas del dispositivo gemelo local estableciendo el estado en **Correcto** y eliminado el objeto **pendingConfig**.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-131">This method updates the local device twin's reported properties setting the status to **Success** and removing the **pendingConfig** object.</span></span> <span data-ttu-id="cd6a2-132">A continuación, actualiza el dispositivo gemelo en el servicio.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-132">It then updates the device twin on the service.</span></span>
   
    <span data-ttu-id="cd6a2-133">Tenga en cuenta que, para ahorrar ancho de banda, las propiedades notificadas se actualizan especificando solo las propiedades que se van a modificar (denominadas **revisión** en el código anterior), en lugar de reemplazar el documento completo.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-133">Note that, to save bandwidth, reported properties are updated by specifying only the properties to be modified (named **patch** in the above code), instead of replacing the whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cd6a2-134">Este tutorial no simula ningún comportamiento de las actualizaciones de configuración simultáneas.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="cd6a2-135">Algunos procesos de actualización de configuración pueden dar cabida a cambios de configuración de destino mientras se está ejecutando la actualización, otros tienen que ponerlos en cola, y otros podrían rechazarlos con una condición de error.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-135">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, others might have to queue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="cd6a2-136">Asegúrese de que considera el comportamiento deseado para el proceso de configuración específica y agregue la lógica adecuada antes de iniciar el cambio de configuración.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-136">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="cd6a2-137">Ejecute la aplicación del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="cd6a2-137">Run the device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="cd6a2-138">Verá el mensaje `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-138">You should see the message `retrieved device twin`.</span></span> <span data-ttu-id="cd6a2-139">Mantenga la aplicación en ejecución.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-139">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="cd6a2-140">Creación de la aplicación de servicio</span><span class="sxs-lookup"><span data-stu-id="cd6a2-140">Create the service app</span></span>
<span data-ttu-id="cd6a2-141">En esta sección, creará una aplicación de consola de Node.js que actualiza las *propiedades deseadas* en el dispositivo gemelo asociado con **myDeviceId** con un nuevo objeto de configuración de telemetría.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-141">In this section, you will create a Node.js console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="cd6a2-142">A continuación, consulta a los dispositivos gemelos almacenados en el centro de IoT y muestra la diferencia entre las configuraciones deseada y notificada del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-142">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="cd6a2-143">Cree una nueva carpeta vacía denominada **setdesiredandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="cd6a2-144">En la carpeta **setdesiredandqueryapp** , cree un nuevo archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-144">In the **setdesiredandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="cd6a2-145">Acepte todos los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="cd6a2-145">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="cd6a2-146">En el símbolo del sistema, en la carpeta **setdesiredandqueryapp**, ejecute el siguiente comando para instalar el paquete **azure-iothub**:</span><span class="sxs-lookup"><span data-stu-id="cd6a2-146">At your command prompt in the **setdesiredandqueryapp** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="cd6a2-147">Con un editor de texto, cree un nuevo archivo **SetDesiredAndQuery.js** en la carpeta **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in the **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="cd6a2-148">Agregue el código siguiente al archivo **SetDesiredAndQuery.js** y sustituya el marcador de posición **{iot hub connection string}** con la cadena de conexión de IoT Hub que copió al crear su centro:</span><span class="sxs-lookup"><span data-stu-id="cd6a2-148">Add the following code to the **SetDesiredAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    <span data-ttu-id="cd6a2-149">El objeto **Registro** expone todos los métodos necesarios para interactuar con dispositivos gemelos del servicio.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-149">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="cd6a2-150">El código anterior, una vez que inicialice el objeto **Registro**, recupera el dispositivo gemelo de **myDeviceId**, y actualiza sus propiedades deseadas con un nuevo objeto de configuración de telemetría.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-150">The previous code, after it initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="cd6a2-151">Después de esto, llama a la función **queryTwins** cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-151">After that, it calls the **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="cd6a2-152">Esta aplicación consulta IoT Hub cada 10 segundos con fines ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="cd6a2-153">Use consultas para generar informes de cara al usuario en muchos dispositivos y no para detectar cambios.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-153">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="cd6a2-154">Si la solución requiere notificaciones en tiempo real de eventos de dispositivo, use [notificaciones gemelas][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="cd6a2-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="cd6a2-155">.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-155">.</span></span>

1. <span data-ttu-id="cd6a2-156">Agregue el siguiente código justo antes de la invocación `registry.getDeviceTwin()` para implementar la función **queryTwins**:</span><span class="sxs-lookup"><span data-stu-id="cd6a2-156">Add the following code right before the `registry.getDeviceTwin()` invocation to implement the **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    <span data-ttu-id="cd6a2-157">El código anterior consulta los dispositivos gemelos almacenados en el centro de IoT e imprime las configuraciones de telemetría deseadas y notificadas.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-157">The previous code queries the device twins stored in the IoT hub and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="cd6a2-158">Consulte el [lenguaje de consulta de IoT Hub][lnk-query] para obtener información sobre cómo generar informes completos en todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-158">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
2. <span data-ttu-id="cd6a2-159">Con **SimulateDeviceConfiguration.js** en ejecución, ejecute la aplicación con:</span><span class="sxs-lookup"><span data-stu-id="cd6a2-159">With **SimulateDeviceConfiguration.js** running, run the application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="cd6a2-160">Debería ver como la configuración notificada cambia de **Correcto** a **Pendiente** a **Correcto** de nuevo con la nueva frecuencia de envío activa de cinco minutos en lugar de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-160">You should see the reported configuration change from **Success** to **Pending** to **Success** again with the new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="cd6a2-161">Hay un retraso de hasta un minuto entre la operación de informe de dispositivo y el resultado de la consulta.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-161">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="cd6a2-162">Esto es para habilitar la infraestructura de consulta para que funcione a gran escala.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-162">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="cd6a2-163">Para recuperar vistas coherentes de un único dispositivo gemelo, use el método **getDeviceTwin** en la clase **Registro**.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-163">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="cd6a2-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cd6a2-164">Next steps</span></span>
<span data-ttu-id="cd6a2-165">En este tutorial, ha establecido una configuración deseada como *propiedades deseadas* desde una aplicación back-end, y ha escrito una aplicación de dispositivo simulado para detectar ese cambio y simular un proceso de actualización de varios pasos que informe de su estado como *propiedades notificadas* para el dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="cd6a2-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app to detect that change and simulate a multi-step update process reporting its status as *reported properties* to the device twin.</span></span>

<span data-ttu-id="cd6a2-166">Use los siguientes recursos para obtener información sobre cómo:</span><span class="sxs-lookup"><span data-stu-id="cd6a2-166">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="cd6a2-167">enviar telemetría desde dispositivos con el tutorial [Introducción a IoT Hub][lnk-iothub-getstarted];</span><span class="sxs-lookup"><span data-stu-id="cd6a2-167">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="cd6a2-168">programar o realizar operaciones en grandes conjuntos de dispositivos (consulte el tutorial [Schedule and broadcast jobs][lnk-schedule-jobs] [Programación y difusión de trabajos]);</span><span class="sxs-lookup"><span data-stu-id="cd6a2-168">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="cd6a2-169">controlar los dispositivos de forma interactiva (por ejemplo, encender un ventilador desde una aplicación controlada por el usuario), con el tutorial [Uso de métodos directos][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="cd6a2-169">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

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
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
