---
title: "aaaMonitor API con administración de API de Azure, los concentradores de eventos y Runscope | Documentos de Microsoft"
description: "Aplicación de ejemplo que muestra la directiva de registro a eventhub Hola conexión administración de API de Azure, los concentradores de eventos de Azure y Runscope para HTTP de supervisión y registro"
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
ms.openlocfilehash: 7456a2436f3a2d7b815b70b65fca9481d39c5fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="57b85-103">Supervisión de API con Administración de API de Azure, Centros de eventos y Runscope</span><span class="sxs-lookup"><span data-stu-id="57b85-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="57b85-104">Hola [servicio de administración de API](api-management-key-concepts.md) proporciona muchas capacidades tooenhance Hola procesamiento de las solicitudes enviadas de HTTP tooyour API HTTP.</span><span class="sxs-lookup"><span data-stu-id="57b85-104">hello [API Management service](api-management-key-concepts.md) provides many capabilities tooenhance hello processing of HTTP requests sent tooyour HTTP API.</span></span> <span data-ttu-id="57b85-105">Sin embargo, Hola existencia de hello solicitudes y respuestas son transitorias.</span><span class="sxs-lookup"><span data-stu-id="57b85-105">However, hello existence of hello requests and responses are transient.</span></span> <span data-ttu-id="57b85-106">se realiza la solicitud de Hola y que fluye a través de backend de tooyour de servicio de administración de API de hello API.</span><span class="sxs-lookup"><span data-stu-id="57b85-106">hello request is made and it flows through hello API Management service tooyour backend API.</span></span> <span data-ttu-id="57b85-107">La API procesa la solicitud de hello y una respuesta fluye a través de consumidor toohello API.</span><span class="sxs-lookup"><span data-stu-id="57b85-107">Your API processes hello request and a response flows back through toohello API consumer.</span></span> <span data-ttu-id="57b85-108">Hola servicio de administración de API mantiene algunas estadísticas importantes sobre hello las API para su presentación en el panel del portal Hola publicador pero, aparte de eso, detalles Hola han desaparecido.</span><span class="sxs-lookup"><span data-stu-id="57b85-108">hello API Management service keeps some important statistics about hello APIs for display in hello Publisher portal dashboard, but beyond that, hello details are gone.</span></span>

