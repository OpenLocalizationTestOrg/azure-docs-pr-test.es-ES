---
title: trabajos de aaaSchedule con el centro de IoT de Azure (nodo) | Documentos de Microsoft
description: "¿Cómo tooschedule un centro de IoT de Azure trabajo tooinvoke un método directo en varios dispositivos. Utilice hello Azure IoT SDK para aplicaciones de dispositivos de Node.js tooimplement Hola simulado y un trabajo de Hola de toorun de aplicación de servicio."
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
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a><span data-ttu-id="cede4-104">Programación y difusión de trabajos (Node)</span><span class="sxs-lookup"><span data-stu-id="cede4-104">Schedule and broadcast jobs (Node)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="cede4-105">Centro de IoT de Azure es un servicio completamente administrado que permite un toocreate de aplicaciones back-end y los trabajos de seguimiento que el programa y actualización millones de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="cede4-105">Azure IoT Hub is a fully managed service that enables a back-end app toocreate and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="cede4-106">Los trabajos pueden utilizarse para hello siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="cede4-106">Jobs can be used for hello following actions:</span></span>

* <span data-ttu-id="cede4-107">Actualizar las propiedades deseadas</span><span class="sxs-lookup"><span data-stu-id="cede4-107">Update desired properties</span></span>
* <span data-ttu-id="cede4-108">Actualizar etiquetas</span><span class="sxs-lookup"><span data-stu-id="cede4-108">Update tags</span></span>
* <span data-ttu-id="cede4-109">Invocar métodos directos</span><span class="sxs-lookup"><span data-stu-id="cede4-109">Invoke direct methods</span></span>

<span data-ttu-id="cede4-110">Conceptualmente, un trabajo contiene una de estas acciones y pistas Hola progreso de la ejecución con un conjunto de dispositivos, que se define mediante una consulta de gemelas de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cede4-110">Conceptually, a job wraps one of these actions and tracks hello progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="cede4-111">Por ejemplo, una aplicación de back-end puede utilizar un trabajo tooinvoke un método de reinicio en 10.000 dispositivos, especificado por una consulta de gemelas de dispositivo y programada en el futuro.</span><span class="sxs-lookup"><span data-stu-id="cede4-111">For example, a back-end app can use a job tooinvoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="cede4-112">Esa aplicación, a continuación, puede seguir el progreso de cada uno de los dispositivos de recepción y ejecutar el método de reinicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="cede4-112">That application can then track progress as each of those devices receive and execute hello reboot method.</span></span>

