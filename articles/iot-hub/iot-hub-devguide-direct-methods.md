---
title: "aaaUnderstand centro de IoT de Azure dirigir métodos | Documentos de Microsoft"
description: "Guía del desarrollador - usar métodos directos tooinvoke código en los dispositivos desde una aplicación de servicio."
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
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="60480-103">Conocimiento e invocación de los métodos directos de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="60480-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="60480-104">Información general</span><span class="sxs-lookup"><span data-stu-id="60480-104">Overview</span></span>
<span data-ttu-id="60480-105">Centro de IoT ofrece métodos directos tooinvoke de capacidad en los dispositivos de la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="60480-105">IoT Hub gives you ability tooinvoke direct methods on devices from hello cloud.</span></span> <span data-ttu-id="60480-106">Métodos directos representan una interacción de solicitud y respuesta con un tooan similar de dispositivo HTTP llamar en que se realizan correctamente o se producirá un error inmediatamente (después de un tiempo de espera especificado por el usuario).</span><span class="sxs-lookup"><span data-stu-id="60480-106">Direct methods represent a request-reply interaction with a device similar tooan HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="60480-107">Esto es útil para escenarios donde el curso de Hola de una acción inmediata es diferente en función de si el dispositivo de hello era capaz de toorespond, como el envío de un dispositivo de reactivación tooa SMS si un dispositivo está sin conexión (que se va a más cara que una llamada al método SMS).</span><span class="sxs-lookup"><span data-stu-id="60480-107">This is useful for scenarios where hello course of immediate action is different depending on whether hello device was able toorespond, such as sending an SMS wake-up tooa device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="60480-108">Cada método de dispositivo se dirige a un único dispositivo.</span><span class="sxs-lookup"><span data-stu-id="60480-108">Each device method targets a single device.</span></span> <span data-ttu-id="60480-109">[Trabajos] [ lnk-devguide-jobs] proporcionan un tooinvoke de forma directa en varios dispositivos y programar la invocación del método de dispositivos desconectados.</span><span class="sxs-lookup"><span data-stu-id="60480-109">[Jobs][lnk-devguide-jobs] provide a way tooinvoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="60480-110">Cualquier persona con permisos de **conexión de servicio** en IoT Hub pueden invocar un método en un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="60480-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="60480-111">Cuando toouse</span><span class="sxs-lookup"><span data-stu-id="60480-111">When toouse</span></span>
<span data-ttu-id="60480-112">Métodos directos siguen un patrón de solicitud-respuesta y están diseñados para las comunicaciones que necesitan confirmación inmediata de su control normalmente interactivo de dispositivo de hello, por ejemplo tooturn en un ventilador de resultados.</span><span class="sxs-lookup"><span data-stu-id="60480-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of hello device, for example tooturn on a fan.</span></span>

