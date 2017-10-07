---
title: "directivas de transformación de administración de API aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de las directivas de transformación de hello disponibles para su uso en la administración de API de Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2891cc52d0017b717b3c12a98bc4941b5fd7ea78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-transformation-policies"></a>Directivas de transformación de API Management
En este tema se proporciona una referencia para hello las siguientes directivas de administración de API. Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="TransformationPolicies"></a> Directivas de transformación  
  
-   [Convertir JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) : convierte solicitar o cuerpo de la respuesta de JSON tooXML.  
  
-   [Convertir XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) : convierte solicitar o cuerpo de la respuesta de XML tooJSON.  
  
-   [Buscar y reemplazar la cadena en el cuerpo](api-management-transformation-policies.md#Findandreplacestringinbody) : encuentra una subcadena de solicitud o de respuesta y la reemplaza por una subcadena diferente.  
  
-   [Enmascarar direcciones URL en contenido](api-management-transformation-policies.md#MaskURLSContent) -reescribe (enmascara) vínculos en la respuesta de hello cuerpo para que apunten toohello vínculo equivalente a través de puerta de enlace de Hola.  
  
-   [Establecer el servicio back-end](api-management-transformation-policies.md#SetBackendService) -cambia el servicio back-end de Hola para una solicitud entrante.  
  
-   [Establecer cuerpo](api-management-transformation-policies.md#SetBody) -establece el cuerpo del mensaje de Hola para las solicitudes entrantes y salientes.  
  
-   [Definir el encabezado HTTP](api-management-transformation-policies.md#SetHTTPheader) : asigna una respuesta de valor tooan existente o un encabezado de solicitud o agrega un nuevo encabezado de respuesta y/o de solicitud.  
  
-   [Establecer el parámetro de cadena de consulta](api-management-transformation-policies.md#SetQueryStringParameter) : agrega, reemplaza el valor o elimina el parámetro de la cadena de consulta de la solicitud.  
  
-   [Reescribir dirección URL](api-management-transformation-policies.md#RewriteURL) -convierte una dirección URL de solicitud desde su formato de toohello de formato público esperado por el servicio web de Hola.  
  
-   [Transformar XML mediante una transformación XSLT](api-management-transformation-policies.md#XSLTransform) -se aplica un tooXML de transformación XSL en el cuerpo de solicitud o respuesta Hola.  
  
##  <a name="ConvertJSONtoXML"></a>Convertir JSON tooXML  
 Hola `json-to-xml` directiva convierte un cuerpo de solicitud o respuesta de JSON tooXML.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>Ejemplo  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|json-to-xml|Elemento raíz.|Sí|  
  
### <a name="attributes"></a>Atributos  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|apply|atributo de Hello debe establecerse tooone de hello después de valores.<br /><br /> -   always: indica que se debe aplicar la conversión siempre.<br />-   content-type-json: especifica que solo se debe realizar la conversión si el encabezado Content-Type indica la presencia de JSON.|Sí|N/D|  
|consider-accept-header|atributo de Hello debe establecerse tooone de hello después de valores.<br /><br /> -   true: especifica que se debe aplicar la conversión si se solicita JSON en el encabezado de aceptación (Accept) de la solicitud.<br />-   false: indica que se debe aplicar siempre la conversión.|No|true|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante, saliente y en caso de error  
  
-   **Ámbitos de la directiva:** global, producto, API y operación  
  
##  <a name="ConvertXMLtoJSON"></a>Convertir XML tooJSON  
 Hola `xml-to-json` directiva convierte un cuerpo de solicitud o respuesta de XML tooJSON. Esta directiva puede ser toomodernize usa las API basadas en servicios web de back-end solo XML.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>Ejemplo  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|xml-to-json|Elemento raíz.|Sí|  
  
### <a name="attributes"></a>Atributos  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|kind|atributo de Hello debe establecerse tooone de hello después de valores.<br /><br /> Hola-javascript friendly: convertir JSON tiene un a los desarrolladores de formularios tooJavaScript descriptivo.<br />-direct: hello JSON convertido refleja Hola original XML estructura de un documento.|Sí|N/D|  
|apply|atributo de Hello debe establecerse tooone de hello después de valores.<br /><br /> -   always: indica que se debe realizar la conversión siempre.<br />-   content-type-XML: especifica que solo se debe realizar la conversión si el encabezado Content-Type indica la presencia de XML.|Sí|N/D|  
|consider-accept-header|atributo de Hello debe establecerse tooone de hello después de valores.<br /><br /> -   true: especifica que se debe aplicar la conversión si se solicita XML en el encabezado de aceptación (Accept) de la solicitud.<br />-   false: indica que se debe aplicar siempre la conversión.|No|true|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante, saliente y en caso de error  
  
-   **Ámbitos de la directiva:** global, producto, API y operación  
  
##  <a name="Findandreplacestringinbody"></a> Buscar y reemplazar la cadena en el cuerpo  
 Hola `find-and-replace` directivas busca una subcadena de solicitud o respuesta y lo reemplaza por una subcadena distinta.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a>Ejemplo  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|find-and-replace|Elemento raíz.|Sí|  
  
### <a name="attributes"></a>Atributos  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|De|Hola toosearch de cadena para.|Sí|N/D|  
|to|cadena de reemplazo de Hola. Especificar una reemplazo cadena tooremove Hola Buscar cadena de longitud cero.|Sí|N/D|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante, saliente, back-end y en caso de error  
  
-   **Ámbitos de la directiva:** global, producto, API y operación  
  
##  <a name="MaskURLSContent"></a> Enmascarar URL en el contenido  
 Hola `redirect-content-urls` directiva reescribe (enmascara) vínculos en el cuerpo de la respuesta de Hola para que apunten toohello vínculo equivalente a través de puerta de enlace de Hola. Utilizarlos en hello sección saliente toore escritura respuesta cuerpo vínculos toomake toohello de punto de puerta de enlace. Uso de Hola entrantes sección para obtener el resultado opuesto.  
  
> [!NOTE]
>  Esta directiva no cambia los valores de los encabezados, como los `Location`. los valores de encabezado toochange, usar hello [encabezado del conjunto](api-management-transformation-policies.md#SetHTTPheader) directiva.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a>Ejemplo  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|redirect-content-urls|Elemento raíz.|Sí|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante y saliente  
  
-   **Ámbitos de la directiva:** global, producto, API y operación  
  
##  <a name="SetBackendService"></a> Establecer el servicio back-end  
 Hola de uso `set-backend-service` tooredirect una entrada de directiva de solicitud back-end diferente de tooa de Hola especificada en la configuración de hello API para esa operación. Esta directiva cambia Hola back-end base dirección URL del servicio de Hola entrantes solicitud toohello especificada en la directiva de Hola.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a>Ejemplo  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
En este Hola de ejemplo establecer la directiva de servicio de back-end enruta las solicitudes según el valor de la versión de Hola pasado Hola consulta cadena tooa diferentes servicio back-end que Hola Hola especificado en una API.
  
Hola inicialmente la dirección URL base del servicio se deriva de la configuración de la API de Hola de back-end. Hola por lo que la dirección URL de solicitud `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` se convierte en `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` donde `http://contoso.com/api/10.4/` es dirección URL de servicio de back-end Hola especificada en la configuración de hello API.  
  
Cuando Hola [< elija\> ](api-management-advanced-policies.md#choose) declaración de directiva se aplica URL base del servicio de back-end Hola puede cambiar de nuevo demasiado`http://contoso.com/api/8.2` o `http://contoso.com/api/9.1`, en función de valor Hola Hola versión solicitud del parámetro de consulta. Por ejemplo, si hello valor es `"2013-15"` se convierte en dirección URL de solicitud final hello `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.  
  
Si aún más la transformación de solicitud de hello es deseado, otros [directivas de transformación](api-management-transformation-policies.md#TransformationPolicies) puede utilizarse. Por ejemplo, tooremove Hola versión consulta enruta parámetro ahora que hello solicitud se está tooa versión específica back-end, hello [establecer el parámetro de cadena de consulta](api-management-transformation-policies.md#SetQueryStringParameter) directiva puede ser usado tooremove Hola ya es redundante version (atributo).  
  
### <a name="example"></a>Ejemplo  
  
```xml  
<policies>  
    <inbound>  
        <set-backend-service backend-id="my-sf-service" sf-partition-key="@(context.Request.Url.Query.GetValueOrDefault("userId","")" sf-replica-type="primary" /> 
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
En este ejemplo Hola directiva rutas Hola solicitud tooa service fabric back-end, mediante cadena de consulta de hello userId como clave de partición de Hola y Hola réplica principal de la partición de Hola.  

### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|set-backend-service|Elemento raíz.|Sí|  
  
### <a name="attributes"></a>Atributos  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|base-url|Nueva dirección URL base del servicio back-end.|No|N/D|  
|backend-id|Identificador de hello tooroute de back-end para.|No|N/D|  
|sf-partition-key|Solo se aplica cuando Hola back-end es un servicio de Service Fabric y se especifica mediante el 'Id. de back-end'. Usar una partición específica del servicio de resolución de nombres de hello tooresolve.|No|N/D|  
|sf-replica-type|Solo se aplica cuando Hola back-end es un servicio de Service Fabric y se especifica mediante el 'Id. de back-end'. Controla si la solicitud de hello debe ir toohello réplica principal o secundaria de una partición. |No|N/D|    
|sf-resolve-condition|Solo se aplica cuando Hola back-end es un servicio de Service Fabric. Identificación de condición si Hola llamar a back-end de tooService tejido tiene toobe repetirse con la resolución de nuevo.|No|N/D|    
|sf-service-instance-name|Solo se aplica cuando Hola back-end es un servicio de Service Fabric. Permite toochange instancias de servicio en tiempo de ejecución. |No|N/D|    

### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante y back-end  
  
-   **Ámbitos de la directiva:** global, producto, API y operación  
  
##  <a name="SetBody"></a> Establecer cuerpo  
 Hola de uso `set-body` cuerpo del mensaje Hola directiva tooset para las solicitudes entrantes y salientes. tooaccess Hola cuerpo del mensaje puede usar hello `context.Request.Body` propiedad o hello `context.Response.Body`, dependiendo de si es la directiva de Hola Hola sección entrante o saliente.  
  
> [!IMPORTANT]
>  Tenga en cuenta que, de forma predeterminada cuando se tiene acceso Hola cuerpo del mensaje utilizando `context.Request.Body` o `context.Response.Body`, mensaje de Hola original cuerpo se pierde y se debe establecer devolviendo el cuerpo de hello en expresión Hola. cuerpo de hello toopreserve contenido, establecer hello `preserveContent` parámetro demasiado`true` al tener acceso a mensajes de bienvenida. Si `preserveContent` se establece demasiado`true` y un cuerpo diferente se devuelve por expresión de hello, Hola devuelve cuerpo se utiliza.  
>   
>  Tenga en cuenta que hello las siguientes consideraciones cuando utilizando hello `set-body` directiva.  
>   
>  -   Si usas hello `set-body` tooreturn directiva un cuerpo nuevo o actualizado no es necesario tooset `preserveContent` demasiado`true` porque está proporcionando explícitamente el contenido del cuerpo de hello nueva.  
> -   Conservar contenido Hola de una respuesta en la canalización de entrada de hello no tiene sentido porque todavía no hay ninguna respuesta.  
> -   Conservar contenido Hola de una solicitud en la canalización de salida de hello no tiene sentido porque Hola ya se ha enviado solicitud toohello back-end en este momento.  
> -   Si esta directiva se usa cuando no hay ningún cuerpo de mensaje, por ejemplo, en un GET entrante, se producirá una excepción.  
  
 Para obtener más información, vea hello `context.Request.Body`, `context.Response.Body`, hello y `IMessage` secciones de hello [variable de contexto](api-management-policy-expressions.md#ContextVariables) tabla.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a>Ejemplos  
  
#### <a name="literal-text-example"></a>Ejemplo de texto literal  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a>Ejemplo de cuerpo de hello como una cadena de acceso. Tenga en cuenta que estamos conservando cuerpo de solicitud original de Hola para que podamos acceder a él más adelante en la canalización de Hola.
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a>Ejemplo de cuerpo de Hola como un JObject de acceso. Tenga en cuenta que, puesto que no nos estamos reservar Hola original cuerpo de la solicitud, el acceso a él más adelante en la canalización de hello dará como resultado una excepción.  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### <a name="filter-response-based-on-product"></a>Filtro de respuesta según un producto  
 Este ejemplo muestra cómo tooperform contenido filtrado mediante la eliminación de elementos de datos de respuesta de Hola recibido del servicio de back-end de hello cuando se usa hello `Starter` producto. Para ver una demostración de cómo configurar y usar esta directiva, consulte [177 episodio abarcan de nube: más características de administración de API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avancemos too34:30. Iniciar en 31:50 toosee una visión general de [Hola API de previsión de Sky oscuro](https://developer.forecast.io/) utilizada para esta demostración.  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  

### <a name="using-liquid-templates-with-set-body"></a>Uso de plantillas Liquid con la directiva de establecer cuerpo 
Hola `set-body` directiva puede ser configurado toouse hello [líquido](https://shopify.github.io/liquid/basics/introduction/) plantillas tootransfom Hola cuerpo de lenguaje una solicitud o respuesta. Esto puede ser muy eficaces si necesita toocompletely remodelación Hola formato del mensaje.

> [!IMPORTANT]
> Hola implementación de líquido utilizado en hello `set-body` directiva está configurada en "modo de C#". Esto es especialmente importante al realizar tareas como el filtrado. Por ejemplo, mediante un filtro de fecha requiere el uso de Hola de Pascal de mayúsculas y minúsculas y C# fecha formato p. ej.:
>
> {{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}

> [!IMPORTANT]
> En orden toocorrectly enlace tooan XML cuerpo mediante plantilla líquido hello, use un `set-header` directiva tooset Content-Type tooeither aplicación/xml, texto/xml (o cualquier tipo que termine con + xml); para un cuerpo JSON, debe ser application/json, texto/json (o el final de cualquier tipo con + json).

#### <a name="convert-json-toosoap-using-a-liquid-template"></a>Convertir tooSOAP JSON utilizando una plantilla líquida
```xml
<set-body template="liquid">
    <soap:Envelope xmlns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <GetOpenOrders>
                <cust>{{body.getOpenOrders.cust}}</cust>
            </GetOpenOrders>
        </soap:Body>
    </soap:Envelope>
</set-body>
```

#### <a name="tranform-json-using-a-liquid-template"></a>Transformación de JSON mediante una plantilla Liquid
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|set-body|Elemento raíz. Contiene el texto del cuerpo de Hola o una expresión que devuelve un cuerpo.|Sí|  

### <a name="properties"></a>Propiedades  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|template|Se ejecutará modo de creación de plantillas de Hola toochange usado que Hola establecer la directiva de cuerpo. Actualmente, el valor de hello solo admitido es:<br /><br />Hola - líquido - establecer la directiva de cuerpo utilizará el motor de plantillas líquido Hola |No|Liquid|  

Para tener acceso a información sobre la solicitud de Hola y respuesta, plantilla líquido Hola puede enlazar el objeto de contexto de tooa con hello propiedades siguientes: <br />
<pre>context.
    Request.
        Url
        Method
        OriginalMethod
        OriginalUrl
        IpAddress
        MatchedParameters
        HasBody
        ClientCertificates
        Headers

    Response.
        StatusCode
        Method
        Headers
Url.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString

OriginalUrl.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString
</pre>



### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante, saliente y back-end  
  
-   **Ámbitos de la directiva:** global, producto, API y operación  
  
##  <a name="SetHTTPheader"></a> Establecer encabezado HTTP  
 Hola `set-header` directiva asigna una respuesta de valor tooan existente o un encabezado de solicitud o agrega un nuevo encabezado de respuesta y/o de solicitud.  
  
 Inserta una lista de encabezados HTTP en un mensaje HTTP. Cuando se coloca en una canalización de entrada, esta directiva establece los encabezados HTTP de Hola para solicitud de Hola que se pasa toohello servicio de destino. Cuando se coloca en una canalización saliente, esta directiva establece los encabezados HTTP de hello para la respuesta de Hola que se envió el cliente de la puerta de enlace de toohello.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a>Ejemplos  
  
#### <a name="example"></a>Ejemplo  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>Reenviar el servicio de back-end de toohello de información de contexto  
 Este ejemplo muestra cómo Directiva tooapply en hello API de nivel de servicio de back-end de toohello de información de contexto de toosupply. Para ver una demostración de cómo configurar y usar esta directiva, consulte [177 episodio abarcan de nube: más características de administración de API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avancemos too10:30. No hay una demostración de llamar a una operación de portal para desarrolladores de Hola donde puede ver la directiva de hello en el trabajo a las 12:10.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 Para obtener más información, consulte [Policy expressions](api-management-policy-expressions.md) (Expresiones de política) y [Context variable](api-management-policy-expressions.md#ContextVariables) (Variable de contexto).  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|set-header|Elemento raíz.|Sí|  
|value|Especifica el valor de Hola de hello encabezado toobe conjunto. Para varios encabezados con hello homónimas agregar más `value` elementos.|Sí|  
  
### <a name="properties"></a>Propiedades  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|exists-action|Especifica qué tootake acción cuando ya se ha especificado el encabezado de Hola. Este atributo debe tener uno de hello después de valores.<br /><br /> -invalidar - reemplaza Hola valor del encabezado existente Hola.<br />-skip: no reemplaza el valor del encabezado de hello existente.<br />-append: anexa el valor del encabezado existente Hola valor toohello.<br />-delete: quita el encabezado de saludo de solicitud de Hola.<br /><br /> Cuando se establece demasiado`override` al enumerar varias entradas con hello igual nombre resultados en el encabezado de Hola que se va a entradas correspondiente del conjunto tooall (que aparecerán enumeradas varias veces); solo los valores mostrados se establecerá en el resultado de hello.|No|override|  
|name|Especifica el nombre del conjunto de toobe de encabezado de Hola.|Sí|N/D|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante, saliente, back-end y en caso de error  
  
-   **Ámbitos de la directiva:** global, producto, API y operación  
  
##  <a name="SetQueryStringParameter"></a> Establecimiento del parámetro de cadena de consulta  
 Hola `set-query-parameter` directiva agrega, reemplaza el valor de, o parámetro de cadena de consulta de solicitud de eliminaciones. Puede ser toopass usa parámetros de consulta esperados por el servicio de back-end de Hola que son opcionales o no están nunca presenten en la solicitud de saludo.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a>Ejemplos  
  
#### <a name="example"></a>Ejemplo  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>Reenviar el servicio de back-end de toohello de información de contexto  
 Este ejemplo muestra cómo Directiva tooapply en hello API de nivel de servicio de back-end de toohello de información de contexto de toosupply. Para ver una demostración de cómo configurar y usar esta directiva, consulte [177 episodio abarcan de nube: más características de administración de API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avancemos too10:30. No hay una demostración de llamar a una operación de portal para desarrolladores de Hola donde puede ver la directiva de hello en el trabajo a las 12:10.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 Para obtener más información, consulte [Policy expressions](api-management-policy-expressions.md) (Expresiones de política) y [Context variable](api-management-policy-expressions.md#ContextVariables) (Variable de contexto).  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|set-query-parameter|Elemento raíz.|Sí|  
|value|Especifica el valor de Hola Hola parámetro toobe del conjunto de consulta. Varios parámetros de consulta con hello homónimas agregar más `value` elementos.|Sí|  
  
### <a name="properties"></a>Propiedades  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|exists-action|Especifica qué tootake acción cuando ya se ha especificado el parámetro de consulta de Hola. Este atributo debe tener uno de hello después de valores.<br /><br /> -invalidar - reemplaza Hola valor de parámetro de hello existente.<br />-skip: no reemplaza el valor del parámetro de consulta existente de Hola.<br />-Anexar - anexa Hola valor toohello parámetro valor de consulta existente.<br />-delete: quita el parámetro de consulta de Hola de solicitud de Hola.<br /><br /> Cuando se establece demasiado`override` al enumerar varias entradas con hello igual nombre resultados en el parámetro de consulta de Hola que se va a entradas correspondiente del conjunto tooall (que aparecerán enumeradas varias veces); solo los valores mostrados se establecerá en el resultado de hello.|No|override|  
|name|Especifica el nombre del conjunto de toobe de parámetros de consulta de Hola.|Sí|N/D|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante y back-end  
  
-   **Ámbitos de la directiva:** global, producto, API y operación  
  
##  <a name="RewriteURL"></a> URL de reescritura  
 Hola `rewrite-uri` directiva convierte una dirección URL de solicitud desde su formato de toohello de formato público esperado por el servicio web de hello, como se muestra en el siguiente ejemplo de Hola.  
  
-   URL pública: `http://api.example.com/storenumber/ordernumber`  
  
-   URL de solicitud: `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`  
  
 Esta directiva puede usarse cuando una dirección URL humana y/o compatible con el explorador debería transformarse en formato de dirección URL de hello esperado por el servicio web de Hola. Esta directiva solo debe toobe aplicado al exponer un formato de dirección URL alternativo, como direcciones URL limpias, direcciones URL RESTful, direcciones URL descriptivas o direcciones URL descriptivas del SEO que son direcciones URL puramente estructurales que no contienen una cadena de consulta y en su lugar contienen sólo ruta de acceso de Hola de Hola recurso (después de esquema de Hola y la autoridad de hello). Este procedimiento se realiza con fines estéticos, de usabilidad o de optimización del motor de búsqueda (SEO).  
  
> [!NOTE]
>  Solo puede agregar parámetros de cadena de consulta mediante la directiva de Hola. No se puede agregar parámetros de ruta de acceso de plantilla adicionales en hello reescribir dirección URL.  

### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a>Ejemplo  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|rewrite-uri|Elemento raíz.|Sí|  
  
### <a name="attributes"></a>Attributes  
  
|Atributo|Descripción|Obligatorio|Valor predeterminado|  
|---------------|-----------------|--------------|-------------|  
|template|Hola web real dirección URL del servicio con los parámetros de cadena de consulta. Cuando se usan expresiones, el valor completo de hello debe ser una expresión.|Sí|N/D|  
|copy-unmatched-params|Especifica si los parámetros de consulta en la solicitud entrante de hello no está presente en la plantilla de dirección URL original de Hola se agregan plantilla volver a escribir la dirección URL de toohello definido por hello|No|true|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante  
  
-   **Ámbitos de la directiva:** producto, API y operación  
  
##  <a name="XSLTransform"></a> Transformar XML mediante una XSLT  
 Hola `Transform XML using an XSLT` un tooXML de transformación XSL en el cuerpo de solicitud o respuesta Hola aplica la directiva.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
        <xsl:output method="xml" indent="yes" />  
        <xsl:param name="User-Agent" />  
        <xsl:template match="* | @* | node()">  
            <xsl:copy>  
                <xsl:if test="self::* and not(parent::*)">  
                    <xsl:attribute name="User-Agent">  
                        <xsl:value-of select="$User-Agent" />  
                    </xsl:attribute>  
                </xsl:if>  
                <xsl:apply-templates select="* | @* | node()" />  
            </xsl:copy>  
        </xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### <a name="example"></a>Ejemplo  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
        <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
            <xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
            <!-- Copy all nodes directly-->  
            <xsl:template match="node()| @*|*">  
                <xsl:copy>  
                    <xsl:apply-templates select="@* | node()|*" />  
                </xsl:copy>  
            </xsl:template>  
        </xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|xsl-transform|Elemento raíz.|Sí|  
|Parámetro|Variables de toodefine usado utilizadas en transformación Hola|No|  
|xsl:stylesheet|Elemento raíz de la hoja de estilo. Todos los elementos y atributos definidos dentro de cumplen el estándar de hello [especificación XSLT](http://www.w3.org/TR/xslt)|Sí|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante y saliente  
  
-   **Ámbitos de la directiva:** global, producto, API y operación  
  
## <a name="next-steps"></a>Pasos siguientes
Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).  
