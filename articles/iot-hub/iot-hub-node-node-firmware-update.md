---
title: "Actualización de firmware de dispositivos con IoT Hub de Azure (Node) | Microsoft Docs"
description: "Describe cómo usar la administración de dispositivos en IoT Hub de Azure para iniciar una actualización de firmware del dispositivo. Usará el SDK de IoT de Azure para Node.js para implementar la aplicación de dispositivo simulado y una aplicación de servicio que desencadena la actualización del firmware."
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
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 350cf1cbec8847d1bbf29814435502af6f098e54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="f23a7-104">Use la administración de dispositivos para iniciar una actualización de firmware del dispositivo (Node/Node)</span><span class="sxs-lookup"><span data-stu-id="f23a7-104">Use device management to initiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="f23a7-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="f23a7-105">Introduction</span></span>
<span data-ttu-id="f23a7-106">En el tutorial de [Introducción a la administración de dispositivos][lnk-dm-getstarted], vimos cómo usar los primitivos de [dispositivo gemelo][lnk-devtwin] y [métodos directos][lnk-c2dmethod] para reiniciar de forma remota un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f23a7-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="f23a7-107">Este tutorial utiliza a los mismos tipos primitivos de IoT Hub. Además, proporciona orientación y muestra cómo realizar una actualización de firmware simulada de extremo a extremo.</span><span class="sxs-lookup"><span data-stu-id="f23a7-107">This tutorial uses the same IoT Hub primitives and provides guidance and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="f23a7-108">Este patrón se utiliza en la implementación de actualización de firmware para el ejemplo de dispositivo Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="f23a7-108">This pattern is used in the firmware update implementation for the Intel Edison device sample.</span></span>

