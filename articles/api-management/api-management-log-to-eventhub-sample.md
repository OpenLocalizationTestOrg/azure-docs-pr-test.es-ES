---
title: "Supervisión de API con Azure API Management, Event Hubs y Runscope | Microsoft Docs"
description: "Aplicación de ejemplo que muestra la directiva log-to-eventhub que conecta API Management de Azure, Event Hubs de Azure y Runscope para el registro y supervisión de HTTP"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: c528cf6f-5f16-4a06-beea-fa1207541a47
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 70ee752c5639c90f77dde104ce85eec0a1062300
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="c6eb1-103">Supervisión de API con Administración de API de Azure, Centros de eventos y Runscope</span><span class="sxs-lookup"><span data-stu-id="c6eb1-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="c6eb1-104">El [servicio Administración de API](api-management-key-concepts.md) proporciona muchas capacidades para mejorar el procesamiento de solicitudes de HTTP enviadas a la API HTTP.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-104">The [API Management service](api-management-key-concepts.md) provides many capabilities to enhance the processing of HTTP requests sent to your HTTP API.</span></span> <span data-ttu-id="c6eb1-105">Sin embargo, la existencia de las solicitudes y respuestas son transitorias.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-105">However, the existence of the requests and responses are transient.</span></span> <span data-ttu-id="c6eb1-106">Se realiza la solicitud y fluye a través del servicio Administración de API a la API de back-end.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-106">The request is made and it flows through the API Management service to your backend API.</span></span> <span data-ttu-id="c6eb1-107">La API procesa la solicitud y se pasa una respuesta al consumidor de API.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-107">Your API processes the request and a response flows back through to the API consumer.</span></span> <span data-ttu-id="c6eb1-108">El servicio Administración de API mantiene algunas estadísticas importantes acerca de las API que se muestran en el panel del portal de Publisher, pero aparte de eso, los detalles desaparecen.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-108">The API Management service keeps some important statistics about the APIs for display in the Publisher portal dashboard, but beyond that, the details are gone.</span></span>

