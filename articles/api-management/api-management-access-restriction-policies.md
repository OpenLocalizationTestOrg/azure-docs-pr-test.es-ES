---
title: "directivas de restricción de acceso de administración de API aaaAzure | Documentos de Microsoft"
description: "Obtenga información sobre directivas de restricción de acceso de hello disponibles para su uso en la administración de API de Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a>Directivas de restricción de acceso de API Management
En este tema se proporciona una referencia para hello las siguientes directivas de administración de API. Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AccessRestrictionPolicies"></a> Directivas de restricción de acceso  
  
-   [Activar encabezado HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) : aplica la existencia o el valor de un encabezado HTTP.  
  
-   [Limitar la frecuencia de llamadas por suscripción](api-management-access-restriction-policies.md#LimitCallRate) : evita los picos de uso de la API limitando la frecuencia de llamadas, por suscripción.  
  
-   [Limitar la frecuencia de llamadas por clave](#LimitCallRateByKey) : evita los picos de uso de la API limitando la frecuencia de llamadas, por clave.  
  
-   [Restringir IP de autor de llamada](api-management-access-restriction-policies.md#RestrictCallerIPs) : filtra (permite/deniega) las llamadas de direcciones IP específicas o de intervalos de direcciones.  
  
-   [Establecer la cuota de uso por suscripción](api-management-access-restriction-policies.md#SetUsageQuota) -permite tooenforce un llamadas renovable o duración volumen o ancho de banda de cuota, por suscripción.  
  
-   [Establecer la cuota de uso clave](#SetUsageQuotaByKey) -permite tooenforce un llamadas renovable o duración volumen o ancho de banda de cuota, de forma por clave.  
  
-   [Validar JWT](api-management-access-restriction-policies.md#ValidateJWT) : aplica la existencia y la validez de un JWT extraído de un encabezado HTTP especificado o un parámetro de consulta especificado.  
  
##  <a name="CheckHTTPHeader"></a> Activar encabezado HTTP  
 Hola de uso `check-header` tooenforce de directiva que una solicitud tiene un encabezado HTTP especificado. Si lo desea, puede comprobar toosee si el encabezado de hello tiene un valor específico o ver un intervalo de valores permitidos. Si se produce un error en la comprobación de hello, directiva de hello finaliza el procesamiento de la solicitud y devuelve Hola código y error de mensaje de estado HTTP especificado por la directiva de Hola.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a>Ejemplo  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|check-header|Elemento raíz.|Sí|  
|value|Valor del encabezado HTTP permitido. Cuando se especifican varios elementos de valor, verificación de Hola se considera correcta si cualquiera de los valores de hello es una coincidencia.|No|  
  
### <a name="attributes"></a>Attributes  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|failed-check-error-message|Tooreturn de mensaje de error en el cuerpo de la respuesta de hello HTTP si el encabezado de hello no existe o tiene un valor no válido. Los caracteres especiales de este mensaje deben incluir los caracteres de escape correctos.|Sí|N/D|  
|failed-check-httpcode|Tooreturn de código de estado HTTP, si el encabezado de hello no existe o tiene un valor no válido.|Sí|N/D|  
|header-name|nombre de Hola de hello toocheck de encabezado HTTP.|Sí|N/D|  
|ignore-case|Se puede establecer tooTrue o False. Si set tooTrue caso se omite cuando el valor del encabezado de Hola se compara con el conjunto de Hola de valores aceptables.|Sí|N/D|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante y saliente  
  
-   **Ámbitos de la directiva:** global, producto, API y operación  
  
##  <a name="LimitCallRate"></a> Limitar la tasa de llamadas por suscripción  
 Hola `rate-limit` directiva impide el uso de la API picos según una suscripción por limitando Hola llamar tooa velocidad especificado número por un período de tiempo especificado. Cuando se activa esta directiva llamador Hola recibe un `429 Too Many Requests` código de estado de respuesta.  
  
> [!IMPORTANT]
>  Esta directiva se puede usar una sola vez por documento de directiva.  
>   
>  [Las expresiones de directiva](api-management-policy-expressions.md) no se puede usar en cualquiera de los atributos de directiva de Hola para esta directiva.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a>Ejemplo  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|set-limit|Elemento raíz.|Sí|  
|api|Agregar uno o varios de estos tooimpose elementos un límite de tasa de llamadas en API dentro del producto de Hola. Los límites de tasa de llamadas a la API y al producto se aplican de forma independiente.|No|  
|operación|Agregue uno o varios de estos tooimpose elementos un límite de tasa de llamadas en operaciones dentro una API. Los límites de tasa de llamadas se aplican de forma independiente a la API, a la operación y al producto.|No|  
  
### <a name="attributes"></a>Attributes  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|name|nombre de Hola de hello API para cuyo límite de velocidad de tooapply Hola.|Sí|N/D|  
|calls|Hola número total máximo de llamadas permitidas durante el intervalo de tiempo de hello especificado en hello `renewal-period`.|Sí|N/D|  
|renewal-period|Hola período de tiempo en segundos tras el cual hello cuota se restablece.|Sí|N/D|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante  
  
-   **Ámbitos de la directiva:** producto  
  
##  <a name="LimitCallRateByKey"></a> Limitar la tasa de llamadas por clave  
 Hola `rate-limit-by-key` directiva impide el uso de la API picos según una clave por limitando Hola llamar tooa velocidad especificado número por un período de tiempo especificado. clave de Hello puede tener un valor de cadena arbitraria y se proporciona normalmente mediante una expresión de directiva. Se pueden agregar condición de incremento opcional toospecify qué solicitudes se deben contar hacia el límite de Hola. Cuando se activa esta directiva llamador Hola recibe un `429 Too Many Requests` código de estado de respuesta.  
  
 Para obtener más información y ver ejemplos de esta directiva, consulte [Limitación avanzada de solicitudes con Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).  
  
> [!IMPORTANT]
>  Esta directiva se puede usar una sola vez por documento de directiva.  
  
### <a name="policy-statement"></a>Declaración de la directiva  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a>Ejemplo  
 En el siguiente ejemplo de Hola, el límite de velocidad de hello es ordenado por dirección IP de hello llamador.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|set-limit|Elemento raíz.|Sí|  
  
### <a name="attributes"></a>Atributos  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|calls|Hola número total máximo de llamadas permitidas durante el intervalo de tiempo de hello especificado en hello `renewal-period`.|Sí|N/D|  
|counter-key|Hola toouse clave de directiva de límite de velocidad de Hola.|Sí|N/D|  
|increment-condition|expresión booleana que Hola especifica si se debe contar solicitud Hola hacia la cuota de hello (`true`).|No|N/D|  
|renewal-period|Hola período de tiempo en segundos tras el cual hello cuota se restablece.|Sí|N/D|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante  
  
-   **Ámbitos de la directiva:** global, producto, API y operación  
  
##  <a name="RestrictCallerIPs"></a> Restringir IP de autor de llamada  
 Hola `ip-filter` directiva filtra (permite o deniega) llamadas de determinadas direcciones IP y/o intervalos de direcciones.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a>Ejemplo  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|ip-filter|Elemento raíz.|Sí|  
|address|Especifica una única dirección IP en qué toofilter.|Es necesario al menos un elemento `address` o `address-range`.|  
|address-range from="address" to="address"|Especifica un intervalo de direcciones IP en qué toofilter.|Es necesario al menos un elemento `address` o `address-range`.|  
  
### <a name="attributes"></a>Attributes  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|address-range from="address" to="address"|Un intervalo de IP direcciones tooallow o denegar el acceso.|Se requiere si hello `address-range` elemento se utiliza.|N/D|  
|ip-filter action="allow &#124; forbid"|Especifica si las llamadas deben permitirse o no para hello especifica intervalos y direcciones IP.|Sí|N/D|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante  
  
-   **Ámbitos de la directiva:** global, producto, API y operación  
  
##  <a name="SetUsageQuota"></a> Establecer cuota de uso por suscripción  
 Hola `quota` la directiva exige un llamadas renovable o duración volumen o ancho de banda de cuota, por suscripción.  
  
> [!IMPORTANT]
>  Esta directiva se puede usar una sola vez por documento de directiva.  
>   
>  [Las expresiones de directiva](api-management-policy-expressions.md) no se puede usar en cualquiera de los atributos de directiva de Hola para esta directiva.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a>Ejemplo  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|quota|Elemento raíz.|Sí|  
|api|Agregar uno o varios de estos tooimpose elementos una cuota en API dentro del producto de Hola. Las cuotas de API y de producto se aplican de forma independiente.|No|  
|operación|Agregue uno o varios de estos tooimpose elementos una cuota en operaciones dentro una API. Las cuotas de API, operación y producto se aplican de forma independiente.|No|  
  
### <a name="attributes"></a>Attributes  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|name|nombre de Hola de API de Hola o la operación para qué hello cuota se aplica.|Sí|N/D|  
|bandwidth|Hola número total máximo de kilobytes permitidos durante el intervalo de tiempo de hello especificado en hello `renewal-period`.|Debe especificarse `calls`, `bandwidth` o ambos.|N/D|  
|calls|Hola número total máximo de llamadas permitidas durante el intervalo de tiempo de hello especificado en hello `renewal-period`.|Debe especificarse `calls`, `bandwidth` o ambos.|N/D|  
|renewal-period|Hola período de tiempo en segundos tras el cual hello cuota se restablece.|Sí|N/D|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante  
  
-   **Ámbitos de la directiva:** producto  
  
##  <a name="SetUsageQuotaByKey"></a>Establecer cuota de uso por clave  
 Hola `quota-by-key` la directiva exige un llamadas renovable o duración volumen o ancho de banda de cuota, según una por cada clave. clave de Hello puede tener un valor de cadena arbitraria y se proporciona normalmente mediante una expresión de directiva. Se pueden agregar condición de incremento opcional toospecify qué solicitudes se deben contar hacia la cuota de Hola.  
  
 Para obtener más información y ver ejemplos de esta directiva, consulte [Limitación avanzada de solicitudes con Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).  
  
> [!IMPORTANT]
>  Esta directiva se puede usar una sola vez por documento de directiva.  
>   
>  [Las expresiones de directiva](api-management-policy-expressions.md) no se puede usar en cualquiera de los atributos de directiva de Hola para esta directiva.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a>Ejemplo  
 En el siguiente ejemplo de Hola, cuota de hello es ordenado por dirección IP de hello llamador.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|quota|Elemento raíz.|Sí|  
  
### <a name="attributes"></a>Atributos  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|bandwidth|Hola número total máximo de kilobytes permitidos durante el intervalo de tiempo de hello especificado en hello `renewal-period`.|Debe especificarse `calls`, `bandwidth` o ambos.|N/D|  
|calls|Hola número total máximo de llamadas permitidas durante el intervalo de tiempo de hello especificado en hello `renewal-period`.|Debe especificarse `calls`, `bandwidth` o ambos.|N/D|  
|counter-key|Hola toouse clave para la directiva de cuota de Hola.|Sí|N/D|  
|increment-condition|expresión booleana que Hola especifica si se debe contar solicitud Hola hacia la cuota de hello (`true`)|No|N/D|  
|renewal-period|Hola período de tiempo en segundos tras el cual hello cuota se restablece.|Sí|N/D|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante  
  
-   **Ámbitos de la directiva:** global, producto, API y operación  
  
##  <a name="ValidateJWT"></a> Validación de JWT  
 Hola `validate-jwt` directiva aplica la existencia y validez de un JWT extraído de un determinado encabezado HTTP o un parámetro de consulta especificado.  
  
> [!IMPORTANT]
>  Hola `validate-jwt` directiva requiere que hello `exp` notificación registrado es incluidos en el token de JWT de hello, a menos que `require-expiration-time` atributo se especifica y se establece demasiado`false`.  
> Hola `validate-jwt` directiva es compatible con HS256 y RS256 los algoritmos de firma. Para HS256 clave Hola debe proporcionarse en línea dentro de la directiva de hello en formato codificado en base64 de Hola. Para RS256 clave hello tiene toobe proporcionan a través de un punto de conexión de configuración Openid.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a>Ejemplos  
  
#### <a name="azure-mobile-services-token-validation"></a>Validación de tokens de Azure Mobile Services  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a>Validación de tokens de Azure Active Directory  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a>Validación de tokens de Azure Active Directory B2C  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a>Autorizar toooperations de acceso basado en notificaciones de tokens  
 Este ejemplo se muestra cómo hello toouse [validar JWT](api-management-access-restriction-policies.md#ValidateJWT) toopre directiva-autorizar toooperations de acceso basado en notificaciones de token. Para ver una demostración de cómo configurar y usar esta directiva, consulte [177 episodio abarcan de nube: más características de administración de API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avancemos too13:50. Avance rápido too15:00 las directivas de hello toosee configuradas en el editor de directiva de hello y, a continuación, too18:50 para ver una demostración de la llamada a una operación de portal para desarrolladores de hello con y sin Hola necesario token de autorización.  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descripción|Obligatorio|  
|-------------|-----------------|--------------|  
|validate-jwt|Elemento raíz.|Sí|  
|audiences|Contiene una lista de notificaciones de audiencia aceptables que pueden estar presentes en el símbolo (token) de Hola. Si existen varios valores de audiencia, se prueban los valores uno a uno hasta que se agoten todos (en cuyo caso no se superará la validación) o hasta que se obtenga un resultado positivo con alguno. Debe especificarse al menos una audiencia.|No|  
|issuer-signing-keys|Una lista de toovalidate de claves que se utilizan con codificación Base64 de seguridad firmado símbolos (tokens). Si existen varias claves de seguridad, se prueban las claves una a una hasta que se agoten todas (en cuyo caso no se superará la validación) o hasta que una sea correcta (lo que es útil para la sustitución de tokens). Elementos claves tienen una función opcional `id` toomatch de atributo que se utiliza con `kid` de notificación.|No|  
|issuers|Una lista de entidades de seguridad aceptables que emitió el token de Hola. Si existen varios valores de emisor, se prueban los valores uno a uno hasta que se agoten todos (en cuyo caso no se superará la validación) o hasta que se obtenga un resultado positivo con alguno.|No|  
|openid-config|elemento de Hello utilizado para especificar un extremo de configuración Openid compatible desde el que se puede obtener las claves y el emisor de la firma.|No|  
|required-claims|Contiene una lista de notificaciones que se espera toobe presente en el token de Hola para que lo toobe considere válido. Cuando Hola `match` atributo está establecido demasiado`all` cada valor de notificación en la directiva de hello debe estar presente en el token de Hola para toosucceed de validación. Cuando Hola `match` atributo está establecido demasiado`any` al menos una notificación debe estar presente en el token de Hola para toosucceed de validación.|No|  
|zumo-master-key|Clave maestra para los tokens que emite Azure Mobile Services.|No|  
  
### <a name="attributes"></a>Attributes  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|clock-skew|Intervalo de tiempo. Proporciona cierto margen de tiempo en caso de notificación de expiración del token de hello está presente en el token de Hola y está más allá de hello actual fecha / hora.|No|0 segundos|  
|failed-validation-error-message|Tooreturn de mensaje de error en el cuerpo de la respuesta HTTP Hola si hello JWT no pasa la validación. Los caracteres especiales de este mensaje deben incluir los caracteres de escape correctos.|No|El mensaje de error predeterminado depende del problema de validación, por ejemplo, la notificación de la ausencia del elemento JWT.|  
|failed-validation-httpcode|Tooreturn de código de estado HTTP si hello JWT no pasa la validación.|No|401|  
|header-name|nombre de Hello del encabezado de hello HTTP que contiene el token de Hola.|Se debe especificar `header-name` o `query-paremeter-name`, pero no ambos.|N/D|  
|id|Hola `id` atributo hello `key` elemento le permite la cadena de hello toospecify que se comparará con `kid` toofind token (si existe) de hello out hello toouse de clave adecuado para la validación de firma de notificación.|No|N/D|  
|match|Hola `match` atributo hello `claim` elemento especifica si cada valor de notificación en la directiva de hello debe estar presente en el token de Hola para toosucceed de validación. Los valores posibles son:<br /><br /> -                          `all`-cada valor de notificación en la directiva de hello debe estar presente en el token de Hola para toosucceed de validación.<br /><br /> -                          `any`-valor de al menos una notificación debe estar presente en el token de Hola para toosucceed de validación.|No|todas|  
|query-paremeter-name|nombre de Hola Hola Hola del parámetro de consulta que contiene el token de Hola.|Se debe especificar `header-name` o `query-paremeter-name`, pero no ambos.|N/D|  
|require-expiration-time|Booleano. Especifica si se requiere una notificación de expiración en el token de Hola.|No|true|
|require-scheme|Hola nombre del esquema de token de hello, p. ej. "Bearer". Cuando se establece este atributo, directiva de Hola se asegurará de que especifica el esquema está presente en el valor del encabezado de autorización de Hola.|No|N/D|
|require-signed-tokens|Booleano. Especifica si un token es necesario toobe firmado.|No|true|  
|url|Dirección URL de punto de conexión de configuración de OpenID desde donde se pueden obtener los metadatos de configuración de OpenID. Para Azure Active Directory usar hello después de la dirección URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` sustituyendo el nombre del inquilino de directorio, por ejemplo, `contoso.onmicrosoft.com`.|Sí|N/D|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante  
  
-   **Ámbitos de la directiva:** global, producto, API y operación  
  
## <a name="next-steps"></a>Pasos siguientes
Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).  
