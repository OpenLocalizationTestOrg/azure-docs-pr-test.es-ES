---
title: "Metadatos de información de dispositivo en la solución de supervisión remota | Microsoft Docs"
description: "Una descripción de la supervisión remota de la solución preconfigurada de IoT de Azure y su arquitectura."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: f8fd452806a0a0b98cf8e434c9bd55700083a6c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="device-information-metadata-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="85647-103">Metadatos de información de dispositivo en la solución preconfigurada de supervisión remota</span><span class="sxs-lookup"><span data-stu-id="85647-103">Device information metadata in the remote monitoring preconfigured solution</span></span>

<span data-ttu-id="85647-104">La solución preconfigurada de supervisión remota del Conjunto de aplicaciones de IoT de Azure muestra un enfoque para administrar los metadatos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="85647-104">The Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="85647-105">En este artículo se describe el enfoque que adopta esta solución para que comprenda:</span><span class="sxs-lookup"><span data-stu-id="85647-105">This article outlines the approach this solution takes to enable you to understand:</span></span>

* <span data-ttu-id="85647-106">Qué metadatos de dispositivo almacena la solución.</span><span class="sxs-lookup"><span data-stu-id="85647-106">What device metadata the solution stores.</span></span>
* <span data-ttu-id="85647-107">Cómo la solución administra los metadatos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="85647-107">How the solution manages the device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="85647-108">Context</span><span class="sxs-lookup"><span data-stu-id="85647-108">Context</span></span>

<span data-ttu-id="85647-109">La solución preconfigurada de supervisión remota usa [Azure IoT Hub][lnk-iot-hub] para que los dispositivos puedan enviar datos a la nube.</span><span class="sxs-lookup"><span data-stu-id="85647-109">The remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] to enable your devices to send data to the cloud.</span></span> <span data-ttu-id="85647-110">La solución almacena información acerca de los dispositivos en tres ubicaciones diferentes:</span><span class="sxs-lookup"><span data-stu-id="85647-110">The solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="85647-111">La ubicación</span><span class="sxs-lookup"><span data-stu-id="85647-111">Location</span></span> | <span data-ttu-id="85647-112">Información almacenada</span><span class="sxs-lookup"><span data-stu-id="85647-112">Information stored</span></span> | <span data-ttu-id="85647-113">Implementación</span><span class="sxs-lookup"><span data-stu-id="85647-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="85647-114">Registro de identidad</span><span class="sxs-lookup"><span data-stu-id="85647-114">Identity registry</span></span> | <span data-ttu-id="85647-115">Identificador de dispositivo, claves de autenticación, estado habilitado</span><span class="sxs-lookup"><span data-stu-id="85647-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="85647-116">Integrado en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="85647-116">Built in to IoT Hub</span></span> |
| <span data-ttu-id="85647-117">Dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="85647-117">Device twins</span></span> | <span data-ttu-id="85647-118">Metadatos: propiedades notificadas, propiedades deseadas, etiquetas</span><span class="sxs-lookup"><span data-stu-id="85647-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="85647-119">Integrado en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="85647-119">Built in to IoT Hub</span></span> |
| <span data-ttu-id="85647-120">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="85647-120">Cosmos DB</span></span> | <span data-ttu-id="85647-121">Historial de comandos y métodos</span><span class="sxs-lookup"><span data-stu-id="85647-121">Command and method history</span></span> | <span data-ttu-id="85647-122">Personalizado para la solución</span><span class="sxs-lookup"><span data-stu-id="85647-122">Custom for solution</span></span> |

<span data-ttu-id="85647-123">IoT Hub incluye un [registro de identidad de dispositivo][lnk-identity-registry] para administrar el acceso a una instancia de IoT Hub y usa [dispositivos gemelos][lnk-device-twin] para administrar los metadatos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="85647-123">IoT Hub includes a [device identity registry][lnk-identity-registry] to manage access to an IoT hub and uses [device twins][lnk-device-twin] to manage device metadata.</span></span> <span data-ttu-id="85647-124">También hay un *registro de dispositivo* específico de la solución de supervisión remota que almacena el historial de comandos y métodos.</span><span class="sxs-lookup"><span data-stu-id="85647-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="85647-125">La solución de supervisión remota usa una base de datos de [Cosmos DB][lnk-docdb] para implementar un almacén personalizado para el historial de comandos y métodos.</span><span class="sxs-lookup"><span data-stu-id="85647-125">The remote monitoring solution uses a [Cosmos DB][lnk-docdb] database to implement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="85647-126">La solución preconfigurada de supervisión remota mantiene sincronizado el registro de identidad del dispositivo con la información de la base de datos de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="85647-126">The remote monitoring preconfigured solution keeps the device identity registry in sync with the information in the Cosmos DB database.</span></span> <span data-ttu-id="85647-127">Ambos utilizan el mismo id. de dispositivo para identificar de forma única cada dispositivo conectado a su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="85647-127">Both use the same device id to uniquely identify each device connected to your IoT hub.</span></span>