<span data-ttu-id="c6eb1-109">Mediante la [directiva](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [log-to-eventhub](api-management-howto-policies.md) en el servicio API Management, puede enviar los detalles de la solicitud y la respuesta a un [Centro de eventos de Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="c6eb1-109">By using the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in the API Management service you can send any details from the request and response to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="c6eb1-110">Existen diversos motivos por los que puede desear generar eventos de mensajes HTTP que se envían a las API.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-110">There are a variety of reasons why you may want to generate events from HTTP messages being sent to your APIs.</span></span> <span data-ttu-id="c6eb1-111">Algunos ejemplos incluyen la traza de auditoría de las actualizaciones, análisis de uso, las alertas de excepción e integraciones de terceros.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="c6eb1-112">Este artículo muestra cómo capturar el mensaje de solicitud y respuesta de HTTP completo, enviarlo a un Centro de eventos y, a continuación, retransmitir ese mensaje a un servicio que proporciona servicios de registro y supervisión de HTTP.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-112">This article demonstrates how to capture the entire HTTP request and response message, send it to an Event Hub and then relay that message to a third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="c6eb1-113">¿Por qué se envían desde el servicio Administración de API?</span><span class="sxs-lookup"><span data-stu-id="c6eb1-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="c6eb1-114">Es posible escribir middleware HTTP que se puede conectar a los marcos API HTTP para capturar solicitudes y respuestas de HTTP e introducirlas en sistemas de registro y supervisión.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-114">It is possible to write HTTP middleware that can plug into HTTP API frameworks to capture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="c6eb1-115">El inconveniente de este enfoque es que el middleware HTTP debe integrarse en la API de back-end y debe coincidir con la plataforma de la API.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-115">The downside to this approach is the HTTP middleware needs to be integrated into the backend API and must match the platform of the API.</span></span> <span data-ttu-id="c6eb1-116">Si hay varias API, todas deben implementar el middleware.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-116">If there are multiple APIs then each one must deploy the middleware.</span></span> <span data-ttu-id="c6eb1-117">A menudo existen motivos por los que no se pueden actualizar las API de back-end.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="c6eb1-118">El usp del servicio Administración de API de Azure para la integración con la infraestructura de registro proporciona una solución centralizada e independiente de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-118">Using the Azure API Management service to integrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="c6eb1-119">También es escalable, en parte debido a las capacidades de [replicación geográfica](api-management-howto-deploy-multi-region.md) de Administración de API de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-119">It is also scalable, in part due to the [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-to-an-azure-event-hub"></a><span data-ttu-id="c6eb1-120">¿Por qué se envía a un Centro de eventos de Azure?</span><span class="sxs-lookup"><span data-stu-id="c6eb1-120">Why send to an Azure Event Hub?</span></span>
<span data-ttu-id="c6eb1-121">Es razonable preguntar por qué crear una directiva que es específica de Centros de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="c6eb1-121">It is a reasonable to ask, why create a policy that is specific to Azure Event Hubs?</span></span> <span data-ttu-id="c6eb1-122">Hay muchos lugares diferentes donde puede ser conveniente registrar mis solicitudes.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-122">There are many different places where I might want to log my requests.</span></span> <span data-ttu-id="c6eb1-123">¿Por qué no simplemente enviar las solicitudes directamente al destino final?</span><span class="sxs-lookup"><span data-stu-id="c6eb1-123">Why not just send the requests directly to the final destination?</span></span>  <span data-ttu-id="c6eb1-124">Es una opción.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-124">That is an option.</span></span> <span data-ttu-id="c6eb1-125">Sin embargo, al realizar solicitudes de registro de un servicio Administración de API, es necesario tener en cuenta cómo afectarán los mensajes de registro al rendimiento de la API.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-125">However, when making logging requests from an API management service, it is necessary to consider how logging messages will impact the performance of the API.</span></span> <span data-ttu-id="c6eb1-126">Para manejar los aumentos graduales de la carga puede aumentar las instancias disponibles de los componentes del sistema o aprovechar las ventajas de la replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="c6eb1-127">Sin embargo, picos de tráfico cortos pueden hacer que las solicitudes se retrasen significativamente si las solicitudes a la infraestructura de registro empiezan a ralentizarse debido a la carga.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-127">However, short spikes in traffic can cause requests to be significantly delayed if requests to logging infrastructure start to slow under load.</span></span>

<span data-ttu-id="c6eb1-128">Centros de eventos de Azure está diseñado para la entrada de grandes volúmenes de datos, con capacidad para tratar con un número mucho mayor de eventos que el número de solicitudes de HTTP que procesan la mayoría de las API.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-128">The Azure Event Hubs is designed to ingress huge volumes of data, with capacity for dealing with a far higher number of events than the number of HTTP requests most APIs process.</span></span> <span data-ttu-id="c6eb1-129">El Centro de eventos actúa como un tipo de búfer sofisticada entre el servicio Administración de API y la infraestructura que almacena y procesa los mensajes.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-129">The Event Hub acts as a kind of sophisticated buffer between your API management service and the infrastructure that will store and process the messages.</span></span> <span data-ttu-id="c6eb1-130">Esto garantiza que no se verá afectado el rendimiento de la API debido a la infraestructura de registro.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-130">This ensures that your API performance will not suffer due to the logging infrastructure.</span></span>  

<span data-ttu-id="c6eb1-131">Una vez que los datos se han pasado a un Centro de eventos, se conservan y esperan a que los consumidores del centro de eventos los procese.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-131">Once the data has been passed to an Event Hub it is persisted and will wait for Event Hub consumers to process it.</span></span> <span data-ttu-id="c6eb1-132">Al Centro de eventos no le importa cómo se procesará, simplemente se ocupa de asegurarse de que el mensaje se entregará correctamente.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-132">The Event Hub does not care how it will be processed, it just cares about making sure the message will be successfully delivered.</span></span>     

<span data-ttu-id="c6eb1-133">Centros de eventos tiene la capacidad de transmitir eventos a varios grupos de consumidores.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-133">Event Hubs have the ability to stream events to multiple consumer groups.</span></span> <span data-ttu-id="c6eb1-134">Esto permite que sistemas completamente diferentes procesen los eventos.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-134">This allows events to be processed by completely different systems.</span></span> <span data-ttu-id="c6eb1-135">Esto permite muchos escenarios de integración sin agregar retrasos en el procesamiento de la solicitud de API dentro del servicio Administración de API, ya que solo es necesario generar un evento.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-135">This enables supporting many integration scenarios without putting addition delays on the processing of the API request within the API Management service as only one event needs to be generated.</span></span>

## <a name="a-policy-to-send-applicationhttp-messages"></a><span data-ttu-id="c6eb1-136">Una directiva para enviar mensajes de aplicación/http</span><span class="sxs-lookup"><span data-stu-id="c6eb1-136">A policy to send application/http messages</span></span>
<span data-ttu-id="c6eb1-137">Un Centro de eventos acepta datos de eventos como una cadena simple.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="c6eb1-138">El contenido de esa cadena depende completamente de usted.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-138">The contents of that string are completely up to you.</span></span> <span data-ttu-id="c6eb1-139">Para poder empaquetar una solicitud de HTTP y enviarla a Centros de eventos, debemos formatear la cadena con la información de solicitud o respuesta.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-139">To be able to package up an HTTP request and send it off to Event Hubs we need to format the string with the request or response information.</span></span> <span data-ttu-id="c6eb1-140">En situaciones como esta, si hay un formato existente que podamos reusar, es posible que no necesitemos escribir nuestro propio código de análisis.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-140">In situations like this, if there is an existing format we can reuse, then we may not have to write our own parsing code.</span></span> <span data-ttu-id="c6eb1-141">Inicialmente consideré el uso de [HAR](http://www.softwareishard.com/blog/har-12-spec/) para enviar solicitudes y respuestas de HTTP.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-141">Initially I considered using the [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="c6eb1-142">Sin embargo, este formato está optimizado para almacenar una secuencia de solicitudes de HTTP en un formato basado en JSON.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="c6eb1-143">Contenía un número de elementos obligatorios que agregaba una complejidad innecesaria para el escenario de pasar el mensaje HTTP a través del cable.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-143">It contained a number of mandatory elements that added unnecessary complexity for the scenario of passing the HTTP message over the wire.</span></span>  

<span data-ttu-id="c6eb1-144">Una opción alternativa era usar el tipo de soporte físico `application/http` , como se describe en la especificación HTTP [RFC 7230](http://tools.ietf.org/html/rfc7230).</span><span class="sxs-lookup"><span data-stu-id="c6eb1-144">An alternative option was to use the `application/http` media type as described in the HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="c6eb1-145">Este tipo de soporte físico usa el mismo formato que se usa para enviar realmente mensajes de HTTP a través del cable, pero el mensaje completo se puede colocar en el cuerpo de otra solicitud de HTTP.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-145">This media type uses the exact same format that is used to actually send HTTP messages over the wire, but the entire message can be put in the body of another HTTP request.</span></span> <span data-ttu-id="c6eb1-146">En nuestro caso simplemente vamos a usar el cuerpo como nuestro mensaje para enviarlo a Centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-146">In our case we are just going to use the body as our message to send to Event Hubs.</span></span> <span data-ttu-id="c6eb1-147">Convenientemente, hay un analizador en las bibliotecas de [Microsoft ASP.NET Web API 2.2 Cliente](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) que puede analizar este formato y convertirlo a `HttpRequestMessage` nativo y objetos `HttpResponseMessage`.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into the native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="c6eb1-148">Para poder crear este mensaje debemos aprovechar las [expresiones de directiva](https://msdn.microsoft.com/library/azure/dn910913.aspx) basadas en C# en Administración de API de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-148">To be able to create this message we need to take advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="c6eb1-149">A continuación se proporciona la directiva que envía un mensaje de solicitud de HTTP a Centros de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-149">Here is the policy which sends a HTTP request message to Azure Event Hubs.</span></span>

```xml
<log-to-eventhub logger-id="conferencelogger" partition-id="0">
@{
   var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                               context.Request.Method,
                                               context.Request.Url.Path + context.Request.Url.QueryString);

   var body = context.Request.Body?.As<string>(true);
   if (body != null && body.Length > 1024)
   {
       body = body.Substring(0, 1024);
   }

   var headers = context.Request.Headers
                          .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                          .ToArray<string>();

   var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

   return "request:"   + context.Variables["message-id"] + "\n"
                       + requestLine + headerString + "\r\n" + body;
}
</log-to-eventhub>
```

### <a name="policy-declaration"></a><span data-ttu-id="c6eb1-150">Declaración de directiva</span><span class="sxs-lookup"><span data-stu-id="c6eb1-150">Policy declaration</span></span>
<span data-ttu-id="c6eb1-151">Hay algunas cosas específicas que merece la pena mencionar acerca de esta expresión de directiva.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="c6eb1-152">La directiva log-to-eventhub tiene un atributo denominado logger-id que hace referencia al nombre del registrador que se ha creado en el servicio Administración de API.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-152">The log-to-eventhub policy has an attribute called logger-id which refers to the name of logger that has been created within the API Management service.</span></span> <span data-ttu-id="c6eb1-153">Los detalles de cómo configurar un registrador del Centro de eventos en el servicio Administración de API pueden encontrarse en el documento [Cómo registrar eventos en los centros de eventos de Azure en Administración de API de Azure](api-management-howto-log-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="c6eb1-153">The details of how to setup an Event Hub logger in the API Management service can be found in the document [How to log events to Azure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="c6eb1-154">El segundo atributo es un parámetro opcional que indica a Centros de eventos en qué partición almacenar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-154">The second attribute is an optional parameter that instructs Event Hubs which partition to store the message in.</span></span> <span data-ttu-id="c6eb1-155">Centros de eventos usa particiones para habilitar la escalabilidad y requiere un mínimo de dos.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-155">Event Hubs use partitions to enable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="c6eb1-156">La entrega ordenada de mensajes solo se garantiza dentro de una partición.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-156">The ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="c6eb1-157">Si no se indica al Centro de eventos en qué partición desea colocar el mensaje, usará un algoritmo round-robin para distribuir la carga.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-157">If we do not instruct Event Hub in which partition to place the message, it will use a round-robin algorithm to distribute the load.</span></span> <span data-ttu-id="c6eb1-158">Sin embargo, eso puede hacer que algunos de nuestros mensajes no se procesen en el orden correcto.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-158">However, that may cause some of our messages to be processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="c6eb1-159">Particiones</span><span class="sxs-lookup"><span data-stu-id="c6eb1-159">Partitions</span></span>
<span data-ttu-id="c6eb1-160">Para garantizar que nuestros mensajes se entregan a los consumidores en orden y aprovechar la capacidad de distribución de carga de las particiones, elegí enviar mensajes de solicitud de HTTP a una partición y los mensajes de respuesta de HTTP a una segunda partición.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-160">To ensure our messages are delivered to consumers in order and take advantage of the load distribution capability of partitions, I chose to send HTTP request messages to one partition and HTTP response messages to a second partition.</span></span> <span data-ttu-id="c6eb1-161">Esto garantiza una distribución equilibrada de la carga y podemos garantizar que se consumirán todas las solicitudes en orden y todas las respuestas se consumirán en orden.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="c6eb1-162">Es posible que una respuesta se consuma antes de la solicitud correspondiente, pero como esto no es un problema porque tenemos un mecanismo diferente para correlacionar las solicitudes a las respuestas y sabemos que las solicitudes van siempre antes las respuestas.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-162">It is possible for a response to be consumed before the corresponding request, but as that is not a problem as we have a different mechanism for correlating requests to responses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="c6eb1-163">Cargas de HTTP</span><span class="sxs-lookup"><span data-stu-id="c6eb1-163">HTTP payloads</span></span>
<span data-ttu-id="c6eb1-164">Después de crear el `requestLine` comprobamos si se debe truncar el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-164">After building the `requestLine` we check to see if the request body should be truncated.</span></span> <span data-ttu-id="c6eb1-165">El cuerpo de la solicitud se trunca a solo 1024.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-165">The request body is truncated to only 1024.</span></span> <span data-ttu-id="c6eb1-166">Esto podría aumentarse; sin embargo, los mensajes individuales del Centro de eventos están limitados a 256 KB, por lo que es probable que algunos cuerpos de los mensajes HTTP no quepan en un único mensaje.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-166">This could be increased, however individual Event Hub messages are limited to 256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="c6eb1-167">Al realizar el registro y análisis, una cantidad significativa de información puede derivarse simplemente de la línea de solicitud de HTTP y los encabezados.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-167">When doing logging and analytics a significant amount of information can be derived from just the HTTP request line and headers.</span></span> <span data-ttu-id="c6eb1-168">Además, muchas solicitudes de API devuelven solo cuerpos pequeños, por lo que la pérdida de valor de la información debido al truncamiento de cuerpos grandes es bastante mínima en comparación con la reducción de los costos de almacenamiento, transferencia y transformación para mantener todo el contenido del cuerpo.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-168">Also, many API requests only return small bodies and so the loss of information value by truncating large bodies is fairly minimal in comparison to the reduction in transfer, processing and storage costs to keep all body contents.</span></span> <span data-ttu-id="c6eb1-169">Una nota final acerca del procesamiento del cuerpo es que necesitamos pasar `true` al método As<string>() porque leemos el contenido del cuerpo, pero también queríamos que la API de back-end pudiera leer el cuerpo.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-169">One final note about processing the body is that we need to pass `true` to the As<string>() method because we are reading the body contents, but was also want the backend API to be able to read the body.</span></span> <span data-ttu-id="c6eb1-170">Al pasar true a este método, hacemos que el cuerpo se almacene en la búfer para que se pueda leer una segunda vez.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-170">By passing true to this method we cause the body to be buffered so that it can be read a second time.</span></span> <span data-ttu-id="c6eb1-171">Es importante tenerlo en cuenta si tiene una API que carga archivos muy grandes o usa el sondeo largo.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-171">This is important to be aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="c6eb1-172">En estos casos, es mejor evitar totalmente la lectura del cuerpo.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-172">In these cases it would be best to avoid reading the body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="c6eb1-173">Encabezados HTTP</span><span class="sxs-lookup"><span data-stu-id="c6eb1-173">HTTP headers</span></span>
<span data-ttu-id="c6eb1-174">Los encabezados HTTP pueden transferirse simplemente al formato del mensaje con un formato simple de par clave/valor.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-174">HTTP Headers can be simply transferred over into the message format in a simple key/value pair format.</span></span> <span data-ttu-id="c6eb1-175">Hemos decidido eliminar ciertos campos de seguridad confidenciales para evitar la pérdida innecesaria de información de credenciales.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-175">We have chosen to strip out certain security sensitive fields, to avoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="c6eb1-176">No es probable que se usen claves de API y otras credenciales para los análisis.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="c6eb1-177">Si deseamos realizar el análisis en el usuario y el producto específico que usan, podíamos obtenerlo desde el objeto `context` y agregarlo al mensaje.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-177">If we wish to do analysis on the user and the particular product they are using then we could get that from the `context` object and add that to the message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="c6eb1-178">Metadatos del mensaje</span><span class="sxs-lookup"><span data-stu-id="c6eb1-178">Message Metadata</span></span>
<span data-ttu-id="c6eb1-179">Cuando se crea el mensaje completo para enviarlo al Centro de eventos, la primera línea no es realmente parte del mensaje `application/http` .</span><span class="sxs-lookup"><span data-stu-id="c6eb1-179">When building the complete message to send to the event hub, the first line is not actually part of the `application/http` message.</span></span> <span data-ttu-id="c6eb1-180">La primera línea son metadatos adicionales que incluyen si el mensaje es un mensaje de solicitud o de respuesta y un identificador de mensaje que se usa para correlacionar las solicitudes y las respuestas.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-180">The first line is additional metadata consisting of whether the message is a request or response message and a message id which is used to correlate requests to responses.</span></span> <span data-ttu-id="c6eb1-181">El identificador del mensaje se crea mediante otra directiva que tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="c6eb1-181">The message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="c6eb1-182">Podríamos haber creado el mensaje de solicitud, almacenarlo en una variable hasta que se devuelva la respuesta y, después, simplemente enviar la solicitud y la respuesta como un solo mensaje.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-182">We could have created the request message, stored that in a variable until the response was returned and then simply sent the request and response as a single message.</span></span> <span data-ttu-id="c6eb1-183">Sin embargo, al enviar la solicitud y la respuesta de forma independiente y usar un identificador de mensaje para correlacionar las dos, obtenemos un poco más flexibilidad en el tamaño de mensaje, la capacidad de aprovechar varias particiones al tiempo que se mantiene el orden de los mensajes y la solicitud aparecerá antes en nuestro panel de registro.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-183">However, by sending the request and response independently and using a message id to correlate the two, we get a bit more flexibility in the message size, the ability to take advantage of multiple partitions whilst maintaining message order and the request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="c6eb1-184">También puede haber algunos escenarios donde nunca se envíe una respuesta válida al Centro de eventos, posiblemente debido a un error de solicitud irrecuperable en el servicio Administración de API, pero aún tendremos un registro de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-184">There also may be some scenarios where a valid response is never sent to the event hub, possibly due to a fatal request error in the API Management service, but we still will have a record of the request.</span></span>

<span data-ttu-id="c6eb1-185">La directiva para enviar el mensaje de respuesta de HTTP es muy parecida a la solicitud; por tanto, la configuración de directiva completa tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="c6eb1-185">The policy to send the response HTTP message looks very similar to the request and so the complete policy configuration looks like this:</span></span>

```xml
<policies>
  <inbound>
      <set-variable name="message-id" value="@(Guid.NewGuid())" />
      <log-to-eventhub logger-id="conferencelogger" partition-id="0">
      @{
          var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                                      context.Request.Method,
                                                      context.Request.Url.Path + context.Request.Url.QueryString);

          var body = context.Request.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Request.Headers
                               .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                               .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                               .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "request:"   + context.Variables["message-id"] + "\n"
                              + requestLine + headerString + "\r\n" + body;
      }
  </log-to-eventhub>
  </inbound>
  <backend>
      <forward-request follow-redirects="true" />
  </backend>
  <outbound>
      <log-to-eventhub logger-id="conferencelogger" partition-id="1">
      @{
          var statusLine = string.Format("HTTP/1.1 {0} {1}\r\n",
                                              context.Response.StatusCode,
                                              context.Response.StatusReason);

          var body = context.Response.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Response.Headers
                                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                                          .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "response:"  + context.Variables["message-id"] + "\n"
                              + statusLine + headerString + "\r\n" + body;
     }
  </log-to-eventhub>
  </outbound>
</policies>
```

<span data-ttu-id="c6eb1-186">La directiva `set-variable` crea un valor que sea accesible por la directiva `log-to-eventhub` en la sección `<inbound>` y la sección `<outbound>`.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-186">The `set-variable` policy creates a value that is accessible by both the `log-to-eventhub` policy in the `<inbound>` section and the `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="c6eb1-187">Recepción de eventos de Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="c6eb1-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="c6eb1-188">Se reciben eventos del Centro de eventos de Azure mediante el [protocolo AMQP](http://www.amqp.org/).</span><span class="sxs-lookup"><span data-stu-id="c6eb1-188">Events from Azure Event Hub are received using the [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="c6eb1-189">El equipo del Bus de servicio de Microsoft hizo que las bibliotecas cliente disponibles para facilitar los eventos de consumo.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-189">The Microsoft Service Bus team have made client libraries available to make the consuming events easier.</span></span> <span data-ttu-id="c6eb1-190">Existen dos enfoques diferentes admitidos, uno se está un *Consumidor directo* y la otra es emplear la clase `EventProcessorHost`.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-190">There are two different approaches supported, one is being a *Direct Consumer* and the other is using the `EventProcessorHost` class.</span></span> <span data-ttu-id="c6eb1-191">Ejemplos de estos dos enfoques pueden encontrarse en la [Guía de programación de Centros de eventos](../event-hubs/event-hubs-programming-guide.md).</span><span class="sxs-lookup"><span data-stu-id="c6eb1-191">Examples of these two approaches can be found in the [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="c6eb1-192">La versión abreviada de las diferencias es que `Direct Consumer` proporciona un control total y `EventProcessorHost` realiza parte del trabajo de fontanería por usted, pero hace determinadas suposiciones sobre cómo procesará los eventos.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-192">The short version of the differences is, `Direct Consumer` gives you complete control and the `EventProcessorHost` does some of the plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="c6eb1-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="c6eb1-193">EventProcessorHost</span></span>
<span data-ttu-id="c6eb1-194">En este ejemplo, usaremos `EventProcessorHost` por motivos de simplicidad; sin embargo es posible que no sea la mejor opción para este escenario concreto.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-194">In this sample, we will use the `EventProcessorHost` for simplicity, however it may not the best choice for this particular scenario.</span></span> <span data-ttu-id="c6eb1-195">`EventProcessorHost` realiza el trabajo duro de asegurarse de que no tiene que preocuparse acerca de problemas de subprocesamiento dentro de una clase de procesador de eventos concreto.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-195">`EventProcessorHost` does the hard work of making sure you don't have to worry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="c6eb1-196">Sin embargo, en nuestro escenario, simplemente estamos convirtiendo el mensaje a otro formato y lo pasamos a otro servicio con un método asincrónico.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-196">However, in our scenario, we are simply converting the message to another format and passing it along to another service using an async method.</span></span> <span data-ttu-id="c6eb1-197">No es necesario actualizar el estado compartido y, por tanto, no hay riesgo de problemas de subprocesamiento.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="c6eb1-198">Para la mayoría de los escenarios, `EventProcessorHost` es probablemente la mejor opción y es ciertamente la opción más fácil.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-198">For most scenarios, `EventProcessorHost` is probably the best choice and it is certainly the easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="c6eb1-199">IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="c6eb1-199">IEventProcessor</span></span>
<span data-ttu-id="c6eb1-200">El concepto central al usar `EventProcessorHost` es crear una implementación de la interfaz `IEventProcessor` que contiene el método `ProcessEventAsync`.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-200">The central concept when using `EventProcessorHost` is to create a an implementation of the `IEventProcessor` interface which contains the method `ProcessEventAsync`.</span></span> <span data-ttu-id="c6eb1-201">La esencia de ese método se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="c6eb1-201">The essence of that method is shown here:</span></span>

```c#
async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
{

   foreach (EventData eventData in messages)
   {
       _Logger.LogInfo(string.Format("Event received from partition: {0} - {1}", context.Lease.PartitionId,eventData.PartitionKey));

       try
       {
           var httpMessage = HttpMessage.Parse(eventData.GetBodyStream());
           await _MessageContentProcessor.ProcessHttpMessage(httpMessage);
       }
       catch (Exception ex)
       {
           _Logger.LogError(ex.Message);
       }
   }
    ... checkpointing code snipped ...
}
```

<span data-ttu-id="c6eb1-202">Se pasa una lista de objetos EventData al método y realizamos la iteración en esa lista.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-202">A list of EventData objects are passed into the method and we iterate over that list.</span></span> <span data-ttu-id="c6eb1-203">Se analizan los bytes de cada método en un objeto HttpMessage y ese objeto se pasa a una instancia de IHttpMessageProcessor.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-203">The bytes of each method are parsed into a HttpMessage object and that object is passed to an instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="c6eb1-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="c6eb1-204">HttpMessage</span></span>
<span data-ttu-id="c6eb1-205">La instancia `HttpMessage` contiene tres elementos de datos:</span><span class="sxs-lookup"><span data-stu-id="c6eb1-205">The `HttpMessage` instance contains three pieces of data:</span></span>

```c#
public class HttpMessage
{
   public Guid MessageId { get; set; }
   public bool IsRequest { get; set; }
   public HttpRequestMessage HttpRequestMessage { get; set; }
   public HttpResponseMessage HttpResponseMessage { get; set; }

... parsing code snipped ...

}
```

<span data-ttu-id="c6eb1-206">La instancia `HttpMessage` contiene un GUID `MessageId` que nos permite conectar la solicitud de HTTP a la respuesta de HTTP correspondiente y un valor booleano que identifica si el objeto contiene una instancia de HttpRequestMessage y HttpResponseMessage.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-206">The `HttpMessage` instance contains a `MessageId` GUID that allows us to connect the HTTP request to the corresponding HTTP response and a boolean value that identifies if the object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="c6eb1-207">Mediante las clases HTTP integradas de `System.Net.Http`, pude aprovechar el código de análisis `application/http` que se incluye en `System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-207">By using the built in HTTP classes from `System.Net.Http`, I was able to take advantage of the `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="c6eb1-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="c6eb1-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="c6eb1-209">La instancia `HttpMessage` se reenvía a la implementación de `IHttpMessageProcessor` que es una interfaz que creé para desacoplar la recepción y la interpretación del evento del Centro de eventos de Azure y el procesamiento real de la misma.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-209">The `HttpMessage` instance is then forwarded to implementation of `IHttpMessageProcessor` which is an interface I created to decouple the receiving and interpretation of the event from Azure Event Hub and the actual processing of it.</span></span>

## <a name="forwarding-the-http-message"></a><span data-ttu-id="c6eb1-210">Reenvío del mensaje HTTP</span><span class="sxs-lookup"><span data-stu-id="c6eb1-210">Forwarding the HTTP message</span></span>
<span data-ttu-id="c6eb1-211">En este ejemplo, decidí que sería interesante insertar la solicitud de HTTP en [Runscope](http://www.runscope.com).</span><span class="sxs-lookup"><span data-stu-id="c6eb1-211">For this sample, I decided it would be interesting to push the HTTP Request over to [Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="c6eb1-212">Runscope es un servicio basado en la nube que se especializa en depuración, registro y supervisión de HTTP.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="c6eb1-213">Tiene un nivel gratuito, por lo que resulta fácil probarlo y nos permite ver en tiempo real cómo fluyen las solicitudes de HTTP a través de nuestro servicio Administración de API.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-213">They have a free tier, so it is easy to try and it allows us to see the HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="c6eb1-214">Las implementación `IHttpMessageProcessor` tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="c6eb1-214">The `IHttpMessageProcessor` implementation looks like this,</span></span>

```c#
public class RunscopeHttpMessageProcessor : IHttpMessageProcessor
{
   private HttpClient _HttpClient;
   private ILogger _Logger;
   private string _BucketKey;
   public RunscopeHttpMessageProcessor(HttpClient httpClient, ILogger logger)
   {
       _HttpClient = httpClient;
       var key = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-KEY", EnvironmentVariableTarget.User);
       _HttpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("bearer", key);
       _HttpClient.BaseAddress = new Uri("https://api.runscope.com");
       _BucketKey = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-BUCKET", EnvironmentVariableTarget.User);
       _Logger = logger;
   }

   public async Task ProcessHttpMessage(HttpMessage message)
   {
       var runscopeMessage = new RunscopeMessage()
       {
           UniqueIdentifier = message.MessageId
       };

       if (message.IsRequest)
       {
           _Logger.LogInfo("Sending HTTP request " + message.MessageId.ToString());
           runscopeMessage.Request = await RunscopeRequest.CreateFromAsync(message.HttpRequestMessage);
       }
       else
       {
           _Logger.LogInfo("Sending HTTP response " + message.MessageId.ToString());
           runscopeMessage.Response = await RunscopeResponse.CreateFromAsync(message.HttpResponseMessage);
       }

       var messagesLink = new MessagesLink() { Method = HttpMethod.Post };
       messagesLink.BucketKey = _BucketKey;
       messagesLink.RunscopeMessage = runscopeMessage;
       var runscopeResponse = await _HttpClient.SendAsync(messagesLink.CreateRequest());
       _Logger.LogDebug("Request sent to Runscope");
   }
}
```

<span data-ttu-id="c6eb1-215">Pude aprovechar una [biblioteca de cliente existente para Runscope`HttpResponseMessage` que facilita inserción de las instancias ](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) y `HttpRequestMessage` a su servicio.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-215">I was able to take advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy to push `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="c6eb1-216">Para tener acceso a la API Runscope, necesitará una cuenta y una clave de API.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-216">In order to access the Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="c6eb1-217">Pueden encontrarse instrucciones para obtener una clave de API en la presentación en pantalla [Creación de aplicaciones para acceder a la API Runscope](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) .</span><span class="sxs-lookup"><span data-stu-id="c6eb1-217">Instructions for getting an API key can be found in the [Creating Applications to Access Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="c6eb1-218">Ejemplo completo</span><span class="sxs-lookup"><span data-stu-id="c6eb1-218">Complete sample</span></span>
<span data-ttu-id="c6eb1-219">El [código fuente](https://github.com/darrelmiller/ApimEventProcessor) y las pruebas del ejemplo se encuentran en GitHub.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-219">The [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for the sample are on GitHub.</span></span> <span data-ttu-id="c6eb1-220">Necesitará un [servicio API Management](api-management-get-started.md), [un Centro de eventos conectado](api-management-howto-log-event-hubs.md) y una [cuenta de almacenamiento](../storage/common/storage-create-storage-account.md) para ejecutar el ejemplo usted mismo.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) to run the sample for yourself.</span></span>   

<span data-ttu-id="c6eb1-221">El ejemplo es simplemente una aplicación de consola simple que realiza escuchas de eventos procedentes del Centro de eventos, los convierte a objetos `HttpRequestMessage` y `HttpResponseMessage` y, a continuación, los reenvía a la API Runscope.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-221">The sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on to the Runscope API.</span></span>

<span data-ttu-id="c6eb1-222">En la siguiente imagen animada, puede ver una solicitud realizada a una API en el portal para desarrolladores, la aplicación de consola que muestra el mensaje que se recibe, procesa y reenvía y, a continuación, la solicitud y respuesta se muestra en el inspector de tráfico Runscope.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-222">In the following animated image, you can see a request being made to an API in the Developer Portal, the Console application showing the message being received, processed and forwarded and then the request and response showing up in the Runscope Traffic inspector.</span></span>

![Demostración de solicitud se reenvía a Runscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="c6eb1-224">Resumen</span><span class="sxs-lookup"><span data-stu-id="c6eb1-224">Summary</span></span>
<span data-ttu-id="c6eb1-225">El servicio de Administración de API de Azure proporciona un lugar ideal para capturar el tráfico de HTTP hacia y desde la API.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-225">Azure API Management service provides an ideal place to capture the HTTP traffic travelling to and from your APIs.</span></span> <span data-ttu-id="c6eb1-226">Centros de eventos de Azure es una solución altamente escalable y de bajo costo para capturar ese tráfico y colocarlo en sistemas de procesamiento secundario para el registro, supervisión y otros análisis sofisticados.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="c6eb1-227">La conexión a sistemas de supervisión del tráfico de terceros como Runscope es tan simple como las pocas docenas de líneas de código.</span><span class="sxs-lookup"><span data-stu-id="c6eb1-227">Connecting to 3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6eb1-228">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c6eb1-228">Next steps</span></span>
* <span data-ttu-id="c6eb1-229">Obtenga más información acerca de los centros de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="c6eb1-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="c6eb1-230">Introducción a los centros de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="c6eb1-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="c6eb1-231">Recepción de mensajes con EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="c6eb1-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="c6eb1-232">Guía de programación de Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="c6eb1-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="c6eb1-233">Obtener más información acerca de la integración de Administración de API y centros de eventos</span><span class="sxs-lookup"><span data-stu-id="c6eb1-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="c6eb1-234">Cómo registrar eventos en los centros de eventos de Azure en la administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="c6eb1-234">How to log events to Azure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="c6eb1-235">Referencia de entidad del registrador</span><span class="sxs-lookup"><span data-stu-id="c6eb1-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="c6eb1-236">referencia de la directiva log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="c6eb1-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
