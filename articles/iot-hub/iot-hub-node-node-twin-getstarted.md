---
title: "Introducción a los dispositivos gemelos de IoT Hub de Azure | Microsoft Docs"
description: "Describe cómo usar dispositivos gemelos de IoT Hub de Azure para agregar etiquetas y, luego, usar una consulta de IoT Hub. El SDK de IoT de Azure para Node.js se usa para implementar la aplicación de dispositivo simulado y una aplicación de servicio que agrega las etiquetas y ejecuta la consulta de IoT Hub."
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
ms.openlocfilehash: 633c9fd4f8a1d017d93148f8c2e860ccba14238c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-device-twins-node"></a><span data-ttu-id="f8c40-104">Introducción a los dispositivos gemelos (Node)</span><span class="sxs-lookup"><span data-stu-id="f8c40-104">Get started with device twins (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="f8c40-105">Al final de este tutorial tendrá dos aplicaciones de consola de Node.js:</span><span class="sxs-lookup"><span data-stu-id="f8c40-105">At the end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="f8c40-106">**AddTagsAndQuery.js**, una aplicación Node.js de back-end diseñada para ejecutarse desde el back-end, que agrega etiquetas y consulta dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="f8c40-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="f8c40-107">**TwinSimulatedDevice.js**, una aplicación de Node.js que simula un dispositivo que se conecta a su centro de IoT con la identidad del dispositivo creada anteriormente e informa de su estado de conectividad.</span><span class="sxs-lookup"><span data-stu-id="f8c40-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="f8c40-108">En el artículo [SDK de IoT de Azure][lnk-hub-sdks] se proporciona información sobre los SDK que puede usar para crear aplicaciones de dispositivo y de back-end.</span><span class="sxs-lookup"><span data-stu-id="f8c40-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="f8c40-109">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f8c40-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="f8c40-110">Node.js versión 0.10.x o posteriores.</span><span class="sxs-lookup"><span data-stu-id="f8c40-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="f8c40-111">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="f8c40-111">An active Azure account.</span></span> <span data-ttu-id="f8c40-112">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="f8c40-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="f8c40-113">Creación de la aplicación de servicio</span><span class="sxs-lookup"><span data-stu-id="f8c40-113">Create the service app</span></span>
<span data-ttu-id="f8c40-114">En esta sección, creará una aplicación de consola de Node.js que agrega metadatos de ubicación al dispositivo gemelo asociado con **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="f8c40-114">In this section, you create a Node.js console app that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="f8c40-115">Después, consulta los dispositivos gemelos almacenados en la instancia de IoT Hub mediante la selección de los dispositivos ubicados en Estados Unidos y, después, los que informan de una conexión de red de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="f8c40-115">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that are reporting a cellular connection.</span></span>

1. <span data-ttu-id="f8c40-116">Cree una nueva carpeta vacía denominada **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="f8c40-116">Create a new empty folder called **addtagsandqueryapp**.</span></span> <span data-ttu-id="f8c40-117">En la carpeta **addtagsandqueryapp** , cree un nuevo archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="f8c40-117">In the **addtagsandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="f8c40-118">Acepte todos los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="f8c40-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="f8c40-119">En el símbolo del sistema, en la carpeta **addtagsandqueryapp**, ejecute el siguiente comando para instalar el paquete **azure-iothub**:</span><span class="sxs-lookup"><span data-stu-id="f8c40-119">At your command prompt in the **addtagsandqueryapp** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="f8c40-120">Con un editor de texto, cree un nuevo archivo **AddTagsAndQuery.js** en la carpeta **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="f8c40-120">Using a text editor, create a new **AddTagsAndQuery.js** file in the **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="f8c40-121">Agregue el código siguiente al archivo **AddTagsAndQuery.js** y sustituya el marcador de posición **{iot hub connection string}** con la cadena de conexión de IoT Hub que copió al crear su centro:</span><span class="sxs-lookup"><span data-stu-id="f8c40-121">Add the following code to the **AddTagsAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span></span>
   
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
   
    <span data-ttu-id="f8c40-122">El objeto **Registro** expone todos los métodos necesarios para interactuar con dispositivos gemelos del servicio.</span><span class="sxs-lookup"><span data-stu-id="f8c40-122">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="f8c40-123">El código anterior inicializa primero el objeto **Registro**, a continuación, recupera el dispositivo gemelo de **myDeviceId**, y por último actualiza sus etiquetas con la información de la ubicación deseada.</span><span class="sxs-lookup"><span data-stu-id="f8c40-123">The previous code first initializes the **Registry** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="f8c40-124">Después de actualizar las etiquetas, llama a la función **queryTwins**.</span><span class="sxs-lookup"><span data-stu-id="f8c40-124">After the updating the tags it calls the **queryTwins** function.</span></span>