## <a name="device-metadata"></a><span data-ttu-id="85647-128">Metadatos del dispositivo</span><span class="sxs-lookup"><span data-stu-id="85647-128">Device metadata</span></span>

<span data-ttu-id="85647-129">IoT Hub mantiene un [dispositivo gemelo][lnk-device-twin] para cada dispositivo simulado y físico conectado a una solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="85647-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected to a remote monitoring solution.</span></span> <span data-ttu-id="85647-130">La solución utiliza dispositivos gemelos para administrar los metadatos asociados con los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="85647-130">The solution uses device twins to manage the metadata associated with devices.</span></span> <span data-ttu-id="85647-131">Un dispositivo gemelo es un documento JSON mantenido por IoT Hub. La solución utiliza la API de IoT Hub para interactuar con los dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="85647-131">A device twin is a JSON document maintained by IoT Hub, and the solution uses the IoT Hub API to interact with device twins.</span></span>

<span data-ttu-id="85647-132">Un dispositivo gemelo almacena tres tipos de metadatos:</span><span class="sxs-lookup"><span data-stu-id="85647-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="85647-133">Un dispositivo envía las *propiedades notificadas* a una instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="85647-133">*Reported properties* are sent to an IoT hub by a device.</span></span> <span data-ttu-id="85647-134">En la solución de supervisión remota, los dispositivos simulados envían las propiedades notificadas durante el inicio y en respuesta a comandos y métodos para **cambiar el estado del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="85647-134">In the remote monitoring solution, simulated devices send reported properties at start-up and in response to **Change device state** commands and methods.</span></span> <span data-ttu-id="85647-135">Puede ver las propiedades notificadas en la **lista de dispositivos** y en **Detalles del dispositivo** en el portal de la solución.</span><span class="sxs-lookup"><span data-stu-id="85647-135">You can view reported properties in the **Device list** and **Device details** in the solution portal.</span></span> <span data-ttu-id="85647-136">Las propiedades notificadas son de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="85647-136">Reported properties are read only.</span></span>
- <span data-ttu-id="85647-137">Los dispositivos recuperan *Las propiedades deseadas* desde IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="85647-137">*Desired properties* are retrieved from the IoT hub by devices.</span></span> <span data-ttu-id="85647-138">Es responsabilidad del dispositivo realizar cualquier cambio de configuración necesario en el mismo.</span><span class="sxs-lookup"><span data-stu-id="85647-138">It is the responsibility of the device to make any necessary configuration change on the device.</span></span> <span data-ttu-id="85647-139">También es responsabilidad del dispositivo notificar el cambio al concentrador como una propiedad notificada.</span><span class="sxs-lookup"><span data-stu-id="85647-139">It is also the responsibility of the device to report the change back to the hub as a reported property.</span></span> <span data-ttu-id="85647-140">Puede establecer un valor de propiedad deseada través del portal de la solución.</span><span class="sxs-lookup"><span data-stu-id="85647-140">You can set a desired property value through the solution portal.</span></span>
- <span data-ttu-id="85647-141">Las *etiquetas* solo existen en el dispositivo gemelo y nunca se sincronizan con un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="85647-141">*Tags* only exist in the device twin and are never synchronized with a device.</span></span> <span data-ttu-id="85647-142">Puede establecer los valores de etiqueta en el portal de la solución y usarlos al filtrar la lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="85647-142">You can set tag values in the solution portal and use them when you filter the list of devices.</span></span> <span data-ttu-id="85647-143">La solución también utiliza una etiqueta para identificar el icono para mostrar de un dispositivo en el portal de la solución.</span><span class="sxs-lookup"><span data-stu-id="85647-143">The solution also uses a tag to identify the icon to display for a device in the solution portal.</span></span>

