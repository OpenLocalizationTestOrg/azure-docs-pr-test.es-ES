---
title: "supervisión de operaciones de centro de IoT aaaAzure | Documentos de Microsoft"
description: "Cómo las operaciones de centro de IoT de Azure toouse supervisión toomonitor Hola estado de las operaciones en el centro de IoT en tiempo real."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a299f3a5-b14d-4586-9c3b-44aea14ed013
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.openlocfilehash: a0b233ef2d9bd0827e19fa30fdbdd49b2b61b813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="8478f-103">Supervisión de operaciones de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="8478f-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="8478f-104">Supervisión de operaciones de centro de IoT permite toomonitor Hola estado de las operaciones en el centro de IoT en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="8478f-104">IoT Hub operations monitoring enables you toomonitor hello status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="8478f-105">IoT Hub realiza el seguimiento de eventos a través de varias categorías de operaciones.</span><span class="sxs-lookup"><span data-stu-id="8478f-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="8478f-106">Puede optar por enviar eventos de uno o más categorías tooan punto de conexión de su centro de IoT para su procesamiento.</span><span class="sxs-lookup"><span data-stu-id="8478f-106">You can opt into sending events from one or more categories tooan endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="8478f-107">Puede supervisar los datos de Hola para errores o establecer un procesamiento más complejo basándose en patrones de datos.</span><span class="sxs-lookup"><span data-stu-id="8478f-107">You can monitor hello data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="8478f-108">IoT Hub supervisa seis categorías de eventos:</span><span class="sxs-lookup"><span data-stu-id="8478f-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="8478f-109">Operaciones de identidad de dispositivos</span><span class="sxs-lookup"><span data-stu-id="8478f-109">Device identity operations</span></span>
* <span data-ttu-id="8478f-110">Telemetría de dispositivo</span><span class="sxs-lookup"><span data-stu-id="8478f-110">Device telemetry</span></span>
* <span data-ttu-id="8478f-111">Mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="8478f-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="8478f-112">Conexiones</span><span class="sxs-lookup"><span data-stu-id="8478f-112">Connections</span></span>
* <span data-ttu-id="8478f-113">Cargas de archivos</span><span class="sxs-lookup"><span data-stu-id="8478f-113">File uploads</span></span>
* <span data-ttu-id="8478f-114">Enrutamiento de mensajes</span><span class="sxs-lookup"><span data-stu-id="8478f-114">Message routing</span></span>

## <a name="how-tooenable-operations-monitoring"></a><span data-ttu-id="8478f-115">La supervisión de operaciones de tooenable</span><span class="sxs-lookup"><span data-stu-id="8478f-115">How tooenable operations monitoring</span></span>

