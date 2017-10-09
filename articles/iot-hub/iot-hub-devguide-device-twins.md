---
title: ': los gemelos de aaaUnderstand centro de IoT de Azure dispositivo | Documentos de Microsoft'
description: "Guía del desarrollador - utilizar dispositivo gemelos toosynchronize los datos de estado y la configuración entre los dispositivos y el centro de IoT"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="a8283-103">Dispositivos gemelos en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="a8283-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="a8283-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a8283-104">Overview</span></span>
<span data-ttu-id="a8283-105">Los *dispositivos gemelos* son documentos JSON que almacenan información sobre el estado de los dispositivos (metadatos, configuraciones y condiciones).</span><span class="sxs-lookup"><span data-stu-id="a8283-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="a8283-106">Centro de IoT conserva a un gemelas de dispositivo para cada dispositivo que conecte tooIoT concentrador.</span><span class="sxs-lookup"><span data-stu-id="a8283-106">IoT Hub persists a device twin for each device that you connect tooIoT Hub.</span></span> <span data-ttu-id="a8283-107">En este artículo se describe:</span><span class="sxs-lookup"><span data-stu-id="a8283-107">This article describes:</span></span>

* <span data-ttu-id="a8283-108">Hola estructura de gemelas de dispositivo de hello: *etiquetas*, *deseado* y *notificado propiedades*, y</span><span class="sxs-lookup"><span data-stu-id="a8283-108">hello structure of hello device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="a8283-109">operaciones de Hola que aplicaciones para dispositivos y back-ends pueden realizar en: los gemelos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a8283-109">hello operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="a8283-110">Actualmente, están accesibles sólo desde los dispositivos que se conectan tooIoT concentrador: los gemelos de dispositivo mediante el protocolo MQTT Hola.</span><span class="sxs-lookup"><span data-stu-id="a8283-110">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="a8283-111">Consulte toohello [compatibilidad MQTT] [ lnk-devguide-mqtt] artículo para obtener instrucciones sobre cómo toouse de aplicación de dispositivo existente de tooconvert MQTT.</span><span class="sxs-lookup"><span data-stu-id="a8283-111">Refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

### <a name="when-toouse"></a><span data-ttu-id="a8283-112">Cuando toouse</span><span class="sxs-lookup"><span data-stu-id="a8283-112">When toouse</span></span>
<span data-ttu-id="a8283-113">Use los dispositivos gemelos para:</span><span class="sxs-lookup"><span data-stu-id="a8283-113">Use device twins to:</span></span>

* <span data-ttu-id="a8283-114">Almacenar metadatos específicos del dispositivo en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8283-114">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="a8283-115">Por ejemplo, hello ubicación de implementación de una máquina expendedora.</span><span class="sxs-lookup"><span data-stu-id="a8283-115">For example, hello deployment location of a vending machine.</span></span>
* <span data-ttu-id="a8283-116">Notificar la información sobre el estado actual, como las funcionalidades y las condiciones disponibles de la aplicación del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a8283-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="a8283-117">Por ejemplo, un dispositivo está conectado tooyour centro de IoT over móvil o Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="a8283-117">For example, a device is connected tooyour IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="a8283-118">Sincronizar el estado de Hola de flujos de trabajo de larga duración entre la aplicación para dispositivos y aplicaciones back-end.</span><span class="sxs-lookup"><span data-stu-id="a8283-118">Synchronize hello state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="a8283-119">Por ejemplo, cuando una copia de solución de hello final especifica Hola nueva tooinstall de versión de firmware e informes de aplicaciones de dispositivos de Hola Hola distintas fases del proceso de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8283-119">For example, when hello solution back end specifies hello new firmware version tooinstall, and hello device app reports hello various stages of hello update process.</span></span>
* <span data-ttu-id="a8283-120">Consultar los metadatos, la configuración o el estado del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a8283-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="a8283-121">Consulte demasiado[Guía de comunicación de dispositivos a la nube] [ lnk-d2c-guidance] para obtener instrucciones sobre el uso de propiedades notificados, mensajes del dispositivo a la nube o cargar el archivo.</span><span class="sxs-lookup"><span data-stu-id="a8283-121">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="a8283-122">Consulte demasiado[orientación para la comunicación en la nube para dispositivos] [ lnk-c2d-guidance] para obtener instrucciones sobre el uso de propiedades que desee, métodos directos o mensajes de la nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a8283-122">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="a8283-123">Dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="a8283-123">Device twins</span></span>
<span data-ttu-id="a8283-124">Los dispositivos gemelos almacenan información relacionada con el dispositivo que:</span><span class="sxs-lookup"><span data-stu-id="a8283-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="a8283-125">Extremos de dispositivo y de vuelta pueden utilizar configuración y las condiciones de dispositivo de toosynchronize.</span><span class="sxs-lookup"><span data-stu-id="a8283-125">Device and back ends can use toosynchronize device conditions and configuration.</span></span>
* <span data-ttu-id="a8283-126">Hola solución back-end puede usar tooquery y operaciones de ejecución prolongada de destino.</span><span class="sxs-lookup"><span data-stu-id="a8283-126">hello solution back end can use tooquery and target long-running operations.</span></span>