<span data-ttu-id="85647-144">Las propiedades notificadas de ejemplo de los dispositivos simulados incluyen fabricante, número de modelo, latitud y longitud.</span><span class="sxs-lookup"><span data-stu-id="85647-144">Example reported properties from the simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="85647-145">Los dispositivos simulados también devuelven la lista de métodos admitidos como una propiedad notificada.</span><span class="sxs-lookup"><span data-stu-id="85647-145">Simulated devices also return the list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="85647-146">El código del dispositivo simulado solo usa las propiedades deseadas **Desired.Config.TemperatureMeanValue** y **Desired.Config.TelemetryInterval** para actualizar las propiedades notificadas devueltas a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="85647-146">The simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties sent back to IoT Hub.</span></span> <span data-ttu-id="85647-147">Todos los demás cambios de propiedades deseadas se omiten.</span><span class="sxs-lookup"><span data-stu-id="85647-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="85647-148">Un documento JSON de metadatos de información de dispositivo almacenado en la base de datos de Cosmos DB del Registro de dispositivos tiene la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="85647-148">A device information metadata JSON document stored in the device registry Cosmos DB database has the following structure:</span></span>

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> <span data-ttu-id="85647-149">La información de dispositivo también puede incluir metadatos para describir la telemetría que envía el dispositivo al Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="85647-149">Device information can also include metadata to describe the telemetry the device sends to IoT Hub.</span></span> <span data-ttu-id="85647-150">La solución de supervisión remota utiliza estos metadatos de telemetría para personalizar cómo se muestra en el panel la [telemetría dinámica][lnk-dynamic-telemetry].</span><span class="sxs-lookup"><span data-stu-id="85647-150">The remote monitoring solution uses this telemetry metadata to customize how the dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>

## <a name="lifecycle"></a><span data-ttu-id="85647-151">Ciclo de vida</span><span class="sxs-lookup"><span data-stu-id="85647-151">Lifecycle</span></span>

<span data-ttu-id="85647-152">Cuando se crea por primera vez un dispositivo en el portal de la solución, esta crea una entrada en la base de datos de Cosmos DB para almacenar el historial de comandos y métodos.</span><span class="sxs-lookup"><span data-stu-id="85647-152">When you first create a device in the solution portal, the solution creates an entry in the Cosmos DB database to store command and method history.</span></span> <span data-ttu-id="85647-153">En este punto, la solución también crea una entrada para el dispositivo en el Registro de identidad del dispositivo que genera las claves que usa el dispositivo para autenticarse en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="85647-153">At this point, the solution also creates an entry for the device in the device identity registry, which generates the keys the device uses to authenticate with IoT Hub.</span></span> <span data-ttu-id="85647-154">También crea un dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="85647-154">It also creates a device twin.</span></span>

<span data-ttu-id="85647-155">Cuando un dispositivo se conecta por primera vez a la solución, envía las propiedades notificadas y un mensaje de información de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="85647-155">When a device first connects to the solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="85647-156">Los valores de las propiedades notificadas se guardan automáticamente en el dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="85647-156">The reported property values are automatically saved in the device twin.</span></span> <span data-ttu-id="85647-157">Las propiedades notificadas incluyen el fabricante del dispositivo, el número de modelo, el número de serie y una lista de los métodos admitidos.</span><span class="sxs-lookup"><span data-stu-id="85647-157">The reported properties include the device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="85647-158">El mensaje de información del dispositivo incluye la lista de los comandos que admite el dispositivo e información sobre los parámetros de comando.</span><span class="sxs-lookup"><span data-stu-id="85647-158">The device information message includes the list of the commands the device supports including information about any command parameters.</span></span> <span data-ttu-id="85647-159">Cuando la solución recibe este mensaje, actualiza la información de dispositivo en la base de datos de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="85647-159">When the solution receives this message, it updates the device information in the Cosmos DB database.</span></span>

### <a name="view-and-edit-device-information-in-the-solution-portal"></a><span data-ttu-id="85647-160">Visualización y edición de la información de dispositivo en el portal de solución</span><span class="sxs-lookup"><span data-stu-id="85647-160">View and edit device information in the solution portal</span></span>

<span data-ttu-id="85647-161">En la lista de dispositivos del portal de la solución, aparecen, de forma predeterminada, las siguientes propiedades de dispositivo en forma de columnas: **Estado**, **Id. de dispositivo**, **Fabricante**, **Número de modelo**, **Número de serie**, **Firmware**, **Plataforma**, **Procesador** y **RAM instalada**.</span><span class="sxs-lookup"><span data-stu-id="85647-161">The device list in the solution portal displays the following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="85647-162">Puede personalizar las columnas haciendo clic en **Editor de columnas**.</span><span class="sxs-lookup"><span data-stu-id="85647-162">You can customize the columns by clicking **Column editor**.</span></span> <span data-ttu-id="85647-163">Las propiedades **Latitud** y **Longitud** controlan la ubicación en el mapa de Bing incluido en el panel.</span><span class="sxs-lookup"><span data-stu-id="85647-163">The device properties **Latitude** and **Longitude** drive the location in the Bing Map on the dashboard.</span></span>

