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
# <a name="using-external-services-from-hello-azure-api-management-service"></a>Uso de servicios externos de hello servicio de administración de API de Azure
las directivas de Hello disponibles en el servicio de administración de API de Azure pueden hacer una amplia gama de trabajo útil basado exclusivamente en la solicitud entrante de hello, respuesta de salida de hello y la información de configuración básica. Sin embargo, que se va a toointeract pueda con servicios externos de la API de administración de directivas abrirá muchas más posibilidades.

Previamente hemos visto cómo podemos interactuamos con hello [servicio del concentrador de eventos de Azure para el registro, supervisión y análisis](api-management-log-to-eventhub-sample.md). En este artículo se indicará el servicio basado en directivas que le permiten toointeract con cualquier HTTP externo. Estas directivas pueden utilizarse para la activación de eventos remotos o para recuperar la información que será la solicitud original de uso toomanipulate Hola y de respuesta de alguna manera.

## <a name="send-one-way-request"></a>Send-One-Way-Request
Posiblemente hello interacción externo más sencilla es Hola enviar y olvidarse estilo de solicitud que permita un toobe de servicio externo una notificación de algún tipo de evento importante. Podemos usar la directiva de flujo de control de hello `choose` toodetect cualquier tipo de condición que está interesados y, a continuación, si hello condición se cumple, podemos hacer que una solicitud HTTP externa mediante hello [envío una manera de solicitud](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) directiva. Podría tratarse de un tooa solicitud mensajería sistema, como Hipchat o demora o un correo electrónico de la API como SendGrid o MailChimp, o para ver incidentes de soporte técnico crítico algo como PagerDuty. Todos estos sistemas de mensajería tienen API HTTP sencillas que se pueden invocar fácilmente.

### <a name="alerting-with-slack"></a>Alerta con Slack
Hola siguiente ejemplo muestra cómo toosend una tooa mensaje salón de chat una demora si el código de estado de respuesta HTTP de hello es mayor que o igual a too500. Un error de 500 rango indica un problema con la API de back-end que Hola cliente de la API no se puede resolver por sí mismos. Normalmente requiere algún tipo de intervención por nuestra parte.  

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

Demora tiene noción de Hola de enlaces de web entrantes. Al configurar un enlace web entrantes, demora genera una dirección URL especial que permite toodo una solicitud POST simple y toopass un mensaje en canales de demora de Hola. Hola cuerpo JSON que creamos se basa en un formato definido por el margen de demora.

