---
title: "aaaAzure Service Fabric invertir diagnósticos proxy | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomonitor y diagnosticar el procesamiento de solicitudes de proxy inverso de Hola."
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: kavyako
ms.openlocfilehash: 9687b9688dc26ba619cbdfab1b1f49a3035345c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-request-processing-at-hello-reverse-proxy"></a><span data-ttu-id="b0dbc-103">Supervisar y diagnosticar el procesamiento de solicitudes de proxy inverso de Hola</span><span class="sxs-lookup"><span data-stu-id="b0dbc-103">Monitor and diagnose request processing at hello reverse proxy</span></span>

<span data-ttu-id="b0dbc-104">A partir de hello 5.7 versión de Service Fabric, eventos de proxy inverso están disponibles para la colección.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-104">Starting with hello 5.7 release of Service Fabric, reverse proxy events are available for collection.</span></span> <span data-ttu-id="b0dbc-105">Hola eventos están disponibles en dos canales, uno con solo los eventos de error relacionados con error de procesamiento de toorequest en proxy inverso de Hola y el segundo canal que contiene eventos detallados de entradas para las solicitudes correctas e incorrectas.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-105">hello events are available in two channels, one with only error events related toorequest processing failure at hello reverse proxy and second channel containing verbose events with entries for both successful and failed requests.</span></span>