![Editor de columnas en la lista de dispositivos][img-device-list]

<span data-ttu-id="85647-165">En el panel **Detalles del dispositivo** del portal de la solución, puede editar las propiedades deseadas y las etiquetas (las propiedades notificadas son de solo lectura).</span><span class="sxs-lookup"><span data-stu-id="85647-165">In the **Device Details** pane in the solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![Panel de detalles del dispositivo][img-device-edit]

<span data-ttu-id="85647-167">Puede usar el portal de solución para quitar un dispositivo de la solución.</span><span class="sxs-lookup"><span data-stu-id="85647-167">You can use the solution portal to remove a device from your solution.</span></span> <span data-ttu-id="85647-168">Cuando se quita un dispositivo, la solución elimina la entrada de dispositivo del registro de identidad y, a continuación, elimina el dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="85647-168">When you remove a device, the solution removes the device entry from identity registry and then deletes the device twin.</span></span> <span data-ttu-id="85647-169">La solución también elimina la información relacionada con el dispositivo de la base de datos de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="85647-169">The solution also removes information related to the device from the Cosmos DB database.</span></span> <span data-ttu-id="85647-170">Para poder quitar un dispositivo, debe deshabilitarlo.</span><span class="sxs-lookup"><span data-stu-id="85647-170">Before you can remove a device, you must disable it.</span></span>

![Quitar dispositivo][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="85647-172">Procesamiento de mensajes de información de dispositivo</span><span class="sxs-lookup"><span data-stu-id="85647-172">Device information message processing</span></span>

<span data-ttu-id="85647-173">Los mensajes de información de dispositivo enviados por un dispositivo son distintos de los mensajes de telemetría.</span><span class="sxs-lookup"><span data-stu-id="85647-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="85647-174">Los mensajes de información de dispositivo incluyen los comandos a los que un dispositivo puede responder y el historial de comandos.</span><span class="sxs-lookup"><span data-stu-id="85647-174">Device information messages include the commands a device can respond to, and any command history.</span></span> <span data-ttu-id="85647-175">El propio Centro de IoT no conoce los metadatos contenidos en un mensaje de información de dispositivo y procesa el mensaje de la misma manera que cualquier mensaje del dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="85647-175">IoT Hub itself has no knowledge of the metadata contained in a device information message and processes the message in the same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="85647-176">En la solución de supervisión remota, un trabajo de [Azure Stream Analytics][lnk-stream-analytics] (ASA) lee los mensajes de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="85647-176">In the remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads the messages from IoT Hub.</span></span> <span data-ttu-id="85647-177">El trabajo **DeviceInfo** de Stream Analytics filtra los mensajes que contienen **"ObjectType": "DeviceInfo"** y los reenvía a la instancia del host **EventProcessorHost**, que se ejecuta en un trabajo web.</span><span class="sxs-lookup"><span data-stu-id="85647-177">The **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them to the **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="85647-178">La lógica de la instancia de **EventProcessorHost** utiliza el identificador de dispositivo para encontrar el registro de Cosmos DB del dispositivo específico y actualizarlo.</span><span class="sxs-lookup"><span data-stu-id="85647-178">Logic in the **EventProcessorHost** instance uses the device id to find the Cosmos DB record for the specific device and update the record.</span></span>

> [!NOTE]
> <span data-ttu-id="85647-179">Un mensaje de información de dispositivo es un mensaje estándar del dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="85647-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="85647-180">La solución distingue entre mensajes de información de dispositivo y mensajes de telemetría mediante consultas ASA.</span><span class="sxs-lookup"><span data-stu-id="85647-180">The solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85647-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="85647-181">Next steps</span></span>

<span data-ttu-id="85647-182">Ahora que ya ha terminado de aprender cómo personalizar las soluciones preconfiguradas, puede explorar algunas de las características y funcionalidades de las soluciones preconfiguradas del conjunto de aplicaciones de IoT:</span><span class="sxs-lookup"><span data-stu-id="85647-182">Now you've finished learning how you can customize the preconfigured solutions, you can explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="85647-183">[Información general de la solución preconfigurada de mantenimiento predictivo][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="85647-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="85647-184">[Preguntas más frecuentes sobre el Conjunto de aplicaciones de IoT][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="85647-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="85647-185">[Seguridad de Internet de las cosas desde el principio][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="85647-185">[IoT security from the ground up][lnk-security-groundup]</span></span>

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