5. <span data-ttu-id="f8c40-125">Agregue el código siguiente al final de  **AddTagsAndQuery.js** para implementar la función **queryTwins**:</span><span class="sxs-lookup"><span data-stu-id="f8c40-125">Add the following code at the end of  **AddTagsAndQuery.js** to implement the **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    <span data-ttu-id="f8c40-126">El código anterior ejecuta dos consultas: la primera selecciona solo los dispositivos gemelos que se encuentran en la planta **Redmond43**, y la segunda mejora la consulta para seleccionar solo los dispositivos que están también conectados a través de la red de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="f8c40-126">The previous code executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="f8c40-127">Tenga en cuenta que el código anterior, cuando crea el objeto de **consulta**, especifica un número máximo de documentos devueltos.</span><span class="sxs-lookup"><span data-stu-id="f8c40-127">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="f8c40-128">El objeto **consulta** contiene una propiedad booleana **hasMoreResults** que puede utilizar para invocar a los métodos **nextAsTwin** varias veces para recuperar todos los resultados.</span><span class="sxs-lookup"><span data-stu-id="f8c40-128">The **query** object contains a **hasMoreResults** boolean property that you can use to invoke the **nextAsTwin** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="f8c40-129">Un método llamado **siguiente** está disponible para los resultados que no son dispositivos gemelos, por ejemplo, los resultados de consultas de agregación.</span><span class="sxs-lookup"><span data-stu-id="f8c40-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span></span>
6. <span data-ttu-id="f8c40-130">Ejecute la aplicación con:</span><span class="sxs-lookup"><span data-stu-id="f8c40-130">Run the application with:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="f8c40-131">Debería ver un dispositivo en los resultados de la consulta que pregunta por todos los dispositivos que se encuentran en **Redmond43** y ninguno para la consulta que restringe los resultados a los dispositivos que utilizan una red de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="f8c40-131">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![][1]

<span data-ttu-id="f8c40-132">En la siguiente sección, creará una aplicación de dispositivo que notifica la información de conectividad y cambia el resultado de la consulta en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="f8c40-132">In the next section you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="f8c40-133">Creación de la aplicación del dispositivo</span><span class="sxs-lookup"><span data-stu-id="f8c40-133">Create the device app</span></span>
<span data-ttu-id="f8c40-134">En esta sección, creará una aplicación de consola de Node.js que se conecta al centro como **myDeviceId**, y luego actualiza las propiedades notificadas de su dispositivo gemelo para contener la información que está conectada mediante una red de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="f8c40-134">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its device twin's reported properties to contain the information that it is connected using a cellular network.</span></span>

> [!NOTE]
> <span data-ttu-id="f8c40-135">En la actualidad, solo se puede acceder a los dispositivos gemelos desde dispositivos conectados a IoT Hub mediante el protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="f8c40-135">At this time, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="f8c40-136">Para instrucciones acerca de cómo convertir la aplicación de dispositivo existente para usar MQTT, consulte el artículo sobre [compatibilidad con MQTT][lnk-devguide-mqtt].</span><span class="sxs-lookup"><span data-stu-id="f8c40-136">Please refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>
> 
> 

