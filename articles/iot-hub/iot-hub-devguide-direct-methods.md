---
title: "Información de los métodos directos de IoT Hub de Azure | Microsoft Docs"
description: "Guía del desarrollador: uso de métodos directos para invocar código en los dispositivos de una aplicación de servicio."
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 77e788a32097edbcb1cd4faaa45f35812eabd94a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="f6ddb-103">Conocimiento e invocación de los métodos directos de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="f6ddb-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="f6ddb-104">Información general</span><span class="sxs-lookup"><span data-stu-id="f6ddb-104">Overview</span></span>
<span data-ttu-id="f6ddb-105">IoT Hub ofrece la posibilidad de invocar métodos directos en dispositivos desde la nube.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-105">IoT Hub gives you ability to invoke direct methods on devices from the cloud.</span></span> <span data-ttu-id="f6ddb-106">Los métodos directos representan una interacción solicitud-respuesta con un dispositivo similar a una llamada HTTP en la cual se completan correctamente o generan un error de inmediato (tras un tiempo de espera que especifica el usuario).</span><span class="sxs-lookup"><span data-stu-id="f6ddb-106">Direct methods represent a request-reply interaction with a device similar to an HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="f6ddb-107">Esto es útil para escenarios en los que la línea de acción inmediata difiere en función de si el dispositivo respondió, por ejemplo, enviando una reactivación por SMS a un dispositivo si este está sin conexión (enviar un SMS cuesta más que una llamada de método).</span><span class="sxs-lookup"><span data-stu-id="f6ddb-107">This is useful for scenarios where the course of immediate action is different depending on whether the device was able to respond, such as sending an SMS wake-up to a device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="f6ddb-108">Cada método de dispositivo se dirige a un único dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-108">Each device method targets a single device.</span></span> <span data-ttu-id="f6ddb-109">Los [trabajos][lnk-devguide-jobs] proporcionan una manera de invocar métodos directos en varios dispositivos y de programar la invocación de métodos para los dispositivos desconectados.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-109">[Jobs][lnk-devguide-jobs] provide a way to invoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="f6ddb-110">Cualquier persona con permisos de **conexión de servicio** en IoT Hub pueden invocar un método en un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="f6ddb-111">Cuándo se deben usar</span><span class="sxs-lookup"><span data-stu-id="f6ddb-111">When to use</span></span>
<span data-ttu-id="f6ddb-112">Los métodos directos siguen un patrón de solicitud-respuesta y se usan para las comunicaciones que necesitan confirmación inmediata de su resultado, normalmente control interactivo del dispositivo, por ejemplo, encender un ventilador.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of the device, for example to turn on a fan.</span></span>