1. <span data-ttu-id="8478f-116">Cree un Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="8478f-116">Create an IoT hub.</span></span> <span data-ttu-id="8478f-117">Encontrará instrucciones sobre cómo toocreate un centro de IoT en hello [Introducción] [ lnk-get-started] guía.</span><span class="sxs-lookup"><span data-stu-id="8478f-117">You can find instructions on how toocreate an IoT hub in hello [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="8478f-118">Abra la hoja de Hola de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="8478f-118">Open hello blade of your IoT hub.</span></span> <span data-ttu-id="8478f-119">Desde allí, haga clic en **Supervisión de operaciones**.</span><span class="sxs-lookup"><span data-stu-id="8478f-119">From there, click **Operations monitoring**.</span></span>

    ![Supervisión de configuración en el portal de Hola de operaciones de acceso][1]

1. <span data-ttu-id="8478f-121">Seleccione Hola supervisión categorías desea toomonitor y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="8478f-121">Select hello monitoring categories you wish toomonitor, and then click **Save**.</span></span> <span data-ttu-id="8478f-122">Hello eventos están disponibles para leer del punto de conexión de hello compatible con el concentrador de eventos enumerado en **configuración de supervisión**.</span><span class="sxs-lookup"><span data-stu-id="8478f-122">hello events are available for reading from hello Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="8478f-123">Hello centro de IoT se denomina `messages/operationsmonitoringevents`.</span><span class="sxs-lookup"><span data-stu-id="8478f-123">hello IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![Configurar operaciones de supervisión en la instancia de IoT Hub][2]

> [!NOTE]
> <span data-ttu-id="8478f-125">Seleccionar **detallado** supervisión de hello **conexiones** categoría hace centro de IoT toogenerate mensajes de diagnóstico adicionales.</span><span class="sxs-lookup"><span data-stu-id="8478f-125">Selecting **Verbose** monitoring for hello **Connections** category causes IoT Hub toogenerate additional diagnostics messages.</span></span> <span data-ttu-id="8478f-126">Para todas las demás categorías, Hola **detallado** cantidad Hola de centro de IoT de la información de cambios de configuración incluyen en cada mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="8478f-126">For all other categories, hello **Verbose** setting changes hello quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-toouse-them"></a><span data-ttu-id="8478f-127">Categorías de eventos y cómo toouse ellos</span><span class="sxs-lookup"><span data-stu-id="8478f-127">Event categories and how toouse them</span></span>

<span data-ttu-id="8478f-128">Cada categoría de supervisión de operaciones realiza el seguimiento de un tipo diferente de interacción con IoT Hub, y cada categoría de supervisión tiene un esquema que define cómo se estructuran los eventos de esa categoría.</span><span class="sxs-lookup"><span data-stu-id="8478f-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="8478f-129">Operaciones de identidad de dispositivos</span><span class="sxs-lookup"><span data-stu-id="8478f-129">Device identity operations</span></span>

<span data-ttu-id="8478f-130">categoría de las operaciones de identidad de dispositivo de Hello realiza un seguimiento de errores que se producen al intentar toocreate, actualizar o eliminar una entrada de registro de la identidad de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="8478f-130">hello device identity operations category tracks errors that occur when you attempt toocreate, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="8478f-131">El seguimiento de esta categoría resulta útil para los escenarios de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="8478f-131">Tracking this category is useful for provisioning scenarios.</span></span>

```json
{
    "time": "UTC timestamp",
        "operationName": "create",
        "category": "DeviceIdentityOperations",
        "level": "Error",
        "statusCode": 4XX,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "durationMs": 1234,
        "userAgent": "userAgent",
        "sharedAccessPolicy": "accessPolicy"
}
```

### <a name="device-telemetry"></a><span data-ttu-id="8478f-132">Telemetría de dispositivo</span><span class="sxs-lookup"><span data-stu-id="8478f-132">Device telemetry</span></span>

<span data-ttu-id="8478f-133">categoría de telemetría de dispositivo de Hello realiza un seguimiento de errores que se producen en el centro de IoT de Hola y canalización de telemetría toohello relacionados.</span><span class="sxs-lookup"><span data-stu-id="8478f-133">hello device telemetry category tracks errors that occur at hello IoT hub and are related toohello telemetry pipeline.</span></span> <span data-ttu-id="8478f-134">Esta categoría incluye los errores que se producen al enviar eventos de telemetría (por ejemplo, la limitación) y recibir eventos de telemetría (por ejemplo, un lector no autorizado).</span><span class="sxs-lookup"><span data-stu-id="8478f-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="8478f-135">Esta categoría no puede capturar errores causados por el código que se ejecuta en el propio dispositivo Hola.</span><span class="sxs-lookup"><span data-stu-id="8478f-135">This category cannot catch errors caused by code running on hello device itself.</span></span>

```json
{
        "messageSizeInBytes": 1234,
        "batching": 0,
        "protocol": "Amqp",
        "authType": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
        "time": "UTC timestamp",
        "operationName": "ingress",
        "category": "DeviceTelemetry",
        "level": "Error",
        "statusCode": 4XX,
        "statusType": 4XX001,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "EventProcessedUtcTime": "UTC timestamp",
        "PartitionId": 1,
        "EventEnqueuedUtcTime": "UTC timestamp"
}
```

### <a name="cloud-to-device-commands"></a><span data-ttu-id="8478f-136">Comandos de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="8478f-136">Cloud-to-device commands</span></span>

<span data-ttu-id="8478f-137">categoría de comandos en la nube al dispositivo de Hello realiza un seguimiento de errores que se producen en el centro de IoT de Hola y canalización de mensaje en la nube a dispositivo toohello relacionados.</span><span class="sxs-lookup"><span data-stu-id="8478f-137">hello cloud-to-device commands category tracks errors that occur at hello IoT hub and are related toohello cloud-to-device message pipeline.</span></span> <span data-ttu-id="8478f-138">Esta categoría incluye errores que se producen al enviar mensajes de nube a dispositivo (por ejemplo, un remitente no autorizado), recibir mensajes de nube a dispositivo (por ejemplo, el número de entregas superado) y recibir mensajes de nube a dispositivo (por ejemplo, comentarios expirados).</span><span class="sxs-lookup"><span data-stu-id="8478f-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="8478f-139">Esta categoría no detecta errores desde un dispositivo que controla incorrectamente un mensaje en la nube al dispositivo si el mensaje de saludo en la nube al dispositivo se ha entregado correctamente.</span><span class="sxs-lookup"><span data-stu-id="8478f-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if hello cloud-to-device message was delivered successfully.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "deliveryAcknowledgement": 0,
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "C2DCommands",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "EventProcessedUtcTime": "UTC timestamp",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": “UTC timestamp"
}
```

### <a name="connections"></a><span data-ttu-id="8478f-140">Conexiones</span><span class="sxs-lookup"><span data-stu-id="8478f-140">Connections</span></span>

<span data-ttu-id="8478f-141">categoría de las conexiones de Hello realiza un seguimiento de errores que se producen cuando los dispositivos conectarán o desconexión de un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="8478f-141">hello connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="8478f-142">El seguimiento de esta categoría resulta útil para identificar intentos de conexión no autorizados y para realizar el seguimiento de las situaciones en que una conexión se pierde para los dispositivos en las áreas de conectividad deficiente.</span><span class="sxs-lookup"><span data-stu-id="8478f-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

```json
{
    "durationMs": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID"
}
```

### <a name="file-uploads"></a><span data-ttu-id="8478f-143">Cargas de archivos</span><span class="sxs-lookup"><span data-stu-id="8478f-143">File uploads</span></span>

<span data-ttu-id="8478f-144">categoría de carga de archivo Hello realiza un seguimiento de errores que se producen en el centro de IoT de Hola y funcionalidad de carga de toofile relacionados.</span><span class="sxs-lookup"><span data-stu-id="8478f-144">hello file upload category tracks errors that occur at hello IoT hub and are related toofile upload functionality.</span></span> <span data-ttu-id="8478f-145">Esta categoría incluye lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8478f-145">This category includes:</span></span>

* <span data-ttu-id="8478f-146">Errores que se producen con hello URI de SAS, como cuándo expira antes de que un dispositivo notifica al concentrador de Hola de una carga completada.</span><span class="sxs-lookup"><span data-stu-id="8478f-146">Errors that occur with hello SAS URI, such as when it expires before a device notifies hello hub of a completed upload.</span></span>
* <span data-ttu-id="8478f-147">No se pudo cargas notificadas por dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8478f-147">Failed uploads reported by hello device.</span></span>
* <span data-ttu-id="8478f-148">Errores que se producen cuando no se encuentra un archivo en el almacenamiento durante la creación del mensaje de notificación de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8478f-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="8478f-149">Esta categoría no puede capturar los errores ocurridos directamente al dispositivo de hello está cargando un archivo toostorage.</span><span class="sxs-lookup"><span data-stu-id="8478f-149">This category cannot catch errors that directly occur while hello device is uploading a file toostorage.</span></span>

```json
{
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "HTTP",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "fileUpload",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "blobUri": "http//bloburi.com",
    "durationMs": 1234
}
```

### <a name="message-routing"></a><span data-ttu-id="8478f-150">Enrutamiento de mensajes</span><span class="sxs-lookup"><span data-stu-id="8478f-150">Message routing</span></span>

<span data-ttu-id="8478f-151">categoría de enrutamiento de mensajes de Hola realiza un seguimiento de errores que se producen durante la evaluación de la ruta de mensajes y el estado de punto de conexión según lo percibido por centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="8478f-151">hello message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="8478f-152">Esta categoría incluye eventos, como cuando se evalúa como una regla demasiado "undefined", al centro de IoT marca un punto de conexión como cola y cualquier otro error recibido de un punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="8478f-152">This category includes events such as when a rule evaluates too"undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="8478f-153">Esta categoría no incluye errores específicos acerca de los mensajes de Hola a sí mismos (por ejemplo, el dispositivo errores de limitación), que se notifican en la categoría de "telemetría de dispositivo" Hola.</span><span class="sxs-lookup"><span data-stu-id="8478f-153">This category does not include specific errors about hello messages themselves (such as device throttling errors), which are reported under hello "device telemetry" category.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "time": "UTC timestamp",
    "operationName": "ingress",
    "category": "routes",
    "level": "Error",
    "deviceId": "device-ID",
    "messageId": "ID of message",
    "routeName": "myroute",
    "endpointName": "myendpoint",
    "details": "ExternalEndpointDisabled"
}
```

