---
title: "Uso del servicio de administración de API para generar solicitudes HTTP"
description: "Aprenda a usar las directivas de solicitud y respuesta en Administración de API para llamar a servicios externos de su API"
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
ms.openlocfilehash: e778943715d6ca5256ad612d82bdc1f82197df0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-external-services-from-the-azure-api-management-service"></a><span data-ttu-id="ffd16-103">Uso de servicios externos del servicio de administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="ffd16-103">Using external services from the Azure API Management service</span></span>
<span data-ttu-id="ffd16-104">Las directivas disponibles en el servicio de administración de API de Azure pueden llevar a cabo una gran variedad de trabajo útil basado exclusivamente en la solicitud entrante, la respuesta saliente y la información de configuración básica.</span><span class="sxs-lookup"><span data-stu-id="ffd16-104">The policies available in Azure API Management service can do a wide range of useful work based purely on the incoming request, the outgoing response and basic configuration information.</span></span> <span data-ttu-id="ffd16-105">Pero la interacción con servicios externos de las directivas de Administración de API brinda muchas más oportunidades.</span><span class="sxs-lookup"><span data-stu-id="ffd16-105">However, being able to interact with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="ffd16-106">Anteriormente hemos visto cómo podemos interactuar con el [servicio del Centro de eventos de Azure con fines de registro, supervisión y análisis](api-management-log-to-eventhub-sample.md).</span><span class="sxs-lookup"><span data-stu-id="ffd16-106">We have previously seen how we can interact with the [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="ffd16-107">En este artículo encontrará las directivas que permiten interactuar con cualquier servicio basado en HTTP externo.</span><span class="sxs-lookup"><span data-stu-id="ffd16-107">In this article we will demonstrate policies that allow you to interact with any external HTTP based service.</span></span> <span data-ttu-id="ffd16-108">Dichas directivas se pueden usar para desencadenar eventos remotos o recuperar información que se utilizará para manipular en cierto modo la solicitud y respuesta originales.</span><span class="sxs-lookup"><span data-stu-id="ffd16-108">These policies can be used for triggering remote events or for retrieving information that will be used to manipulate the original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="ffd16-109">Send-One-Way-Request</span><span class="sxs-lookup"><span data-stu-id="ffd16-109">Send-One-Way-Request</span></span>
<span data-ttu-id="ffd16-110">Es posible que la interacción externa más sencilla sea el estilo de fire and forget de solicitud que permite que se notifique a un servicio externo de algún tipo de evento importante.</span><span class="sxs-lookup"><span data-stu-id="ffd16-110">Possibly the simplest external interaction is the fire-and-forget style of request that allows an external service to be notified of some kind of important event.</span></span> <span data-ttu-id="ffd16-111">Se puede usar la directiva de flujo de control `choose` para detectar cualquier tipo de condición que suscite interés y después, si se cumple esta, se puede realizar una solicitud HTTP externa mediante la directiva [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) .</span><span class="sxs-lookup"><span data-stu-id="ffd16-111">We can use the control flow policy `choose` to detect any kind of condition that we are interested in and then, if the condition is satisfied, we can make an external HTTP request using the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="ffd16-112">Podría tratarse de una solicitud para un sistema de mensajería como Hipchat o Slack o una API de Correo como SendGrid o MailChimp, o bien para incidentes de soporte técnico críticos como PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="ffd16-112">This could be a request to a messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="ffd16-113">Todos estos sistemas de mensajería tienen API HTTP sencillas que se pueden invocar fácilmente.</span><span class="sxs-lookup"><span data-stu-id="ffd16-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="ffd16-114">Alerta con Slack</span><span class="sxs-lookup"><span data-stu-id="ffd16-114">Alerting with Slack</span></span>
<span data-ttu-id="ffd16-115">En el siguiente ejemplo puede ver cómo enviar un mensaje a un salón de chat de Slack si el código de estado de respuesta HTTP es mayor o igual que 500.</span><span class="sxs-lookup"><span data-stu-id="ffd16-115">The following example demonstrates how to send a message to a Slack chat room if the HTTP response status code is greater than or equal to 500.</span></span> <span data-ttu-id="ffd16-116">Un error de intervalo 500 indica un problema con nuestra API de back-end que el cliente de la misma no puede resolver por sí mismo.</span><span class="sxs-lookup"><span data-stu-id="ffd16-116">A 500 range error indicates a problem with our backend API that the client of our API cannot resolve themselves.</span></span> <span data-ttu-id="ffd16-117">Normalmente requiere algún tipo de intervención por nuestra parte.</span><span class="sxs-lookup"><span data-stu-id="ffd16-117">It usually requires some kind of intervention on our part.</span></span>  

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

<span data-ttu-id="ffd16-118">Slack tiene la noción de enlaces web entrantes.</span><span class="sxs-lookup"><span data-stu-id="ffd16-118">Slack has the notion of inbound web hooks.</span></span> <span data-ttu-id="ffd16-119">Al configurar un enlace web entrante, Slack genera una dirección URL especial que permite hacer una sencilla solicitud POST y pasar un mensaje al canal de Slack.</span><span class="sxs-lookup"><span data-stu-id="ffd16-119">When configuring an inbound web hook, Slack generates a special URL which allows you to do a simple POST request and to pass a message into the Slack channel.</span></span> <span data-ttu-id="ffd16-120">El cuerpo JSON creado se basa en un formato definido por Slack.</span><span class="sxs-lookup"><span data-stu-id="ffd16-120">The JSON body that we create is based on a format defined by Slack.</span></span>

![Enlace web de Slack](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="ffd16-122">¿Es fire and forget lo suficientemente bueno?</span><span class="sxs-lookup"><span data-stu-id="ffd16-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="ffd16-123">Existen ciertos compromisos cuando se usa un estilo de fire and forget de solicitud.</span><span class="sxs-lookup"><span data-stu-id="ffd16-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="ffd16-124">Si por algún motivo se produce un error en la solicitud, este no se notificará.</span><span class="sxs-lookup"><span data-stu-id="ffd16-124">If for some reason, the request fails, then the failure will not be reported.</span></span> <span data-ttu-id="ffd16-125">En esta situación concreta, no se garantizan la complejidad de tener un sistema de informe de errores secundario ni el costo de rendimiento adicional de esperar la respuesta.</span><span class="sxs-lookup"><span data-stu-id="ffd16-125">In this particular situation, the complexity of having a secondary failure reporting system and the additional performance cost of waiting for the response is not warranted.</span></span> <span data-ttu-id="ffd16-126">En aquellos escenarios donde sea esencial comprobar la respuesta, la directiva [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) constituye una mejor opción.</span><span class="sxs-lookup"><span data-stu-id="ffd16-126">For scenarios where it is essential to check the response, then the [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="ffd16-127">send-request</span><span class="sxs-lookup"><span data-stu-id="ffd16-127">Send-Request</span></span>
<span data-ttu-id="ffd16-128">La directiva `send-request` permite usar un servicio externo para realizar funciones complejas de procesamiento y devolver datos al servicio de Administración de API que pueden usarse para un posterior procesamiento de directivas.</span><span class="sxs-lookup"><span data-stu-id="ffd16-128">The `send-request` policy enables using an external service to perform complex processing functions and return data to the API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="ffd16-129">Autorización de tokens de referencia</span><span class="sxs-lookup"><span data-stu-id="ffd16-129">Authorizing reference tokens</span></span>
<span data-ttu-id="ffd16-130">Una de las funciones principales de Administración de API es proteger los recursos de back-end.</span><span class="sxs-lookup"><span data-stu-id="ffd16-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="ffd16-131">Si el servidor de autorización que usa su API crea [tokens de JWT](http://jwt.io/) como parte de su flujo de OAuth2, igual que hace [Azure Active Directory](../active-directory/active-directory-aadconnect.md), puede usar la directiva `validate-jwt` para comprobar la validez del token.</span><span class="sxs-lookup"><span data-stu-id="ffd16-131">If the authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use the `validate-jwt` policy to verify the validity of the token.</span></span> <span data-ttu-id="ffd16-132">Pero algunos servidores de autorización crean lo que se denomina [tokens de referencia](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) , que no se pueden comprobar sin llamar de vuelta al servidor de autorización.</span><span class="sxs-lookup"><span data-stu-id="ffd16-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back to the authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="ffd16-133">Introspección estandarizada</span><span class="sxs-lookup"><span data-stu-id="ffd16-133">Standardized introspection</span></span>
<span data-ttu-id="ffd16-134">En el pasado no existía una forma estandarizada de comprobar un token de referencia con un servidor de autorización.</span><span class="sxs-lookup"><span data-stu-id="ffd16-134">In the past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="ffd16-135">Pero IETF publicó un estándar propuesto recientemente, [RFC 7662](https://tools.ietf.org/html/rfc7662) , que define cómo un servidor de recursos puede comprobar la validez de un token.</span><span class="sxs-lookup"><span data-stu-id="ffd16-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by the IETF that defines how a resource server can verify the validity of a token.</span></span>

### <a name="extracting-the-token"></a><span data-ttu-id="ffd16-136">Extracción del token</span><span class="sxs-lookup"><span data-stu-id="ffd16-136">Extracting the token</span></span>
<span data-ttu-id="ffd16-137">El primer paso es extraer el token del encabezado de autorización.</span><span class="sxs-lookup"><span data-stu-id="ffd16-137">The first step is to extract the token from the Authorization header.</span></span> <span data-ttu-id="ffd16-138">El formato del valor de encabezado debe constar del esquema de autorización `Bearer` , un espacio y el token de autorización según [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="ffd16-138">The header value should be formatted with the `Bearer` authorization scheme, a single space and then the authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="ffd16-139">Desafortunadamente, hay casos donde se omite el esquema de autorización.</span><span class="sxs-lookup"><span data-stu-id="ffd16-139">Unfortunately there are cases where the authorization scheme is omitted.</span></span> <span data-ttu-id="ffd16-140">Para tener esto en cuenta cuando se analiza, se divide el valor de encabezado en un espacio y se selecciona la última cadena en la matriz de cadenas devuelta.</span><span class="sxs-lookup"><span data-stu-id="ffd16-140">To account for this when parsing, we split the header value on a space and select the last string from the returned array of strings.</span></span> <span data-ttu-id="ffd16-141">Esto proporciona una solución alternativa para los encabezados de autorización con formato incorrecto.</span><span class="sxs-lookup"><span data-stu-id="ffd16-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-the-validation-request"></a><span data-ttu-id="ffd16-142">Realización de la solicitud de validación</span><span class="sxs-lookup"><span data-stu-id="ffd16-142">Making the validation request</span></span>
<span data-ttu-id="ffd16-143">Una vez que tenemos el token de autorización, podemos realizar la solicitud para validarlo.</span><span class="sxs-lookup"><span data-stu-id="ffd16-143">Once we have the authorization token, we can make the request to validate the token.</span></span> <span data-ttu-id="ffd16-144">RFC 7662 llama introspección a este proceso y requiere que `POST` un formulario HTML en el recurso de introspección.</span><span class="sxs-lookup"><span data-stu-id="ffd16-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form to the introspection resource.</span></span> <span data-ttu-id="ffd16-145">El formulario HTML debe contener al menos un par clave-valor con la clave `token`.</span><span class="sxs-lookup"><span data-stu-id="ffd16-145">The HTML form must at least contain a key/value pair with the key `token`.</span></span> <span data-ttu-id="ffd16-146">Esta solicitud para el servidor de autorización también debe autenticarse a fin de garantizar que los clientes malintencionados no puedan rastrear tokens válidos.</span><span class="sxs-lookup"><span data-stu-id="ffd16-146">This request to the authorization server must also be authenticated to ensure that malicious clients cannot go trawling for valid tokens.</span></span>

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

### <a name="checking-the-response"></a><span data-ttu-id="ffd16-147">Comprobación de la respuesta</span><span class="sxs-lookup"><span data-stu-id="ffd16-147">Checking the response</span></span>
<span data-ttu-id="ffd16-148">El atributo `response-variable-name` sirve para proporcionar acceso a la respuesta devuelta.</span><span class="sxs-lookup"><span data-stu-id="ffd16-148">The `response-variable-name` attribute is used to give access the returned response.</span></span> <span data-ttu-id="ffd16-149">El nombre definido en esta propiedad se puede usar como clave en el diccionario `context.Variables` para acceder al objeto `IResponse`.</span><span class="sxs-lookup"><span data-stu-id="ffd16-149">The name defined in this property can be used as a key into the `context.Variables` dictionary to access the `IResponse` object.</span></span>

<span data-ttu-id="ffd16-150">En el objeto de respuesta, se puede recuperar el cuerpo, y RFC 7622 indica que la respuesta debe ser un objeto JSON que contenga al menos una propiedad denominada `active` , que es un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="ffd16-150">From the response object we can retrieve the body and RFC 7622 tells us that the response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="ffd16-151">Cuando `active` es true, el token se considera válido.</span><span class="sxs-lookup"><span data-stu-id="ffd16-151">When `active` is true then the token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="ffd16-152">Notificación de error</span><span class="sxs-lookup"><span data-stu-id="ffd16-152">Reporting failure</span></span>
<span data-ttu-id="ffd16-153">Se usa una directiva `<choose>` para detectar si el token no es válido y, en caso de no serlo, devolver una respuesta 401.</span><span class="sxs-lookup"><span data-stu-id="ffd16-153">We use a `<choose>` policy to detect if the token is invalid and if so, return a 401 response.</span></span>

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

<span data-ttu-id="ffd16-154">Según [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3), que describe cómo se deben usar los tokens de `bearer`, también se devuelve un encabezado `WWW-Authenticate` con la respuesta 401.</span><span class="sxs-lookup"><span data-stu-id="ffd16-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with the 401 response.</span></span> <span data-ttu-id="ffd16-155">WWW-Authenticate está pensado para indicar a un cliente cómo crear una solicitud debidamente autorizada.</span><span class="sxs-lookup"><span data-stu-id="ffd16-155">The WWW-Authenticate is intended to instruct a client on how to construct a properly authorized request.</span></span> <span data-ttu-id="ffd16-156">Debido a la gran variedad de enfoques posibles con el marco OAuth2, es difícil comunicar toda la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="ffd16-156">Due to the wide variety of approaches possible with the OAuth2 framework, it is difficult to communicate all the needed information.</span></span> <span data-ttu-id="ffd16-157">Por fortuna, se están adoptando medidas para enseñar a los [clientes a autorizar debidamente las solicitudes a un servidor de recursos](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span><span class="sxs-lookup"><span data-stu-id="ffd16-157">Fortunately there are efforts underway to help [clients discover how to properly authorize requests to a resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="ffd16-158">Solución final</span><span class="sxs-lookup"><span data-stu-id="ffd16-158">Final solution</span></span>
<span data-ttu-id="ffd16-159">Al unir todas las piezas, se obtiene la siguiente directiva:</span><span class="sxs-lookup"><span data-stu-id="ffd16-159">Putting all the pieces together, we get the following policy:</span></span>

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request to Token Server to validate token (see RFC 7662) -->
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

<span data-ttu-id="ffd16-160">Este ejemplo es solo uno de los muchos que hay sobre cómo puede usarse la directiva `send-request` para integrar servicios externos útiles en el proceso de solicitudes y respuestas que fluyen a través del servicio de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="ffd16-160">This is only one of many examples of how the `send-request` policy can be used to integrate useful external services into the process of requests and responses flowing through the API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="ffd16-161">Composición de respuesta</span><span class="sxs-lookup"><span data-stu-id="ffd16-161">Response Composition</span></span>
<span data-ttu-id="ffd16-162">La directiva `send-request` se puede emplear para mejorar una solicitud principal a un sistema de back-end, como vimos en el ejemplo anterior, o bien se puede usar como una sustitución íntegra de la llamada de back-end.</span><span class="sxs-lookup"><span data-stu-id="ffd16-162">The `send-request` policy can be used for enhancing a primary request to a backend system, as we saw in the previous example, or it can be used as a complete replace for of the backend call.</span></span> <span data-ttu-id="ffd16-163">Gracias a esta técnica se pueden crear fácilmente recursos compuestos que se agregan desde varios sistemas diferentes.</span><span class="sxs-lookup"><span data-stu-id="ffd16-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="ffd16-164">Creación de un panel</span><span class="sxs-lookup"><span data-stu-id="ffd16-164">Building a dashboard</span></span>
<span data-ttu-id="ffd16-165">A veces le gustaría exponer información existente en varios sistemas de back-end, por ejemplo, para realizar un panel.</span><span class="sxs-lookup"><span data-stu-id="ffd16-165">Sometimes you want to be able to expose information that exists in multiple backend systems, for example, to drive a dashboard.</span></span> <span data-ttu-id="ffd16-166">Los KPI proceden de los distintos back-end, pero prefiere no proporcionarles acceso directo y sería mejor si se pudiera recuperar toda la información en una única solicitud.</span><span class="sxs-lookup"><span data-stu-id="ffd16-166">The KPIs come from all different back-ends, but you would prefer not to provide direct access to them and it would be nice if all the information could be retrieved in a single request.</span></span> <span data-ttu-id="ffd16-167">Es posible que parte de la información de back-end deba segmentarse, desglosarse y corregirse un poco primero.</span><span class="sxs-lookup"><span data-stu-id="ffd16-167">Perhaps some of the backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="ffd16-168">Poder almacenar en caché ese recurso compuesto sería útil para reducir la carga de back-end, pues ya sabe que los usuarios tienen la costumbre de recurrir a la tecla F5 para ver si pueden cambiar sus métricas de déficit de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="ffd16-168">Being able to cache that composite resource would be a useful to reduce the backend load as you know users have a habit of hammering the F5 key in order to see if their underperforming metrics might change.</span></span>    

### <a name="faking-the-resource"></a><span data-ttu-id="ffd16-169">Emulación del recurso</span><span class="sxs-lookup"><span data-stu-id="ffd16-169">Faking the resource</span></span>
<span data-ttu-id="ffd16-170">El primer paso para crear nuestro recurso del panel es configurar una nueva operación en el portal del publicador de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="ffd16-170">The first step to building our dashboard resource is to configure a new operation in the API Management publisher portal.</span></span> <span data-ttu-id="ffd16-171">Será una operación de marcador de posición usada para configurar nuestra directiva de composición a fin de crear nuestro recurso dinámico.</span><span class="sxs-lookup"><span data-stu-id="ffd16-171">This will be a placeholder operation used to configure our composition policy to build our dynamic resource.</span></span>

![Operación del panel](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-the-requests"></a><span data-ttu-id="ffd16-173">Realización de las solicitudes</span><span class="sxs-lookup"><span data-stu-id="ffd16-173">Making the requests</span></span>
<span data-ttu-id="ffd16-174">Una vez creada la operación de `dashboard` , se puede configurar una directiva para esa operación en concreto.</span><span class="sxs-lookup"><span data-stu-id="ffd16-174">Once the `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![Operación del panel](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="ffd16-176">El primer paso es extraer los parámetros de consulta de la solicitud entrante, de modo que puedan reenviarse al back-end.</span><span class="sxs-lookup"><span data-stu-id="ffd16-176">The first step  is to extract any query parameters from the incoming request, so that we can forward them to our backend.</span></span> <span data-ttu-id="ffd16-177">En este ejemplo, nuestro panel muestra información basada en un período de tiempo y, por tanto, tiene un parámetro `fromDate` y `toDate`.</span><span class="sxs-lookup"><span data-stu-id="ffd16-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="ffd16-178">Se puede usar la directiva `set-variable` para extraer la información de la dirección URL de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="ffd16-178">We can use the `set-variable` policy to extract the information from the request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="ffd16-179">Una vez que se tiene esta información, se pueden realizar solicitudes a todos los sistemas de back-end.</span><span class="sxs-lookup"><span data-stu-id="ffd16-179">Once we have this information we can make requests to all the backend systems.</span></span> <span data-ttu-id="ffd16-180">Cada solicitud construye una nueva dirección URL con la información de los parámetros y llama a su servidor correspondiente y almacena la respuesta en una variable de contexto.</span><span class="sxs-lookup"><span data-stu-id="ffd16-180">Each request constructs a new URL with the parameter information and calls its respective server and stores the response in a context variable.</span></span>

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

<span data-ttu-id="ffd16-181">Estas solicitudes se ejecutarán en secuencia, que no es lo ideal.</span><span class="sxs-lookup"><span data-stu-id="ffd16-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="ffd16-182">En una próxima versión, se introducirá una nueva directiva llamada `wait` que permitirá la ejecución en paralelo de todas estas solicitudes.</span><span class="sxs-lookup"><span data-stu-id="ffd16-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests to execute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="ffd16-183">Respuesta</span><span class="sxs-lookup"><span data-stu-id="ffd16-183">Responding</span></span>
<span data-ttu-id="ffd16-184">Para construir la respuesta compuesta, se puede usar la directiva [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) .</span><span class="sxs-lookup"><span data-stu-id="ffd16-184">To construct the composite response we can use the [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="ffd16-185">El elemento `set-body` puede usar una expresión para construir un nuevo elemento `JObject` con todas las representaciones de componentes insertadas como propiedades.</span><span class="sxs-lookup"><span data-stu-id="ffd16-185">The `set-body` element can use an expression to construct a new `JObject` with all the component representations embedded as properties.</span></span>

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

<span data-ttu-id="ffd16-186">Este es el aspecto de la directiva completa:</span><span class="sxs-lookup"><span data-stu-id="ffd16-186">The complete policy looks as follows:</span></span>

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

<span data-ttu-id="ffd16-187">En la configuración de la operación de marcador de posición se puede configurar el recurso del panel que se va a almacenar en caché durante al menos una hora porque conocemos la naturaleza de los datos, que aunque lleven una hora sin actualizarse seguirán siendo lo suficientemente efectivos para transmitir información valiosa a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="ffd16-187">In the configuration of the placeholder operation we can configure the dashboard resource to be cached for at least an hour because we understand the nature of the data means that even if it is an hour out of date, it will still be sufficiently effective to convey valuable information to the users.</span></span>

## <a name="summary"></a><span data-ttu-id="ffd16-188">Resumen</span><span class="sxs-lookup"><span data-stu-id="ffd16-188">Summary</span></span>
<span data-ttu-id="ffd16-189">El servicio de administración de API de Azure proporciona directivas flexibles que se pueden aplicar de forma selectiva al tráfico HTTP y permite la composición de servicios de back-end.</span><span class="sxs-lookup"><span data-stu-id="ffd16-189">Azure API Management service provides flexible policies that can be selectively applied to HTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="ffd16-190">Si desea mejorar la puerta de enlace de la API con funciones de alerta, comprobación, capacidades de validación o crear nuevos recursos compuestos basados en varios servicios de back-end, la directiva `send-request` y otras relacionadas ofrecen todo un mundo de posibilidades.</span><span class="sxs-lookup"><span data-stu-id="ffd16-190">Whether you want to enhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, the `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="ffd16-191">Ver un vídeo de información general de estas directivas</span><span class="sxs-lookup"><span data-stu-id="ffd16-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="ffd16-192">Para más información sobre las directivas [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) y [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) que se describen en este artículo, vea el siguiente vídeo.</span><span class="sxs-lookup"><span data-stu-id="ffd16-192">For more information on the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