<span data-ttu-id="f6ddb-113">Si duda entre el uso de las propiedades deseadas, los métodos directos o los mensajes de nube a dispositivo, consulte [Cloud-to-device communication guidance][lnk-c2d-guidance] (Guía de comunicaciones de nube a dispositivo).</span><span class="sxs-lookup"><span data-stu-id="f6ddb-113">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="f6ddb-114">Ciclo de vida de los métodos</span><span class="sxs-lookup"><span data-stu-id="f6ddb-114">Method lifecycle</span></span>
<span data-ttu-id="f6ddb-115">Los métodos directos se implementan en el dispositivo y pueden requerir de ninguna entrada a varias en la carga de método para crear instancias correctamente.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-115">Direct methods are implemented on the device and may require zero or more inputs in the method payload to correctly instantiate.</span></span> <span data-ttu-id="f6ddb-116">Se invoca un método directo mediante un URI orientado al servicio (`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="f6ddb-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="f6ddb-117">Un dispositivo recibe métodos directos a través de un tema MQTT específico del dispositivo (`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="f6ddb-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="f6ddb-118">Es posible que más adelante se admitan métodos directos en otros protocolos de red del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-118">We may support direct methods on additional device-side networking protocols in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="f6ddb-119">Cuando se invoca un método directo en un dispositivo, los valores y los nombres de propiedad solo pueden contener caracteres alfanuméricos US-ASCII imprimibles, excepto los del siguiente conjunto: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="f6ddb-120">Los métodos directos son sincrónicos y se completan correctamente o producen un error tras el período de tiempo de espera (valor predeterminado: 30 segundos; valor máximo: 3600 segundos).</span><span class="sxs-lookup"><span data-stu-id="f6ddb-120">Direct methods are synchronous and either succeed or fail after the timeout period (default: 30 seconds, settable up to 3600 seconds).</span></span> <span data-ttu-id="f6ddb-121">Los métodos directos son útiles en escenarios interactivos en los que quiere que un dispositivo actúe únicamente si está conectado y recibiendo comandos, como encender una luz desde un teléfono.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-121">Direct methods are useful in interactive scenarios where you want a device to act if and only if the device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="f6ddb-122">En estos escenarios, quiere saber de inmediato si la acción se ha completado o no para que el servicio en la nube pueda actuar lo antes posible en función del resultado.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-122">In these scenarios, you want to see an immediate success or failure so the cloud service can act on the result as soon as possible.</span></span> <span data-ttu-id="f6ddb-123">El dispositivo puede devolver un cuerpo de mensaje como resultado del método, pero no es necesario que el método lo haga.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-123">The device may return some message body as a result of the method, but it isn't required for the method to do so.</span></span> <span data-ttu-id="f6ddb-124">No hay ninguna garantía respecto al orden o la semántica de simultaneidad en las llamadas de método.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="f6ddb-125">El método directo es solo HTTP desde el lado de la nube y solo MQTT desde el lado del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-125">Direct method are HTTP-only from the cloud side, and MQTT-only from the device side.</span></span>

<span data-ttu-id="f6ddb-126">La carga útil de solicitudes y respuestas del método es un documento JSON de hasta 8 KB.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-126">The payload for method requests and responses is a JSON document up to 8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="f6ddb-127">Temas de referencia:</span><span class="sxs-lookup"><span data-stu-id="f6ddb-127">Reference topics:</span></span>
<span data-ttu-id="f6ddb-128">Los siguientes temas de referencia proporcionan más información sobre el uso de métodos directos.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-128">The following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="f6ddb-129">Invocación de un método directo desde una aplicación de back-end</span><span class="sxs-lookup"><span data-stu-id="f6ddb-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="f6ddb-130">Invocación de método</span><span class="sxs-lookup"><span data-stu-id="f6ddb-130">Method invocation</span></span>
<span data-ttu-id="f6ddb-131">Las invocaciones de método directo en un dispositivo son llamadas HTTP compuestas por:</span><span class="sxs-lookup"><span data-stu-id="f6ddb-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="f6ddb-132">El *URI* específico del dispositivo (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="f6ddb-132">The *URI* specific to the device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="f6ddb-133">El *método* POST</span><span class="sxs-lookup"><span data-stu-id="f6ddb-133">The POST *method*</span></span>
* <span data-ttu-id="f6ddb-134">*Encabezados* que contienen la autorización, el id. de solicitud, el tipo de contenido y la codificación del contenido</span><span class="sxs-lookup"><span data-stu-id="f6ddb-134">*Headers* which contain the authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="f6ddb-135">Un *cuerpo* JSON transparente en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="f6ddb-135">A transparent JSON *body* in the following format:</span></span>

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

<span data-ttu-id="f6ddb-136">El tiempo de espera se expresa en segundos.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-136">Timeout is in seconds.</span></span> <span data-ttu-id="f6ddb-137">Si no se establece el tiempo de espera, el valor predeterminado es 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-137">If timeout is not set, it defaults to 30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="f6ddb-138">Response</span><span class="sxs-lookup"><span data-stu-id="f6ddb-138">Response</span></span>
<span data-ttu-id="f6ddb-139">La aplicación de back-end recibe una respuesta que consta de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f6ddb-139">The back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="f6ddb-140">*Código de estado HTTP*, que se usa para errores procedentes de IoT Hub, incluido el error 404 para los dispositivos que no estén conectados</span><span class="sxs-lookup"><span data-stu-id="f6ddb-140">*HTTP status code*, which is used for errors coming from the IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="f6ddb-141">*Encabezados* que contienen la etiqueta ETag, el identificador de solicitud, el tipo de contenido y la codificación del contenido</span><span class="sxs-lookup"><span data-stu-id="f6ddb-141">*Headers* which contain the ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="f6ddb-142">Un *cuerpo* JSON en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="f6ddb-142">A JSON *body* in the following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="f6ddb-143">El dispositivo proporciona tanto `status` como `body`, que se utilizan para responder con el código de estado o la descripción propios del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-143">Both `status` and `body` are provided by the device and used to respond with the device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="f6ddb-144">Control de un método directo en un dispositivo</span><span class="sxs-lookup"><span data-stu-id="f6ddb-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="f6ddb-145">Invocación de método</span><span class="sxs-lookup"><span data-stu-id="f6ddb-145">Method invocation</span></span>
<span data-ttu-id="f6ddb-146">Los dispositivos reciben las solicitudes de método directo en el tema MQTT: `$iothub/methods/POST/{method name}/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-146">Devices receive direct method requests on the MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="f6ddb-147">El cuerpo que recibe el dispositivo está en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="f6ddb-147">The body which the device receives is in the following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="f6ddb-148">Las solicitudes de método son QoS 0.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="f6ddb-149">Response</span><span class="sxs-lookup"><span data-stu-id="f6ddb-149">Response</span></span>
<span data-ttu-id="f6ddb-150">El dispositivo envía las respuestas a `$iothub/methods/res/{status}/?$rid={request id}`, donde:</span><span class="sxs-lookup"><span data-stu-id="f6ddb-150">The device sends responses to `$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="f6ddb-151">La propiedad `status` es el estado de la ejecución del método proporcionado por el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-151">The `status` property is the device-supplied status of method execution.</span></span>
* <span data-ttu-id="f6ddb-152">La propiedad `$rid` es el identificador de solicitud de la invocación de método recibido de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-152">The `$rid` property is the request ID from the method invocation received from IoT Hub.</span></span>

<span data-ttu-id="f6ddb-153">El dispositivo establece el cuerpo y puede tener cualquier estado.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-153">The body is set by the device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="f6ddb-154">Material de referencia adicional</span><span class="sxs-lookup"><span data-stu-id="f6ddb-154">Additional reference material</span></span>
<span data-ttu-id="f6ddb-155">Otros temas de referencia en la guía del desarrollador de IoT Hub son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="f6ddb-155">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="f6ddb-156">En [Puntos de conexión de IoT Hub][lnk-endpoints], se describen los diferentes puntos de conexión que expone cada centro de IoT Hub para las operaciones en tiempo de ejecución y de administración.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-156">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="f6ddb-157">En [Cuotas y limitación][lnk-quotas], se describen las cuotas que se aplican al servicio IoT Hub y el comportamiento de limitación que se espera al usar el servicio.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-157">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="f6ddb-158">En [SDK de dispositivo y servicio IoT de Azure][lnk-sdks] se muestran los diversos SDK de lenguaje que puede usar para desarrollar aplicaciones para dispositivo y de servicio que interactúen con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-158">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="f6ddb-159">En [Referencia: Lenguaje de consulta de IoT Hub para dispositivos gemelos, trabajos y enrutamiento de mensajes][lnk-query], se describe el lenguaje de consulta de IoT Hub que se puede usar para recuperar información de IoT Hub sobre los dispositivos gemelos y trabajos.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="f6ddb-160">En [Compatibilidad con MQTT de IoT Hub][lnk-devguide-mqtt], se proporciona más información sobre la compatibilidad de IoT Hub con el protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="f6ddb-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6ddb-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f6ddb-161">Next steps</span></span>
<span data-ttu-id="f6ddb-162">Ahora que ha aprendido a usar métodos directos, puede interesarle el siguiente tema de la Guía del desarrollador de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="f6ddb-162">Now you have learned how to use direct methods, you may be interested in the following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="f6ddb-163">[Programación de trabajos en varios dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="f6ddb-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="f6ddb-164">Si desea probar algunos de los conceptos descritos en este artículo, puede interesarle el siguiente tutorial de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="f6ddb-164">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="f6ddb-165">[Use direct methods][lnk-methods-tutorial] (Uso de métodos directos)</span><span class="sxs-lookup"><span data-stu-id="f6ddb-165">[Use direct methods][lnk-methods-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