## <a name="view-events"></a><span data-ttu-id="8478f-154">Ver eventos</span><span class="sxs-lookup"><span data-stu-id="8478f-154">View events</span></span>

<span data-ttu-id="8478f-155">Puede usar hello *el centro de IOT explorador* tooquickly de la herramienta de prueba que el centro de IoT está generando eventos de supervisión.</span><span class="sxs-lookup"><span data-stu-id="8478f-155">You can use hello *iothub-explorer* tool tooquickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="8478f-156">Hola tooinstall herramienta, consulte las instrucciones de Hola Hola [el centro de IOT explorador] [ lnk-iothub-explorer] repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="8478f-156">tooinstall hello tool, see hello instructions in hello [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="8478f-157">Realizar Hola seguro **conexiones** supervisión categoría se establece demasiado**detallado** en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="8478f-157">Make sure hello **Connections** monitoring category is set too**Verbose** in hello portal.</span></span>

1. <span data-ttu-id="8478f-158">En una línea de comandos, ejecute hello siguientes tooread de comando de hello extremo de supervisión:</span><span class="sxs-lookup"><span data-stu-id="8478f-158">At a command-prompt, run hello following command tooread from hello monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="8478f-159">En otro símbolo, ejecute hello después comando toosimulate un dispositivo que envía mensajes de dispositivo para la nube:</span><span class="sxs-lookup"><span data-stu-id="8478f-159">In another command-prompt, run hello following command toosimulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="8478f-160">símbolo primera Hello muestra eventos de supervisión de hello tooyour centro de IoT se conecta el dispositivo simulado Hola.</span><span class="sxs-lookup"><span data-stu-id="8478f-160">hello first command-prompt shows hello monitoring events as hello simulated device connects tooyour IoT hub.</span></span>

## <a name="connect-toohello-monitoring-endpoint"></a><span data-ttu-id="8478f-161">Conectar toohello extremo de supervisión</span><span class="sxs-lookup"><span data-stu-id="8478f-161">Connect toohello monitoring endpoint</span></span>

<span data-ttu-id="8478f-162">Hola supervisión de extremo en el centro de IoT es un punto de conexión compatible de concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="8478f-162">hello monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="8478f-163">Puede utilizar cualquier mecanismo que funciona con los concentradores de eventos tooread supervisión mensajes desde este punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="8478f-163">You can use any mechanism that works with Event Hubs tooread monitoring messages from this endpoint.</span></span> <span data-ttu-id="8478f-164">Hello en el ejemplo siguiente crea un lector básico que no es adecuado para una implementación de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="8478f-164">hello following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="8478f-165">Para obtener más información acerca de cómo tooprocess mensajes desde los centros de eventos, vea hello [empezar a trabajar con concentradores de eventos] [ lnk-eventhubs-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="8478f-165">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="8478f-166">extremo de supervisión de toohello tooconnect, se necesita un nombre de punto de conexión de hello y cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="8478f-166">tooconnect toohello monitoring endpoint, you need a connection string and hello endpoint name.</span></span> <span data-ttu-id="8478f-167">Hola siguientes pasos muestra cómo toofind Hola valores necesarios en el portal de hello:</span><span class="sxs-lookup"><span data-stu-id="8478f-167">hello following steps show you how toofind hello necessary values in hello portal:</span></span>

1. <span data-ttu-id="8478f-168">En el portal de hello, navegue tooyour hoja de recursos del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="8478f-168">In hello portal, navigate tooyour IoT Hub resource blade.</span></span>

1. <span data-ttu-id="8478f-169">Elija **supervisión de operaciones**y tome nota de hello **nombre de concentrador de eventos-compatible con** y **punto de conexión de concentrador de eventos-compatible con** valores:</span><span class="sxs-lookup"><span data-stu-id="8478f-169">Choose **Operations monitoring**, and make a note of hello **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![Valores del punto de conexión compatible con centro de eventos][img-endpoints]

1. <span data-ttu-id="8478f-171">Elija **Directivas de acceso compartido** y, a continuación, elija **servicio**.</span><span class="sxs-lookup"><span data-stu-id="8478f-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="8478f-172">Tome nota de hello **clave principal** valor:</span><span class="sxs-lookup"><span data-stu-id="8478f-172">Make a note of hello **Primary key** value:</span></span>

    ![Clave principal de directiva de acceso compartido del servicio][img-service-key]

<span data-ttu-id="8478f-174">Hello siguiente ejemplo de código de C# procede desde Visual Studio **escritorio clásico de Windows** aplicación de consola de C#.</span><span class="sxs-lookup"><span data-stu-id="8478f-174">hello following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="8478f-175">proyecto de Hello tiene hello **WindowsAzure.ServiceBus** instalado el paquete de NuGet.</span><span class="sxs-lookup"><span data-stu-id="8478f-175">hello project has hello **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="8478f-176">Reemplace el marcador de posición de cadena de conexión de hello con una cadena de conexión que utiliza hello **punto de conexión de concentrador de eventos-compatible con** y el servicio **clave principal** valores que anotó anteriormente como se muestra en la siguiente Hola ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8478f-176">Replace hello connection string placeholder with a connection string that uses hello **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in hello following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="8478f-177">Reemplace Hola supervisión de marcador de posición de nombre de punto de conexión con hello **nombre de concentrador de eventos-compatible con** valor que anotó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8478f-177">Replace hello monitoring endpoint name placeholder with hello **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key tooexit.\n");

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, monitoringEndpointName);
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
        CancellationTokenSource cts = new CancellationTokenSource();
        var tasks = new List<Task>();

        foreach (string partition in d2cPartitions)
        {
            tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }

        Console.ReadLine();
        Console.WriteLine("Exiting...");
        cts.Cancel();
        Task.WaitAll(tasks.ToArray());
    }

    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested)
            {
                await eventHubReceiver.CloseAsync();
                break;
            }

            EventData eventData = await eventHubReceiver.ReceiveAsync(new TimeSpan(0,0,10));

            if (eventData != null)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="8478f-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8478f-178">Next steps</span></span>
<span data-ttu-id="8478f-179">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="8478f-179">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="8478f-180">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="8478f-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="8478f-181">[Simular un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="8478f-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links and images -->
[1]: media/iot-hub-operations-monitoring/enable-OM-1.png
[2]: media/iot-hub-operations-monitoring/enable-OM-2.png
[img-endpoints]: media/iot-hub-operations-monitoring/monitoring-endpoint.png
[img-service-key]: media/iot-hub-operations-monitoring/service-key.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-diagnostic-metrics]: iot-hub-metrics.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md