![Enlace web de Slack](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a>¿Es fire and forget lo suficientemente bueno?
Existen ciertos compromisos cuando se usa un estilo de fire and forget de solicitud. Si por algún motivo, se produce un error en la solicitud de hello, a continuación, no se notificará el error Hola. En este caso concreto, no se ofrecen garantías complejidad Hola de tener un sistema de informes de error secundario y el costo de rendimiento adicionales de Hola de espera de respuesta de Hola. Para escenarios donde resulta esencial toocheck respuesta de hello, a continuación, Hola [solicitud de envío](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) Directiva constituye una mejor opción.

## <a name="send-request"></a>send-request
Hola `send-request` directiva se habilita mediante un tooperform de servicio externo compleja funciones y servicio de administración de datos de retorno toohello API que se puede usar para su posterior procesamiento de directiva de procesamiento.

### <a name="authorizing-reference-tokens"></a>Autorización de tokens de referencia
Una de las funciones principales de Administración de API es proteger los recursos de back-end. Si crea el servidor de autorización de hello utilizada por la API [tokens JWT](http://jwt.io/) como parte de su flujo de OAuth2, como [Azure Active Directory](../active-directory/active-directory-aadconnect.md) es así, puede usar hello `validate-jwt` validez de hello tooverify de directiva de token de Hola. Sin embargo, algunos servidores de autorización crean lo que se conoce como [hacen referencia a tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) que no se puede comprobar sin establecimiento de un servidor de autorización de llamada toohello atrás.

### <a name="standardized-introspection"></a>Introspección estandarizada
Hola pasado no ha habido ninguna manera estándar de comprobar un símbolo (token) de referencia con un servidor de autorización. Sin embargo estándar recientemente propuesto [7662 RFC](https://tools.ietf.org/html/rfc7662) publicó Hola IETF que define cómo un servidor de recursos puede comprobar la validez de Hola de un token.

### <a name="extracting-hello-token"></a>Extraer el token de Hola
Hola primer paso es tooextract Hola símbolo (token) de encabezado de autorización de Hola. valor del encabezado Hola debe tener el formato con hello `Bearer` esquema de autorización, un espacio único y, a continuación, autorización de hello token según [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1). Desafortunadamente, hay casos donde se omite el esquema de autorización de Hola. tooaccount para esto en el análisis, dividiremos el valor del encabezado de hello en un espacio y la cadena última de select Hola de hello devuelve la matriz de cadenas. Esto proporciona una solución alternativa para los encabezados de autorización con formato incorrecto.

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a>Realizar la solicitud de validación de Hola
Una vez que tenemos el token de autorización de hello, podemos hacer token de hello solicitud toovalidate Hola. RFC 7662 llama a este introspección de proceso y requiere que se `POST` un recurso de introspección de toohello de formulario HTML. Hola formulario HTML debe contener al menos un par de clave/valor con la clave de hello `token`. Este servidor de autorización de solicitud toohello también debe ser autenticado tooensure que los clientes malintencionados no pueden ir se podrá para tokens válidos.

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

### <a name="checking-hello-response"></a>Comprobación de respuesta de Hola
Hola `response-variable-name` atributo es hello de acceso de toogive usado devolvió una respuesta. Hello nombre definido en esta propiedad puede utilizarse como una clave en hello `context.Variables` Hola de diccionario tooaccess `IResponse` objeto.

Desde el objeto de respuesta de hello podemos recuperar cuerpo hello y RFC 7622 nos indica que la respuesta de hello debe ser un objeto JSON y debe contener al menos una propiedad denominada `active` que es un valor booleano. Cuando `active` es true, a continuación, Hola token se considera válido.

### <a name="reporting-failure"></a>Notificación de error
Utilizamos un `<choose>` toodetect directiva si Hola token no es válido y si es así, devolver una respuesta 401.

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

Según [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) que describe cómo `bearer` se deberían usar tokens, también devolvemos un `WWW-Authenticate` encabezado con la respuesta de hello 401. Hola WWW-Authenticate está previsto tooinstruct un cliente acerca de cómo tooconstruct una solicitud autorizada correctamente. Pagar toohello gran variedad de enfoques posibles con el marco de trabajo de hello OAuth2, resulta difícil toocommunicate Hola a todos información necesaria. Afortunadamente hay trabajos en curso toohelp [clientes descubrir cómo tooproperly autorizar el servidor de recursos de las solicitudes tooa](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).

### <a name="final-solution"></a>Solución final
Reunir todas las piezas de hello, obtenemos Hola después de la directiva:

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

Esto es solo uno de muchos ejemplos de cómo hello `send-request` directiva puede ser servicios externos útil de toointegrate usado en proceso de Hola de solicitudes y respuestas que fluyen a través del servicio de administración de API de Hola.

## <a name="response-composition"></a>Composición de respuesta
Hola `send-request` directiva se puede usar para mejorar un sistema de back-end de la solicitud primaria tooa, tal y como vimos en el ejemplo anterior de hello, o se puede utilizar como un reemplazo completo para de llamada de back-end de Hola. Gracias a esta técnica se pueden crear fácilmente recursos compuestos que se agregan desde varios sistemas diferentes.

### <a name="building-a-dashboard"></a>Creación de un panel
A veces desea toobe tooexpose capaz de información que existe en varios sistemas de back-end, por ejemplo, toodrive un panel. Hola KPI proceden de todos los diferentes back-end, pero prefiere no tooprovide acceso directo toothem y sería estupendo si se puede recuperar toda la información de hello en una sola solicitud. Quizás parte de información de back-end de hello necesita algunos segmentación y reorganización e inmunizar un poco en primer lugar. Que se va a toocache puede que el recurso compuesto sería un tooreduce útil cargar Hola back-end ya que sabe que los usuarios tienen un hábito de ataques tecla F5 de hello en orden toosee si sus métricas underperforming podrían cambiar.    

### <a name="faking-hello-resource"></a>Falsificación de recursos de Hola
Hola primera toobuilding paso nuestro recurso panel sea tooconfigure una operación de nuevo en el portal para desarrolladores de administración de API Hola. Esto será una tooconfigure de operación utilizada de marcador de posición nuestro toobuild de directiva de composición nuestro recurso dinámico.

![Operación del panel](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a>Realizar solicitudes de Hola
Una vez Hola `dashboard` se ha creado la operación podemos configurar una directiva específicamente para esa operación. 

![Operación del panel](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

primer paso de Hello es tooextract los parámetros de consulta de solicitud entrante de hello, por lo que podemos reenviarlos tooour back-end. En este ejemplo, nuestro panel muestra información basada en un período de tiempo y, por tanto, tiene un parámetro `fromDate` y `toDate`. Podemos usar hello `set-variable` información de hello tooextract la directiva de dirección URL de solicitud de saludo.

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

Una vez que tenemos esta información podemos hacer que las solicitudes de sistemas de back-end de tooall Hola. Cada solicitud construye una nueva dirección URL con información de parámetros de Hola y llama a su servidor respectivo y almacena la respuesta de hello en una variable de contexto.

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

Estas solicitudes se ejecutarán en secuencia, que no es lo ideal. En una próxima versión presentaremos una directiva nueva llamada `wait` que permitirá a todos estos tooexecute solicitudes en paralelo.

### <a name="responding"></a>Respuesta
podemos usar Hola respuesta tooconstruct Hola compuesta [respuesta devuelto](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) directiva. Hola `set-body` elemento puede usar una expresión tooconstruct un nuevo `JObject` con todas las representaciones de componente de hello incrustadas como propiedades.

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

directiva completa Hello tiene el siguiente aspecto:

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

En la configuración de Hola de operación de marcador de posición de hello que podemos configurar Hola panel recurso toobe en caché durante al menos una hora como entendemos naturaleza Hola de datos de hello significa que incluso si es una hora desfasada seguirá estando lo suficientemente eficaces usuarios de toohello de tooconvey información valiosa.

## <a name="summary"></a>Resumen
Servicio de administración de API de Azure proporciona directivas flexibles que pueden ser de forma selectiva aplicarán tooHTTP tráfico y habilita la composición de servicios back-end. Si desea tooenhance la puerta de enlace de API con acciones, comprobación, capacidades de validación de la alerta o crear nuevos recursos compuestos en función de varios servicios de back-end, Hola `send-request` y directivas relacionadas abre todo un mundo de posibilidades.

## <a name="watch-a-video-overview-of-these-policies"></a>Ver un vídeo de información general de estas directivas
Para obtener más información sobre hello [envío una manera de solicitud](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [solicitud de envío](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), y [respuesta devuelto](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) las directivas que se describen en este artículo, consulte Hola después de vídeo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

