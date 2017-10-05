---
title: "Cómo programar trabajos con IoT Hub de Azure | Microsoft Docs"
description: "Cómo programar un trabajo de IoT Hub de Azure para invocar un método directo en varios dispositivos. El SDK de IoT de Azure para Node.js se usa para implementar la aplicación de dispositivo simulado y una aplicación de servicio para ejecutar el trabajo."
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
ms.openlocfilehash: 42e594dc6a8a8be619b5652bf8e44cf883650489
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a><span data-ttu-id="069cd-104">Programación y difusión de trabajos (Node)</span><span class="sxs-lookup"><span data-stu-id="069cd-104">Schedule and broadcast jobs (Node)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="069cd-105">IoT Hub de Azure es un servicio completamente administrado que permite a una aplicación back-end crear y realizar un seguimiento de los trabajos que programan y actualizan millones de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="069cd-105">Azure IoT Hub is a fully managed service that enables a back-end app to create and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="069cd-106">Los trabajos pueden utilizarse para las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="069cd-106">Jobs can be used for the following actions:</span></span>

* <span data-ttu-id="069cd-107">Actualizar las propiedades deseadas</span><span class="sxs-lookup"><span data-stu-id="069cd-107">Update desired properties</span></span>
* <span data-ttu-id="069cd-108">Actualizar etiquetas</span><span class="sxs-lookup"><span data-stu-id="069cd-108">Update tags</span></span>
* <span data-ttu-id="069cd-109">Invocar métodos directos</span><span class="sxs-lookup"><span data-stu-id="069cd-109">Invoke direct methods</span></span>

<span data-ttu-id="069cd-110">Conceptualmente, un trabajo contiene una de estas acciones y realiza un seguimiento del progreso de ejecución en un conjunto de dispositivos, que define una consulta de dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="069cd-110">Conceptually, a job wraps one of these actions and tracks the progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="069cd-111">Por ejemplo, una aplicación back-end puede usar un trabajo para invocar un método de reinicio en 10 000 dispositivos, especificado por una consulta de dispositivos gemelos y programada en el futuro.</span><span class="sxs-lookup"><span data-stu-id="069cd-111">For example, a back-end app can use a job to invoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="069cd-112">Esa aplicación puede después seguir el progreso cuando cada uno de estos dispositivos reciben y ejecutan el método de reinicio.</span><span class="sxs-lookup"><span data-stu-id="069cd-112">That application can then track progress as each of those devices receive and execute the reboot method.</span></span>