<span data-ttu-id="f23a7-109">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="f23a7-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="f23a7-110">Crear una aplicación de consola de Node.js que llame al método directo firmwareUpdate en la aplicación de dispositivo simulado a través de su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f23a7-110">Create a Node.js console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="f23a7-111">Cree una aplicación de dispositivo simulado que implemente un método directo **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="f23a7-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="f23a7-112">Este método inicia un proceso de varias fases que espera para descargar la imagen de firmware, la descarga y, por último, la aplica.</span><span class="sxs-lookup"><span data-stu-id="f23a7-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="f23a7-113">Durante cada fase de la actualización, el dispositivo usa las propiedades notificadas para informar sobre el progreso.</span><span class="sxs-lookup"><span data-stu-id="f23a7-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="f23a7-114">Al final de este tutorial tendrá dos aplicaciones de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="f23a7-114">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="f23a7-115">**dmpatterns_fwupdate_service.js**, que llama a un método directo en la aplicación de dispositivo simulado, muestra la respuesta y muestra periódicamente (cada 500 ms) las propiedades notificadas actualizadas.</span><span class="sxs-lookup"><span data-stu-id="f23a7-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="f23a7-116">**dmpatterns_fwupdate_device.js**, que se conecta a IoT Hub con la identidad del dispositivo creada anteriormente, recibe un método directo firmwareUpdate y se ejecuta mediante un proceso de varios estado para simular una actualización de firmware; entre ellas, la espera para la descarga de imágenes, la descarga de la nueva imagen y, finalmente, la aplicación de dicha imagen.</span><span class="sxs-lookup"><span data-stu-id="f23a7-116">**dmpatterns_fwupdate_device.js**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="f23a7-117">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f23a7-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="f23a7-118">Node.js versión 0.12.x o posteriores.</span><span class="sxs-lookup"><span data-stu-id="f23a7-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="f23a7-119">En [Preparación del entorno de desarrollo][lnk-dev-setup] se describe cómo instalar Node.js para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="f23a7-119">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="f23a7-120">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="f23a7-120">An active Azure account.</span></span> <span data-ttu-id="f23a7-121">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="f23a7-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="f23a7-122">Siga los pasos del artículo de [introducción a la administración de dispositivos](iot-hub-node-node-device-management-get-started.md) para crear su instancia de IoT Hub y obtener la cadena de conexión de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f23a7-122">Follow the [Get started with device management](iot-hub-node-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="f23a7-123">Desencadenamiento de una actualización de firmware remota en el dispositivo con un método directo</span><span class="sxs-lookup"><span data-stu-id="f23a7-123">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="f23a7-124">En esta sección, creará una aplicación de consola de Node.js que inicia una actualización de firmware remota en un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f23a7-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="f23a7-125">La aplicación usa un método directo para iniciar la actualización y utiliza consultas de dispositivos gemelos para obtener periódicamente el estado de la actualización del firmware activa.</span><span class="sxs-lookup"><span data-stu-id="f23a7-125">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="f23a7-126">Cree una carpeta vacía denominada **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="f23a7-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="f23a7-127">En la carpeta **triggerfwupdateondevice** , cree un archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="f23a7-127">In the **triggerfwupdateondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="f23a7-128">Acepte todos los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="f23a7-128">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="f23a7-129">En el símbolo del sistema, en la carpeta **triggerfwupdateondevice**, ejecute el siguiente comando para instalar los paquetes del SDK de dispositivo **azure-iothub** y **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="f23a7-129">At your command prompt in the **triggerfwupdateondevice** folder, run the following command to install the **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="f23a7-130">Con un editor de texto, cree un archivo **dmpatterns_getstarted_service.js** en la carpeta **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="f23a7-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="f23a7-131">Agregue las siguientes instrucciones "require" al principio del archivo **dmpatterns_getstarted_service.js**:</span><span class="sxs-lookup"><span data-stu-id="f23a7-131">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="f23a7-132">Agregue las siguientes declaraciones de variable y reemplace los valores de marcador de posición:</span><span class="sxs-lookup"><span data-stu-id="f23a7-132">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="f23a7-133">Agregue la siguiente función para buscar y mostrar el valor de la propiedad notificada firmwareUpdate.</span><span class="sxs-lookup"><span data-stu-id="f23a7-133">Add the following function to find and display the value of the firmwareUpdate reported property.</span></span>
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. <span data-ttu-id="f23a7-134">Agregue la siguiente función para invocar el método firmwareUpdate con el fin de reiniciar el dispositivo de destino:</span><span class="sxs-lookup"><span data-stu-id="f23a7-134">Add the following function to invoke the firmwareUpdate method to reboot the target device:</span></span>
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start the firmware update on the device: ' + err.message)
        } 
      });
    };
    ```
8. <span data-ttu-id="f23a7-135">Finalmente, agregue la siguiente función al código para iniciar la secuencia de actualización de firmware e iníciela periódicamente mostrando las propiedades notificadas:</span><span class="sxs-lookup"><span data-stu-id="f23a7-135">Finally, Add the following function to code to start the firmware update sequence and start periodically showing the reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="f23a7-136">Guarde y cierre el archivo **dmpatterns_fwupdate_service.js**.</span><span class="sxs-lookup"><span data-stu-id="f23a7-136">Save and close the **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="f23a7-137">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f23a7-137">Run the apps</span></span>
<span data-ttu-id="f23a7-138">Ya está preparado para ejecutar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f23a7-138">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="f23a7-139">En el símbolo del sistema dentro de la carpeta **manageddevice**, ejecute el siguiente comando para iniciar la escucha del método directo de reinicio.</span><span class="sxs-lookup"><span data-stu-id="f23a7-139">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="f23a7-140">En el símbolo del sistema dentro de la carpeta **triggerfwupdateondevice**, ejecute el siguiente comando para desencadenar el reinicio remoto y la consulta en el dispositivo gemelo para buscar la hora del último reinicio.</span><span class="sxs-lookup"><span data-stu-id="f23a7-140">At the command prompt in the **triggerfwupdateondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="f23a7-141">Verá la respuesta del dispositivo al método directo en la consola.</span><span class="sxs-lookup"><span data-stu-id="f23a7-141">You see the device response to the direct method in the console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f23a7-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f23a7-142">Next steps</span></span>
<span data-ttu-id="f23a7-143">En este tutorial, ha usado un método directo para desencadenar una actualización de firmware remota en un dispositivo y ha utilizado las propiedades notificadas para entender el progreso del proceso de actualización del firmware.</span><span class="sxs-lookup"><span data-stu-id="f23a7-143">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="f23a7-144">Para información sobre cómo ampliar la solución de IoT y programar llamadas de método en varios dispositivos, consulte el tutorial [Programación de trabajos en varios dispositivos][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="f23a7-144">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
