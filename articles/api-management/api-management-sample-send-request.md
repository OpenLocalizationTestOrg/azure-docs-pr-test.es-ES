---
title: "solicitudes de toogenerate HTTP de servicio de administración de API de aaaUsing"
description: "Obtenga información acerca de las directivas de solicitud y respuesta de toouse en servicios externos de toocall de administración de API a través de la API"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 4539c0fa-21ef-4b1c-a1d4-d89a38c242fa
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 8002ee453057513340328d99f298703c3b3a9531
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-external-services-from-hello-azure-api-management-service"></a><span data-ttu-id="4c9a8-103">Uso de servicios externos de hello servicio de administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="4c9a8-103">Using external services from hello Azure API Management service</span></span>
<span data-ttu-id="4c9a8-104">las directivas de Hello disponibles en el servicio de administración de API de Azure pueden hacer una amplia gama de trabajo útil basado exclusivamente en la solicitud entrante de hello, respuesta de salida de hello y la información de configuración básica.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-104">hello policies available in Azure API Management service can do a wide range of useful work based purely on hello incoming request, hello outgoing response and basic configuration information.</span></span> <span data-ttu-id="4c9a8-105">Sin embargo, que se va a toointeract pueda con servicios externos de la API de administración de directivas abrirá muchas más posibilidades.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-105">However, being able toointeract with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="4c9a8-106">Previamente hemos visto cómo podemos interactuamos con hello [servicio del concentrador de eventos de Azure para el registro, supervisión y análisis](api-management-log-to-eventhub-sample.md).</span><span class="sxs-lookup"><span data-stu-id="4c9a8-106">We have previously seen how we can interact with hello [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="4c9a8-107">En este artículo se indicará el servicio basado en directivas que le permiten toointeract con cualquier HTTP externo.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-107">In this article we will demonstrate policies that allow you toointeract with any external HTTP based service.</span></span> <span data-ttu-id="4c9a8-108">Estas directivas pueden utilizarse para la activación de eventos remotos o para recuperar la información que será la solicitud original de uso toomanipulate Hola y de respuesta de alguna manera.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-108">These policies can be used for triggering remote events or for retrieving information that will be used toomanipulate hello original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="4c9a8-109">Send-One-Way-Request</span><span class="sxs-lookup"><span data-stu-id="4c9a8-109">Send-One-Way-Request</span></span>
<span data-ttu-id="4c9a8-110">Posiblemente hello interacción externo más sencilla es Hola enviar y olvidarse estilo de solicitud que permita un toobe de servicio externo una notificación de algún tipo de evento importante.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-110">Possibly hello simplest external interaction is hello fire-and-forget style of request that allows an external service toobe notified of some kind of important event.</span></span> <span data-ttu-id="4c9a8-111">Podemos usar la directiva de flujo de control de hello `choose` toodetect cualquier tipo de condición que está interesados y, a continuación, si hello condición se cumple, podemos hacer que una solicitud HTTP externa mediante hello [envío una manera de solicitud](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) directiva.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-111">We can use hello control flow policy `choose` toodetect any kind of condition that we are interested in and then, if hello condition is satisfied, we can make an external HTTP request using hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="4c9a8-112">Podría tratarse de un tooa solicitud mensajería sistema, como Hipchat o demora o un correo electrónico de la API como SendGrid o MailChimp, o para ver incidentes de soporte técnico crítico algo como PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-112">This could be a request tooa messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="4c9a8-113">Todos estos sistemas de mensajería tienen API HTTP sencillas que se pueden invocar fácilmente.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="4c9a8-114">Alerta con Slack</span><span class="sxs-lookup"><span data-stu-id="4c9a8-114">Alerting with Slack</span></span>
<span data-ttu-id="4c9a8-115">Hola siguiente ejemplo muestra cómo toosend una tooa mensaje salón de chat una demora si el código de estado de respuesta HTTP de hello es mayor que o igual a too500.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-115">hello following example demonstrates how toosend a message tooa Slack chat room if hello HTTP response status code is greater than or equal too500.</span></span> <span data-ttu-id="4c9a8-116">Un error de 500 rango indica un problema con la API de back-end que Hola cliente de la API no se puede resolver por sí mismos.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-116">A 500 range error indicates a problem with our backend API that hello client of our API cannot resolve themselves.</span></span> <span data-ttu-id="4c9a8-117">Normalmente requiere algún tipo de intervención por nuestra parte.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-117">It usually requires some kind of intervention on our part.</span></span>  

```xml
<choose>
    <when condition="@(context.Response.StatusCode >= 500)">
      <send-one-way-request mode="new">
        <set-url>https://hooks.slack.com/services/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</set-url>
        <set-method>POST</set-method>
        <set-body>@{
                return new JObject(
                        new JProperty("username","APIM Alert"),
                        new JProperty("icon_emoji", ":ghost:"),
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",
                                                context.Request.Method,
                                                context.Request.Url.Path + context.Request.Url.QueryString,
                                                context.Request.Url.Host,
                                                context.Response.StatusCode,
                                                context.Response.StatusReason,
                                                context.User.Email
                                                ))
                        ).ToString();
            }</set-body>
      </send-one-way-request>
    </when>
</choose>
```

<span data-ttu-id="4c9a8-118">Demora tiene noción de Hola de enlaces de web entrantes.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-118">Slack has hello notion of inbound web hooks.</span></span> <span data-ttu-id="4c9a8-119">Al configurar un enlace web entrantes, demora genera una dirección URL especial que permite toodo una solicitud POST simple y toopass un mensaje en canales de demora de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-119">When configuring an inbound web hook, Slack generates a special URL which allows you toodo a simple POST request and toopass a message into hello Slack channel.</span></span> <span data-ttu-id="4c9a8-120">Hola cuerpo JSON que creamos se basa en un formato definido por el margen de demora.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-120">hello JSON body that we create is based on a format defined by Slack.</span></span>

![Enlace web de Slack](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="4c9a8-122">¿Es fire and forget lo suficientemente bueno?</span><span class="sxs-lookup"><span data-stu-id="4c9a8-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="4c9a8-123">Existen ciertos compromisos cuando se usa un estilo de fire and forget de solicitud.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="4c9a8-124">Si por algún motivo, se produce un error en la solicitud de hello, a continuación, no se notificará el error Hola.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-124">If for some reason, hello request fails, then hello failure will not be reported.</span></span> <span data-ttu-id="4c9a8-125">En este caso concreto, no se ofrecen garantías complejidad Hola de tener un sistema de informes de error secundario y el costo de rendimiento adicionales de Hola de espera de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-125">In this particular situation, hello complexity of having a secondary failure reporting system and hello additional performance cost of waiting for hello response is not warranted.</span></span> <span data-ttu-id="4c9a8-126">Para escenarios donde resulta esencial toocheck respuesta de hello, a continuación, Hola [solicitud de envío](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) Directiva constituye una mejor opción.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-126">For scenarios where it is essential toocheck hello response, then hello [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="4c9a8-127">send-request</span><span class="sxs-lookup"><span data-stu-id="4c9a8-127">Send-Request</span></span>
<span data-ttu-id="4c9a8-128">Hola `send-request` directiva se habilita mediante un tooperform de servicio externo compleja funciones y servicio de administración de datos de retorno toohello API que se puede usar para su posterior procesamiento de directiva de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-128">hello `send-request` policy enables using an external service tooperform complex processing functions and return data toohello API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="4c9a8-129">Autorización de tokens de referencia</span><span class="sxs-lookup"><span data-stu-id="4c9a8-129">Authorizing reference tokens</span></span>
<span data-ttu-id="4c9a8-130">Una de las funciones principales de Administración de API es proteger los recursos de back-end.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="4c9a8-131">Si crea el servidor de autorización de hello utilizada por la API [tokens JWT](http://jwt.io/) como parte de su flujo de OAuth2, como [Azure Active Directory](../active-directory/active-directory-aadconnect.md) es así, puede usar hello `validate-jwt` validez de hello tooverify de directiva de token de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-131">If hello authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use hello `validate-jwt` policy tooverify hello validity of hello token.</span></span> <span data-ttu-id="4c9a8-132">Sin embargo, algunos servidores de autorización crean lo que se conoce como [hacen referencia a tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) que no se puede comprobar sin establecimiento de un servidor de autorización de llamada toohello atrás.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back toohello authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="4c9a8-133">Introspección estandarizada</span><span class="sxs-lookup"><span data-stu-id="4c9a8-133">Standardized introspection</span></span>
<span data-ttu-id="4c9a8-134">Hola pasado no ha habido ninguna manera estándar de comprobar un símbolo (token) de referencia con un servidor de autorización.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-134">In hello past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="4c9a8-135">Sin embargo estándar recientemente propuesto [7662 RFC](https://tools.ietf.org/html/rfc7662) publicó Hola IETF que define cómo un servidor de recursos puede comprobar la validez de Hola de un token.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by hello IETF that defines how a resource server can verify hello validity of a token.</span></span>

### <a name="extracting-hello-token"></a><span data-ttu-id="4c9a8-136">Extraer el token de Hola</span><span class="sxs-lookup"><span data-stu-id="4c9a8-136">Extracting hello token</span></span>
<span data-ttu-id="4c9a8-137">Hola primer paso es tooextract Hola símbolo (token) de encabezado de autorización de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-137">hello first step is tooextract hello token from hello Authorization header.</span></span> <span data-ttu-id="4c9a8-138">valor del encabezado Hola debe tener el formato con hello `Bearer` esquema de autorización, un espacio único y, a continuación, autorización de hello token según [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="4c9a8-138">hello header value should be formatted with hello `Bearer` authorization scheme, a single space and then hello authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="4c9a8-139">Desafortunadamente, hay casos donde se omite el esquema de autorización de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-139">Unfortunately there are cases where hello authorization scheme is omitted.</span></span> <span data-ttu-id="4c9a8-140">tooaccount para esto en el análisis, dividiremos el valor del encabezado de hello en un espacio y la cadena última de select Hola de hello devuelve la matriz de cadenas.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-140">tooaccount for this when parsing, we split hello header value on a space and select hello last string from hello returned array of strings.</span></span> <span data-ttu-id="4c9a8-141">Esto proporciona una solución alternativa para los encabezados de autorización con formato incorrecto.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a><span data-ttu-id="4c9a8-142">Realizar la solicitud de validación de Hola</span><span class="sxs-lookup"><span data-stu-id="4c9a8-142">Making hello validation request</span></span>
<span data-ttu-id="4c9a8-143">Una vez que tenemos el token de autorización de hello, podemos hacer token de hello solicitud toovalidate Hola.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-143">Once we have hello authorization token, we can make hello request toovalidate hello token.</span></span> <span data-ttu-id="4c9a8-144">RFC 7662 llama a este introspección de proceso y requiere que se `POST` un recurso de introspección de toohello de formulario HTML.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form toohello introspection resource.</span></span> <span data-ttu-id="4c9a8-145">Hola formulario HTML debe contener al menos un par de clave/valor con la clave de hello `token`.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-145">hello HTML form must at least contain a key/value pair with hello key `token`.</span></span> <span data-ttu-id="4c9a8-146">Este servidor de autorización de solicitud toohello también debe ser autenticado tooensure que los clientes malintencionados no pueden ir se podrá para tokens válidos.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-146">This request toohello authorization server must also be authenticated tooensure that malicious clients cannot go trawling for valid tokens.</span></span>

```xml
<send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
  <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
  <set-method>POST</set-method>
  <set-header name="Authorization" exists-action="override">
    <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
  </set-header>
  <set-header name="Content-Type" exists-action="override">
    <value>application/x-www-form-urlencoded</value>
  </set-header>
  <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
</send-request>
```

### <a name="checking-hello-response"></a><span data-ttu-id="4c9a8-147">Comprobación de respuesta de Hola</span><span class="sxs-lookup"><span data-stu-id="4c9a8-147">Checking hello response</span></span>
<span data-ttu-id="4c9a8-148">Hola `response-variable-name` atributo es hello de acceso de toogive usado devolvió una respuesta.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-148">hello `response-variable-name` attribute is used toogive access hello returned response.</span></span> <span data-ttu-id="4c9a8-149">Hello nombre definido en esta propiedad puede utilizarse como una clave en hello `context.Variables` Hola de diccionario tooaccess `IResponse` objeto.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-149">hello name defined in this property can be used as a key into hello `context.Variables` dictionary tooaccess hello `IResponse` object.</span></span>

<span data-ttu-id="4c9a8-150">Desde el objeto de respuesta de hello podemos recuperar cuerpo hello y RFC 7622 nos indica que la respuesta de hello debe ser un objeto JSON y debe contener al menos una propiedad denominada `active` que es un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-150">From hello response object we can retrieve hello body and RFC 7622 tells us that hello response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="4c9a8-151">Cuando `active` es true, a continuación, Hola token se considera válido.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-151">When `active` is true then hello token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="4c9a8-152">Notificación de error</span><span class="sxs-lookup"><span data-stu-id="4c9a8-152">Reporting failure</span></span>
<span data-ttu-id="4c9a8-153">Utilizamos un `<choose>` toodetect directiva si Hola token no es válido y si es así, devolver una respuesta 401.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-153">We use a `<choose>` policy toodetect if hello token is invalid and if so, return a 401 response.</span></span>

```xml
<choose>
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
    <return-response response-variable-name="existing response variable">
      <set-status code="401" reason="Unauthorized" />
      <set-header name="WWW-Authenticate" exists-action="override">
        <value>Bearer error="invalid_token"</value>
      </set-header>
    </return-response>
  </when>
</choose>
```

<span data-ttu-id="4c9a8-154">Según [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) que describe cómo `bearer` se deberían usar tokens, también devolvemos un `WWW-Authenticate` encabezado con la respuesta de hello 401.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with hello 401 response.</span></span> <span data-ttu-id="4c9a8-155">Hola WWW-Authenticate está previsto tooinstruct un cliente acerca de cómo tooconstruct una solicitud autorizada correctamente.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-155">hello WWW-Authenticate is intended tooinstruct a client on how tooconstruct a properly authorized request.</span></span> <span data-ttu-id="4c9a8-156">Pagar toohello gran variedad de enfoques posibles con el marco de trabajo de hello OAuth2, resulta difícil toocommunicate Hola a todos información necesaria.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-156">Due toohello wide variety of approaches possible with hello OAuth2 framework, it is difficult toocommunicate all hello needed information.</span></span> <span data-ttu-id="4c9a8-157">Afortunadamente hay trabajos en curso toohelp [clientes descubrir cómo tooproperly autorizar el servidor de recursos de las solicitudes tooa](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span><span class="sxs-lookup"><span data-stu-id="4c9a8-157">Fortunately there are efforts underway toohelp [clients discover how tooproperly authorize requests tooa resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="4c9a8-158">Solución final</span><span class="sxs-lookup"><span data-stu-id="4c9a8-158">Final solution</span></span>
<span data-ttu-id="4c9a8-159">Reunir todas las piezas de hello, obtenemos Hola después de la directiva:</span><span class="sxs-lookup"><span data-stu-id="4c9a8-159">Putting all hello pieces together, we get hello following policy:</span></span>

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
    <set-method>POST</set-method>
    <set-header name="Authorization" exists-action="override">
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
    </set-header>
    <set-header name="Content-Type" exists-action="override">
      <value>application/x-www-form-urlencoded</value>
    </set-header>
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
  </send-request>

  <choose>
          <!-- Check active property in response -->
          <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
              <!-- Return 401 Unauthorized with http-problem payload -->
              <return-response response-variable-name="existing response variable">
                  <set-status code="401" reason="Unauthorized" />
                  <set-header name="WWW-Authenticate" exists-action="override">
                      <value>Bearer error="invalid_token"</value>
                  </set-header>
              </return-response>
          </when>
      </choose>
  <base />
</inbound>
```

<span data-ttu-id="4c9a8-160">Esto es solo uno de muchos ejemplos de cómo hello `send-request` directiva puede ser servicios externos útil de toointegrate usado en proceso de Hola de solicitudes y respuestas que fluyen a través del servicio de administración de API de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-160">This is only one of many examples of how hello `send-request` policy can be used toointegrate useful external services into hello process of requests and responses flowing through hello API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="4c9a8-161">Composición de respuesta</span><span class="sxs-lookup"><span data-stu-id="4c9a8-161">Response Composition</span></span>
<span data-ttu-id="4c9a8-162">Hola `send-request` directiva se puede usar para mejorar un sistema de back-end de la solicitud primaria tooa, tal y como vimos en el ejemplo anterior de hello, o se puede utilizar como un reemplazo completo para de llamada de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-162">hello `send-request` policy can be used for enhancing a primary request tooa backend system, as we saw in hello previous example, or it can be used as a complete replace for of hello backend call.</span></span> <span data-ttu-id="4c9a8-163">Gracias a esta técnica se pueden crear fácilmente recursos compuestos que se agregan desde varios sistemas diferentes.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="4c9a8-164">Creación de un panel</span><span class="sxs-lookup"><span data-stu-id="4c9a8-164">Building a dashboard</span></span>
<span data-ttu-id="4c9a8-165">A veces desea toobe tooexpose capaz de información que existe en varios sistemas de back-end, por ejemplo, toodrive un panel.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-165">Sometimes you want toobe able tooexpose information that exists in multiple backend systems, for example, toodrive a dashboard.</span></span> <span data-ttu-id="4c9a8-166">Hola KPI proceden de todos los diferentes back-end, pero prefiere no tooprovide acceso directo toothem y sería estupendo si se puede recuperar toda la información de hello en una sola solicitud.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-166">hello KPIs come from all different back-ends, but you would prefer not tooprovide direct access toothem and it would be nice if all hello information could be retrieved in a single request.</span></span> <span data-ttu-id="4c9a8-167">Quizás parte de información de back-end de hello necesita algunos segmentación y reorganización e inmunizar un poco en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-167">Perhaps some of hello backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="4c9a8-168">Que se va a toocache puede que el recurso compuesto sería un tooreduce útil cargar Hola back-end ya que sabe que los usuarios tienen un hábito de ataques tecla F5 de hello en orden toosee si sus métricas underperforming podrían cambiar.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-168">Being able toocache that composite resource would be a useful tooreduce hello backend load as you know users have a habit of hammering hello F5 key in order toosee if their underperforming metrics might change.</span></span>    

### <a name="faking-hello-resource"></a><span data-ttu-id="4c9a8-169">Falsificación de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="4c9a8-169">Faking hello resource</span></span>
<span data-ttu-id="4c9a8-170">Hola primera toobuilding paso nuestro recurso panel sea tooconfigure una operación de nuevo en el portal para desarrolladores de administración de API Hola.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-170">hello first step toobuilding our dashboard resource is tooconfigure a new operation in hello API Management publisher portal.</span></span> <span data-ttu-id="4c9a8-171">Esto será una tooconfigure de operación utilizada de marcador de posición nuestro toobuild de directiva de composición nuestro recurso dinámico.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-171">This will be a placeholder operation used tooconfigure our composition policy toobuild our dynamic resource.</span></span>

![Operación del panel](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a><span data-ttu-id="4c9a8-173">Realizar solicitudes de Hola</span><span class="sxs-lookup"><span data-stu-id="4c9a8-173">Making hello requests</span></span>
<span data-ttu-id="4c9a8-174">Una vez Hola `dashboard` se ha creado la operación podemos configurar una directiva específicamente para esa operación.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-174">Once hello `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![Operación del panel](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="4c9a8-176">primer paso de Hello es tooextract los parámetros de consulta de solicitud entrante de hello, por lo que podemos reenviarlos tooour back-end.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-176">hello first step  is tooextract any query parameters from hello incoming request, so that we can forward them tooour backend.</span></span> <span data-ttu-id="4c9a8-177">En este ejemplo, nuestro panel muestra información basada en un período de tiempo y, por tanto, tiene un parámetro `fromDate` y `toDate`.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="4c9a8-178">Podemos usar hello `set-variable` información de hello tooextract la directiva de dirección URL de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-178">We can use hello `set-variable` policy tooextract hello information from hello request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="4c9a8-179">Una vez que tenemos esta información podemos hacer que las solicitudes de sistemas de back-end de tooall Hola.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-179">Once we have this information we can make requests tooall hello backend systems.</span></span> <span data-ttu-id="4c9a8-180">Cada solicitud construye una nueva dirección URL con información de parámetros de Hola y llama a su servidor respectivo y almacena la respuesta de hello en una variable de contexto.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-180">Each request constructs a new URL with hello parameter information and calls its respective server and stores hello response in a context variable.</span></span>

```xml
<send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
  <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
  <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="4c9a8-181">Estas solicitudes se ejecutarán en secuencia, que no es lo ideal.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="4c9a8-182">En una próxima versión presentaremos una directiva nueva llamada `wait` que permitirá a todos estos tooexecute solicitudes en paralelo.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests tooexecute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="4c9a8-183">Respuesta</span><span class="sxs-lookup"><span data-stu-id="4c9a8-183">Responding</span></span>
<span data-ttu-id="4c9a8-184">podemos usar Hola respuesta tooconstruct Hola compuesta [respuesta devuelto](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) directiva.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-184">tooconstruct hello composite response we can use hello [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="4c9a8-185">Hola `set-body` elemento puede usar una expresión tooconstruct un nuevo `JObject` con todas las representaciones de componente de hello incrustadas como propiedades.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-185">hello `set-body` element can use an expression tooconstruct a new `JObject` with all hello component representations embedded as properties.</span></span>

```xml
<return-response response-variable-name="existing response variable">
  <set-status code="200" reason="OK" />
  <set-header name="Content-Type" exists-action="override">
    <value>application/json</value>
  </set-header>
  <set-body>
    @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                  new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                  new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                  new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                  ).ToString())
  </set-body>
</return-response>
```

<span data-ttu-id="4c9a8-186">directiva completa Hello tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="4c9a8-186">hello complete policy looks as follows:</span></span>

```xml
<policies>
    <inbound>

  <set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
  <set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">

    <send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
      <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
      <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <return-response response-variable-name="existing response variable">
      <set-status code="200" reason="OK" />
      <set-header name="Content-Type" exists-action="override">
        <value>application/json</value>
      </set-header>
      <set-body>
        @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                      new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                      new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                      new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                      ).ToString())
      </set-body>
    </return-response>
    </inbound>
    <backend>
        <base />
    </backend>
    <outbound>
        <base />
    </outbound>
</policies>
```

<span data-ttu-id="4c9a8-187">En la configuración de Hola de operación de marcador de posición de hello que podemos configurar Hola panel recurso toobe en caché durante al menos una hora como entendemos naturaleza Hola de datos de hello significa que incluso si es una hora desfasada seguirá estando lo suficientemente eficaces usuarios de toohello de tooconvey información valiosa.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-187">In hello configuration of hello placeholder operation we can configure hello dashboard resource toobe cached for at least an hour because we understand hello nature of hello data means that even if it is an hour out of date, it will still be sufficiently effective tooconvey valuable information toohello users.</span></span>

## <a name="summary"></a><span data-ttu-id="4c9a8-188">Resumen</span><span class="sxs-lookup"><span data-stu-id="4c9a8-188">Summary</span></span>
<span data-ttu-id="4c9a8-189">Servicio de administración de API de Azure proporciona directivas flexibles que pueden ser de forma selectiva aplicarán tooHTTP tráfico y habilita la composición de servicios back-end.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-189">Azure API Management service provides flexible policies that can be selectively applied tooHTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="4c9a8-190">Si desea tooenhance la puerta de enlace de API con acciones, comprobación, capacidades de validación de la alerta o crear nuevos recursos compuestos en función de varios servicios de back-end, Hola `send-request` y directivas relacionadas abre todo un mundo de posibilidades.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-190">Whether you want tooenhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, hello `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="4c9a8-191">Ver un vídeo de información general de estas directivas</span><span class="sxs-lookup"><span data-stu-id="4c9a8-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="4c9a8-192">Para obtener más información sobre hello [envío una manera de solicitud](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [solicitud de envío](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), y [respuesta devuelto](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) las directivas que se describen en este artículo, consulte Hola después de vídeo.</span><span class="sxs-lookup"><span data-stu-id="4c9a8-192">For more information on hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

