---
title: "aaaGet partió gemelos de dispositivo del centro de IoT de Azure (nodo) | Documentos de Microsoft"
description: "¿Cómo toouse centro de IoT de Azure dispositivo: los gemelos tooadd etiquetas y, a continuación, utilice una consulta de centro de IoT. Utilice hello Azure IoT SDK para Node.js tooimplement Hola simulada del dispositivo y una aplicación de servicio que agrega las etiquetas de Hola y ejecuta Hola consultas del centro de IoT."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: d60b8c3de85e9285e496b86e27d4ee31a0554a1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-node"></a><span data-ttu-id="957f5-104">Introducción a los dispositivos gemelos (Node)</span><span class="sxs-lookup"><span data-stu-id="957f5-104">Get started with device twins (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="957f5-105">Al final de Hola de este tutorial, tendrá dos aplicaciones de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="957f5-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="957f5-106">**AddTagsAndQuery.js**, una aplicación Node.js de back-end diseñada para ejecutarse desde el back-end, que agrega etiquetas y consulta dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="957f5-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="957f5-107">**TwinSimulatedDevice.js**, una aplicación Node.js que simula un dispositivo que conecta el centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente e informa acerca de su condición de conectividad.</span><span class="sxs-lookup"><span data-stu-id="957f5-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="957f5-108">artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que se puede usar toobuild aplicaciones de dispositivo y back-end.</span><span class="sxs-lookup"><span data-stu-id="957f5-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="957f5-109">toocomplete este tutorial necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="957f5-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="957f5-110">Node.js versión 0.10.x, o posteriores.</span><span class="sxs-lookup"><span data-stu-id="957f5-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="957f5-111">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="957f5-111">An active Azure account.</span></span> <span data-ttu-id="957f5-112">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="957f5-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="957f5-113">Crear aplicación de servicio de hello</span><span class="sxs-lookup"><span data-stu-id="957f5-113">Create hello service app</span></span>
<span data-ttu-id="957f5-114">En esta sección, creará una aplicación de consola de Node.js que agrega gemelas de dispositivo de toohello ubicación metadatos asociados a **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="957f5-114">In this section, you create a Node.js console app that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="957f5-115">A continuación, consulta: los gemelos de hello dispositivo almacenan en Centro de IoT Hola seleccionar dispositivos de hello ubicados en hello nos y, a continuación, Hola que dependen de una conexión de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="957f5-115">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that are reporting a cellular connection.</span></span>