<span data-ttu-id="cede4-113">Más información sobre estas funcionalidades en estos artículos:</span><span class="sxs-lookup"><span data-stu-id="cede4-113">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="cede4-114">Gemelos de dispositivo y propiedades: [empezar a trabajar con: los gemelos de dispositivo] [ lnk-get-started-twin] y [Tutorial: cómo toouse dispositivo dos propiedades][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="cede4-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="cede4-115">Métodos directos: [Guía del desarrollador de IoT Hub: métodos directos][lnk-dev-methods] y [Tutorial: Uso de métodos directos][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="cede4-115">direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="cede4-116">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="cede4-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="cede4-117">Crear una aplicación de dispositivo simulado que tiene un método directo que permite **lockDoor** que puede llamarse mediante Hola solución back-end.</span><span class="sxs-lookup"><span data-stu-id="cede4-117">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by hello solution back end.</span></span>
* <span data-ttu-id="cede4-118">Crear una aplicación de consola Node.js ese Hola llamadas **lockDoor** método directo en aplicación de dispositivo simulado de hello mediante un Hola de trabajo y las actualizaciones de las propiedades con un trabajo del dispositivo adecuadas.</span><span class="sxs-lookup"><span data-stu-id="cede4-118">Create a Node.js console app that calls hello **lockDoor** direct method in hello simulated device app using a job and updates hello desired properties using a device job.</span></span>

<span data-ttu-id="cede4-119">Al final de Hola de este tutorial, tiene dos aplicaciones de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="cede4-119">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="cede4-120">**simDevice.js**, que se conecta el centro de IoT tooyour con la identidad del dispositivo hello y recibe un **lockDoor** método directo.</span><span class="sxs-lookup"><span data-stu-id="cede4-120">**simDevice.js**, which connects tooyour IoT hub with hello device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="cede4-121">**scheduleJobService.js**, que llama a un método directo en el dispositivo de Hola de aplicación y la actualización del dispositivo simulado Hola propiedades deseadas de gemelas con un trabajo.</span><span class="sxs-lookup"><span data-stu-id="cede4-121">**scheduleJobService.js**, which calls a direct method in hello simulated device app and update hello device twin's desired properties using a job.</span></span>

<span data-ttu-id="cede4-122">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="cede4-122">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="cede4-123">Node.js versión 0.12.x o posteriores.</span><span class="sxs-lookup"><span data-stu-id="cede4-123">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="cede4-124">[Preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall Node.js para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="cede4-124">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="cede4-125">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="cede4-125">An active Azure account.</span></span> <span data-ttu-id="cede4-126">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="cede4-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="cede4-127">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="cede4-127">Create a simulated device app</span></span>
<span data-ttu-id="cede4-128">En esta sección, creará una aplicación de consola de Node.js que responde tooa método directo llamado a la nube de hello, lo que desencadena un reinicio del dispositivo simulado y utiliza Hola notificado propiedades tooenable dispositivos gemelas consultas tooidentify dispositivos y cuando reinició por última vez.</span><span class="sxs-lookup"><span data-stu-id="cede4-128">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="cede4-129">Cree una nueva carpeta vacía denominada **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="cede4-129">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="cede4-130">Hola **simDevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="cede4-130">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="cede4-131">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="cede4-131">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="cede4-132">En el símbolo del sistema en hello **simDevice** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure** paquete del SDK de dispositivo y **azure-iot-dispositivo-mqtt** paquete:</span><span class="sxs-lookup"><span data-stu-id="cede4-132">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="cede4-133">Con un editor de texto, cree un nuevo **simDevice.js** archivo Hola **simDevice** carpeta.</span><span class="sxs-lookup"><span data-stu-id="cede4-133">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>
4. <span data-ttu-id="cede4-134">Agregar siguiente hello 'requiere' instrucciones al principio de Hola de hello **simDevice.js** archivo:</span><span class="sxs-lookup"><span data-stu-id="cede4-134">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="cede4-135">Agregar un **connectionString** variable y utilizar toocreate un **cliente** instancia.</span><span class="sxs-lookup"><span data-stu-id="cede4-135">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="cede4-136">Agregar Hola después Hola de función toohandle **lockDoor** método.</span><span class="sxs-lookup"><span data-stu-id="cede4-136">Add hello following function toohandle hello **lockDoor** method.</span></span>
   
    ```
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
7. <span data-ttu-id="cede4-137">Agregar Hola siguiente controlador de hello tooregister de código de hello **lockDoor** método.</span><span class="sxs-lookup"><span data-stu-id="cede4-137">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. <span data-ttu-id="cede4-138">Guarde y cierre hello **simDevice.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="cede4-138">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="cede4-139">tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento.</span><span class="sxs-lookup"><span data-stu-id="cede4-139">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="cede4-140">En el código de producción, debe implementar directivas de reintento (por ejemplo, un retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="cede4-140">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="cede4-141">Programación de trabajos para llamar un método directo y actualización de las propiedades de un dispositivo gemelo</span><span class="sxs-lookup"><span data-stu-id="cede4-141">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="cede4-142">En esta sección, creará una aplicación de consola de Node.js que inicia un equipo remoto **lockDoor** en un dispositivo mediante las propiedades de un directo método y actualización Hola dispositivo gemelas.</span><span class="sxs-lookup"><span data-stu-id="cede4-142">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update hello device twin's properties.</span></span>

1. <span data-ttu-id="cede4-143">Cree una nueva carpeta vacía denominada **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="cede4-143">Create a new empty folder called **scheduleJobService**.</span></span>  <span data-ttu-id="cede4-144">Hola **scheduleJobService** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="cede4-144">In hello **scheduleJobService** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="cede4-145">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="cede4-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="cede4-146">En el símbolo del sistema en hello **scheduleJobService** carpeta, ejecute hello después comando tooinstall hello **el centro de IOT de azure** paquete del SDK de dispositivo y **azure iot dispositivo-mqtt**paquete:</span><span class="sxs-lookup"><span data-stu-id="cede4-146">At your command prompt in hello **scheduleJobService** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub uuid --save
    ```
3. <span data-ttu-id="cede4-147">Con un editor de texto, cree un nuevo **scheduleJobService.js** archivo Hola **scheduleJobService** carpeta.</span><span class="sxs-lookup"><span data-stu-id="cede4-147">Using a text editor, create a new **scheduleJobService.js** file in hello **scheduleJobService** folder.</span></span>
4. <span data-ttu-id="cede4-148">Agregar siguiente hello 'requiere' instrucciones al principio de Hola de hello **dmpatterns_gscheduleJobServiceetstarted_service.js** archivo:</span><span class="sxs-lookup"><span data-stu-id="cede4-148">Add hello following 'require' statements at hello start of hello **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. <span data-ttu-id="cede4-149">Agregue Hola siguiendo las declaraciones de variable y reemplace los valores de marcador de posición de hello:</span><span class="sxs-lookup"><span data-stu-id="cede4-149">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="cede4-150">Agregue Hola después de la función que será usado toomonitor Hola ejecución del trabajo de hello:</span><span class="sxs-lookup"><span data-stu-id="cede4-150">Add hello following function that will be used toomonitor hello execution of hello job:</span></span>
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. <span data-ttu-id="cede4-151">Agregue Hola siguiendo el trabajo de hello tooschedule de código que llama el método de dispositivo de hello:</span><span class="sxs-lookup"><span data-stu-id="cede4-151">Add hello following code tooschedule hello job that calls hello device method:</span></span>
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. <span data-ttu-id="cede4-152">Agregue Hola después a gemelas de código tooschedule Hola trabajo tooupdate Hola dispositivo:</span><span class="sxs-lookup"><span data-stu-id="cede4-152">Add hello following code tooschedule hello job tooupdate hello device twin:</span></span>
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. <span data-ttu-id="cede4-153">Guarde y cierre hello **scheduleJobService.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="cede4-153">Save and close hello **scheduleJobService.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="cede4-154">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="cede4-154">Run hello applications</span></span>
<span data-ttu-id="cede4-155">Ya estás listo toorun aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="cede4-155">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="cede4-156">En línea de comandos de Hola Hola **simDevice** carpeta, ejecute hello después toobegin comando realizar escuchas de método directo de reinicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="cede4-156">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node simDevice.js
    ```
2. <span data-ttu-id="cede4-157">En línea de comandos de Hola Hola **scheduleJobService** carpeta, ejecute hello después comando tootrigger Hola trabajos toolock Hola puerta y actualización Hola gemelas</span><span class="sxs-lookup"><span data-stu-id="cede4-157">At hello command prompt in hello **scheduleJobService** folder, run hello following command tootrigger hello jobs toolock hello door and update hello twin</span></span>
   
    ```
    node scheduleJobService.js
    ```
3. <span data-ttu-id="cede4-158">Consulte dispositivo respuesta toohello directo método hello en la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="cede4-158">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cede4-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cede4-159">Next steps</span></span>
<span data-ttu-id="cede4-160">En este tutorial, ha utilizado un trabajo tooschedule un dispositivo de tooa método directo y actualización de Hola de las propiedades del doble del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cede4-160">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="cede4-161">toocontinue Introducción a centro de IoT y patrones de la administración de dispositivos como el remoto a través de la actualización de firmware de aire hello, vea:</span><span class="sxs-lookup"><span data-stu-id="cede4-161">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, see:</span></span>

<span data-ttu-id="cede4-162">[Tutorial: Cómo toodo un firmware actualizar][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="cede4-162">[Tutorial: How toodo a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="cede4-163">toocontinue Introducción a centro de IoT, consulte [Introducción a Azure IoT borde][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="cede4-163">toocontinue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span></span>

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
