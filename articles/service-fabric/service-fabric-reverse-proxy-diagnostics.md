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
# <a name="monitor-and-diagnose-request-processing-at-hello-reverse-proxy"></a>Supervisar y diagnosticar el procesamiento de solicitudes de proxy inverso de Hola

A partir de hello 5.7 versión de Service Fabric, eventos de proxy inverso están disponibles para la colección. Hola eventos están disponibles en dos canales, uno con solo los eventos de error relacionados con error de procesamiento de toorequest en proxy inverso de Hola y el segundo canal que contiene eventos detallados de entradas para las solicitudes correctas e incorrectas.

Consulte demasiado[recopilar eventos de proxy inverso](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable recopilar eventos de estos canales de clústeres de Azure Service Fabric y local.

## <a name="troubleshoot-using-diagnostics-logs"></a>Solución de problemas mediante la herramienta de diagnóstico
Estos son algunos ejemplos de cómo puede encontrar los que uno de los registros de error comunes toointerpret hello:

1. El proxy inverso devuelve el código de estado de respuesta 504 (tiempo de espera agotado).

    Un motivo puede ser debido a error del servicio toohello tooreply dentro del período de tiempo de espera de solicitud de Hola.
evento primera Hola siguiente registra los detalles de Hola de solicitud de saludo recibida en proxy inverso de Hola. Hello segundo evento indica que Hola solicitud un error mientras tooservice de reenvío, mucha demasiado "error interno = ERROR_WINHTTP_TIMEOUT" 

    Hola carga incluye:

    *  **traceId**: este GUID se puede utilizar toocorrelate todos los eventos de hello correspondiente tooa única solicitud. Hola por debajo de los dos eventos, Hola traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, lo que implica pertenecen toohello misma solicitud.
    *  **requestUrl**: Hola URL (dirección URL de proxy inverso) toowhich Hola solicitud fue enviada.
    *  **verb**: verbo HTTP.
    *  **remoteAddress**: dirección del cliente que envía la solicitud de saludo.
    *  **resolvedServiceUrl**: solicitud entrante de Hola de toowhich punto de conexión de dirección URL de servicio se ha resuelto. 
    *  **errorDetails**: información adicional sobre los errores de Hola.

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

2. El proxy inverso devuelve el código de estado de respuesta 404 (no encontrado). 
    
    Este es un evento de ejemplo donde proxy inverso devuelve 404 porque se produjo un error hello toofind que coincidan con el extremo de servicio.
    las entradas de carga de Hola de interés aquí son:
    *  **processRequestPhase**: indica la fase de Hola durante el procesamiento de la solicitud cuando se produjo el error de hello, ***TryGetEndpoint*** sólo al tratar de toofetch Hola servicio extremo tooforward a. 
    *  **errorDetails**: enumera los criterios de búsqueda de extremo de Hola. Aquí puede ver que listenerName Hola especificado = **FrontEndListener** , mientras que la lista de extremos de réplica de hello contiene sólo un agente de escucha con el nombre de hello **OldListener**.
    
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
    Otro ejemplo donde proxy inverso puede devolver 404 no encontrado es: parámetro de configuración de ApplicationGateway\Http **SecureOnlyMode** se establece tootrue con proxy inverso Hola escuchando en **HTTPS**, Sin embargo, todos los puntos de conexión de réplica de hello son no seguras (escucha de HTTP).
    Invertir devuelve proxy 404 puesto que no se encuentra un punto de conexión escuchando en la solicitud HTTPS tooforward Hola. Analizar los parámetros de Hola de carga del evento Hola ayuda toonarrow problema hello:
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. Error de proxy inverso de toohello con un error de tiempo de espera de la solicitud. 
    registros de eventos de Hello contienen un evento con los detalles de la solicitud de hello recibido (no mostradas aquí).
    siguiente evento de Hello muestra que el servicio de hello respondió con un código de 404 estado y proxy inverso inicia volver a resolver. 

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
    Al recopilar todos los eventos de hello, verá un tren de eventos que muestra cada resolución y el intento de reenvío.
    último evento de Hello en serie de hello muestra error al procesar la solicitud Hola con un tiempo de espera, junto con el número de Hola de intentos de resolución correcta.
    
    > [!NOTE]
    > Se recomienda la recopilación de eventos de canal detallado tookeep Hola deshabilitada de forma predeterminada y habilitarla para solucionar el problema según una necesidad.

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
    
    Si está habilitada la recolección crítico/error solo para eventos de, verá un evento con detalles sobre el tiempo de espera de Hola y número de Hola de intentos de resolución. 
    
    Si tiene intención de servicio de hello toosend un usuario toohello atrás de código de 404 estado, debe ir acompañado de un encabezado "X-ServiceFabric". Después de solucionar esto, verá que el proxy inverso reenvía Hola estado código toohello atrás cliente.  

4. Casos cuando se ha desconectado el cliente de Hola Hola solicitud.

    Hola por debajo de evento se registra cuando el proxy inverso está reenviando Hola respuesta tooclient pero Hola cliente se desconecta:

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
> Procesamiento de solicitudes de eventos relacionados toowebsocket no han iniciado sesión. Se agregará en la siguiente versión de Hola.

## <a name="next-steps"></a>Pasos siguientes
* [Agregación de eventos y recopilación mediante Microsoft Azure Dignostics](service-fabric-diagnostics-event-aggregation-wad.md) para habilitar la recopilación de registros en clústeres de Azure.
* eventos de Service Fabric tooview en Visual Studio, vea [Monitor y diagnosticar localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).
* Consulte demasiado[configurar los servicios de proxy inverso tooconnect toosecure](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) ejemplos de plantilla para el Administrador de recursos de Azure tooconfigure proxy inverso seguro con opciones de validación de certificados de servicio diferente de Hola.
* Lectura [proxy inverso de Service Fabric](service-fabric-reverseproxy.md) toolearn más.