1. <span data-ttu-id="f8c40-137">Cree una nueva carpeta vacía denominada **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="f8c40-137">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="f8c40-138">En la carpeta **reportconnectivity** , cree un nuevo archivo package.json con el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="f8c40-138">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="f8c40-139">Acepte todos los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="f8c40-139">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="f8c40-140">En el símbolo del sistema, en la carpeta **reportconnectivity**, ejecute el siguiente comando para instalar **azure-iot-device** y el paquete **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="f8c40-140">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="f8c40-141">Con un editor de texto, cree un nuevo archivo **ReportConnectivity.js** en la carpeta **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="f8c40-141">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
4. <span data-ttu-id="f8c40-142">Agregue el código siguiente al archivo **ReportConnectivity.js** y sustituya el marcador de posición **{device connection string}** con la cadena de conexión que copió al crear la identidad de dispositivo **myDeviceId**:</span><span class="sxs-lookup"><span data-stu-id="f8c40-142">Add the following code to the **ReportConnectivity.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="f8c40-143">El objeto **Cliente** expone todos los métodos necesarios para interactuar con dispositivos gemelos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f8c40-143">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="f8c40-144">El código anterior, una vez que inicialice el objeto **Cliente**, recupera el dispositivo gemelo de **myDeviceId**, y actualiza su propiedad notificada con la información de conectividad.</span><span class="sxs-lookup"><span data-stu-id="f8c40-144">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
5. <span data-ttu-id="f8c40-145">Ejecute la aplicación del dispositivo</span><span class="sxs-lookup"><span data-stu-id="f8c40-145">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="f8c40-146">Verá el mensaje `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="f8c40-146">You should see the message `twin state reported`.</span></span>
6. <span data-ttu-id="f8c40-147">Ahora que el dispositivo ha informado sobre su información de conectividad, debe aparecer en ambas consultas.</span><span class="sxs-lookup"><span data-stu-id="f8c40-147">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="f8c40-148">Vuelva a la carpeta **addtagsandqueryapp** y vuelva a ejecutar las consultas:</span><span class="sxs-lookup"><span data-stu-id="f8c40-148">Go back in the **addtagsandqueryapp** folder and run the queries again:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="f8c40-149">Esta vez **myDeviceId** debe aparecer en los resultados de ambas consulta.</span><span class="sxs-lookup"><span data-stu-id="f8c40-149">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][3]

## <a name="next-steps"></a><span data-ttu-id="f8c40-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f8c40-150">Next steps</span></span>
<span data-ttu-id="f8c40-151">En este tutorial, configuró un centro de IoT nuevo en Azure Portal y, después, creó una identidad de dispositivo en el registro de identidades del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="f8c40-151">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="f8c40-152">Ha agregado metadatos de dispositivo como etiquetas desde una aplicación back-end y ha escrito una aplicación de dispositivo simulado para notificar la información de conectividad de dispositivos en el dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="f8c40-152">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="f8c40-153">También ha aprendido cómo consultar esta información mediante el lenguaje de consulta de IoT Hub de tipo SQL.</span><span class="sxs-lookup"><span data-stu-id="f8c40-153">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="f8c40-154">Use los siguientes recursos para obtener información sobre cómo:</span><span class="sxs-lookup"><span data-stu-id="f8c40-154">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="f8c40-155">enviar telemetría desde dispositivos con el tutorial [Introducción a IoT Hub][lnk-iothub-getstarted];</span><span class="sxs-lookup"><span data-stu-id="f8c40-155">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="f8c40-156">configurar dispositivos mediante las propiedades deseadas del dispositivo gemelo con el tutorial [Uso de las propiedades deseadas para configurar dispositivos][lnk-twin-how-to-configure];</span><span class="sxs-lookup"><span data-stu-id="f8c40-156">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="f8c40-157">controlar los dispositivos de forma interactiva (por ejemplo, encender un ventilador desde una aplicación controlada por el usuario), con el tutorial [Uso de métodos directos][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="f8c40-157">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