1. <span data-ttu-id="957f5-116">Cree una nueva carpeta vacía denominada **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="957f5-116">Create a new empty folder called **addtagsandqueryapp**.</span></span> <span data-ttu-id="957f5-117">Hola **addtagsandqueryapp** carpeta, cree un nuevo archivo package.json mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="957f5-117">In hello **addtagsandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="957f5-118">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="957f5-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="957f5-119">En el símbolo del sistema en hello **addtagsandqueryapp** carpeta, ejecute hello después comando tooinstall hello **el centro de IOT de azure** paquete:</span><span class="sxs-lookup"><span data-stu-id="957f5-119">At your command prompt in hello **addtagsandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="957f5-120">Con un editor de texto, cree un nuevo **AddTagsAndQuery.js** archivo Hola **addtagsandqueryapp** carpeta.</span><span class="sxs-lookup"><span data-stu-id="957f5-120">Using a text editor, create a new **AddTagsAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="957f5-121">Agregar Hola después código toohello **AddTagsAndQuery.js** archivo y sustituya hello **{cadena de conexión de base de datos central de iot}** marcador de posición con hello copió cuando creó el centro de la cadena de conexión de centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="957f5-121">Add hello following code toohello **AddTagsAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    <span data-ttu-id="957f5-122">Hola **registro** objeto expone métodos toointeract necesarios de hello con: los gemelos de dispositivo del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="957f5-122">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="957f5-123">código anterior Hola inicializa por primera vez hello **registro** objeto, a continuación, recupera Hola gemelas de dispositivo para **myDeviceId**y por último actualiza sus etiquetas con información de ubicación de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="957f5-123">hello previous code first initializes hello **Registry** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="957f5-124">Después de hello actualizar Hola etiquetas Hola llamadas **queryTwins** (función).</span><span class="sxs-lookup"><span data-stu-id="957f5-124">After hello updating hello tags it calls hello **queryTwins** function.</span></span>
5. <span data-ttu-id="957f5-125">Agregar Hola siguiente código al final de Hola de **AddTagsAndQuery.js** tooimplement hello **queryTwins** función:</span><span class="sxs-lookup"><span data-stu-id="957f5-125">Add hello following code at hello end of  **AddTagsAndQuery.js** tooimplement hello **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    <span data-ttu-id="957f5-126">código de Hello anterior ejecuta dos consultas: Hola primero selecciona solo Hola dispositivo: los gemelos de dispositivos que se encuentran en hello **Redmond43** planta Hola segundo perfecciona Hola consulta tooselect solo Hola dispositivos y que también están conectados a través de red de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="957f5-126">hello previous code executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="957f5-127">Tenga en cuenta ese código Hola anterior, cuando crea hello **consulta** de objetos, especifica un número máximo de documentos devueltos.</span><span class="sxs-lookup"><span data-stu-id="957f5-127">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="957f5-128">Hola **consulta** objeto contiene un **hasMoreResults** propiedad booleana que se puede usar hello tooinvoke **nextAsTwin** métodos varias veces tooretrieve todos los resultados.</span><span class="sxs-lookup"><span data-stu-id="957f5-128">hello **query** object contains a **hasMoreResults** boolean property that you can use tooinvoke hello **nextAsTwin** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="957f5-129">Un método llamado **siguiente** está disponible para los resultados que no son dispositivos gemelos, por ejemplo, los resultados de consultas de agregación.</span><span class="sxs-lookup"><span data-stu-id="957f5-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span></span>
6. <span data-ttu-id="957f5-130">Ejecutar la aplicación hello con:</span><span class="sxs-lookup"><span data-stu-id="957f5-130">Run hello application with:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="957f5-131">Debería ver un dispositivo en los resultados de Hola para hello formular de consulta para todos los dispositivos ubicados en **Redmond43** y ninguno para consulta de Hola que restringe Hola resultados toodevices que usan una red móvil.</span><span class="sxs-lookup"><span data-stu-id="957f5-131">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![][1]

<span data-ttu-id="957f5-132">En la sección siguiente Hola crear una aplicación de dispositivo que contiene información de conectividad de Hola y cambios Hola resultado de consulta de hello en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="957f5-132">In hello next section you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="957f5-133">Crear aplicación de dispositivo de hello</span><span class="sxs-lookup"><span data-stu-id="957f5-133">Create hello device app</span></span>
<span data-ttu-id="957f5-134">En esta sección, creará una aplicación de consola de Node.js que conecta el concentrador de tooyour como **myDeviceId**y, a continuación, las actualizaciones de su gemelas de dispositivo del notificado información de Hola de toocontain de propiedades que está conectado mediante una red de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="957f5-134">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its device twin's reported properties toocontain hello information that it is connected using a cellular network.</span></span>

> [!NOTE]
> <span data-ttu-id="957f5-135">En este momento, son accesibles únicamente desde dispositivos que se conectan tooIoT concentrador: los gemelos de dispositivo mediante el protocolo MQTT Hola.</span><span class="sxs-lookup"><span data-stu-id="957f5-135">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="957f5-136">Consulte toohello [compatibilidad MQTT] [ lnk-devguide-mqtt] artículo para obtener instrucciones sobre cómo toouse de aplicación de dispositivo existente de tooconvert MQTT.</span><span class="sxs-lookup"><span data-stu-id="957f5-136">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

