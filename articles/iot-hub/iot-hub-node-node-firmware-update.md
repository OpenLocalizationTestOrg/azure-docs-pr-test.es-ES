---
title: "actualización de firmware de aaaDevice con el centro de IoT de Azure (nodo) | Documentos de Microsoft"
description: "Cómo actualizar toouse la administración de dispositivos en el centro de IoT de Azure tooinitiate un firmware del dispositivo. Utilice hello Azure IoT SDK para Node.js tooimplement una aplicación de dispositivo simulado y una aplicación de servicio que desencadena la actualización de firmware de Hola."
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
ms.openlocfilehash: 99d4b369e7aba334bf713e0c657e6e5d227fb691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="cf9ab-104">Use Administración de dispositivo tooinitiate una actualización de firmware del dispositivo (nodo)</span><span class="sxs-lookup"><span data-stu-id="cf9ab-104">Use device management tooinitiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="cf9ab-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="cf9ab-105">Introduction</span></span>
<span data-ttu-id="cf9ab-106">Hola [empezar a trabajar con la administración de dispositivos] [ lnk-dm-getstarted] tutorial, ha visto cómo hello toouse [gemelas dispositivo] [ lnk-devtwin] y [directo métodos] [ lnk-c2dmethod] tooremotely primitivas reiniciar un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="cf9ab-107">Este tutorial se utiliza Hola mismos tipos primitivos de centro de IoT y proporciona orientación y muestra cómo toodo un extremo a otro simula la actualización de firmware.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-107">This tutorial uses hello same IoT Hub primitives and provides guidance and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="cf9ab-108">Este patrón se utiliza en la implementación de actualización de firmware de Hola de ejemplo de Hola Intel Edison dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-108">This pattern is used in hello firmware update implementation for hello Intel Edison device sample.</span></span>