<span data-ttu-id="b0dbc-106">Consulte demasiado[recopilar eventos de proxy inverso](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable recopilar eventos de estos canales de clústeres de Azure Service Fabric y local.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-106">Refer too[Collect reverse proxy events](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable collecting events from these channels in local and Azure Service Fabric clusters.</span></span>

## <a name="troubleshoot-using-diagnostics-logs"></a><span data-ttu-id="b0dbc-107">Solución de problemas mediante la herramienta de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="b0dbc-107">Troubleshoot using diagnostics logs</span></span>
<span data-ttu-id="b0dbc-108">Estos son algunos ejemplos de cómo puede encontrar los que uno de los registros de error comunes toointerpret hello:</span><span class="sxs-lookup"><span data-stu-id="b0dbc-108">Here are some examples on how toointerpret hello common failure logs that one can encounter:</span></span>

1. <span data-ttu-id="b0dbc-109">El proxy inverso devuelve el código de estado de respuesta 504 (tiempo de espera agotado).</span><span class="sxs-lookup"><span data-stu-id="b0dbc-109">Reverse proxy returns response status code 504 (Timeout).</span></span>

    <span data-ttu-id="b0dbc-110">Un motivo puede ser debido a error del servicio toohello tooreply dentro del período de tiempo de espera de solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-110">One reason could be due toohello service failing tooreply within hello request timeout period.</span></span>
<span data-ttu-id="b0dbc-111">evento primera Hola siguiente registra los detalles de Hola de solicitud de saludo recibida en proxy inverso de Hola.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-111">hello first event below logs hello details of hello request received at hello reverse proxy.</span></span> <span data-ttu-id="b0dbc-112">Hello segundo evento indica que Hola solicitud un error mientras tooservice de reenvío, mucha demasiado "error interno = ERROR_WINHTTP_TIMEOUT"</span><span class="sxs-lookup"><span data-stu-id="b0dbc-112">hello second event indicates that hello request failed while forwarding tooservice, due too"internal error = ERROR_WINHTTP_TIMEOUT"</span></span> 

    <span data-ttu-id="b0dbc-113">Hola carga incluye:</span><span class="sxs-lookup"><span data-stu-id="b0dbc-113">hello payload includes:</span></span>

    *  <span data-ttu-id="b0dbc-114">**traceId**: este GUID se puede utilizar toocorrelate todos los eventos de hello correspondiente tooa única solicitud.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-114">**traceId**: This GUID can be used toocorrelate all hello events corresponding tooa single request.</span></span> <span data-ttu-id="b0dbc-115">Hola por debajo de los dos eventos, Hola traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, lo que implica pertenecen toohello misma solicitud.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-115">In hello below two events, hello traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, implying they belong toohello same request.</span></span>
    *  <span data-ttu-id="b0dbc-116">**requestUrl**: Hola URL (dirección URL de proxy inverso) toowhich Hola solicitud fue enviada.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-116">**requestUrl**: hello URL (Reverse proxy URL) toowhich hello request was sent.</span></span>
    *  <span data-ttu-id="b0dbc-117">**verb**: verbo HTTP.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-117">**verb**: HTTP verb.</span></span>
    *  <span data-ttu-id="b0dbc-118">**remoteAddress**: dirección del cliente que envía la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-118">**remoteAddress**: Address of client sending hello request.</span></span>
    *  <span data-ttu-id="b0dbc-119">**resolvedServiceUrl**: solicitud entrante de Hola de toowhich punto de conexión de dirección URL de servicio se ha resuelto.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-119">**resolvedServiceUrl**: Service endpoint URL toowhich hello incoming request was resolved.</span></span> 
    *  <span data-ttu-id="b0dbc-120">**errorDetails**: información adicional sobre los errores de Hola.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-120">**errorDetails**: Additional information about hello failure.</span></span>

    ```
    {
      "Timestamp": "2017-07-20T15:57:59.9871163-07:00",
      "ProviderName": "Microsoft-ServiceFabric",
      "Id": 51477,
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Request url = https://localhost:19081/LocationApp/LocationFEService?zipcode=98052, verb = GET, remote (client) address = ::1, resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052, request processing start time =     15:58:00.074114 (745,608.196 MSec) ",
      "ProcessId": 57696,
      "Level": "Informational",
      "Keywords": "0x1000000000000021",
      "EventName": "ReverseProxy",
      "ActivityID": null,
      "RelatedActivityID": null,
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?zipcode=98052",
        "verb": "GET",
        "remoteAddress": "::1",
        "resolvedServiceUrl": "Https://localhost:8491/LocationApp/?zipcode=98052",
        "requestStartTime": "2017-07-20T15:58:00.0741142-07:00"
      }
    }

    {
      "Timestamp": "2017-07-20T16:00:01.3173605-07:00",
      ...
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Error while forwarding request tooservice: response status code = 504, description = Reverse proxy Timeout, phase = FinishSendRequest, internal error = ERROR_WINHTTP_TIMEOUT ",
      ...
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "statusCode": 504,
        "description": "Reverse Proxy Timeout",
        "sendRequestPhase": "FinishSendRequest",
        "errorDetails": "internal error = ERROR_WINHTTP_TIMEOUT"
      }
    }
    ```

2. <span data-ttu-id="b0dbc-121">El proxy inverso devuelve el código de estado de respuesta 404 (no encontrado).</span><span class="sxs-lookup"><span data-stu-id="b0dbc-121">Reverse proxy returns response status code 404 (Not Found).</span></span> 
    
    <span data-ttu-id="b0dbc-122">Este es un evento de ejemplo donde proxy inverso devuelve 404 porque se produjo un error hello toofind que coincidan con el extremo de servicio.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-122">Here is an example event where reverse proxy returns 404 since it failed toofind hello matching service endpoint.</span></span>
    <span data-ttu-id="b0dbc-123">las entradas de carga de Hola de interés aquí son:</span><span class="sxs-lookup"><span data-stu-id="b0dbc-123">hello payload  entries of interest here are:</span></span>
    *  <span data-ttu-id="b0dbc-124">**processRequestPhase**: indica la fase de Hola durante el procesamiento de la solicitud cuando se produjo el error de hello, ***TryGetEndpoint*** sólo</span><span class="sxs-lookup"><span data-stu-id="b0dbc-124">**processRequestPhase**: Indicates hello phase during request processing when hello failure occurred, ***TryGetEndpoint*** i.e</span></span> <span data-ttu-id="b0dbc-125">al tratar de toofetch Hola servicio extremo tooforward a.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-125">while trying toofetch hello service endpoint tooforward to.</span></span> 
    *  <span data-ttu-id="b0dbc-126">**errorDetails**: enumera los criterios de búsqueda de extremo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-126">**errorDetails**: Lists hello endpoint search criteria.</span></span> <span data-ttu-id="b0dbc-127">Aquí puede ver que listenerName Hola especificado = **FrontEndListener** , mientras que la lista de extremos de réplica de hello contiene sólo un agente de escucha con el nombre de hello **OldListener**.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-127">Here you can see that hello listenerName specified = **FrontEndListener** whereas hello replica endpoint list only contains a listener with hello name **OldListener**.</span></span>
    
    ```
    {
      ...
      "Message": "c1cca3b7-f85d-4fef-a162-88af23604343 Error while processing request, cannot forward tooservice: request url = https://localhost:19081/LocationApp/LocationFEService?ListenerName=FrontEndListener&zipcode=98052, verb = GET, remote (client) address = ::1, request processing start time = 16:43:02.686271 (3,448,220.353 MSec), error = FABRIC_E_ENDPOINT_NOT_FOUND, message = , phase = TryGetEndoint, SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"\":\"Https:\/\/localhost:8491\/LocationApp\/\"}} ",
      "ProcessId": 57696,
      "Level": "Warning",
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "c1cca3b7-f85d-4fef-a162-88af23604343",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?ListenerName=NewListener&zipcode=98052",
        ...
        "processRequestPhase": "TryGetEndoint",
        "errorDetails": "SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Https:\/\/localhost:8491\/LocationApp\/\"}}"
      }
    }
    ```
    <span data-ttu-id="b0dbc-128">Otro ejemplo donde proxy inverso puede devolver 404 no encontrado es: parámetro de configuración de ApplicationGateway\Http **SecureOnlyMode** se establece tootrue con proxy inverso Hola escuchando en **HTTPS**, Sin embargo, todos los puntos de conexión de réplica de hello son no seguras (escucha de HTTP).</span><span class="sxs-lookup"><span data-stu-id="b0dbc-128">Another example where reverse proxy can return 404 Not Found is: ApplicationGateway\Http configuration parameter **SecureOnlyMode** is set tootrue with hello reverse proxy listening on **HTTPS**, however all of hello replica endpoints are unsecure (listening on HTTP).</span></span>
    <span data-ttu-id="b0dbc-129">Invertir devuelve proxy 404 puesto que no se encuentra un punto de conexión escuchando en la solicitud HTTPS tooforward Hola.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-129">Reverse proxy returns 404 since it cannot find an endpoint listening on HTTPS tooforward hello request.</span></span> <span data-ttu-id="b0dbc-130">Analizar los parámetros de Hola de carga del evento Hola ayuda toonarrow problema hello:</span><span class="sxs-lookup"><span data-stu-id="b0dbc-130">Analyzing hello parameters in hello event payload helps toonarrow down hello issue:</span></span>
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. <span data-ttu-id="b0dbc-131">Error de proxy inverso de toohello con un error de tiempo de espera de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-131">Request toohello reverse proxy fails with a timeout error.</span></span> 
    <span data-ttu-id="b0dbc-132">registros de eventos de Hello contienen un evento con los detalles de la solicitud de hello recibido (no mostradas aquí).</span><span class="sxs-lookup"><span data-stu-id="b0dbc-132">hello event logs contain an event with hello received request details (not shown here).</span></span>
    <span data-ttu-id="b0dbc-133">siguiente evento de Hello muestra que el servicio de hello respondió con un código de 404 estado y proxy inverso inicia volver a resolver.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-133">hello next event shows that hello service responded with a 404 status code and reverse proxy initiates a re-resolve.</span></span> 

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Request tooservice returned: status code = 404, status description = , Reresolving ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "statusCode": 404,
        "statusDescription": ""
      }
    }
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Re-resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052 ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "requestUrl": "Https://localhost:8491/LocationApp/?zipcode=98052"
      }
    }
    ```
    <span data-ttu-id="b0dbc-134">Al recopilar todos los eventos de hello, verá un tren de eventos que muestra cada resolución y el intento de reenvío.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-134">When collecting all hello events, you see a train of events showing every resolve and forward attempt.</span></span>
    <span data-ttu-id="b0dbc-135">último evento de Hello en serie de hello muestra error al procesar la solicitud Hola con un tiempo de espera, junto con el número de Hola de intentos de resolución correcta.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-135">hello last event in hello series shows hello request processing has failed with a timeout, along with hello number of successful resolve attempts.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="b0dbc-136">Se recomienda la recopilación de eventos de canal detallado tookeep Hola deshabilitada de forma predeterminada y habilitarla para solucionar el problema según una necesidad.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-136">It is recommended tookeep hello  verbose channel event collection disabled by default and enable it for troubleshooting on a need basis.</span></span>

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Error while processing request: number of successful resolve attempts = 12, error = FABRIC_E_TIMEOUT, message = , phase = ResolveServicePartition,  ",
      "EventName": "ReverseProxy",
      ...
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "resolveCount": 12,
        "errorval": -2147017729,
        "errorMessage": "",
        "processRequestPhase": "ResolveServicePartition",
        "errorDetails": ""
      }
    }
    ```
    
    <span data-ttu-id="b0dbc-137">Si está habilitada la recolección crítico/error solo para eventos de, verá un evento con detalles sobre el tiempo de espera de Hola y número de Hola de intentos de resolución.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-137">If collection is enabled for critical/error events only, you see one event with details about hello timeout and hello number of resolve attempts.</span></span> 
    
    <span data-ttu-id="b0dbc-138">Si tiene intención de servicio de hello toosend un usuario toohello atrás de código de 404 estado, debe ir acompañado de un encabezado "X-ServiceFabric".</span><span class="sxs-lookup"><span data-stu-id="b0dbc-138">If hello service intends toosend a 404 status code back toohello user, it should be accompanied by an "X-ServiceFabric" header.</span></span> <span data-ttu-id="b0dbc-139">Después de solucionar esto, verá que el proxy inverso reenvía Hola estado código toohello atrás cliente.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-139">After fixing this, you will see that reverse proxy forwards hello status code back toohello client.</span></span>  