<span data-ttu-id="60480-113">Consulte demasiado[orientación para la comunicación en la nube para dispositivos] [ lnk-c2d-guidance] en caso de duda entre el uso de propiedades que desee, dirigir métodos o mensajes de la nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="60480-113">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="60480-114">Ciclo de vida de los métodos</span><span class="sxs-lookup"><span data-stu-id="60480-114">Method lifecycle</span></span>
<span data-ttu-id="60480-115">Métodos directos se implementan en dispositivos de Hola y pueden requerir cero o más entradas en hello método carga toocorrectly crear instancias.</span><span class="sxs-lookup"><span data-stu-id="60480-115">Direct methods are implemented on hello device and may require zero or more inputs in hello method payload toocorrectly instantiate.</span></span> <span data-ttu-id="60480-116">Se invoca un método directo mediante un URI orientado al servicio (`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="60480-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="60480-117">Un dispositivo recibe métodos directos a través de un tema MQTT específico del dispositivo (`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="60480-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="60480-118">Podemos admitimos métodos directos en protocolos de red del dispositivo adicionales en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="60480-118">We may support direct methods on additional device-side networking protocols in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="60480-119">Cuando se invoca un método directo en un dispositivo, valores y nombres de propiedad solo pueden contener US-ASCII imprimible alfanumérico, excepto los Hola siguiendo conjunto: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="60480-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="60480-120">Dirigir métodos son sincrónicos y ya sea correctamente o producirá un error tras el período de tiempo de espera de hello (predeterminado: 30 segundos, puede establecer seguridad too3600 segundos).</span><span class="sxs-lookup"><span data-stu-id="60480-120">Direct methods are synchronous and either succeed or fail after hello timeout period (default: 30 seconds, settable up too3600 seconds).</span></span> <span data-ttu-id="60480-121">Métodos directos son útiles en escenarios interactivos donde desea un tooact de dispositivo si y solo si el dispositivo de hello es comandos en línea y la recepción, como activar una luz desde un teléfono.</span><span class="sxs-lookup"><span data-stu-id="60480-121">Direct methods are useful in interactive scenarios where you want a device tooact if and only if hello device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="60480-122">En estos casos, desea toosee un error o éxito inmediata para que servicio de nube de hello puede actuar en el resultado de hello tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="60480-122">In these scenarios, you want toosee an immediate success or failure so hello cloud service can act on hello result as soon as possible.</span></span> <span data-ttu-id="60480-123">dispositivo de Hello puede devolver algunas cuerpo del mensaje como resultado del método hello, pero no es necesario para hello método toodo para.</span><span class="sxs-lookup"><span data-stu-id="60480-123">hello device may return some message body as a result of hello method, but it isn't required for hello method toodo so.</span></span> <span data-ttu-id="60480-124">No hay ninguna garantía respecto al orden o la semántica de simultaneidad en las llamadas de método.</span><span class="sxs-lookup"><span data-stu-id="60480-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="60480-125">Método directo son solo HTTP del lado de la nube de Hola y MQTT solo desde el lado del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="60480-125">Direct method are HTTP-only from hello cloud side, and MQTT-only from hello device side.</span></span>

<span data-ttu-id="60480-126">carga de Hello para el método solicitudes y respuestas es un documento JSON hacia arriba too8KB.</span><span class="sxs-lookup"><span data-stu-id="60480-126">hello payload for method requests and responses is a JSON document up too8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="60480-127">Temas de referencia:</span><span class="sxs-lookup"><span data-stu-id="60480-127">Reference topics:</span></span>
<span data-ttu-id="60480-128">Hello temas de referencia siguientes proporcionan más información sobre el uso de métodos directos.</span><span class="sxs-lookup"><span data-stu-id="60480-128">hello following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="60480-129">Invocación de un método directo desde una aplicación de back-end</span><span class="sxs-lookup"><span data-stu-id="60480-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="60480-130">Invocación de método</span><span class="sxs-lookup"><span data-stu-id="60480-130">Method invocation</span></span>
<span data-ttu-id="60480-131">Las invocaciones de método directo en un dispositivo son llamadas HTTP compuestas por:</span><span class="sxs-lookup"><span data-stu-id="60480-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="60480-132">Hola *URI* dispositivo toohello específico (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="60480-132">hello *URI* specific toohello device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="60480-133">Hola POST *(método)*</span><span class="sxs-lookup"><span data-stu-id="60480-133">hello POST *method*</span></span>
* <span data-ttu-id="60480-134">*Encabezados de* que contienen Hola authorization, Id., el tipo de contenido y la codificación de contenido de solicitud</span><span class="sxs-lookup"><span data-stu-id="60480-134">*Headers* which contain hello authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="60480-135">JSON transparente *cuerpo* Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="60480-135">A transparent JSON *body* in hello following format:</span></span>

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

<span data-ttu-id="60480-136">El tiempo de espera se expresa en segundos.</span><span class="sxs-lookup"><span data-stu-id="60480-136">Timeout is in seconds.</span></span> <span data-ttu-id="60480-137">Si no se establece el tiempo de espera, el valor predeterminado es too30 segundos.</span><span class="sxs-lookup"><span data-stu-id="60480-137">If timeout is not set, it defaults too30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="60480-138">Response</span><span class="sxs-lookup"><span data-stu-id="60480-138">Response</span></span>
<span data-ttu-id="60480-139">aplicaciones de back-end de Hello recibe una respuesta que consta de:</span><span class="sxs-lookup"><span data-stu-id="60480-139">hello back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="60480-140">*Código de estado HTTP*, que se utiliza para errores procedentes de hello centro de IoT, incluido un error 404 para dispositivos no está conectado</span><span class="sxs-lookup"><span data-stu-id="60480-140">*HTTP status code*, which is used for errors coming from hello IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="60480-141">*Encabezados de* que contienen Hola ETag, Id., el tipo de contenido y la codificación de contenido de solicitud</span><span class="sxs-lookup"><span data-stu-id="60480-141">*Headers* which contain hello ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="60480-142">JSON *cuerpo* Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="60480-142">A JSON *body* in hello following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="60480-143">Ambos `status` y `body` se proporcionan por dispositivo de Hola y usar toorespond con código de estado del dispositivo de Hola o descripción.</span><span class="sxs-lookup"><span data-stu-id="60480-143">Both `status` and `body` are provided by hello device and used toorespond with hello device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="60480-144">Control de un método directo en un dispositivo</span><span class="sxs-lookup"><span data-stu-id="60480-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="60480-145">Invocación de método</span><span class="sxs-lookup"><span data-stu-id="60480-145">Method invocation</span></span>
<span data-ttu-id="60480-146">Dispositivos reciben las solicitudes de método directo en el tema de Hola MQTT:`$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="60480-146">Devices receive direct method requests on hello MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="60480-147">cuerpo de Hello qué dispositivo Hola recibe es Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="60480-147">hello body which hello device receives is in hello following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="60480-148">Las solicitudes de método son QoS 0.</span><span class="sxs-lookup"><span data-stu-id="60480-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="60480-149">Response</span><span class="sxs-lookup"><span data-stu-id="60480-149">Response</span></span>
<span data-ttu-id="60480-150">dispositivo de Hello envía las respuestas demasiado`$iothub/methods/res/{status}/?$rid={request id}`, donde:</span><span class="sxs-lookup"><span data-stu-id="60480-150">hello device sends responses too`$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="60480-151">Hola `status` propiedad es el estado proporcionado por el dispositivo de Hola de ejecución del método.</span><span class="sxs-lookup"><span data-stu-id="60480-151">hello `status` property is hello device-supplied status of method execution.</span></span>
* <span data-ttu-id="60480-152">Hola `$rid` propiedad es Id. de solicitud de saludo de la invocación del método hello recibida desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="60480-152">hello `$rid` property is hello request ID from hello method invocation received from IoT Hub.</span></span>

<span data-ttu-id="60480-153">cuerpo de Hola se establece por dispositivo de Hola y puede ser cualquier tipo de estado.</span><span class="sxs-lookup"><span data-stu-id="60480-153">hello body is set by hello device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="60480-154">Material de referencia adicional</span><span class="sxs-lookup"><span data-stu-id="60480-154">Additional reference material</span></span>
<span data-ttu-id="60480-155">Otros temas de referencia en la Guía del desarrollador de centro de IoT Hola incluyen:</span><span class="sxs-lookup"><span data-stu-id="60480-155">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="60480-156">[Los extremos del centro de IoT] [ lnk-endpoints] describe Hola varios extremos que cada centro de IoT expone las operaciones de tiempo de ejecución y administración.</span><span class="sxs-lookup"><span data-stu-id="60480-156">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="60480-157">[Limitación y las cuotas] [ lnk-quotas] describe las cuotas de Hola que se aplican toohello servicio del centro de IoT y Hola limitación tooexpect de comportamiento cuando se usa el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="60480-157">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="60480-158">[SDK de dispositivos y servicios de Azure IoT] [ lnk-sdks] listas Hola lenguaje varios SDK que se puede usar cuando se desarrollan aplicaciones de dispositivos y servicios que interactúan con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="60480-158">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="60480-159">[Lenguaje de consulta de centro de IoT para: los gemelos de dispositivo, los trabajos y el enrutamiento de mensajes] [ lnk-query] describe Hola lenguaje de consultas del centro de IoT puede usar información de tooretrieve centro de IoT de: los gemelos de dispositivo y trabajos.</span><span class="sxs-lookup"><span data-stu-id="60480-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="60480-160">[Compatibilidad de IoT Hub MQTT] [ lnk-devguide-mqtt] proporciona más información acerca del soporte técnico de centro de IoT para el protocolo MQTT Hola.</span><span class="sxs-lookup"><span data-stu-id="60480-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60480-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="60480-161">Next steps</span></span>
<span data-ttu-id="60480-162">Ahora que ha aprendido cómo toouse métodos directos, puede que esté interesado en hello siguiente tema de la Guía de centro de IoT para desarrolladores:</span><span class="sxs-lookup"><span data-stu-id="60480-162">Now you have learned how toouse direct methods, you may be interested in hello following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="60480-163">[Programación de trabajos en varios dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="60480-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="60480-164">Si desea que tootry algunos de los conceptos de hello descritos en este artículo, es posible que interesa Hola sigue tutorial del centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="60480-164">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="60480-165">[Use direct methods][lnk-methods-tutorial] (Uso de métodos directos)</span><span class="sxs-lookup"><span data-stu-id="60480-165">[Use direct methods][lnk-methods-tutorial]</span></span>

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
