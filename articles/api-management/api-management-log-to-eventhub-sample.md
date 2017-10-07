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
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a>Supervisión de API con Administración de API de Azure, Centros de eventos y Runscope
Hola [servicio de administración de API](api-management-key-concepts.md) proporciona muchas capacidades tooenhance Hola procesamiento de las solicitudes enviadas de HTTP tooyour API HTTP. Sin embargo, Hola existencia de hello solicitudes y respuestas son transitorias. se realiza la solicitud de Hola y que fluye a través de backend de tooyour de servicio de administración de API de hello API. La API procesa la solicitud de hello y una respuesta fluye a través de consumidor toohello API. Hola servicio de administración de API mantiene algunas estadísticas importantes sobre hello las API para su presentación en el panel del portal Hola publicador pero, aparte de eso, detalles Hola han desaparecido.

Mediante el uso de hello [registro a eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [directiva](api-management-howto-policies.md) Hola servicio de administración de API puede enviar los detalles de tooan de solicitud y respuesta de hello [concentrador de eventos de Azure](../event-hubs/event-hubs-what-is-event-hubs.md). Hay una variedad de razones por las que puede toogenerate eventos de mensajes HTTP que se envían tooyour API. Algunos ejemplos incluyen la traza de auditoría de las actualizaciones, análisis de uso, las alertas de excepción e integraciones de terceros.   

Este artículo demuestra cómo toocapture Hola toda solicitud y respuesta de mensaje HTTP, enviar tooan concentrador de eventos y, a continuación, ese servicio de terceros de tooa de mensaje que proporciona servicios de supervisión y registro de HTTP de retransmisión.

## <a name="why-send-from-api-management-service"></a>¿Por qué se envían desde el servicio Administración de API?
Es posible toowrite middleware HTTP que se conecte a la API HTTP marcos toocapture solicitudes y respuestas HTTP e introducirlos en sistemas de supervisión y registro. Hola inconveniente toothis consiste Hola HTTP middleware necesita toobe integrado en hello back-end de API y debe coincidir con la plataforma de Hola de hello API. Si hay varias API, a continuación, cada uno de ellos debe implementar middleware de Hola. A menudo existen motivos por los que no se pueden actualizar las API de back-end.

Usar toointegrate de servicio de administración de API de Azure de hello con infraestructura de registro proporciona una solución centralizada e independiente de la plataforma. También es escalable, en parte debido toohello [georreplicación](api-management-howto-deploy-multi-region.md) capacidades de administración de API de Azure.

## <a name="why-send-tooan-azure-event-hub"></a>¿Por qué enviar tooan concentrador de eventos de Azure?
Es un tooask razonable, ¿por qué crear una directiva de centros de eventos de tooAzure específico? Hay muchos lugares diferentes que me interesa toolog Mis solicitudes. ¿Por qué no enviar simplemente Hola directamente solicitudes destino final toohello?  Es una opción. Sin embargo, al realizar solicitudes de registro de un servicio de administración de API, es necesario tooconsider cómo los mensajes de registro afectará al rendimiento de Hola de hello API. Para manejar los aumentos graduales de la carga puede aumentar las instancias disponibles de los componentes del sistema o aprovechar las ventajas de la replicación geográfica. Sin embargo, short picos de tráfico pueden provocar toobe solicitudes retrasada significativamente si tooslow bajo una carga de inicio de la infraestructura de toologging de solicitudes.

Hola centros de eventos de Azure está diseñado tooingress grandes volúmenes de datos, con capacidad para tratar con un número mucho mayor de eventos que número Hola de HTTP solicita el proceso la mayoría de las API. Hola concentrador de eventos actúa como un tipo de búfer sofisticada entre la API hello y servicio de infraestructura de administración que almacenar y procesar mensajes de saludo. Esto garantiza que no se verá afectado el rendimiento de la API debido a la infraestructura de registro de toohello.  

Una vez tooan concentrador de eventos se conserva y va a esperar tooprocess de los consumidores del centro de eventos se ha pasado datos Hola. Hola concentrador de eventos no importa cómo se procesarán, simplemente se ocupa asegurarse de que se entregarán correctamente el mensaje de bienvenida.     

Los concentradores de eventos tienen grupos de consumidores de hello capacidad toostream eventos toomultiple. Esto permite toobe de eventos procesado por sistemas completamente diferentes. Esto permite admitir muchos escenarios de integración sin contar con retrasos de adición en hello del proceso de solicitud de API de hello en servicio de administración de API de Hola como un solo evento necesita toobe generado.

## <a name="a-policy-toosend-applicationhttp-messages"></a>Una directiva toosend aplicación/http los mensajes
Un Centro de eventos acepta datos de eventos como una cadena simple. contenido de Hola de dicha cadena completamente está funcionando tooyou. toobe puede toopackage una copia de seguridad una solicitud HTTP y envíelo tooEvent concentradores necesitamos cadena de hello tooformat con la información de solicitud o respuesta de Hola. En situaciones como esta, si hay un formato existente que se puede volver a utilizar, a continuación, podemos no tenemos toowrite nuestro propio análisis de código. Inicialmente considera utilizando hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) para el envío de solicitudes y respuestas HTTP. Sin embargo, este formato está optimizado para almacenar una secuencia de solicitudes de HTTP en un formato basado en JSON. Contenía un número de elementos obligatorios que agrega una complejidad innecesaria de escenario de Hola de pasar mensajes de bienvenida HTTP a través de la conexión de Hola.  

