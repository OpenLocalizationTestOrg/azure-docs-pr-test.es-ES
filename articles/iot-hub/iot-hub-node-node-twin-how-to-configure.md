---
title: propiedades gemelas (nodo) del dispositivo de centro de IoT de Azure de aaaUse | Documentos de Microsoft
description: "Cómo los dispositivos del centro de IoT de Azure toouse gemelos tooconfigure dispositivos. Utilice hello Azure IoT SDK para Node.js tooimplement una aplicación de dispositivo simulado y una aplicación de servicio que modifica una configuración de dispositivo mediante un doble de dispositivo."
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
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a><span data-ttu-id="7835c-104">Dispositivos de tooconfigure de propiedades de uso deseado (nodo)</span><span class="sxs-lookup"><span data-stu-id="7835c-104">Use desired properties tooconfigure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="7835c-105">Al final de Hola de este tutorial, tendrá dos aplicaciones de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="7835c-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="7835c-106">**SimulateDeviceConfiguration.js**, una aplicación de dispositivo simulado que espera una actualización de la configuración deseada e informa del estado de Hola de un proceso de actualización de configuración simulada.</span><span class="sxs-lookup"><span data-stu-id="7835c-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="7835c-107">**SetDesiredConfigurationAndQuery.js**, una aplicación de back-end de Node.js, que establece Hola la configuración en un dispositivo deseado y consultas Hola el proceso de actualización de configuración.</span><span class="sxs-lookup"><span data-stu-id="7835c-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="7835c-108">artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que se puede usar toobuild aplicaciones de dispositivo y back-end.</span><span class="sxs-lookup"><span data-stu-id="7835c-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="7835c-109">toocomplete este tutorial necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="7835c-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="7835c-110">Node.js versión 0.10.x, o posteriores.</span><span class="sxs-lookup"><span data-stu-id="7835c-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="7835c-111">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="7835c-111">An active Azure account.</span></span> <span data-ttu-id="7835c-112">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="7835c-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="7835c-113">Si ha seguido hello [empezar a trabajar con: los gemelos de dispositivo] [ lnk-twin-tutorial] tutorial, ya tiene un centro de IoT y una identidad de dispositivo llama **myDeviceId**; y puede omitir toohello [ Crear aplicación de dispositivo simulado de hello] [ lnk-how-to-configure-createapp] sección.</span><span class="sxs-lookup"><span data-stu-id="7835c-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="7835c-114">Crear aplicación de dispositivo simulado de hello</span><span class="sxs-lookup"><span data-stu-id="7835c-114">Create hello simulated device app</span></span>
<span data-ttu-id="7835c-115">En esta sección, creará una aplicación de consola de Node.js que conecta el concentrador de tooyour como **myDeviceId**, espera a que una actualización de la configuración deseada y, a continuación, informa de las actualizaciones en el proceso de actualización de configuración de Hola simulada.</span><span class="sxs-lookup"><span data-stu-id="7835c-115">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="7835c-116">Cree una nueva carpeta vacía denominada **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="7835c-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="7835c-117">Hola **simulatedeviceconfiguration** carpeta, cree un nuevo archivo package.json mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="7835c-117">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="7835c-118">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="7835c-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="7835c-119">En el símbolo del sistema en hello **simulatedeviceconfiguration** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure**, y **azure iot dispositivo-mqtt**paquete:</span><span class="sxs-lookup"><span data-stu-id="7835c-119">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="7835c-120">Con un editor de texto, cree un nuevo **SimulateDeviceConfiguration.js** archivo Hola **simulatedeviceconfiguration** carpeta.</span><span class="sxs-lookup"><span data-stu-id="7835c-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="7835c-121">Agregar Hola después código toohello **SimulateDeviceConfiguration.js** archivo y sustituya hello **{cadena de conexión de dispositivo}** marcador de posición con la cadena de conexión de dispositivo Hola copió cuando se crea hello **myDeviceId** identidad del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="7835c-121">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="7835c-122">Hola **cliente** objeto expone métodos toointeract necesarios de hello con: los gemelos de dispositivo del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7835c-122">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="7835c-123">Hola código anterior, una vez que inicialice hello **cliente** objeto, recupera Hola gemelas de dispositivo para **myDeviceId**y asocia un controlador de actualización de hello en propiedades que desee.</span><span class="sxs-lookup"><span data-stu-id="7835c-123">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and attaches a handler for hello update on desired properties.</span></span> <span data-ttu-id="7835c-124">controlador de Hello comprueba que hay es una solicitud de cambio de la configuración real mediante la comparación de hello configIds, a continuación, invoca un método que inicia el cambio de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="7835c-124">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="7835c-125">Tenga en cuenta que para hello simplificar, código anterior hello usa el valor predeterminado codificado de forma rígida para la configuración inicial de Hola.</span><span class="sxs-lookup"><span data-stu-id="7835c-125">Note that for hello sake of simplicity, hello previous code uses a hard-coded default for hello inital configuration.</span></span> <span data-ttu-id="7835c-126">Una aplicación real probablemente cargaría esa configuración desde un almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="7835c-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="7835c-127">Eventos de cambio de propiedad deseada siempre se emiten una vez en la conexión del dispositivo, asegúrese de que toocheck que hay un cambio real en hello las propiedades adecuadas antes de realizar cualquier acción.</span><span class="sxs-lookup"><span data-stu-id="7835c-127">Desired property change events are always emitted once at device connection, make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="7835c-128">Agregar Hola siguientes métodos antes de hello `client.open()` invocación:</span><span class="sxs-lookup"><span data-stu-id="7835c-128">Add hello following methods before hello `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="7835c-129">Hola **initConfigChange** método actualiza notifica las propiedades en objeto de gemelas dispositivo local de hello en solicitud de actualización de configuración de Hola y conjuntos de Hola estado demasiado**pendiente**, a continuación, las actualizaciones de Hola dispositivo gemelas en servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="7835c-129">hello **initConfigChange** method updates reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="7835c-130">Después de actualizar correctamente los gemelos de dispositivo de hello, simula un proceso de ejecución prolongada que finaliza en la ejecución de Hola de **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="7835c-130">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="7835c-131">Este gemelas de dispositivo local método hello de actualizaciones del notificado propiedades establecer el estado de hello demasiado**correcto** y quitar hello **pendingConfig** objeto.</span><span class="sxs-lookup"><span data-stu-id="7835c-131">This method updates hello local device twin's reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="7835c-132">A continuación, actualiza a gemelas de dispositivo de hello en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="7835c-132">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="7835c-133">Tenga en cuenta que, ancho de banda toosave, indica que se actualizan propiedades especificando solo Hola propiedades toobe modificado (denominado **revisión** Hola por encima del código), en lugar de reemplazar todo el documento Hola.</span><span class="sxs-lookup"><span data-stu-id="7835c-133">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7835c-134">Este tutorial no simula ningún comportamiento de las actualizaciones de configuración simultáneas.</span><span class="sxs-lookup"><span data-stu-id="7835c-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="7835c-135">Algunos procesos de actualización de la configuración podrían ser capaz de tooaccommodate cambios de configuración de destino mientras se ejecuta la actualización de hello, otros podrían tener tooqueue ellos así como otros pudieron rechazar ellos con una condición de error.</span><span class="sxs-lookup"><span data-stu-id="7835c-135">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, others might have tooqueue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="7835c-136">Asegúrese de tooconsider seguro Hola comportamiento deseado para el proceso de configuración específica y cómo agregar lógica adecuada de hello antes de iniciar el cambio de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="7835c-136">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="7835c-137">Ejecute la aplicación de dispositivo de hello:</span><span class="sxs-lookup"><span data-stu-id="7835c-137">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="7835c-138">Debe aparecer un mensaje Hola `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="7835c-138">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="7835c-139">Mantenga la aplicación hello ejecutando.</span><span class="sxs-lookup"><span data-stu-id="7835c-139">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="7835c-140">Crear aplicación de servicio de hello</span><span class="sxs-lookup"><span data-stu-id="7835c-140">Create hello service app</span></span>
<span data-ttu-id="7835c-141">En esta sección, aprenderá a crear una aplicación de consola de Node.js ese Hola actualizaciones *deseado propiedades* en hello dispositivo gemelas asociada **myDeviceId** con un nuevo objeto de configuración de telemetría.</span><span class="sxs-lookup"><span data-stu-id="7835c-141">In this section, you will create a Node.js console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="7835c-142">A continuación, consulta: los gemelos de dispositivo de hello almacenados en el centro de IoT de Hola y muestra diferenciar hello en hello deseado y notifica las configuraciones de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7835c-142">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="7835c-143">Cree una nueva carpeta vacía denominada **setdesiredandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="7835c-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="7835c-144">Hola **setdesiredandqueryapp** carpeta, cree un nuevo archivo package.json mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="7835c-144">In hello **setdesiredandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="7835c-145">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="7835c-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="7835c-146">En el símbolo del sistema en hello **setdesiredandqueryapp** carpeta, ejecute hello después comando tooinstall hello **el centro de IOT de azure** paquete:</span><span class="sxs-lookup"><span data-stu-id="7835c-146">At your command prompt in hello **setdesiredandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="7835c-147">Con un editor de texto, cree un nuevo **SetDesiredAndQuery.js** archivo Hola **addtagsandqueryapp** carpeta.</span><span class="sxs-lookup"><span data-stu-id="7835c-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="7835c-148">Agregar Hola después código toohello **SetDesiredAndQuery.js** archivo y sustituya hello **{cadena de conexión de base de datos central de iot}** marcador de posición con hello copió cuando creó el centro de la cadena de conexión de centro de IoT :</span><span class="sxs-lookup"><span data-stu-id="7835c-148">Add hello following code toohello **SetDesiredAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
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

    <span data-ttu-id="7835c-149">Hola **registro** objeto expone métodos toointeract necesarios de hello con: los gemelos de dispositivo del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="7835c-149">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="7835c-150">Hola código anterior, una vez que inicialice hello **registro** objeto, recupera Hola gemelas de dispositivo para **myDeviceId**y actualiza sus propiedades deseados con un nuevo objeto de configuración de telemetría.</span><span class="sxs-lookup"><span data-stu-id="7835c-150">hello previous code, after it initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="7835c-151">Después de esto, llama hello **queryTwins** función eventos 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="7835c-151">After that, it calls hello **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7835c-152">Esta aplicación consulta IoT Hub cada 10 segundos con fines ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="7835c-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="7835c-153">Use consultas toogenerate orientadas al usuario informes a través de varios dispositivos y no toodetect cambios.</span><span class="sxs-lookup"><span data-stu-id="7835c-153">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="7835c-154">Si la solución requiere notificaciones en tiempo real de eventos de dispositivo, use [notificaciones gemelas][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="7835c-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="7835c-155">.</span><span class="sxs-lookup"><span data-stu-id="7835c-155">.</span></span>

1. <span data-ttu-id="7835c-156">Agregar Hola después el código justo antes de hello `registry.getDeviceTwin()` Hola de invocación tooimplement **queryTwins** función:</span><span class="sxs-lookup"><span data-stu-id="7835c-156">Add hello following code right before hello `registry.getDeviceTwin()` invocation tooimplement hello **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
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
   
    <span data-ttu-id="7835c-157">consultas de código anteriores Hola Hola: los gemelos de dispositivo almacenados en el centro de IoT de Hola y Hola imprime deseado y notifica las configuraciones de telemetría.</span><span class="sxs-lookup"><span data-stu-id="7835c-157">hello previous code queries hello device twins stored in hello IoT hub and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="7835c-158">Consulte toohello [lenguaje de consultas del centro de IoT] [ lnk-query] toolearn cómo toogenerate enriquecido informes en todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="7835c-158">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
2. <span data-ttu-id="7835c-159">Con **SimulateDeviceConfiguration.js** , ejecutar la aplicación hello con:</span><span class="sxs-lookup"><span data-stu-id="7835c-159">With **SimulateDeviceConfiguration.js** running, run hello application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="7835c-160">Debería ver Hola notificado configuración cambia de **correcto** demasiado**pendiente** demasiado**correcto** nuevo con activo nuevo Hola enviar frecuencia de cinco minutos en lugar de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="7835c-160">You should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="7835c-161">Hay un retraso de tooa minuto entre la operación de informe de dispositivo de Hola y el resultado de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="7835c-161">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="7835c-162">Se trata de tooenable Hola consulta infraestructura toowork a gran escala.</span><span class="sxs-lookup"><span data-stu-id="7835c-162">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="7835c-163">tooretrieve vistas coherentes de doble de un único dispositivo usan hello **getDeviceTwin** método Hola **registro** clase.</span><span class="sxs-lookup"><span data-stu-id="7835c-163">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="7835c-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7835c-164">Next steps</span></span>
<span data-ttu-id="7835c-165">En este tutorial, establezca una configuración deseada como *deseado propiedades* desde una aplicación back-end y una toodetect de aplicación de dispositivo simulado que cambian y simular un proceso de actualización de varios pasos que se envían informes de su estado como se escribió * notifica propiedades* toohello gemelas de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7835c-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app toodetect that change and simulate a multi-step update process reporting its status as *reported properties* toohello device twin.</span></span>

<span data-ttu-id="7835c-166">Hola de uso después cómo toolearn de recursos para:</span><span class="sxs-lookup"><span data-stu-id="7835c-166">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="7835c-167">enviar telemetría desde dispositivos con hello [empezar a trabajar con el centro de IoT] [ lnk-iothub-getstarted] tutorial,</span><span class="sxs-lookup"><span data-stu-id="7835c-167">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="7835c-168">programar o realizar operaciones en conjuntos grandes de dispositivos Consulte hello [programación y los trabajos de difusión] [ lnk-schedule-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="7835c-168">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="7835c-169">controlar los dispositivos de forma interactiva (por ejemplo, al activar un ventilador desde una aplicación controlada por el usuario), con hello [usar métodos directos] [ lnk-methods-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="7835c-169">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