<span data-ttu-id="57b85-109">Mediante el uso de hello [registro a eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [directiva](api-management-howto-policies.md) Hola servicio de administración de API puede enviar los detalles de tooan de solicitud y respuesta de hello [concentrador de eventos de Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="57b85-109">By using hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in hello API Management service you can send any details from hello request and response tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="57b85-110">Hay una variedad de razones por las que puede toogenerate eventos de mensajes HTTP que se envían tooyour API.</span><span class="sxs-lookup"><span data-stu-id="57b85-110">There are a variety of reasons why you may want toogenerate events from HTTP messages being sent tooyour APIs.</span></span> <span data-ttu-id="57b85-111">Algunos ejemplos incluyen la traza de auditoría de las actualizaciones, análisis de uso, las alertas de excepción e integraciones de terceros.</span><span class="sxs-lookup"><span data-stu-id="57b85-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="57b85-112">Este artículo demuestra cómo toocapture Hola toda solicitud y respuesta de mensaje HTTP, enviar tooan concentrador de eventos y, a continuación, ese servicio de terceros de tooa de mensaje que proporciona servicios de supervisión y registro de HTTP de retransmisión.</span><span class="sxs-lookup"><span data-stu-id="57b85-112">This article demonstrates how toocapture hello entire HTTP request and response message, send it tooan Event Hub and then relay that message tooa third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="57b85-113">¿Por qué se envían desde el servicio Administración de API?</span><span class="sxs-lookup"><span data-stu-id="57b85-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="57b85-114">Es posible toowrite middleware HTTP que se conecte a la API HTTP marcos toocapture solicitudes y respuestas HTTP e introducirlos en sistemas de supervisión y registro.</span><span class="sxs-lookup"><span data-stu-id="57b85-114">It is possible toowrite HTTP middleware that can plug into HTTP API frameworks toocapture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="57b85-115">Hola inconveniente toothis consiste Hola HTTP middleware necesita toobe integrado en hello back-end de API y debe coincidir con la plataforma de Hola de hello API.</span><span class="sxs-lookup"><span data-stu-id="57b85-115">hello downside toothis approach is hello HTTP middleware needs toobe integrated into hello backend API and must match hello platform of hello API.</span></span> <span data-ttu-id="57b85-116">Si hay varias API, a continuación, cada uno de ellos debe implementar middleware de Hola.</span><span class="sxs-lookup"><span data-stu-id="57b85-116">If there are multiple APIs then each one must deploy hello middleware.</span></span> <span data-ttu-id="57b85-117">A menudo existen motivos por los que no se pueden actualizar las API de back-end.</span><span class="sxs-lookup"><span data-stu-id="57b85-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="57b85-118">Usar toointegrate de servicio de administración de API de Azure de hello con infraestructura de registro proporciona una solución centralizada e independiente de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="57b85-118">Using hello Azure API Management service toointegrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="57b85-119">También es escalable, en parte debido toohello [georreplicación](api-management-howto-deploy-multi-region.md) capacidades de administración de API de Azure.</span><span class="sxs-lookup"><span data-stu-id="57b85-119">It is also scalable, in part due toohello [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-tooan-azure-event-hub"></a><span data-ttu-id="57b85-120">¿Por qué enviar tooan concentrador de eventos de Azure?</span><span class="sxs-lookup"><span data-stu-id="57b85-120">Why send tooan Azure Event Hub?</span></span>
<span data-ttu-id="57b85-121">Es un tooask razonable, ¿por qué crear una directiva de centros de eventos de tooAzure específico?</span><span class="sxs-lookup"><span data-stu-id="57b85-121">It is a reasonable tooask, why create a policy that is specific tooAzure Event Hubs?</span></span> <span data-ttu-id="57b85-122">Hay muchos lugares diferentes que me interesa toolog Mis solicitudes.</span><span class="sxs-lookup"><span data-stu-id="57b85-122">There are many different places where I might want toolog my requests.</span></span> <span data-ttu-id="57b85-123">¿Por qué no enviar simplemente Hola directamente solicitudes destino final toohello?</span><span class="sxs-lookup"><span data-stu-id="57b85-123">Why not just send hello requests directly toohello final destination?</span></span>  <span data-ttu-id="57b85-124">Es una opción.</span><span class="sxs-lookup"><span data-stu-id="57b85-124">That is an option.</span></span> <span data-ttu-id="57b85-125">Sin embargo, al realizar solicitudes de registro de un servicio de administración de API, es necesario tooconsider cómo los mensajes de registro afectará al rendimiento de Hola de hello API.</span><span class="sxs-lookup"><span data-stu-id="57b85-125">However, when making logging requests from an API management service, it is necessary tooconsider how logging messages will impact hello performance of hello API.</span></span> <span data-ttu-id="57b85-126">Para manejar los aumentos graduales de la carga puede aumentar las instancias disponibles de los componentes del sistema o aprovechar las ventajas de la replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="57b85-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="57b85-127">Sin embargo, short picos de tráfico pueden provocar toobe solicitudes retrasada significativamente si tooslow bajo una carga de inicio de la infraestructura de toologging de solicitudes.</span><span class="sxs-lookup"><span data-stu-id="57b85-127">However, short spikes in traffic can cause requests toobe significantly delayed if requests toologging infrastructure start tooslow under load.</span></span>

<span data-ttu-id="57b85-128">Hola centros de eventos de Azure está diseñado tooingress grandes volúmenes de datos, con capacidad para tratar con un número mucho mayor de eventos que número Hola de HTTP solicita el proceso la mayoría de las API.</span><span class="sxs-lookup"><span data-stu-id="57b85-128">hello Azure Event Hubs is designed tooingress huge volumes of data, with capacity for dealing with a far higher number of events than hello number of HTTP requests most APIs process.</span></span> <span data-ttu-id="57b85-129">Hola concentrador de eventos actúa como un tipo de búfer sofisticada entre la API hello y servicio de infraestructura de administración que almacenar y procesar mensajes de saludo.</span><span class="sxs-lookup"><span data-stu-id="57b85-129">hello Event Hub acts as a kind of sophisticated buffer between your API management service and hello infrastructure that will store and process hello messages.</span></span> <span data-ttu-id="57b85-130">Esto garantiza que no se verá afectado el rendimiento de la API debido a la infraestructura de registro de toohello.</span><span class="sxs-lookup"><span data-stu-id="57b85-130">This ensures that your API performance will not suffer due toohello logging infrastructure.</span></span>  

<span data-ttu-id="57b85-131">Una vez tooan concentrador de eventos se conserva y va a esperar tooprocess de los consumidores del centro de eventos se ha pasado datos Hola.</span><span class="sxs-lookup"><span data-stu-id="57b85-131">Once hello data has been passed tooan Event Hub it is persisted and will wait for Event Hub consumers tooprocess it.</span></span> <span data-ttu-id="57b85-132">Hola concentrador de eventos no importa cómo se procesarán, simplemente se ocupa asegurarse de que se entregarán correctamente el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="57b85-132">hello Event Hub does not care how it will be processed, it just cares about making sure hello message will be successfully delivered.</span></span>     

<span data-ttu-id="57b85-133">Los concentradores de eventos tienen grupos de consumidores de hello capacidad toostream eventos toomultiple.</span><span class="sxs-lookup"><span data-stu-id="57b85-133">Event Hubs have hello ability toostream events toomultiple consumer groups.</span></span> <span data-ttu-id="57b85-134">Esto permite toobe de eventos procesado por sistemas completamente diferentes.</span><span class="sxs-lookup"><span data-stu-id="57b85-134">This allows events toobe processed by completely different systems.</span></span> <span data-ttu-id="57b85-135">Esto permite admitir muchos escenarios de integración sin contar con retrasos de adición en hello del proceso de solicitud de API de hello en servicio de administración de API de Hola como un solo evento necesita toobe generado.</span><span class="sxs-lookup"><span data-stu-id="57b85-135">This enables supporting many integration scenarios without putting addition delays on hello processing of hello API request within hello API Management service as only one event needs toobe generated.</span></span>

## <a name="a-policy-toosend-applicationhttp-messages"></a><span data-ttu-id="57b85-136">Una directiva toosend aplicación/http los mensajes</span><span class="sxs-lookup"><span data-stu-id="57b85-136">A policy toosend application/http messages</span></span>
<span data-ttu-id="57b85-137">Un Centro de eventos acepta datos de eventos como una cadena simple.</span><span class="sxs-lookup"><span data-stu-id="57b85-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="57b85-138">contenido de Hola de dicha cadena completamente está funcionando tooyou.</span><span class="sxs-lookup"><span data-stu-id="57b85-138">hello contents of that string are completely up tooyou.</span></span> <span data-ttu-id="57b85-139">toobe puede toopackage una copia de seguridad una solicitud HTTP y envíelo tooEvent concentradores necesitamos cadena de hello tooformat con la información de solicitud o respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="57b85-139">toobe able toopackage up an HTTP request and send it off tooEvent Hubs we need tooformat hello string with hello request or response information.</span></span> <span data-ttu-id="57b85-140">En situaciones como esta, si hay un formato existente que se puede volver a utilizar, a continuación, podemos no tenemos toowrite nuestro propio análisis de código.</span><span class="sxs-lookup"><span data-stu-id="57b85-140">In situations like this, if there is an existing format we can reuse, then we may not have toowrite our own parsing code.</span></span> <span data-ttu-id="57b85-141">Inicialmente considera utilizando hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) para el envío de solicitudes y respuestas HTTP.</span><span class="sxs-lookup"><span data-stu-id="57b85-141">Initially I considered using hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="57b85-142">Sin embargo, este formato está optimizado para almacenar una secuencia de solicitudes de HTTP en un formato basado en JSON.</span><span class="sxs-lookup"><span data-stu-id="57b85-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="57b85-143">Contenía un número de elementos obligatorios que agrega una complejidad innecesaria de escenario de Hola de pasar mensajes de bienvenida HTTP a través de la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="57b85-143">It contained a number of mandatory elements that added unnecessary complexity for hello scenario of passing hello HTTP message over hello wire.</span></span>  

<span data-ttu-id="57b85-144">Una opción alternativa era hello toouse `application/http` tipo de medio como se describe en la especificación de hello HTTP [7230 RFC](http://tools.ietf.org/html/rfc7230).</span><span class="sxs-lookup"><span data-stu-id="57b85-144">An alternative option was toouse hello `application/http` media type as described in hello HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="57b85-145">Este tipo de medio usa Hola exactamente el mismo formato que es usado tooactually enviar mensajes de HTTP a través de la conexión de hello, pero se pueden colocar mensajes de bienvenida del todo en cuerpo Hola de otra solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="57b85-145">This media type uses hello exact same format that is used tooactually send HTTP messages over hello wire, but hello entire message can be put in hello body of another HTTP request.</span></span> <span data-ttu-id="57b85-146">En nuestro caso vamos solo cuerpo de hello toouse como nuestro tooEvent de toosend mensaje concentradores.</span><span class="sxs-lookup"><span data-stu-id="57b85-146">In our case we are just going toouse hello body as our message toosend tooEvent Hubs.</span></span> <span data-ttu-id="57b85-147">Afortunadamente, hay un analizador que existe en [cliente 2.2 de Microsoft ASP.NET Web API](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) bibliotecas que pueden analizar este formato y convertirlos a nativo hello `HttpRequestMessage` y `HttpResponseMessage` objetos.</span><span class="sxs-lookup"><span data-stu-id="57b85-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into hello native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="57b85-148">toobe puede toocreate este mensaje necesitamos tootake aprovechar en función de C# [expresiones de directiva](https://msdn.microsoft.com/library/azure/dn910913.aspx) en administración de API de Azure.</span><span class="sxs-lookup"><span data-stu-id="57b85-148">toobe able toocreate this message we need tootake advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="57b85-149">Aquí es la directiva Hola que envía un mensaje de solicitud HTTP tooAzure centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="57b85-149">Here is hello policy which sends a HTTP request message tooAzure Event Hubs.</span></span>

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

### <a name="policy-declaration"></a><span data-ttu-id="57b85-150">Declaración de directiva</span><span class="sxs-lookup"><span data-stu-id="57b85-150">Policy declaration</span></span>
<span data-ttu-id="57b85-151">Hay algunas cosas específicas que merece la pena mencionar acerca de esta expresión de directiva.</span><span class="sxs-lookup"><span data-stu-id="57b85-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="57b85-152">Directiva de registro a eventhub de Hello tiene un atributo denominado identificador de registrador que hace referencia el nombre de toohello de registrador que se ha creado en el servicio de administración de API de Hola.</span><span class="sxs-lookup"><span data-stu-id="57b85-152">hello log-to-eventhub policy has an attribute called logger-id which refers toohello name of logger that has been created within hello API Management service.</span></span> <span data-ttu-id="57b85-153">Hola detalles de cómo toosetup un registrador de concentrador de eventos en el servicio de administración de API de hello puede encontrarse en el documento de hello [cómo toolog eventos tooAzure concentradores de eventos de administración de API de Azure](api-management-howto-log-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="57b85-153">hello details of how toosetup an Event Hub logger in hello API Management service can be found in hello document [How toolog events tooAzure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="57b85-154">segundo atributo de Hello es un parámetro opcional que indica qué mensaje de saludo de toostore de partición de a centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="57b85-154">hello second attribute is an optional parameter that instructs Event Hubs which partition toostore hello message in.</span></span> <span data-ttu-id="57b85-155">Utilice particiones tooenable escalabilidad y requieren un mínimo de dos centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="57b85-155">Event Hubs use partitions tooenable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="57b85-156">sólo se garantiza la entrega ordenada de mensajes de Hola dentro de una partición.</span><span class="sxs-lookup"><span data-stu-id="57b85-156">hello ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="57b85-157">Si no se indica a centro de eventos en los mensajes de bienvenida de partición tooplace, usará un algoritmo round-robin toodistribute Hola de carga.</span><span class="sxs-lookup"><span data-stu-id="57b85-157">If we do not instruct Event Hub in which partition tooplace hello message, it will use a round-robin algorithm toodistribute hello load.</span></span> <span data-ttu-id="57b85-158">Sin embargo, pueden producirse algunos de nuestro toobe de mensajes procesado desordenados.</span><span class="sxs-lookup"><span data-stu-id="57b85-158">However, that may cause some of our messages toobe processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="57b85-159">Particiones</span><span class="sxs-lookup"><span data-stu-id="57b85-159">Partitions</span></span>
<span data-ttu-id="57b85-160">tooensure nuestros mensajes se entregan tooconsumers en orden y aprovechar las ventajas de la capacidad de distribución de carga de Hola de particiones, que deseaba toosend HTTP solicitud mensajes tooone HTTP respuesta mensajes tooa partición y otra.</span><span class="sxs-lookup"><span data-stu-id="57b85-160">tooensure our messages are delivered tooconsumers in order and take advantage of hello load distribution capability of partitions, I chose toosend HTTP request messages tooone partition and HTTP response messages tooa second partition.</span></span> <span data-ttu-id="57b85-161">Esto garantiza una distribución equilibrada de la carga y podemos garantizar que se consumirán todas las solicitudes en orden y todas las respuestas se consumirán en orden.</span><span class="sxs-lookup"><span data-stu-id="57b85-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="57b85-162">Es posible que un toobe de respuesta que se utilicen antes de solicitud correspondiente hello, pero ya que no es un problema que tenemos un mecanismo diferente para poner en correlación las solicitudes tooresponses y sabemos que las solicitudes procedan siempre antes de las respuestas.</span><span class="sxs-lookup"><span data-stu-id="57b85-162">It is possible for a response toobe consumed before hello corresponding request, but as that is not a problem as we have a different mechanism for correlating requests tooresponses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="57b85-163">Cargas de HTTP</span><span class="sxs-lookup"><span data-stu-id="57b85-163">HTTP payloads</span></span>
<span data-ttu-id="57b85-164">Después de compilar hello `requestLine` comprobamos toosee si se debe truncar el cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="57b85-164">After building hello `requestLine` we check toosee if hello request body should be truncated.</span></span> <span data-ttu-id="57b85-165">cuerpo de la solicitud de Hello es tooonly truncado 1024.</span><span class="sxs-lookup"><span data-stu-id="57b85-165">hello request body is truncated tooonly 1024.</span></span> <span data-ttu-id="57b85-166">Esto podría aumentar, sin embargo los mensajes individuales de concentrador de eventos son too256KB limitado, por lo que es probable que algunas HTTP cuerpos will no caben en un único mensaje.</span><span class="sxs-lookup"><span data-stu-id="57b85-166">This could be increased, however individual Event Hub messages are limited too256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="57b85-167">Al realizar el registro y análisis de una cantidad significativa de información puede derivarse de simplemente línea de solicitud HTTP de Hola y encabezados.</span><span class="sxs-lookup"><span data-stu-id="57b85-167">When doing logging and analytics a significant amount of information can be derived from just hello HTTP request line and headers.</span></span> <span data-ttu-id="57b85-168">Además, muchas solicitudes de API solo devuelven cuerpos pequeños y por lo que es bastante mínima reducción de toohello de comparación de transferencia de la pérdida de Hola de valor de la información mediante el truncamiento de cuerpos de gran tamaño, el procesamiento y el almacenamiento de costos tookeep todo el contenido de cuerpo.</span><span class="sxs-lookup"><span data-stu-id="57b85-168">Also, many API requests only return small bodies and so hello loss of information value by truncating large bodies is fairly minimal in comparison toohello reduction in transfer, processing and storage costs tookeep all body contents.</span></span> <span data-ttu-id="57b85-169">Una nota final acerca del procesamiento de cuerpo de hello es que necesitamos toopass `true` toohello como<string>método () porque estamos leyendo contenido del cuerpo de hello, pero era también desee Hola back-end API toobe tooread capaz de hello cuerpo.</span><span class="sxs-lookup"><span data-stu-id="57b85-169">One final note about processing hello body is that we need toopass `true` toohello As<string>() method because we are reading hello body contents, but was also want hello backend API toobe able tooread hello body.</span></span> <span data-ttu-id="57b85-170">De forma pasar true toothis método se producen Hola cuerpo toobe almacenado en búfer para que sólo pueda leerlo la segunda vez.</span><span class="sxs-lookup"><span data-stu-id="57b85-170">By passing true toothis method we cause hello body toobe buffered so that it can be read a second time.</span></span> <span data-ttu-id="57b85-171">Esto es importante toobe tenga en cuenta si tiene una API que no la carga de archivos muy grandes o usa sondeo prolongado.</span><span class="sxs-lookup"><span data-stu-id="57b85-171">This is important toobe aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="57b85-172">En estos casos sería mejor tooavoid leer el cuerpo de hello en absoluto.</span><span class="sxs-lookup"><span data-stu-id="57b85-172">In these cases it would be best tooavoid reading hello body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="57b85-173">Encabezados HTTP</span><span class="sxs-lookup"><span data-stu-id="57b85-173">HTTP headers</span></span>
<span data-ttu-id="57b85-174">Encabezados HTTP se pueden transferir simplemente en formato de mensaje de Hola en un formato de par clave/valor simple.</span><span class="sxs-lookup"><span data-stu-id="57b85-174">HTTP Headers can be simply transferred over into hello message format in a simple key/value pair format.</span></span> <span data-ttu-id="57b85-175">Que hemos elegido toostrip ciertos seguridad campos confidenciales, tooavoid innecesariamente pierde la información de credenciales.</span><span class="sxs-lookup"><span data-stu-id="57b85-175">We have chosen toostrip out certain security sensitive fields, tooavoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="57b85-176">No es probable que se usen claves de API y otras credenciales para los análisis.</span><span class="sxs-lookup"><span data-stu-id="57b85-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="57b85-177">Si se desea toodo análisis en el usuario de Hola y producto en particular Hola usaran, a continuación, se pudo obtener de hello `context` objeto y agregar ese mensaje toohello.</span><span class="sxs-lookup"><span data-stu-id="57b85-177">If we wish toodo analysis on hello user and hello particular product they are using then we could get that from hello `context` object and add that toohello message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="57b85-178">Metadatos del mensaje</span><span class="sxs-lookup"><span data-stu-id="57b85-178">Message Metadata</span></span>
<span data-ttu-id="57b85-179">Al compilar el concentrador de eventos de hello mensaje completo toosend toohello, Hola primera línea no es realmente parte de hello `application/http` mensaje.</span><span class="sxs-lookup"><span data-stu-id="57b85-179">When building hello complete message toosend toohello event hub, hello first line is not actually part of hello `application/http` message.</span></span> <span data-ttu-id="57b85-180">primera línea de Hello es metadatos adicionales que se compone de si el mensaje de bienvenida es un mensaje de solicitud o respuesta y un identificador de mensaje que es usado toocorrelate solicita tooresponses.</span><span class="sxs-lookup"><span data-stu-id="57b85-180">hello first line is additional metadata consisting of whether hello message is a request or response message and a message id which is used toocorrelate requests tooresponses.</span></span> <span data-ttu-id="57b85-181">Id. de mensaje Hola se crea mediante el uso de otra directiva este aspecto:</span><span class="sxs-lookup"><span data-stu-id="57b85-181">hello message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="57b85-182">Podríamos haber creado el mensaje de solicitud de hello, almacenado que, en una variable hasta Hola respuesta se devuelve y enviar, a continuación, simplemente Hola solicitud y respuesta como un solo mensaje.</span><span class="sxs-lookup"><span data-stu-id="57b85-182">We could have created hello request message, stored that in a variable until hello response was returned and then simply sent hello request and response as a single message.</span></span> <span data-ttu-id="57b85-183">Sin embargo, enviar Hola solicitud y respuesta de forma independiente y usando un toocorrelate de Id. de mensaje Hola dos, obtenemos un poco más flexibilidad en el tamaño del mensaje Hola, Hola capacidad tootake aprovechar varias particiones, aunque manteniendo hello y orden de los mensajes solicitud aparecerá en el panel de registro antes.</span><span class="sxs-lookup"><span data-stu-id="57b85-183">However, by sending hello request and response independently and using a message id toocorrelate hello two, we get a bit more flexibility in hello message size, hello ability tootake advantage of multiple partitions whilst maintaining message order and hello request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="57b85-184">También puede haber algunos escenarios donde una respuesta válida nunca se envía el concentrador de eventos toohello, posiblemente debido a error de solicitud irrecuperable tooa en el servicio de administración de API de hello, pero todavía tenemos un registro de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="57b85-184">There also may be some scenarios where a valid response is never sent toohello event hub, possibly due tooa fatal request error in hello API Management service, but we still will have a record of hello request.</span></span>

<span data-ttu-id="57b85-185">mensaje de Hola directiva toosend Hola respuesta HTTP parece muy similar solicitud toohello y Hola completar la configuración de directiva se ve así:</span><span class="sxs-lookup"><span data-stu-id="57b85-185">hello policy toosend hello response HTTP message looks very similar toohello request and so hello complete policy configuration looks like this:</span></span>

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

<span data-ttu-id="57b85-186">Hola `set-variable` directiva crea un valor que sea accesible para ambos hello `log-to-eventhub` directiva Hola `<inbound>` hello y sección `<outbound>` sección.</span><span class="sxs-lookup"><span data-stu-id="57b85-186">hello `set-variable` policy creates a value that is accessible by both hello `log-to-eventhub` policy in hello `<inbound>` section and hello `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="57b85-187">Recepción de eventos de Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="57b85-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="57b85-188">Se reciben eventos de concentrador de eventos de Azure con hello [protocolo AMQP](http://www.amqp.org/).</span><span class="sxs-lookup"><span data-stu-id="57b85-188">Events from Azure Event Hub are received using hello [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="57b85-189">equipo de Bus de servicio de Microsoft de Hello realizaron cliente hello toomake disponibles de bibliotecas cómo consumir eventos más fáciles.</span><span class="sxs-lookup"><span data-stu-id="57b85-189">hello Microsoft Service Bus team have made client libraries available toomake hello consuming events easier.</span></span> <span data-ttu-id="57b85-190">Existen dos enfoques diferentes admitidos, uno se está un *consumidor directo* y Hola otro usan hello `EventProcessorHost` clase.</span><span class="sxs-lookup"><span data-stu-id="57b85-190">There are two different approaches supported, one is being a *Direct Consumer* and hello other is using hello `EventProcessorHost` class.</span></span> <span data-ttu-id="57b85-191">Pueden encontrar ejemplos de estos dos enfoques en hello [Guía de programación de los centros de eventos](../event-hubs/event-hubs-programming-guide.md).</span><span class="sxs-lookup"><span data-stu-id="57b85-191">Examples of these two approaches can be found in hello [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="57b85-192">es la versión abreviada de Hola de diferencias de hello, `Direct Consumer` le ofrece un control total y hello `EventProcessorHost` no parte del trabajo de establecimiento de hello pero realiza determinadas suposiciones sobre la forma de procesar los eventos.</span><span class="sxs-lookup"><span data-stu-id="57b85-192">hello short version of hello differences is, `Direct Consumer` gives you complete control and hello `EventProcessorHost` does some of hello plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="57b85-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="57b85-193">EventProcessorHost</span></span>
<span data-ttu-id="57b85-194">En este ejemplo, usaremos hello `EventProcessorHost` para simplificar, sin embargo puede no Hola mejor opción para este escenario en particular.</span><span class="sxs-lookup"><span data-stu-id="57b85-194">In this sample, we will use hello `EventProcessorHost` for simplicity, however it may not hello best choice for this particular scenario.</span></span> <span data-ttu-id="57b85-195">`EventProcessorHost`Hola duro trabajo de asegurándose de que no tiene tooworry acerca del subprocesamiento problemas dentro de una clase de procesador de evento determinado.</span><span class="sxs-lookup"><span data-stu-id="57b85-195">`EventProcessorHost` does hello hard work of making sure you don't have tooworry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="57b85-196">Sin embargo, en nuestro escenario, estamos basta con convertir el formato de tooanother del mensaje de Hola y pasarlo a lo largo de servicio de tooanother mediante un método asincrónico.</span><span class="sxs-lookup"><span data-stu-id="57b85-196">However, in our scenario, we are simply converting hello message tooanother format and passing it along tooanother service using an async method.</span></span> <span data-ttu-id="57b85-197">No es necesario actualizar el estado compartido y, por tanto, no hay riesgo de problemas de subprocesamiento.</span><span class="sxs-lookup"><span data-stu-id="57b85-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="57b85-198">Para la mayoría de los escenarios, `EventProcessorHost` es probablemente la mejor opción de Hola y es seguro opción más fácil de Hola.</span><span class="sxs-lookup"><span data-stu-id="57b85-198">For most scenarios, `EventProcessorHost` is probably hello best choice and it is certainly hello easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="57b85-199">IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="57b85-199">IEventProcessor</span></span>
<span data-ttu-id="57b85-200">concepto de Hello central cuando se usa `EventProcessorHost` es toocreate un una implementación de hello `IEventProcessor` interfaz que contiene el método hello `ProcessEventAsync`.</span><span class="sxs-lookup"><span data-stu-id="57b85-200">hello central concept when using `EventProcessorHost` is toocreate a an implementation of hello `IEventProcessor` interface which contains hello method `ProcessEventAsync`.</span></span> <span data-ttu-id="57b85-201">aquí se muestra la esencia de Hola de ese método:</span><span class="sxs-lookup"><span data-stu-id="57b85-201">hello essence of that method is shown here:</span></span>

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

<span data-ttu-id="57b85-202">Una lista de objetos EventData se pasan al método hello y procesamos una iteración en esa lista.</span><span class="sxs-lookup"><span data-stu-id="57b85-202">A list of EventData objects are passed into hello method and we iterate over that list.</span></span> <span data-ttu-id="57b85-203">bytes de Hola de cada método se analiza en un objeto HttpMessage y ese objeto se pasa una instancia de tooan de IHttpMessageProcessor.</span><span class="sxs-lookup"><span data-stu-id="57b85-203">hello bytes of each method are parsed into a HttpMessage object and that object is passed tooan instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="57b85-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="57b85-204">HttpMessage</span></span>
<span data-ttu-id="57b85-205">Hola `HttpMessage` instancia contiene tres elementos de datos:</span><span class="sxs-lookup"><span data-stu-id="57b85-205">hello `HttpMessage` instance contains three pieces of data:</span></span>

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

<span data-ttu-id="57b85-206">Hola `HttpMessage` instancia contiene un `MessageId` GUID que nos permite tooconnect solicitud de hello HTTP toohello correspondiente respuesta HTTP y un valor booleano de valor que identifica si el objeto de hello contiene una instancia de un HttpRequestMessage y HttpResponseMessage.</span><span class="sxs-lookup"><span data-stu-id="57b85-206">hello `HttpMessage` instance contains a `MessageId` GUID that allows us tooconnect hello HTTP request toohello corresponding HTTP response and a boolean value that identifies if hello object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="57b85-207">Mediante el uso de hello integrada en las clases HTTP de `System.Net.Http`, he logrado tootake puede aprovechar hello `application/http` analizar el código que se incluye en `System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="57b85-207">By using hello built in HTTP classes from `System.Net.Http`, I was able tootake advantage of hello `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="57b85-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="57b85-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="57b85-209">Hola `HttpMessage` instancia, a continuación, se reenvía tooimplementation de `IHttpMessageProcessor` que es una interfaz que he creado recepción de hello toodecouple e interpretación de los eventos de Hola de concentrador de eventos de Azure y Hola real de procesamiento del mismo.</span><span class="sxs-lookup"><span data-stu-id="57b85-209">hello `HttpMessage` instance is then forwarded tooimplementation of `IHttpMessageProcessor` which is an interface I created toodecouple hello receiving and interpretation of hello event from Azure Event Hub and hello actual processing of it.</span></span>

## <a name="forwarding-hello-http-message"></a><span data-ttu-id="57b85-210">Enviando el mensaje de Hola HTTP</span><span class="sxs-lookup"><span data-stu-id="57b85-210">Forwarding hello HTTP message</span></span>
<span data-ttu-id="57b85-211">En este ejemplo, se decidió sería interesante toopush Hola solicitud HTTP sobre demasiado[Runscope](http://www.runscope.com).</span><span class="sxs-lookup"><span data-stu-id="57b85-211">For this sample, I decided it would be interesting toopush hello HTTP Request over too[Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="57b85-212">Runscope es un servicio basado en la nube que se especializa en depuración, registro y supervisión de HTTP.</span><span class="sxs-lookup"><span data-stu-id="57b85-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="57b85-213">Tienen un nivel gratis, por lo que resulta fácil tootry y nos permite las solicitudes HTTP de toosee hello en tiempo real que fluyen a través de nuestro servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="57b85-213">They have a free tier, so it is easy tootry and it allows us toosee hello HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="57b85-214">Hola `IHttpMessageProcessor` implementación este aspecto:</span><span class="sxs-lookup"><span data-stu-id="57b85-214">hello `IHttpMessageProcessor` implementation looks like this,</span></span>

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
       _Logger.LogDebug("Request sent tooRunscope");
   }
}
```

<span data-ttu-id="57b85-215">He logrado tootake puede aprovechar una [biblioteca de cliente existente para Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) que resulta fácil toopush `HttpRequestMessage` y `HttpResponseMessage` instancias seguridad en su servicio.</span><span class="sxs-lookup"><span data-stu-id="57b85-215">I was able tootake advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy toopush `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="57b85-216">En orden tooaccess Hola API Runscope necesitará una cuenta y una clave de API.</span><span class="sxs-lookup"><span data-stu-id="57b85-216">In order tooaccess hello Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="57b85-217">Encontrará instrucciones para obtener una clave de API en hello [tooAccess Runscope API de creación de aplicaciones](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) presentación en pantalla.</span><span class="sxs-lookup"><span data-stu-id="57b85-217">Instructions for getting an API key can be found in hello [Creating Applications tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="57b85-218">Ejemplo completo</span><span class="sxs-lookup"><span data-stu-id="57b85-218">Complete sample</span></span>
<span data-ttu-id="57b85-219">Hola [código fuente](https://github.com/darrelmiller/ApimEventProcessor) a pruebas de ejemplo de Hola en GitHub.</span><span class="sxs-lookup"><span data-stu-id="57b85-219">hello [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for hello sample are on GitHub.</span></span> <span data-ttu-id="57b85-220">Necesitará un [servicio de administración de API](api-management-get-started.md), [un centro de eventos conectado](api-management-howto-log-event-hubs.md)y un [cuenta de almacenamiento](../storage/common/storage-create-storage-account.md) ejemplo de Hola a toorun por sí mismo.</span><span class="sxs-lookup"><span data-stu-id="57b85-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) toorun hello sample for yourself.</span></span>   

<span data-ttu-id="57b85-221">ejemplo Hello es simplemente una aplicación de consola simple que realiza escuchas de eventos procedentes de concentrador de eventos, se convierte en una `HttpRequestMessage` y `HttpResponseMessage` objetos y, a continuación, reenvía en toohello Runscope API.</span><span class="sxs-lookup"><span data-stu-id="57b85-221">hello sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on toohello Runscope API.</span></span>

<span data-ttu-id="57b85-222">Hola después imagen animada, puede ver una solicitud realizada tooan API Hola Portal para desarrolladores, mensaje Hola consola aplicación mostrando Hola recibe, procesa y reenvía y Hola, a continuación, la solicitud y respuesta aparece en hello Runscope tráfico inspector.</span><span class="sxs-lookup"><span data-stu-id="57b85-222">In hello following animated image, you can see a request being made tooan API in hello Developer Portal, hello Console application showing hello message being received, processed and forwarded and then hello request and response showing up in hello Runscope Traffic inspector.</span></span>

![Demostración de la solicitud que se reenvían tooRunscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="57b85-224">Resumen</span><span class="sxs-lookup"><span data-stu-id="57b85-224">Summary</span></span>
<span data-ttu-id="57b85-225">Servicio de administración de API de Azure proporciona un lugar ideal toocapture Hola HTTP del tráfico a versiones anteriores tooand de las API.</span><span class="sxs-lookup"><span data-stu-id="57b85-225">Azure API Management service provides an ideal place toocapture hello HTTP traffic travelling tooand from your APIs.</span></span> <span data-ttu-id="57b85-226">Centros de eventos de Azure es una solución altamente escalable y de bajo costo para capturar ese tráfico y colocarlo en sistemas de procesamiento secundario para el registro, supervisión y otros análisis sofisticados.</span><span class="sxs-lookup"><span data-stu-id="57b85-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="57b85-227">Tráfico de entidad too3rd supervisar sistemas como Runscope es tan simple como unas cuantas docenas líneas de código de la conexión.</span><span class="sxs-lookup"><span data-stu-id="57b85-227">Connecting too3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57b85-228">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="57b85-228">Next steps</span></span>
* <span data-ttu-id="57b85-229">Obtenga más información acerca de los centros de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="57b85-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="57b85-230">Introducción a los centros de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="57b85-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="57b85-231">Recepción de mensajes con EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="57b85-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="57b85-232">Guía de programación de Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="57b85-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="57b85-233">Obtener más información acerca de la integración de Administración de API y centros de eventos</span><span class="sxs-lookup"><span data-stu-id="57b85-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="57b85-234">¿Cómo toolog eventos tooAzure concentradores de eventos de administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="57b85-234">How toolog events tooAzure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="57b85-235">Referencia de entidad del registrador</span><span class="sxs-lookup"><span data-stu-id="57b85-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="57b85-236">referencia de la directiva log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="57b85-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