4. <span data-ttu-id="b0dbc-140">Casos cuando se ha desconectado el cliente de Hola Hola solicitud.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-140">Cases when hello client has disconnected hello request.</span></span>

    <span data-ttu-id="b0dbc-141">Hola por debajo de evento se registra cuando el proxy inverso está reenviando Hola respuesta tooclient pero Hola cliente se desconecta:</span><span class="sxs-lookup"><span data-stu-id="b0dbc-141">hello below event is recorded when reverse proxy is forwarding hello response tooclient but hello client disconnects:</span></span>

    ```
    {
      ...
      "Message": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8 Unable toosend response tooclient: phase = SendResponseHeaders, error = -805306367, internal error = ERROR_SUCCESS ",
      "ProcessId": 57696,
      "Level": "Warning",
      ...
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8",
        "sendResponsePhase": "SendResponseHeaders",
        "errorval": -805306367,
        "winHttpError": "ERROR_SUCCESS"
      }
    }
    ```

> [!NOTE]
> <span data-ttu-id="b0dbc-142">Procesamiento de solicitudes de eventos relacionados toowebsocket no han iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-142">Events related toowebsocket request processing are not currently logged.</span></span> <span data-ttu-id="b0dbc-143">Se agregará en la siguiente versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-143">This will be added in hello next release.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0dbc-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b0dbc-144">Next steps</span></span>
* <span data-ttu-id="b0dbc-145">[Agregación de eventos y recopilación mediante Microsoft Azure Dignostics](service-fabric-diagnostics-event-aggregation-wad.md) para habilitar la recopilación de registros en clústeres de Azure.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-145">[Event aggregation and collection using Windows Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) for enabling log collection in Azure clusters.</span></span>
* <span data-ttu-id="b0dbc-146">eventos de Service Fabric tooview en Visual Studio, vea [Monitor y diagnosticar localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="b0dbc-146">tooview Service Fabric events in Visual Studio, see [Monitor and diagnose locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>
* <span data-ttu-id="b0dbc-147">Consulte demasiado[configurar los servicios de proxy inverso tooconnect toosecure](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) ejemplos de plantilla para el Administrador de recursos de Azure tooconfigure proxy inverso seguro con opciones de validación de certificados de servicio diferente de Hola.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-147">Refer too[Configure reverse proxy tooconnect toosecure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples tooconfigure secure reverse proxy with hello different service certificate validation options.</span></span>
* <span data-ttu-id="b0dbc-148">Lectura [proxy inverso de Service Fabric](service-fabric-reverseproxy.md) toolearn más.</span><span class="sxs-lookup"><span data-stu-id="b0dbc-148">Read [Service Fabric reverse proxy](service-fabric-reverseproxy.md) toolearn more.</span></span>