<span data-ttu-id="cf9ab-109">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="cf9ab-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="cf9ab-110">Crear una aplicación de consola de Node.js que llama a métodos directas de hello firmwareUpdate en aplicación del dispositivo simulado de hello a través de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-110">Create a Node.js console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="cf9ab-111">Cree una aplicación de dispositivo simulado que implemente un método directo **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="cf9ab-112">Este método inicia un proceso de varias fase que espera a que la imagen de firmware de hello toodownload, descarga la imagen de firmware de Hola y por último, se aplica la imagen de firmware Hola.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="cf9ab-113">Durante cada fase de actualización de hello, Hola dispositivo usa Hola notifica propiedades tooreport en progreso.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="cf9ab-114">Al final de Hola de este tutorial, tiene dos aplicaciones de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="cf9ab-114">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="cf9ab-115">**dmpatterns_fwupdate_service.js**, que llama a un método directo en la aplicación de dispositivo simulado de hello, muestra la respuesta de Hola y periódicamente (cada 500 ms) hello muestra actualizado notificado propiedades.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="cf9ab-116">**dmpatterns_fwupdate_device.js**, centro de IoT tooyour que conecta con la identidad del dispositivo Hola creado anteriormente, recibe un método directo firmwareUpdate, se ejecuta a través de un proceso de varios Estados toosimulate un incluidos de actualización de firmware: esperando Hola Descargar imagen, descarga la nueva imagen de hello y, por último, aplicar imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-116">**dmpatterns_fwupdate_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="cf9ab-117">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="cf9ab-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="cf9ab-118">Node.js versión 0.12.x o posteriores.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="cf9ab-119">[Preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall Node.js para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-119">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="cf9ab-120">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-120">An active Azure account.</span></span> <span data-ttu-id="cf9ab-121">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="cf9ab-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="cf9ab-122">Siga hello [empezar a trabajar con la administración de dispositivos](iot-hub-node-node-device-management-get-started.md) artículo toocreate su centro de IoT y obtener la cadena de conexión de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-122">Follow hello [Get started with device management](iot-hub-node-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="cf9ab-123">Desencadenar una actualización de firmware remoto en dispositivo Hola utilizando un método directo</span><span class="sxs-lookup"><span data-stu-id="cf9ab-123">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="cf9ab-124">En esta sección, creará una aplicación de consola de Node.js que inicia una actualización de firmware remota en un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="cf9ab-125">aplicación Hello usa una actualización de hello tooinitiate método directo y usa dispositivos gemelas consultas tooperiodically obtener estado de Hola de actualización de firmware active Hola.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-125">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="cf9ab-126">Cree una carpeta vacía denominada **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="cf9ab-127">Hola **triggerfwupdateondevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-127">In hello **triggerfwupdateondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="cf9ab-128">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="cf9ab-128">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="cf9ab-129">En el símbolo del sistema en hello **triggerfwupdateondevice** carpeta, ejecute hello después comando tooinstall hello **centro de iot de azure** y **azure-iot-dispositivo-mqtt** dispositivo Paquetes SDK:</span><span class="sxs-lookup"><span data-stu-id="cf9ab-129">At your command prompt in hello **triggerfwupdateondevice** folder, run hello following command tooinstall hello **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="cf9ab-130">Con un editor de texto, cree un **dmpatterns_getstarted_service.js** archivo Hola **triggerfwupdateondevice** carpeta.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="cf9ab-131">Agregar siguiente hello 'requiere' instrucciones al principio de Hola de hello **dmpatterns_getstarted_service.js** archivo:</span><span class="sxs-lookup"><span data-stu-id="cf9ab-131">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="cf9ab-132">Agregue Hola siguiendo las declaraciones de variable y reemplace los valores de marcador de posición de hello:</span><span class="sxs-lookup"><span data-stu-id="cf9ab-132">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="cf9ab-133">Agregar siguiente Hola función toofind y mostrar el valor de Hola de hello firmwareUpdate informa de la propiedad.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-133">Add hello following function toofind and display hello value of hello firmwareUpdate reported property.</span></span>
   
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
7. <span data-ttu-id="cf9ab-134">Agregue Hola después de la función tooinvoke hello firmwareUpdate método tooreboot Hola dispositivo de destino:</span><span class="sxs-lookup"><span data-stu-id="cf9ab-134">Add hello following function tooinvoke hello firmwareUpdate method tooreboot hello target device:</span></span>
   
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
          console.error('Could not start hello firmware update on hello device: ' + err.message)
        } 
      });
    };
    ```
8. <span data-ttu-id="cf9ab-135">Por último, siguiente de hello Agregar función secuencia de actualización de firmware de toocode toostart hello y comienzan a mostrarse los periódicamente Hola notificado propiedades:</span><span class="sxs-lookup"><span data-stu-id="cf9ab-135">Finally, Add hello following function toocode toostart hello firmware update sequence and start periodically showing hello reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="cf9ab-136">Guarde y cierre hello **dmpatterns_fwupdate_service.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-136">Save and close hello **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="cf9ab-137">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="cf9ab-137">Run hello apps</span></span>
<span data-ttu-id="cf9ab-138">Ya estás listo toorun Hola aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-138">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="cf9ab-139">En línea de comandos de Hola Hola **manageddevice** carpeta, ejecute hello después toobegin comando realizar escuchas de método directo de reinicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-139">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="cf9ab-140">En línea de comandos de Hola Hola **triggerfwupdateondevice** carpeta, ejecute hello después comando tootrigger Hola remoto de reinicio y de consulta de Hola de hello dispositivo gemelas toofind reiniciar última hora.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-140">At hello command prompt in hello **triggerfwupdateondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="cf9ab-141">Consulte dispositivo respuesta toohello directo método hello en la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-141">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf9ab-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf9ab-142">Next steps</span></span>
<span data-ttu-id="cf9ab-143">En este tutorial, ha utilizado un tootrigger método directo un control remoto actualización de firmware en un dispositivo y Hola usado informó sobre el progreso de hello toofollow de propiedades de actualización de firmware de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-143">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="cf9ab-144">toolearn cómo tooextend llama a su método de programación y de solución de IoT en varios dispositivos, vea hello [programación y los trabajos de difusión] [ lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="cf9ab-144">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