<span data-ttu-id="069cd-113">Más información sobre estas funcionalidades en estos artículos:</span><span class="sxs-lookup"><span data-stu-id="069cd-113">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="069cd-114">Dispositivo gemelo y propiedades: [Introducción a los dispositivos gemelos][lnk-get-started-twin] y [Tutorial: Uso de las propiedades deseadas para configurar dispositivos][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="069cd-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="069cd-115">Métodos directos: [Guía del desarrollador de IoT Hub: métodos directos][lnk-dev-methods] y [Tutorial: Uso de métodos directos][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="069cd-115">direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="069cd-116">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="069cd-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="069cd-117">Crear una aplicación de dispositivo simulado con un método directo que permita **lockDoor** que se pueda llamar por la solución back-end.</span><span class="sxs-lookup"><span data-stu-id="069cd-117">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by the solution back end.</span></span>
* <span data-ttu-id="069cd-118">Crear una aplicación de consola de Node.js que llame al método directo **lockDoor** en la aplicación de dispositivo simulado mediante un trabajo y actualice las propiedades deseadas mediante un trabajo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="069cd-118">Create a Node.js console app that calls the **lockDoor** direct method in the simulated device app using a job and updates the desired properties using a device job.</span></span>

<span data-ttu-id="069cd-119">Al final de este tutorial tendrá dos aplicaciones de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="069cd-119">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="069cd-120">**simDevice.js**, que se conecta al centro de IoT con la identidad del dispositivo y recibe un método directo **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="069cd-120">**simDevice.js**, which connects to your IoT hub with the device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="069cd-121">**scheduleJobService.js**, que llama a un método directo en la aplicación de dispositivo simulado y actualiza las propiedades deseadas del dispositivo gemelo mediante un trabajo.</span><span class="sxs-lookup"><span data-stu-id="069cd-121">**scheduleJobService.js**, which calls a direct method in the simulated device app and update the device twin's desired properties using a job.</span></span>

<span data-ttu-id="069cd-122">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="069cd-122">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="069cd-123">Node.js versión 0.12.x o posteriores.</span><span class="sxs-lookup"><span data-stu-id="069cd-123">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="069cd-124">En [Preparación del entorno de desarrollo][lnk-dev-setup] se describe cómo instalar Node.js para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="069cd-124">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="069cd-125">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="069cd-125">An active Azure account.</span></span> <span data-ttu-id="069cd-126">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="069cd-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="069cd-127">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="069cd-127">Create a simulated device app</span></span>
<span data-ttu-id="069cd-128">En esta sección, creará una aplicación de consola de Node.js que responde a un método directo que se invoca desde la nube, que desencadena un reinicio del dispositivo simulado y utiliza las propiedades notificadas para habilitar consultas en el dispositivo gemelo con el fin de identificar los dispositivos y cuándo se reiniciaron por última vez.</span><span class="sxs-lookup"><span data-stu-id="069cd-128">In this section, you create a Node.js console app that responds to a direct method called by the cloud, which triggers a simulated device reboot and uses the reported properties to enable device twin queries to identify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="069cd-129">Cree una nueva carpeta vacía denominada **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="069cd-129">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="069cd-130">En la carpeta **simDevice**, cree un archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="069cd-130">In the **simDevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="069cd-131">Acepte todos los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="069cd-131">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="069cd-132">En el símbolo del sistema, en la carpeta **simDevice**, ejecute el siguiente comando para instalar el paquete del SDK de dispositivo **azure-iot-device** y el paquete **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="069cd-132">At your command prompt in the **simDevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="069cd-133">Con un editor de texto, cree un nuevo archivo **simDevice.js** en la carpeta **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="069cd-133">Using a text editor, create a new **simDevice.js** file in the **simDevice** folder.</span></span>
4. <span data-ttu-id="069cd-134">Agregue las siguientes instrucciones "require" al principio del archivo **simDevice.js**:</span><span class="sxs-lookup"><span data-stu-id="069cd-134">Add the following 'require' statements at the start of the **simDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="069cd-135">Agregue una variable **connectionString** y utilícela para crear una instancia de **cliente**.</span><span class="sxs-lookup"><span data-stu-id="069cd-135">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="069cd-136">Agregue la siguiente función para controlar el método **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="069cd-136">Add the following function to handle the **lockDoor** method.</span></span>
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. <span data-ttu-id="069cd-137">Agregue el código siguiente para registrar el controlador del método **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="069cd-137">Add the following code to register the handler for the **lockDoor** method.</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect to IotHub client.');
        }  else {
            console.log('Client connected to IoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. <span data-ttu-id="069cd-138">Guarde y cierre el archivo **simDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="069cd-138">Save and close the **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="069cd-139">Por simplificar, este tutorial no implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="069cd-139">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="069cd-140">En el código de producción, deberá implementar directivas de reintentos (por ejemplo, retroceso exponencial), tal y como se sugiere en el artículo de MSDN [Transient Fault Handling][lnk-transient-faults] (Tratamiento de errores temporales).</span><span class="sxs-lookup"><span data-stu-id="069cd-140">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="069cd-141">Programación de trabajos para llamar un método directo y actualización de las propiedades de un dispositivo gemelo</span><span class="sxs-lookup"><span data-stu-id="069cd-141">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="069cd-142">En esta sección, creará una aplicación de consola de Node.js que inicia un **lockDook** remoto en un dispositivo con un método directo y actualiza las propiedades del dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="069cd-142">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update the device twin's properties.</span></span>

1. <span data-ttu-id="069cd-143">Cree una nueva carpeta vacía denominada **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="069cd-143">Create a new empty folder called **scheduleJobService**.</span></span>  <span data-ttu-id="069cd-144">En la carpeta **scheduleJobService**, cree un archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="069cd-144">In the **scheduleJobService** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="069cd-145">Acepte todos los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="069cd-145">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="069cd-146">En el símbolo del sistema, en la carpeta **scheduleJobService**, ejecute el siguiente comando para instalar el paquete del SDK de dispositivo **azure-iothub** y el paquete **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="069cd-146">At your command prompt in the **scheduleJobService** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub uuid --save
    ```
3. <span data-ttu-id="069cd-147">Con un editor de texto, cree un nuevo archivo **scheduleJobService.js** en la carpeta **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="069cd-147">Using a text editor, create a new **scheduleJobService.js** file in the **scheduleJobService** folder.</span></span>
4. <span data-ttu-id="069cd-148">Agregue las siguientes instrucciones "require" al principio del archivo **dmpatterns_gscheduleJobServiceetstarted_service.js**:</span><span class="sxs-lookup"><span data-stu-id="069cd-148">Add the following 'require' statements at the start of the **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. <span data-ttu-id="069cd-149">Agregue las siguientes declaraciones de variable y reemplace los valores de marcador de posición:</span><span class="sxs-lookup"><span data-stu-id="069cd-149">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="069cd-150">Agregue la función siguiente que se utilizará para supervisar la ejecución del trabajo:</span><span class="sxs-lookup"><span data-stu-id="069cd-150">Add the following function that will be used to monitor the execution of the job:</span></span>
   
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
7. <span data-ttu-id="069cd-151">Agregue el código siguiente para programar el trabajo que llama al método de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="069cd-151">Add the following code to schedule the job that calls the device method:</span></span>
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable to process method
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
8. <span data-ttu-id="069cd-152">Agregue el código siguiente para programar el trabajo para que actualice el dispositivo gemelo:</span><span class="sxs-lookup"><span data-stu-id="069cd-152">Add the following code to schedule the job to update the device twin:</span></span>
   
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
9. <span data-ttu-id="069cd-153">Guarde y cierre el archivo **scheduleJobService.js**.</span><span class="sxs-lookup"><span data-stu-id="069cd-153">Save and close the **scheduleJobService.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="069cd-154">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="069cd-154">Run the applications</span></span>
<span data-ttu-id="069cd-155">Ahora está preparado para ejecutar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="069cd-155">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="069cd-156">En el símbolo del sistema dentro de la carpeta **simDevice**, ejecute el siguiente comando para iniciar la escucha del método directo de reinicio.</span><span class="sxs-lookup"><span data-stu-id="069cd-156">At the command prompt in the **simDevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node simDevice.js
    ```
2. <span data-ttu-id="069cd-157">En el símbolo del sistema de la carpeta **scheduleJobService**, ejecute el siguiente comando para desencadenar los trabajos a fin de bloquear la puerta y actualizar el dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="069cd-157">At the command prompt in the **scheduleJobService** folder, run the following command to trigger the jobs to lock the door and update the twin</span></span>
   
    ```
    node scheduleJobService.js
    ```
3. <span data-ttu-id="069cd-158">Verá la respuesta del dispositivo al método directo en la consola.</span><span class="sxs-lookup"><span data-stu-id="069cd-158">You see the device response to the direct method in the console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="069cd-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="069cd-159">Next steps</span></span>
<span data-ttu-id="069cd-160">En este tutorial, ha utilizado un trabajo para programar un método directo para un dispositivo y la actualización de las propiedades del dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="069cd-160">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span></span>

<span data-ttu-id="069cd-161">Para continuar con la introducción de IoT Hub y los patrones de administración de dispositivos como remoto a través de la actualización de firmware de aire, consulte:</span><span class="sxs-lookup"><span data-stu-id="069cd-161">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, see:</span></span>

<span data-ttu-id="069cd-162">[Tutorial: Realización de una actualización de firmware][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="069cd-162">[Tutorial: How to do a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="069cd-163">Para continuar con la introducción a IoT Hub, consulte [Introducción a Azure IoT Edge][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="069cd-163">To continue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span></span>

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