<span data-ttu-id="a8283-127">ciclo de vida de Hola de un doble de dispositivo está vinculado correspondiente toohello [identidad del dispositivo][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="a8283-127">hello lifecycle of a device twin is linked toohello corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="a8283-128">Los dispositivos gemelos se crean y se eliminan implícitamente cuando se crea o se elimina una nueva identidad de dispositivo en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a8283-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="a8283-129">Un dispositivo gemelo es un documento JSON que incluye:</span><span class="sxs-lookup"><span data-stu-id="a8283-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="a8283-130">**Etiquetas**.</span><span class="sxs-lookup"><span data-stu-id="a8283-130">**Tags**.</span></span> <span data-ttu-id="a8283-131">Puede leer de y escribir en una sección del documento JSON de Hola Hola back-end de la solución.</span><span class="sxs-lookup"><span data-stu-id="a8283-131">A section of hello JSON document that hello solution back end can read from and write to.</span></span> <span data-ttu-id="a8283-132">Las etiquetas no son aplicaciones de toodevice visible.</span><span class="sxs-lookup"><span data-stu-id="a8283-132">Tags are not visible toodevice apps.</span></span>
* <span data-ttu-id="a8283-133">**Propiedades deseadas**.</span><span class="sxs-lookup"><span data-stu-id="a8283-133">**Desired properties**.</span></span> <span data-ttu-id="a8283-134">Se utiliza junto con la configuración del dispositivo notificado propiedades toosynchronize o condiciones.</span><span class="sxs-lookup"><span data-stu-id="a8283-134">Used along with reported properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="a8283-135">Propiedades deseadas solo pueden establecerse por solución de hello volver final y pueden ser leídos por la aplicación de dispositivo de hello.</span><span class="sxs-lookup"><span data-stu-id="a8283-135">Desired properties can only be set by hello solution back end and can be read by hello device app.</span></span> <span data-ttu-id="a8283-136">aplicación de dispositivo de Hello también puede recibir una notificación en tiempo real de los cambios en las propiedades de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="a8283-136">hello device app can also be notified in real time of changes in hello desired properties.</span></span>
* <span data-ttu-id="a8283-137">**Propiedades notificadas**.</span><span class="sxs-lookup"><span data-stu-id="a8283-137">**Reported properties**.</span></span> <span data-ttu-id="a8283-138">Se utiliza junto con la configuración de dispositivo de toosynchronize de propiedades que desee o condiciones.</span><span class="sxs-lookup"><span data-stu-id="a8283-138">Used along with desired properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="a8283-139">Propiedades incluidos solo puede establecerse mediante la aplicación de dispositivo de hello y se pueden leer y consultar Hola solución back-end.</span><span class="sxs-lookup"><span data-stu-id="a8283-139">Reported properties can only be set by hello device app and can be read and queried by hello solution back end.</span></span>

<span data-ttu-id="a8283-140">Además, raíz de Hola de documento JSON de hello dispositivo gemelas contiene las propiedades de solo lectura de Hola de identidad hello de dispositivo correspondiente almacenado en hello [del registro de identidad][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="a8283-140">Additionally, hello root of hello device twin JSON document contains hello read-only properties from hello corresponding device identity stored in hello [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="a8283-141">Hola de ejemplo siguiente muestra a un documento JSON gemelas de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="a8283-141">hello following example shows a device twin JSON document:</span></span>

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

<span data-ttu-id="a8283-142">En el objeto raíz de hello, es propiedades del sistema de Hola y contenedor de objetos para `tags` y `reported` y `desired` propiedades.</span><span class="sxs-lookup"><span data-stu-id="a8283-142">In hello root object, are hello system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="a8283-143">Hola `properties` contenedor contiene algunos elementos de solo lectura (`$metadata`, `$etag`, y `$version`) descrito en hello [dispositivo gemelas metadatos] [ lnk-twin-metadata] y [ Simultaneidad optimista] [ lnk-concurrency] secciones.</span><span class="sxs-lookup"><span data-stu-id="a8283-143">hello `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in hello [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="a8283-144">Ejemplo de propiedad notificada</span><span class="sxs-lookup"><span data-stu-id="a8283-144">Reported property example</span></span>
<span data-ttu-id="a8283-145">En el ejemplo anterior de hello, gemelos de dispositivo de hello contiene un `batteryLevel` propiedad notificado por la aplicación de dispositivo de hello.</span><span class="sxs-lookup"><span data-stu-id="a8283-145">In hello previous example, hello device twin contains a `batteryLevel` property that is reported by hello device app.</span></span> <span data-ttu-id="a8283-146">Esta propiedad resulta posible tooquery y operar con dispositivos basados en el último nivel de batería notificado Hola.</span><span class="sxs-lookup"><span data-stu-id="a8283-146">This property makes it possible tooquery and operate on devices based on hello last reported battery level.</span></span> <span data-ttu-id="a8283-147">Otros ejemplos incluyen funciones de dispositivo informes de aplicación de dispositivo de Hola u opciones de conectividad.</span><span class="sxs-lookup"><span data-stu-id="a8283-147">Other examples include hello device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="a8283-148">Propiedades notificados simplifican los escenarios donde hello solución back-end está interesado en hello última conocida el valor de una propiedad.</span><span class="sxs-lookup"><span data-stu-id="a8283-148">Reported properties simplify scenarios where hello solution back end is interested in hello last known value of a property.</span></span> <span data-ttu-id="a8283-149">Use [mensajes del dispositivo a la nube] [ lnk-d2c] si Hola solución back-end debe tooprocess telemetría de dispositivo en forma de Hola de secuencias de eventos con marca de tiempo, como la serie temporal.</span><span class="sxs-lookup"><span data-stu-id="a8283-149">Use [device-to-cloud messages][lnk-d2c] if hello solution back end needs tooprocess device telemetry in hello form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="a8283-150">Ejemplo de propiedad deseada</span><span class="sxs-lookup"><span data-stu-id="a8283-150">Desired property example</span></span>
<span data-ttu-id="a8283-151">En el ejemplo anterior de hello, Hola `telemetryConfig` gemelas dispositivo deseado y back-end de soluciones de Hola y configuración de telemetría de Hola de hello dispositivos aplicación toosynchronize utiliza propiedades notificados para este dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a8283-151">In hello previous example, hello `telemetryConfig` device twin desired and reported properties are used by hello solution back end and hello device app toosynchronize hello telemetry configuration for this device.</span></span> <span data-ttu-id="a8283-152">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a8283-152">For example:</span></span>

1. <span data-ttu-id="a8283-153">Hola solución back-end establece la propiedad Hola deseado con el valor de configuración de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="a8283-153">hello solution back end sets hello desired property with hello desired configuration value.</span></span> <span data-ttu-id="a8283-154">Aquí es parte de hello del documento de hello con conjunto de propiedades de hello deseado:</span><span class="sxs-lookup"><span data-stu-id="a8283-154">Here is hello portion of hello document with hello desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="a8283-155">Hola del dispositivo es una notificación de cambio de hello inmediatamente si conectado o en hello en primer lugar la reconexión.</span><span class="sxs-lookup"><span data-stu-id="a8283-155">hello device app is notified of hello change immediately if connected, or at hello first reconnect.</span></span> <span data-ttu-id="a8283-156">Hello del dispositivo, a continuación, notifica Hola actualizar configuración (o una condición de error mediante hello `status` propiedad).</span><span class="sxs-lookup"><span data-stu-id="a8283-156">hello device app then reports hello updated configuration (or an error condition using hello `status` property).</span></span> <span data-ttu-id="a8283-157">Aquí es parte de Hola de hello notificado propiedades:</span><span class="sxs-lookup"><span data-stu-id="a8283-157">Here is hello portion of hello reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="a8283-158">Hola solución back-end puede realizar un seguimiento Hola resultados de la operación de configuración de hello en varios dispositivos, por [consultar] [ lnk-query] : los gemelos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a8283-158">hello solution back end can track hello results of hello configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="a8283-159">Hello fragmentos de código anteriores se muestran son ejemplos optimizado para mejorar la legibilidad, de una manera tooencode una configuración de dispositivo y su estado.</span><span class="sxs-lookup"><span data-stu-id="a8283-159">hello preceding snippets are examples, optimized for readability, of one way tooencode a device configuration and its status.</span></span> <span data-ttu-id="a8283-160">Centro de IoT no impone un esquema específico para gemelas de hello dispositivo desean y notifican propiedades en: los gemelos de hello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a8283-160">IoT Hub does not impose a specific schema for hello device twin desired and reported properties in hello device twins.</span></span>
> 
> 

<span data-ttu-id="a8283-161">Puede usar operaciones de larga duración: los gemelos toosynchronize como actualizaciones de firmware.</span><span class="sxs-lookup"><span data-stu-id="a8283-161">You can use twins toosynchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="a8283-162">Para obtener más información sobre cómo toouse propiedades toosynchronize y realizar un seguimiento de una operación larga en todos los dispositivos, consulte [uso deseado propiedades de dispositivos con tooconfigure][lnk-twin-properties].</span><span class="sxs-lookup"><span data-stu-id="a8283-162">For more information on how toouse properties toosynchronize and track a long running operation across devices, see [Use desired properties tooconfigure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="a8283-163">Operaciones de back-end</span><span class="sxs-lookup"><span data-stu-id="a8283-163">Back-end operations</span></span>
<span data-ttu-id="a8283-164">back-end de Hello solución funciona en gemelas de dispositivo de hello mediante hello las siguientes operaciones atómicas, expuestas a través de HTTP:</span><span class="sxs-lookup"><span data-stu-id="a8283-164">hello solution back end operates on hello device twin using hello following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="a8283-165">**Recuperación del dispositivo gemelo por el id**. Esta operación devuelve Hola dispositivo gemelas, incluidas las etiquetas y documentos deseado, notifican y propiedades del sistema.</span><span class="sxs-lookup"><span data-stu-id="a8283-165">**Retrieve device twin by id**. This operation returns hello device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="a8283-166">**Actualización parcial de los dispositivos gemelos**.</span><span class="sxs-lookup"><span data-stu-id="a8283-166">**Partially update device twin**.</span></span> <span data-ttu-id="a8283-167">Esta operación permite Hola solución back-end toopartially actualización hello las etiquetas o propiedades que desee en un doble de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a8283-167">This operation enables hello solution back end toopartially update hello tags or desired properties in a device twin.</span></span> <span data-ttu-id="a8283-168">actualización parcial de Hola se expresa como un documento JSON que agrega o actualiza cualquier propiedad.</span><span class="sxs-lookup"><span data-stu-id="a8283-168">hello partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="a8283-169">Se establecen demasiado`null` se quitan.</span><span class="sxs-lookup"><span data-stu-id="a8283-169">Properties set too`null` are removed.</span></span> <span data-ttu-id="a8283-170">Hello en el ejemplo siguiente se crea una nueva propiedad deseada con valor `{"newProperty": "newValue"}`, sobrescribe el valor existente de Hola de `existingProperty` con `"otherNewValue"`y quita `otherOldProperty`.</span><span class="sxs-lookup"><span data-stu-id="a8283-170">hello following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites hello existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="a8283-171">Se realiza ningún otro cambio tooexisting deseado propiedades o etiquetas:</span><span class="sxs-lookup"><span data-stu-id="a8283-171">No other changes are made tooexisting desired properties or tags:</span></span>
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. <span data-ttu-id="a8283-172">**Reemplazar propiedades deseadas**.</span><span class="sxs-lookup"><span data-stu-id="a8283-172">**Replace desired properties**.</span></span> <span data-ttu-id="a8283-173">Esta toocompletely de back-end de soluciones de Hola de operación permite sobrescribir todas las propiedades deseadas existentes y sustituir un nuevo documento JSON para `properties/desired`.</span><span class="sxs-lookup"><span data-stu-id="a8283-173">This operation enables hello solution back end toocompletely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="a8283-174">**Reemplazar etiquetas**.</span><span class="sxs-lookup"><span data-stu-id="a8283-174">**Replace tags**.</span></span> <span data-ttu-id="a8283-175">Esta toocompletely de back-end de soluciones de Hola de operación permite sobrescribir todas las etiquetas existentes y sustituir un nuevo documento JSON para `tags`.</span><span class="sxs-lookup"><span data-stu-id="a8283-175">This operation enables hello solution back end toocompletely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
5. <span data-ttu-id="a8283-176">**Recibir notificaciones gemelas**.</span><span class="sxs-lookup"><span data-stu-id="a8283-176">**Receive twin notifications**.</span></span> <span data-ttu-id="a8283-177">Esta operación permite toobe de back-end de soluciones de Hola una notificación cuando se modifican gemelas Hola.</span><span class="sxs-lookup"><span data-stu-id="a8283-177">This operation allows hello solution back end toobe notified when hello twin is modified.</span></span> <span data-ttu-id="a8283-178">toodo por lo tanto, la solución de IoT necesita toocreate una ruta e igual de origen de datos de hello tooset demasiado*twinChangeEvents*.</span><span class="sxs-lookup"><span data-stu-id="a8283-178">toodo so, your IoT solution needs toocreate a route and tooset hello Data Source equal too*twinChangeEvents*.</span></span> <span data-ttu-id="a8283-179">De forma predeterminada, no se envían notificaciones gemelas, es decir, no existen previamente tales rutas.</span><span class="sxs-lookup"><span data-stu-id="a8283-179">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="a8283-180">Si es demasiado alta tasa de Hola de cambio o por otras razones, como los errores internos, Hola centro de IoT puede enviar solo una notificación que contiene todos los cambios.</span><span class="sxs-lookup"><span data-stu-id="a8283-180">If hello rate of change is too high, or for other reasons, such as internal failures, hello IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="a8283-181">Por lo tanto, si la aplicación necesita registro y auditoría confiables de todos los estados intermedios, la recomendación sigue siendo usar mensajes D2C.</span><span class="sxs-lookup"><span data-stu-id="a8283-181">So, if your application needs reliable auditing and logging of all intermediate states, then it is still recommended that you use D2C messages.</span></span> <span data-ttu-id="a8283-182">mensaje de notificación de Hello gemelas incluye propiedades y cuerpo.</span><span class="sxs-lookup"><span data-stu-id="a8283-182">hello twin notification message includes properties, and body.</span></span>

    - <span data-ttu-id="a8283-183">Propiedades</span><span class="sxs-lookup"><span data-stu-id="a8283-183">Properties</span></span>

    | <span data-ttu-id="a8283-184">Nombre</span><span class="sxs-lookup"><span data-stu-id="a8283-184">Name</span></span> | <span data-ttu-id="a8283-185">Valor</span><span class="sxs-lookup"><span data-stu-id="a8283-185">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="a8283-186">$content-type</span><span class="sxs-lookup"><span data-stu-id="a8283-186">$content-type</span></span> | <span data-ttu-id="a8283-187">application/json</span><span class="sxs-lookup"><span data-stu-id="a8283-187">application/json</span></span> |
    <span data-ttu-id="a8283-188">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="a8283-188">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="a8283-189">Hora de envían de notificaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="a8283-189">Time when hello notification was sent</span></span> |
    <span data-ttu-id="a8283-190">$iothub-message-source</span><span class="sxs-lookup"><span data-stu-id="a8283-190">$iothub-message-source</span></span> | <span data-ttu-id="a8283-191">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="a8283-191">twinChangeEvents</span></span> |
    <span data-ttu-id="a8283-192">$content-encoding</span><span class="sxs-lookup"><span data-stu-id="a8283-192">$content-encoding</span></span> | <span data-ttu-id="a8283-193">utf-8</span><span class="sxs-lookup"><span data-stu-id="a8283-193">utf-8</span></span> |
    <span data-ttu-id="a8283-194">deviceId</span><span class="sxs-lookup"><span data-stu-id="a8283-194">deviceId</span></span> | <span data-ttu-id="a8283-195">Id. de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="a8283-195">Id of hello device</span></span> |
    <span data-ttu-id="a8283-196">hubName</span><span class="sxs-lookup"><span data-stu-id="a8283-196">hubName</span></span> | <span data-ttu-id="a8283-197">Nombre de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="a8283-197">Name of IoT Hub</span></span> |
    <span data-ttu-id="a8283-198">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="a8283-198">operationTimestamp</span></span> | <span data-ttu-id="a8283-199">Marca de tiempo [ISO8601] de operación</span><span class="sxs-lookup"><span data-stu-id="a8283-199">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="a8283-200">iothub-message-schema</span><span class="sxs-lookup"><span data-stu-id="a8283-200">iothub-message-schema</span></span> | <span data-ttu-id="a8283-201">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="a8283-201">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="a8283-202">opType</span><span class="sxs-lookup"><span data-stu-id="a8283-202">opType</span></span> | <span data-ttu-id="a8283-203">"replaceTwin" o "updateTwin"</span><span class="sxs-lookup"><span data-stu-id="a8283-203">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="a8283-204">Propiedades de sistema de mensajes tienen el prefijo hello `'$'` símbolos.</span><span class="sxs-lookup"><span data-stu-id="a8283-204">Message system properties are prefixed with hello `'$'` symbol.</span></span>

    - <span data-ttu-id="a8283-205">Cuerpo</span><span class="sxs-lookup"><span data-stu-id="a8283-205">Body</span></span>
        
    <span data-ttu-id="a8283-206">Esta sección incluye todos los cambios de hello gemelas en un formato JSON.</span><span class="sxs-lookup"><span data-stu-id="a8283-206">This section includes all hello twin changes in a JSON format.</span></span> <span data-ttu-id="a8283-207">Utiliza Hola mismo formato como una revisión, con la diferencia de Hola que TI puede contener todas las secciones de gemelas: etiquetas, properties.reported, properties.desired y que contiene elementos de Hola "$metadata".</span><span class="sxs-lookup"><span data-stu-id="a8283-207">It uses hello same format as a patch, with hello difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains hello “$metadata” elements.</span></span> <span data-ttu-id="a8283-208">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="a8283-208">For example,</span></span>
    ```
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ``` 

<span data-ttu-id="a8283-209">Todos los Hola compatibilidad anterior de operations [simultaneidad optimista] [ lnk-concurrency] y requieren hello **ServiceConnect** permiso, tal como se define en hello [seguridad ] [ lnk-security] artículo.</span><span class="sxs-lookup"><span data-stu-id="a8283-209">All hello preceding operations support [Optimistic concurrency][lnk-concurrency] and require hello **ServiceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="a8283-210">Además operaciones toothese, solución de hello realice copia final puede:</span><span class="sxs-lookup"><span data-stu-id="a8283-210">In addition toothese operations, hello solution back end can:</span></span>

* <span data-ttu-id="a8283-211">: Los gemelos de dispositivo de hello mediante Hola de consulta similar a SQL [lenguaje de consultas del centro de IoT][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="a8283-211">Query hello device twins using hello SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="a8283-212">Realizar operaciones en conjuntos grandes de dispositivos gemelos usando [trabajos][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="a8283-212">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="a8283-213">Operaciones de dispositivo</span><span class="sxs-lookup"><span data-stu-id="a8283-213">Device operations</span></span>
<span data-ttu-id="a8283-214">aplicación de dispositivo de Hello opera en gemelas de dispositivo de hello mediante las siguientes operaciones atómicas de hello:</span><span class="sxs-lookup"><span data-stu-id="a8283-214">hello device app operates on hello device twin using hello following atomic operations:</span></span>

1. <span data-ttu-id="a8283-215">**Recuperación del dispositivo gemelo**.</span><span class="sxs-lookup"><span data-stu-id="a8283-215">**Retrieve device twin**.</span></span> <span data-ttu-id="a8283-216">Esta operación devuelve el documento de hello dispositivo gemelas (incluidas las etiquetas y deseado, notifican y propiedades del sistema) de hello dispositivo está conectado actualmente.</span><span class="sxs-lookup"><span data-stu-id="a8283-216">This operation returns hello device twin document (including tags and desired, reported and system properties) for hello currently connected device.</span></span>
2. <span data-ttu-id="a8283-217">**Actualizar parcialmente propiedades notificadas**.</span><span class="sxs-lookup"><span data-stu-id="a8283-217">**Partially update reported properties**.</span></span> <span data-ttu-id="a8283-218">Esta actualización parcial de operación habilita Hola de hello informó de propiedades de dispositivo de hello conectado actualmente.</span><span class="sxs-lookup"><span data-stu-id="a8283-218">This operation enables hello partial update of hello reported properties of hello currently connected device.</span></span> <span data-ttu-id="a8283-219">Este Hola de usos de operación actualizar JSON mismo formato que Hola solución back-end usa para una actualización parcial de propiedades que desee.</span><span class="sxs-lookup"><span data-stu-id="a8283-219">This operation uses hello same JSON update format that hello solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="a8283-220">**Observar las propiedades deseadas**.</span><span class="sxs-lookup"><span data-stu-id="a8283-220">**Observe desired properties**.</span></span> <span data-ttu-id="a8283-221">dispositivo conectado actualmente Hola puede toobe una notificación de propiedades de toohello deseado de las actualizaciones que se produzcan.</span><span class="sxs-lookup"><span data-stu-id="a8283-221">hello currently connected device can choose toobe notified of updates toohello desired properties when they happen.</span></span> <span data-ttu-id="a8283-222">dispositivo de Hello recibe Hola mismo formulario de actualización (reemplazo completo o parcial) ejecuta Hola solución back-end.</span><span class="sxs-lookup"><span data-stu-id="a8283-222">hello device receives hello same form of update (partial or full replacement) executed by hello solution back end.</span></span>

<span data-ttu-id="a8283-223">Todas las operaciones anteriores de Hola requieren hello **DeviceConnect** permiso, tal como se define en hello [seguridad] [ lnk-security] artículo.</span><span class="sxs-lookup"><span data-stu-id="a8283-223">All hello preceding operations require hello **DeviceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="a8283-224">Hola [dispositivos de IoT de Azure SDK] [ lnk-sdks] facilitan hello toouse fácil anterior a las operaciones de muchos lenguajes y plataformas.</span><span class="sxs-lookup"><span data-stu-id="a8283-224">hello [Azure IoT device SDKs][lnk-sdks] make it easy toouse hello preceding operations from many languages and platforms.</span></span> <span data-ttu-id="a8283-225">Puede encontrar más información sobre los detalles de Hola de primitivas del centro de IoT para sincronización de propiedades que desee en [flujo de reconexión de dispositivo][lnk-reconnection].</span><span class="sxs-lookup"><span data-stu-id="a8283-225">More information on hello details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="a8283-226">Actualmente, están accesibles sólo desde los dispositivos que se conectan tooIoT concentrador: los gemelos de dispositivo mediante el protocolo MQTT Hola.</span><span class="sxs-lookup"><span data-stu-id="a8283-226">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="a8283-227">Temas de referencia:</span><span class="sxs-lookup"><span data-stu-id="a8283-227">Reference topics:</span></span>
<span data-ttu-id="a8283-228">Hello temas de referencia siguientes proporcionan más información sobre el centro de IoT de controlar acceso tooyour.</span><span class="sxs-lookup"><span data-stu-id="a8283-228">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="a8283-229">Formato de etiquetas y propiedades</span><span class="sxs-lookup"><span data-stu-id="a8283-229">Tags and properties format</span></span>
<span data-ttu-id="a8283-230">Etiquetas, propiedades deseadas y se notificará son objetos JSON con hello siguientes restricciones:</span><span class="sxs-lookup"><span data-stu-id="a8283-230">Tags, desired, and reported properties are JSON objects with hello following restrictions:</span></span>

* <span data-ttu-id="a8283-231">Todas las claves en objetos JSON son cadenas UNICODE UTF-8 de 64 caracteres que distinguen entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="a8283-231">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="a8283-232">Entre los caracteres permitidos no se incluyen los caracteres de control UNICODE (segmentos C0 y C1), ni `'.'`, `' '` y `'$'`.</span><span class="sxs-lookup"><span data-stu-id="a8283-232">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="a8283-233">Todos los valores en objetos JSON pueden ser de los siguientes tipos JSON de hello: un valor booleano, número, cadena, objeto.</span><span class="sxs-lookup"><span data-stu-id="a8283-233">All values in JSON objects can be of hello following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="a8283-234">No se permiten matrices.</span><span class="sxs-lookup"><span data-stu-id="a8283-234">Arrays are not allowed.</span></span>
* <span data-ttu-id="a8283-235">Todos los objetos JSON en etiquetas y propiedades deseadas y notificadas pueden tener una profundidad máxima de 5.</span><span class="sxs-lookup"><span data-stu-id="a8283-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="a8283-236">Por ejemplo, hello después el objeto es válido:</span><span class="sxs-lookup"><span data-stu-id="a8283-236">For instance, hello following object is valid:</span></span>

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* <span data-ttu-id="a8283-237">Todos los valores de cadena pueden tener como máximo una longitud de 512 bytes.</span><span class="sxs-lookup"><span data-stu-id="a8283-237">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="a8283-238">Tamaño del dispositivo gemelo</span><span class="sxs-lookup"><span data-stu-id="a8283-238">Device twin size</span></span>
<span data-ttu-id="a8283-239">Centro de IoT exige una limitación de tamaño de 8KB en valores de hello de `tags`, `properties/desired`, y `properties/reported`, excluir elementos de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="a8283-239">IoT Hub enforces an 8KB size limitation on hello values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="a8283-240">Hello tamaño se calcula el recuento de todos los caracteres excepto UNICODE controlan caracteres (segmentos C0 y C1) y los espacios `' '` cuando aparece fuera de una constante de cadena.</span><span class="sxs-lookup"><span data-stu-id="a8283-240">hello size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="a8283-241">Centro de IoT rechaza con un error todas las operaciones que podrían aumentar el tamaño de Hola de esos documentos por encima del límite de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8283-241">IoT Hub rejects with an error all operations that would increase hello size of those documents above hello limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="a8283-242">Metadatos de dispositivo gemelo</span><span class="sxs-lookup"><span data-stu-id="a8283-242">Device twin metadata</span></span>
<span data-ttu-id="a8283-243">Centro de IoT mantiene Hola marca de tiempo de la última actualización de Hola para cada objeto JSON de gemelas dispositivo deseado y notifica propiedades.</span><span class="sxs-lookup"><span data-stu-id="a8283-243">IoT Hub maintains hello timestamp of hello last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="a8283-244">las marcas de tiempo de Hello en formato UTC y codifica en hello [ISO8601] formato `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span><span class="sxs-lookup"><span data-stu-id="a8283-244">hello timestamps are in UTC and encoded in hello [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="a8283-245">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a8283-245">For example:</span></span>

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

<span data-ttu-id="a8283-246">Esta información se mantiene en cada nivel actualizaciones de toopreserve (hojas de hello no solo de hello estructura JSON) que quitar claves de objeto.</span><span class="sxs-lookup"><span data-stu-id="a8283-246">This information is kept at every level (not just hello leaves of hello JSON structure) toopreserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="a8283-247">Simultaneidad optimista</span><span class="sxs-lookup"><span data-stu-id="a8283-247">Optimistic concurrency</span></span>
<span data-ttu-id="a8283-248">Tanto las etiquetas como las propiedades deseadas y notificadas admiten la simultaneidad optimista.</span><span class="sxs-lookup"><span data-stu-id="a8283-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="a8283-249">Las etiquetas tienen un valor de ETag, como por [RFC7232], que representa la representación JSON de la etiqueta de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8283-249">Tags have an ETag, as per [RFC7232], that represents hello tag's JSON representation.</span></span> <span data-ttu-id="a8283-250">Puede usar ETags en operaciones de actualización condicional de coherencia de tooensure de back-end de soluciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8283-250">You can use ETags in conditional update operations from hello solution back end tooensure consistency.</span></span>

<span data-ttu-id="a8283-251">Gemelas dispositivo deseado y notifica propiedades no tienen valores de ETag, pero tienen un `$version` valor confirmado toobe incremental.</span><span class="sxs-lookup"><span data-stu-id="a8283-251">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed toobe incremental.</span></span> <span data-ttu-id="a8283-252">De igual forma tooan ETag, versión de Hola puede utilizarse por hello coherencia tooenforce de entidad de las actualizaciones de la actualización.</span><span class="sxs-lookup"><span data-stu-id="a8283-252">Similarly tooan ETag, hello version can be used by hello updating party tooenforce consistency of updates.</span></span> <span data-ttu-id="a8283-253">Por ejemplo, una aplicación de dispositivo para un notificado propiedad o hello solución back-end para una propiedad deseada.</span><span class="sxs-lookup"><span data-stu-id="a8283-253">For example, a device app for a reported property or hello solution back end for a desired property.</span></span>

<span data-ttu-id="a8283-254">Versiones también son útiles cuando un agente de observación (por ejemplo, la aplicación de dispositivo de hello observar propiedades Hola deseado) deberá conciliar los carreras entre una notificación de actualización y el resultado de hello de una operación de recuperación.</span><span class="sxs-lookup"><span data-stu-id="a8283-254">Versions are also useful when an observing agent (such as hello device app observing hello desired properties) must reconcile races between hello result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="a8283-255">Hola sección [flujo de reconexión de dispositivo] [ lnk-reconnection] proporciona más información.</span><span class="sxs-lookup"><span data-stu-id="a8283-255">hello section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="a8283-256">Flujo de reconexión de dispositivos</span><span class="sxs-lookup"><span data-stu-id="a8283-256">Device reconnection flow</span></span>
<span data-ttu-id="a8283-257">IoT Hub no conserva las notificaciones de actualización de las propiedades deseadas para los dispositivos desconectados.</span><span class="sxs-lookup"><span data-stu-id="a8283-257">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="a8283-258">Después de que un dispositivo que se está conectando debe recuperar el documento de todas las propiedades deseadas de hello, en toosubscribing de suma para notificaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="a8283-258">It follows that a device that is connecting must retrieve hello full desired properties document, in addition toosubscribing for update notifications.</span></span> <span data-ttu-id="a8283-259">Dada la posibilidad de Hola de carreras entre notificaciones de actualización y la recuperación completa, debe garantizarse Hola siga flujo:</span><span class="sxs-lookup"><span data-stu-id="a8283-259">Given hello possibility of races between update notifications and full retrieval, hello following flow must be ensured:</span></span>

1. <span data-ttu-id="a8283-260">Aplicación de dispositivo conecta tooan centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="a8283-260">Device app connects tooan IoT hub.</span></span>
2. <span data-ttu-id="a8283-261">La aplicación de dispositivo se suscribe a las notificaciones de actualización de las propiedades deseadas.</span><span class="sxs-lookup"><span data-stu-id="a8283-261">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="a8283-262">Aplicación de dispositivo recupera el documento "hello" completo de propiedades que desee.</span><span class="sxs-lookup"><span data-stu-id="a8283-262">Device app retrieves hello full document for desired properties.</span></span>

<span data-ttu-id="a8283-263">aplicación de dispositivo de Hello puede pasar por alto todas las notificaciones con `$version` inferior o igual a la versión de Hola de documento recuperado "hello" completo.</span><span class="sxs-lookup"><span data-stu-id="a8283-263">hello device app can ignore all notifications with `$version` less or equal than hello version of hello full retrieved document.</span></span> <span data-ttu-id="a8283-264">Este enfoque es posible porque IoT Hub garantiza que las versiones siempre se incrementan.</span><span class="sxs-lookup"><span data-stu-id="a8283-264">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="a8283-265">Esta lógica se ha implementado en hello [dispositivos de IoT de Azure SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="a8283-265">This logic is already implemented in hello [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="a8283-266">Esta descripción es útil sólo si Hola del dispositivo no puede usar cualquiera de los dispositivos de IoT de Azure SDK y debe programar la interfaz de hello MQTT directamente.</span><span class="sxs-lookup"><span data-stu-id="a8283-266">This description is useful only if hello device app cannot use any of Azure IoT device SDKs and must program hello MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="a8283-267">Material de referencia adicional</span><span class="sxs-lookup"><span data-stu-id="a8283-267">Additional reference material</span></span>
<span data-ttu-id="a8283-268">Otros temas de referencia en la Guía del desarrollador de centro de IoT Hola incluyen:</span><span class="sxs-lookup"><span data-stu-id="a8283-268">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="a8283-269">Hola [los extremos del centro de IoT] [ lnk-endpoints] artículo describe Hola varios extremos que cada centro de IoT expone las operaciones de tiempo de ejecución y administración.</span><span class="sxs-lookup"><span data-stu-id="a8283-269">hello [IoT Hub endpoints][lnk-endpoints] article describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="a8283-270">Hola [limitación y las cuotas] [ lnk-quotas] artículo describen las cuotas de Hola que se aplican toohello servicio del centro de IoT y Hola limitación tooexpect de comportamiento cuando se usa el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8283-270">hello [Throttling and quotas][lnk-quotas] article describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="a8283-271">Hola [SDK de dispositivos y servicios de Azure IoT] [ lnk-sdks] listas de artículo Hola SDK idioma puede usar cuando se desarrollan aplicaciones de dispositivos y servicios que interactúan con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="a8283-271">hello [Azure IoT device and service SDKs][lnk-sdks] article lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="a8283-272">Hola [lenguaje de consulta de centro de IoT para: los gemelos de dispositivo, los trabajos y el enrutamiento de mensajes] [ lnk-query] artículo describe Hola lenguaje de consultas del centro de IoT puede usar información de tooretrieve centro de IoT de: los gemelos de dispositivo y trabajos .</span><span class="sxs-lookup"><span data-stu-id="a8283-272">hello [IoT Hub query language for device twins, jobs, and message routing][lnk-query] article describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="a8283-273">Hola [compatibilidad IoT Hub MQTT] [ lnk-devguide-mqtt] artículo proporciona más información acerca del soporte técnico de centro de IoT para el protocolo MQTT Hola.</span><span class="sxs-lookup"><span data-stu-id="a8283-273">hello [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8283-274">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a8283-274">Next steps</span></span>
<span data-ttu-id="a8283-275">Ahora que ha aprendido: los gemelos de dispositivo, es posible que interesa Hola temas de guía para desarrolladores de centro de IoT siguientes:</span><span class="sxs-lookup"><span data-stu-id="a8283-275">Now you have learned about device twins, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="a8283-276">[Invocación de un método directo en un dispositivo][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="a8283-276">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="a8283-277">[Programación de trabajos en varios dispositivos][lnk-jobs]</span><span class="sxs-lookup"><span data-stu-id="a8283-277">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="a8283-278">Si desea que tootry algunos de los conceptos de hello descritos en este artículo, es posible que interesa Hola centro de IoT tutoriales:</span><span class="sxs-lookup"><span data-stu-id="a8283-278">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="a8283-279">[¿Cómo toouse Hola gemelas de dispositivo][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="a8283-279">[How toouse hello device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="a8283-280">[¿Cómo toouse dispositivo dos propiedades][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="a8283-280">[How toouse device twin properties][lnk-twin-properties]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png