1. <span data-ttu-id="957f5-137">Cree una nueva carpeta vacía denominada **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="957f5-137">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="957f5-138">Hola **reportconnectivity** carpeta, cree un nuevo archivo package.json mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="957f5-138">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="957f5-139">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="957f5-139">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="957f5-140">En el símbolo del sistema en hello **reportconnectivity** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure**, y **azure-iot-dispositivo-mqtt** paquete :</span><span class="sxs-lookup"><span data-stu-id="957f5-140">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="957f5-141">Con un editor de texto, cree un nuevo **ReportConnectivity.js** archivo Hola **reportconnectivity** carpeta.</span><span class="sxs-lookup"><span data-stu-id="957f5-141">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
4. <span data-ttu-id="957f5-142">Agregar Hola después código toohello **ReportConnectivity.js** archivo y sustituya hello **{cadena de conexión de dispositivo}** marcador de posición con la cadena de conexión de dispositivo de Hola que copió al crear Hola **myDeviceId** identidad del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="957f5-142">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    <span data-ttu-id="957f5-143">Hola **cliente** objeto expone todos los métodos de hello requieren toointeract con: los gemelos de dispositivo del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="957f5-143">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="957f5-144">Hola código anterior, una vez que inicialice hello **cliente** objeto, recupera Hola gemelas de dispositivo para **myDeviceId** y actualiza su propiedad incluido con información de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="957f5-144">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
5. <span data-ttu-id="957f5-145">Ejecutar la aplicación de dispositivo de hello</span><span class="sxs-lookup"><span data-stu-id="957f5-145">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="957f5-146">Debe aparecer un mensaje Hola `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="957f5-146">You should see hello message `twin state reported`.</span></span>
6. <span data-ttu-id="957f5-147">Ahora que hello dispositivo había notificado su información de conectividad, debe aparecer en las dos consultas.</span><span class="sxs-lookup"><span data-stu-id="957f5-147">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="957f5-148">Vaya en hello **addtagsandqueryapp** Hola de carpeta y ejecutar las consultas de nuevo:</span><span class="sxs-lookup"><span data-stu-id="957f5-148">Go back in hello **addtagsandqueryapp** folder and run hello queries again:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="957f5-149">Esta vez **myDeviceId** debe aparecer en los resultados de ambas consulta.</span><span class="sxs-lookup"><span data-stu-id="957f5-149">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][3]

## <a name="next-steps"></a><span data-ttu-id="957f5-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="957f5-150">Next steps</span></span>
<span data-ttu-id="957f5-151">En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="957f5-151">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="957f5-152">Agrega los metadatos del dispositivo como etiquetas desde una aplicación de back-end y una información de conectividad del dispositivo de tooreport de aplicación de dispositivo simulado se escribió en gemelas de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="957f5-152">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="957f5-153">También habrá aprendido cómo tooquery esta información mediante el lenguaje de consulta de hello centro de IoT similar a SQL.</span><span class="sxs-lookup"><span data-stu-id="957f5-153">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="957f5-154">Hola de uso después cómo toolearn de recursos para:</span><span class="sxs-lookup"><span data-stu-id="957f5-154">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="957f5-155">enviar telemetría desde dispositivos con hello [empezar a trabajar con el centro de IoT] [ lnk-iothub-getstarted] tutorial,</span><span class="sxs-lookup"><span data-stu-id="957f5-155">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="957f5-156">configurar dispositivos mediante propiedades que desee del doble del dispositivo con hello [uso deseado propiedades de dispositivos con tooconfigure] [ lnk-twin-how-to-configure] tutorial,</span><span class="sxs-lookup"><span data-stu-id="957f5-156">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="957f5-157">controlar los dispositivos de forma interactiva (por ejemplo, al activar un ventilador desde una aplicación controlada por el usuario), con hello [usar métodos directos] [ lnk-methods-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="957f5-157">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