Una opción alternativa era hello toouse `application/http` tipo de medio como se describe en la especificación de hello HTTP [7230 RFC](http://tools.ietf.org/html/rfc7230). Este tipo de medio usa Hola exactamente el mismo formato que es usado tooactually enviar mensajes de HTTP a través de la conexión de hello, pero se pueden colocar mensajes de bienvenida del todo en cuerpo Hola de otra solicitud HTTP. En nuestro caso vamos solo cuerpo de hello toouse como nuestro tooEvent de toosend mensaje concentradores. Afortunadamente, hay un analizador que existe en [cliente 2.2 de Microsoft ASP.NET Web API](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) bibliotecas que pueden analizar este formato y convertirlos a nativo hello `HttpRequestMessage` y `HttpResponseMessage` objetos.

toobe puede toocreate este mensaje necesitamos tootake aprovechar en función de C# [expresiones de directiva](https://msdn.microsoft.com/library/azure/dn910913.aspx) en administración de API de Azure. Aquí es la directiva Hola que envía un mensaje de solicitud HTTP tooAzure centros de eventos.

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

### <a name="policy-declaration"></a>Declaración de directiva
Hay algunas cosas específicas que merece la pena mencionar acerca de esta expresión de directiva. Directiva de registro a eventhub de Hello tiene un atributo denominado identificador de registrador que hace referencia el nombre de toohello de registrador que se ha creado en el servicio de administración de API de Hola. Hola detalles de cómo toosetup un registrador de concentrador de eventos en el servicio de administración de API de hello puede encontrarse en el documento de hello [cómo toolog eventos tooAzure concentradores de eventos de administración de API de Azure](api-management-howto-log-event-hubs.md). segundo atributo de Hello es un parámetro opcional que indica qué mensaje de saludo de toostore de partición de a centros de eventos. Utilice particiones tooenable escalabilidad y requieren un mínimo de dos centros de eventos. sólo se garantiza la entrega ordenada de mensajes de Hola dentro de una partición. Si no se indica a centro de eventos en los mensajes de bienvenida de partición tooplace, usará un algoritmo round-robin toodistribute Hola de carga. Sin embargo, pueden producirse algunos de nuestro toobe de mensajes procesado desordenados.  

### <a name="partitions"></a>Particiones
tooensure nuestros mensajes se entregan tooconsumers en orden y aprovechar las ventajas de la capacidad de distribución de carga de Hola de particiones, que deseaba toosend HTTP solicitud mensajes tooone HTTP respuesta mensajes tooa partición y otra. Esto garantiza una distribución equilibrada de la carga y podemos garantizar que se consumirán todas las solicitudes en orden y todas las respuestas se consumirán en orden. Es posible que un toobe de respuesta que se utilicen antes de solicitud correspondiente hello, pero ya que no es un problema que tenemos un mecanismo diferente para poner en correlación las solicitudes tooresponses y sabemos que las solicitudes procedan siempre antes de las respuestas.

### <a name="http-payloads"></a>Cargas de HTTP
Después de compilar hello `requestLine` comprobamos toosee si se debe truncar el cuerpo de la solicitud de saludo. cuerpo de la solicitud de Hello es tooonly truncado 1024. Esto podría aumentar, sin embargo los mensajes individuales de concentrador de eventos son too256KB limitado, por lo que es probable que algunas HTTP cuerpos will no caben en un único mensaje. Al realizar el registro y análisis de una cantidad significativa de información puede derivarse de simplemente línea de solicitud HTTP de Hola y encabezados. Además, muchas solicitudes de API solo devuelven cuerpos pequeños y por lo que es bastante mínima reducción de toohello de comparación de transferencia de la pérdida de Hola de valor de la información mediante el truncamiento de cuerpos de gran tamaño, el procesamiento y el almacenamiento de costos tookeep todo el contenido de cuerpo. Una nota final acerca del procesamiento de cuerpo de hello es que necesitamos toopass `true` toohello como<string>método () porque estamos leyendo contenido del cuerpo de hello, pero era también desee Hola back-end API toobe tooread capaz de hello cuerpo. De forma pasar true toothis método se producen Hola cuerpo toobe almacenado en búfer para que sólo pueda leerlo la segunda vez. Esto es importante toobe tenga en cuenta si tiene una API que no la carga de archivos muy grandes o usa sondeo prolongado. En estos casos sería mejor tooavoid leer el cuerpo de hello en absoluto.   

### <a name="http-headers"></a>Encabezados HTTP
Encabezados HTTP se pueden transferir simplemente en formato de mensaje de Hola en un formato de par clave/valor simple. Que hemos elegido toostrip ciertos seguridad campos confidenciales, tooavoid innecesariamente pierde la información de credenciales. No es probable que se usen claves de API y otras credenciales para los análisis. Si se desea toodo análisis en el usuario de Hola y producto en particular Hola usaran, a continuación, se pudo obtener de hello `context` objeto y agregar ese mensaje toohello.     

### <a name="message-metadata"></a>Metadatos del mensaje
Al compilar el concentrador de eventos de hello mensaje completo toosend toohello, Hola primera línea no es realmente parte de hello `application/http` mensaje. primera línea de Hello es metadatos adicionales que se compone de si el mensaje de bienvenida es un mensaje de solicitud o respuesta y un identificador de mensaje que es usado toocorrelate solicita tooresponses. Id. de mensaje Hola se crea mediante el uso de otra directiva este aspecto:

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

Podríamos haber creado el mensaje de solicitud de hello, almacenado que, en una variable hasta Hola respuesta se devuelve y enviar, a continuación, simplemente Hola solicitud y respuesta como un solo mensaje. Sin embargo, enviar Hola solicitud y respuesta de forma independiente y usando un toocorrelate de Id. de mensaje Hola dos, obtenemos un poco más flexibilidad en el tamaño del mensaje Hola, Hola capacidad tootake aprovechar varias particiones, aunque manteniendo hello y orden de los mensajes solicitud aparecerá en el panel de registro antes. También puede haber algunos escenarios donde una respuesta válida nunca se envía el concentrador de eventos toohello, posiblemente debido a error de solicitud irrecuperable tooa en el servicio de administración de API de hello, pero todavía tenemos un registro de solicitud de saludo.

mensaje de Hola directiva toosend Hola respuesta HTTP parece muy similar solicitud toohello y Hola completar la configuración de directiva se ve así:

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

Hola `set-variable` directiva crea un valor que sea accesible para ambos hello `log-to-eventhub` directiva Hola `<inbound>` hello y sección `<outbound>` sección.  

## <a name="receiving-events-from-event-hubs"></a>Recepción de eventos de Centros de eventos
Se reciben eventos de concentrador de eventos de Azure con hello [protocolo AMQP](http://www.amqp.org/). equipo de Bus de servicio de Microsoft de Hello realizaron cliente hello toomake disponibles de bibliotecas cómo consumir eventos más fáciles. Existen dos enfoques diferentes admitidos, uno se está un *consumidor directo* y Hola otro usan hello `EventProcessorHost` clase. Pueden encontrar ejemplos de estos dos enfoques en hello [Guía de programación de los centros de eventos](../event-hubs/event-hubs-programming-guide.md). es la versión abreviada de Hola de diferencias de hello, `Direct Consumer` le ofrece un control total y hello `EventProcessorHost` no parte del trabajo de establecimiento de hello pero realiza determinadas suposiciones sobre la forma de procesar los eventos.  

### <a name="eventprocessorhost"></a>EventProcessorHost
En este ejemplo, usaremos hello `EventProcessorHost` para simplificar, sin embargo puede no Hola mejor opción para este escenario en particular. `EventProcessorHost`Hola duro trabajo de asegurándose de que no tiene tooworry acerca del subprocesamiento problemas dentro de una clase de procesador de evento determinado. Sin embargo, en nuestro escenario, estamos basta con convertir el formato de tooanother del mensaje de Hola y pasarlo a lo largo de servicio de tooanother mediante un método asincrónico. No es necesario actualizar el estado compartido y, por tanto, no hay riesgo de problemas de subprocesamiento. Para la mayoría de los escenarios, `EventProcessorHost` es probablemente la mejor opción de Hola y es seguro opción más fácil de Hola.     

### <a name="ieventprocessor"></a>IEventProcessor
concepto de Hello central cuando se usa `EventProcessorHost` es toocreate un una implementación de hello `IEventProcessor` interfaz que contiene el método hello `ProcessEventAsync`. aquí se muestra la esencia de Hola de ese método:

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

Una lista de objetos EventData se pasan al método hello y procesamos una iteración en esa lista. bytes de Hola de cada método se analiza en un objeto HttpMessage y ese objeto se pasa una instancia de tooan de IHttpMessageProcessor.

### <a name="httpmessage"></a>HttpMessage
Hola `HttpMessage` instancia contiene tres elementos de datos:

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

Hola `HttpMessage` instancia contiene un `MessageId` GUID que nos permite tooconnect solicitud de hello HTTP toohello correspondiente respuesta HTTP y un valor booleano de valor que identifica si el objeto de hello contiene una instancia de un HttpRequestMessage y HttpResponseMessage. Mediante el uso de hello integrada en las clases HTTP de `System.Net.Http`, he logrado tootake puede aprovechar hello `application/http` analizar el código que se incluye en `System.Net.Http.Formatting`.  

### <a name="ihttpmessageprocessor"></a>IHttpMessageProcessor
Hola `HttpMessage` instancia, a continuación, se reenvía tooimplementation de `IHttpMessageProcessor` que es una interfaz que he creado recepción de hello toodecouple e interpretación de los eventos de Hola de concentrador de eventos de Azure y Hola real de procesamiento del mismo.

## <a name="forwarding-hello-http-message"></a>Enviando el mensaje de Hola HTTP
En este ejemplo, se decidió sería interesante toopush Hola solicitud HTTP sobre demasiado[Runscope](http://www.runscope.com). Runscope es un servicio basado en la nube que se especializa en depuración, registro y supervisión de HTTP. Tienen un nivel gratis, por lo que resulta fácil tootry y nos permite las solicitudes HTTP de toosee hello en tiempo real que fluyen a través de nuestro servicio de administración de API.

Hola `IHttpMessageProcessor` implementación este aspecto:

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

He logrado tootake puede aprovechar una [biblioteca de cliente existente para Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) que resulta fácil toopush `HttpRequestMessage` y `HttpResponseMessage` instancias seguridad en su servicio. En orden tooaccess Hola API Runscope necesitará una cuenta y una clave de API. Encontrará instrucciones para obtener una clave de API en hello [tooAccess Runscope API de creación de aplicaciones](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) presentación en pantalla.

## <a name="complete-sample"></a>Ejemplo completo
Hola [código fuente](https://github.com/darrelmiller/ApimEventProcessor) a pruebas de ejemplo de Hola en GitHub. Necesitará un [servicio de administración de API](api-management-get-started.md), [un centro de eventos conectado](api-management-howto-log-event-hubs.md)y un [cuenta de almacenamiento](../storage/common/storage-create-storage-account.md) ejemplo de Hola a toorun por sí mismo.   

ejemplo Hello es simplemente una aplicación de consola simple que realiza escuchas de eventos procedentes de concentrador de eventos, se convierte en una `HttpRequestMessage` y `HttpResponseMessage` objetos y, a continuación, reenvía en toohello Runscope API.

Hola después imagen animada, puede ver una solicitud realizada tooan API Hola Portal para desarrolladores, mensaje Hola consola aplicación mostrando Hola recibe, procesa y reenvía y Hola, a continuación, la solicitud y respuesta aparece en hello Runscope tráfico inspector.

![Demostración de la solicitud que se reenvían tooRunscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a>Resumen
Servicio de administración de API de Azure proporciona un lugar ideal toocapture Hola HTTP del tráfico a versiones anteriores tooand de las API. Centros de eventos de Azure es una solución altamente escalable y de bajo costo para capturar ese tráfico y colocarlo en sistemas de procesamiento secundario para el registro, supervisión y otros análisis sofisticados. Tráfico de entidad too3rd supervisar sistemas como Runscope es tan simple como unas cuantas docenas líneas de código de la conexión.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información acerca de los centros de eventos de Azure
  * [Introducción a los centros de eventos de Azure](../event-hubs/event-hubs-c-getstarted-send.md)
  * [Recepción de mensajes con EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [Guía de programación de Centros de eventos](../event-hubs/event-hubs-programming-guide.md)
* Obtener más información acerca de la integración de Administración de API y centros de eventos
  * [¿Cómo toolog eventos tooAzure concentradores de eventos de administración de API de Azure](api-management-howto-log-event-hubs.md)
  * [Referencia de entidad del registrador](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [referencia de la directiva log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
