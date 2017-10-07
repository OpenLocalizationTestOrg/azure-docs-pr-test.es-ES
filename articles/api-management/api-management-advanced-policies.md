---
title: "aaaAzure directivas avanzadas de administración de API | Documentos de Microsoft"
description: "Obtenga información acerca de hello avanzada de directivas disponibles para su uso en la administración de API de Azure."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 8a13348b-7856-428f-8e35-9e4273d94323
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8245e7a4c9d432b7b4d362192e357829fcabad55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-advanced-policies"></a>Directivas avanzadas de API Management
En este tema se proporciona una referencia para hello las siguientes directivas de administración de API. Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AdvancedPolicies"></a> Directivas avanzadas  
  
-   [Flujo de control](api-management-advanced-policies.md#choose) - condicionalmente aplica las instrucciones de directiva en función de los resultados de Hola de evaluación de Hola de tipo Boolean [expresiones](api-management-policy-expressions.md).  
  
-   [Reenviar la solicitud](#ForwardRequest) -reenvía el servicio back-end de hello solicitud toohello.

-   [Limitar la simultaneidad](#LimitConcurrency) -evita entre las directivas de ejecución más Hola cantidad especificada de solicitudes a la vez.
  
-   [Inicie sesión tooEvent concentrador](#log-to-eventhub) -envía los mensajes de Hola especificado tooan formato concentrador de eventos definido por una entidad de registrador. 

-   [Simular respuesta](#mock-response) -ejecución de canalización de anulaciones y devuelve una respuesta simulada directamente toohello autor de la llamada.
  
-   [Vuelva a intentar](#Retry) -ejecución de reintentos de hello entre las instrucciones de directiva, si y hasta que se cumpla la condición de Hola. Ejecución se repetirá en intervalos de tiempo especificados de Hola y seguridad toohello especificada el número de reintentos.  
  
-   [Devolver la respuesta](#ReturnResponse) -Hola de ejecución y devuelve de la canalización de anulaciones especificado respuesta directamente toohello autor de la llamada. 
  
-   [Enviar solicitud unidireccionales](#SendOneWayRequest) -envía una solicitud toohello especificó la dirección URL sin tener que esperar una respuesta.  
  
-   [Enviar solicitud](#SendRequest) -envía una solicitud toohello URL especificada.  

-   [Establecer el proxy HTTP](#SetHttpProxy) -permite tooroute reenviar solicitudes a través de un proxy HTTP.  

-   [Establecer el método de solicitud](#SetRequestMethod) -permite toochange método de hello HTTP para una solicitud.  
  
-   [Código de estado del conjunto de](#SetStatus) -toohello de código de estado HTTP de Hola de cambios de valor especificado.  
  
-   [Establecimiento de variable](api-management-advanced-policies.md#set-variable): conserva un valor en una variable [context](api-management-policy-expressions.md#ContextVariables) con nombre para su posterior acceso.  

-   [Seguimiento](#Trace) -agrega una cadena en hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) salida.  
  
-   [Espere](#Wait) -espera entre [solicitud de envío](api-management-advanced-policies.md#SendRequest), [obtener el valor de caché](api-management-caching-policies.md#GetFromCacheByKey), o [flujo de Control](api-management-advanced-policies.md#choose) toocomplete directivas antes de continuar.  
  
##  <a name="choose"></a> Flujo de control  
 Hola `choose` directiva aplica a instrucciones en función de resultado de hello de la evaluación de expresiones booleanas, similar tooan if-then-else o un conmutador que se construyen en un lenguaje de programación de directiva adjuntas.  
  
###  <a name="ChoosePolicyStatement"></a> Declaración de la directiva  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements toobe applied if none of hello above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 Hello directiva de flujo de control debe contener al menos un `<when/>` elemento. Hola `<otherwise/>` elemento es opcional. Las condiciones en `<when/>` elementos se evalúan en orden de aparición dentro de la directiva de Hola. Directivas adjuntas en hello primero `<when/>` elemento con el atributo de condición es igual a `true` se aplicarán. Directivas delimitadas hello `<otherwise/>` elemento, si está presente, se aplicará si todas las de hello `<when/>` los atributos de condición de elemento son `false`.  
  
### <a name="examples"></a>Ejemplos  
  
####  <a name="ChooseExample"></a> Ejemplo  
 Hello en el ejemplo siguiente se muestra cómo un [set-variable](api-management-advanced-policies.md#set-variable) directiva y dos directivas de flujo de control.  
  
 Hola establecer la variable directiva está en Hola sección de entrada y crea un `isMobile` booleano [contexto](api-management-policy-expressions.md#ContextVariables) variable que se establece tootrue si hello `User-Agent` solicitud encabezado contiene texto hello `iPad` o `iPhone`.  
  
 Hola primera directiva de flujo de control también está en Hola sección de entrada y aplica condicionalmente uno de dos [establecer el parámetro de cadena de consulta](api-management-transformation-policies.md#SetQueryStringParameter) directivas según valor Hola de hello `isMobile` variable de contexto.  
  
 segunda directiva de flujo de control Hello en la sección de salida de hello y aplica condicionalmente hello [convertir XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) directiva cuando `isMobile` se establece demasiado`true`.  
  
```xml  
<policies>  
    <inbound>  
        <set-variable name="isMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
        <base />  
        <choose>  
            <when condition="@(context.Variables.GetValueOrDefault<bool>("isMobile"))">  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>true</value>  
                </set-query-parameter>  
            </when>  
            <otherwise>  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>false</value>  
                </set-query-parameter>  
            </otherwise>  
        </choose>  
    </inbound>  
    <outbound>  
        <base />  
        <choose>  
            <when condition="@(context.GetValueOrDefault<bool>("isMobile"))">  
                <xml-to-json kind="direct" apply="always" consider-accept-header="false"/>  
            </when>  
        </choose>  
    </outbound>  
</policies>  
```  
  
#### <a name="example"></a>Ejemplo  
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
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descripción|Obligatorio|  
|-------------|-----------------|--------------|  
|choose|Elemento raíz.|Sí|  
|when|Hola toouse de condición para hello `if` o `ifelse` partes de hello `choose` directiva. Si hello `choose` directiva tenga varias `when` secciones, se evalúan de forma secuencial. Una vez Hola `condition` de cuando el elemento se evalúa demasiado`true`, ningún otro `when` se evalúan las condiciones.|Sí|  
|otherwise|Contiene toobe de fragmento de código de directiva de Hola utilizado si ninguna de hello `when` condiciones se evalúan demasiado`true`.|No|  
  
### <a name="attributes"></a>Attributes  
  
|Atributo|Descripción|Obligatorio|  
|---------------|-----------------|--------------|  
|condition="Constante booleana &#124; Constante booleana"|expresión booleana de Hola o constante tooevaluated cuando Hola que contiene `when` se evalúa la instrucción de directiva.|Sí|  
  
###  <a name="ChooseUsage"></a> Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante, saliente, back-end y en caso de error  
  
-   **Ámbitos de la directiva:** todos los ámbitos  
  
##  <a name="ForwardRequest"></a> Reenvío de solicitud  
 Hola `forward-request` directiva reenvía Hola entrantes solicitud toohello servicio back-end especificado en la solicitud de hello [contexto](api-management-policy-expressions.md#ContextVariables). dirección URL del servicio back-end Hello se especifica una API de Hola [configuración](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) y se puede cambiar mediante hello [establecer el servicio back-end](api-management-transformation-policies.md) directiva.  
  
> [!NOTE]
>  Quitar este resultados de directivas de solicitud de hello no se reenvían las directivas de hello y servicio del back-end de toohello en la sección de salida de hello se evalúan inmediatamente tras la finalización correcta de Hola de directivas de Hola Hola sección de entrada.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a>Ejemplos  
  
#### <a name="example"></a>Ejemplo  
 Hello siguientes directivas de nivel de API reenvía todas las solicitudes de servicio de back-end de toohello con un intervalo de tiempo de espera de 60 segundos.  
  
```xml  
<!-- api level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="60"/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>Ejemplo  
 Esta directiva de nivel de operación utiliza hello `base` directiva de elemento tooinherit Hola back-end de ámbito de nivel de elemento primario API Hola.  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <base/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>Ejemplo  
 Esta directiva de nivel de operación explícitamente reenvía todas las solicitudes back-end de toohello de servicio con un tiempo de espera de 120 y no hereda a primario Hola directiva de nivel de back-end de API.  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note hello absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>Ejemplo  
 Esta directiva de nivel de operación no reenvía las solicitudes de servicio de back-end de toohello.  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding toobackend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descripción|Obligatorio|  
|-------------|-----------------|--------------|  
|forward-request|Elemento raíz.|Sí|  
  
### <a name="attributes"></a>Attributes  
  
|Atributo|Descripción|Obligatorio|Valor predeterminado|  
|---------------|-----------------|--------------|-------------|  
|timeout="entero"|intervalo de tiempo de espera de saludo en segundos antes de que se produce un error en el servicio de back-end de hello llamada toohello.|No|Sin tiempo de espera|  
|follow-redirects="true &#124; false"|Especifica si redirecciones desde el servicio de back-end de Hola se seguido de puerta de enlace de Hola o devuelve toohello autor de la llamada.|No|false|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** back-end  
  
-   **Ámbitos de la directiva:** todos los ámbitos  
  
##  <a name="LimitConcurrency"></a> Limitar la simultaneidad  
 Hola `limit-concurrency` directiva impide que las directivas entre ejecutar más de Hola cantidad especificada de solicitudes en un momento dado. Al superar el umbral de hello, las nuevas solicitudes se agregan tooa cola, hasta que se logra la longitud máxima de la cola de Hola. Cuando la cola se agota, al intentar agregar nuevas solicitudes se produce un error inmediatamente.
  
###  <a name="LimitConcurrencyStatement"></a> Declaración de la directiva  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a>Ejemplos  
  
####  <a name="ChooseExample"></a> Ejemplo  
 Hello en el ejemplo siguiente se muestra cómo toolimit número de solicitudes reenviados tooa back-end basado en valor de Hola de una variable de contexto.
 
```xml  
<policies>
  <inbound>…</inbound>
  <backend>
    <limit-concurrency key="@((string)context.Variables["connectionId"])" max-count="3" timeout="60">
      <forward-request timeout="120"/>
    <limit-concurrency/>
  </backend>
  <outbound>…</outbound>
</policies>
```

### <a name="elements"></a>Elementos  
  
|Elemento|Descripción|Obligatorio|  
|-------------|-----------------|--------------|    
|límite de simultaneidad|Elemento raíz.|Sí|  
  
### <a name="attributes"></a>Attributes  
  
|Atributo|Descripción|Obligatorio|Valor predeterminado|  
|---------------|-----------------|--------------|--------------|  
|key|Una cadena. Expresión que se permite. Especifica el ámbito de la simultaneidad de Hola. Puede compartirse entre varias directivas.|Sí|N/D|  
|número máximo|Un entero. Especifica un número máximo de solicitudes que se permiten la directiva de hello tooenter.|Sí|N/D|  
|timeout|Un entero. Expresión que se permite. Especifica el número de Hola de segundos que una solicitud debe esperar tooenter un ámbito antes de generar "403 demasiados muchas solicitudes"|No|Infinity|  
|longitud máxima de cola|Un entero. Expresión que se permite. Especifica la longitud máxima de la cola de Hola. Las solicitudes entrantes intentar tooenter esta directiva se terminará con "403 demasiados muchas solicitudes" inmediatamente cuando se agota la cola de Hola.|No|Infinity|  
  
###  <a name="ChooseUsage"></a> Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante, saliente, back-end y en caso de error  
  
-   **Ámbitos de la directiva:** todos los ámbitos  

##  <a name="log-to-eventhub"></a>Registro tooEvent concentrador  
 Hola `log-to-eventhub` envía directiva mensajes de Hola especificado formato tooan concentrador de eventos definidos por una entidad de registrador. Como su nombre implica, directiva de Hola se usa para guardar información de contexto seleccionada de solicitud o respuesta para un análisis en línea o sin conexión.  
  
> [!NOTE]
>  Para obtener una guía paso a paso acerca de cómo configurar un concentrador de eventos y eventos de registro, consulte [cómo toolog eventos de administración de API con concentradores de eventos de Azure](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a>Ejemplo  
 Puede utilizar cualquier cadena como Hola valor toobe registrado en los centros de eventos. En este ejemplo Hola fecha y hora, el nombre del servicio de implementación, Id. de solicitud, dirección ip y nombre de la operación para todas las llamadas entrantes son concentrador de eventos registrados toohello registrador registrado con hello `contoso-logger` id.  
  
```xml  
<policies>  
  <inbound>  
    <log-to-eventhub logger-id ='contoso-logger'>  
      @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name) )   
    </log-to-eventhub>  
  </inbound>  
  <outbound>          
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descripción|Obligatorio|  
|-------------|-----------------|--------------|  
|log-to-eventhub|Elemento raíz. valor Hola de este elemento es el concentrador de eventos de hello cadena toolog tooyour.|Sí|  
  
### <a name="attributes"></a>Attributes  
  
|Atributo|Descripción|Obligatorio|  
|---------------|-----------------|--------------|  
|logger-id|Id. de Hola de hello registrador registrados con el servicio de administración de API.|Sí|  
|partition-id|Especifica el índice de Hola de partición de Hola dónde se envían los mensajes.|Opcional. Este atributo no se puede utilizar cuando se usa `partition-key`.|  
|partition-key|Especifica el valor de Hola que se usa para la asignación de partición cuando se envían mensajes.|Opcional. Este atributo no se puede utilizar cuando se usa `partition-id`.|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante, saliente, back-end y en caso de error  
  
-   **Ámbitos de la directiva:** todos los ámbitos  

##  <a name="mock-response"></a> Similar respuesta  
Hola `mock-response`, como nombre de hello implica, se utiliza toomock API y operaciones. Se anula la ejecución de la canalización normal y devuelve un autor de llamada de respuesta simuladas toohello. Directiva de Hello siempre intenta tooreturn respuestas de mayor fidelidad. Prefiere ejemplos de contenido de respuesta, siempre que estén disponibles. Genera las respuestas de ejemplo a partir de esquemas, cuando se proporcionan esquemas y no ejemplos. Si no se encuentran ni ejemplos ni esquemas, se devuelven las respuestas sin contenido.
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a>Ejemplos  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descripción|Obligatorio|  
|-------------|-----------------|--------------|  
|mock-response|Elemento raíz.|Sí|  
  
### <a name="attributes"></a>Attributes  
  
|Atributo|Descripción|Obligatorio|Valor predeterminado|  
|---------------|-----------------|--------------|--------------|  
|status-code|Especifica el código de estado de respuesta y tooselect utilizados correspondiente en el ejemplo se o un esquema.|No|200|  
|content-type|Especifica `Content-Type` el valor del encabezado de respuesta y tooselect usados correspondientes en el ejemplo se o un esquema.|No|None|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante, saliente y en caso de error  
  
-   **Ámbitos de la directiva:** todos los ámbitos

##  <a name="Retry"></a> Reintento  
 Hola `retry` directiva ejecuta sus directivas secundario una vez y, a continuación, vuelve a intentar su ejecución hasta el reintento de hello `condition` se convierte en `false` o vuelva a intentar `count` está agotada.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
  
<retry  
    condition="boolean expression or literal"  
    count="number of retry attempts"  
    interval="retry interval in seconds"  
    max-interval="maximum retry interval in seconds"  
    delta="retry interval delta in seconds"  
    first-fast-retry="boolean expression or literal">  
        <!-- One or more child policies. No restrictions -->  
</retry>  
  
```  
  
### <a name="example"></a>Ejemplo  
 Hola después forewarding de solicitud de ejemplo se vuelve a intentar la tooten veces mediante el algoritmo de reintento exponencial. Puesto que `first-fast-retry` se establece toofalse, todos los intentos de reintento son el algoritmo de reintento de asunto toohello exponsntial.  
  
```xml  
  
<retry  
    condition="@(context.Response.StatusCode == 500)"  
    count="10"  
    interval="10"  
    max-interval="100"  
    delta="10"  
    first-fast-retry="false">  
        <forward-request />  
</retry>  
  
```  
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descripción|Obligatorio|  
|-------------|-----------------|--------------|  
|retry|Elemento raíz. Puede contener cualquier otra directiva como elemento secundario.|Sí|  
  
### <a name="attributes"></a>Attributes  
  
|Atributo|Descripción|Obligatorio|Valor predeterminado|  
|---------------|-----------------|--------------|-------------|  
|condition|[Expresión](api-management-policy-expressions.md) o literal booleanos que especifican si los reintentos se deben detener (`false`) o continuar (`true`).|Sí|N/D|  
|count|Un número positivo que especifica el número máximo de Hola de reintentos tooattempt.|Sí|N/D|  
|interval|Un número positivo en segundos que especifica el intervalo de espera de hello entre los reintentos de Hola.|Sí|N/D|  
|max-interval|Un número positivo en segundos que especifica el intervalo de espera máximo de saludo entre los reintentos de Hola. Es tooimplement usa un algoritmo exponencial de reintentos.|No|N/D|  
|delta|Un número positivo en segundos que especifica el incremento de intervalo de espera de Hola. Es algoritmos de reintento lineal y exponencial de hello tooimplement usado.|No|N/D|  
|first-fast-retry|Si establece demasiado `true` , Hola primer intento de reintento se lleva a cabo inmediatamente.|No|`false`|  
  
> [!NOTE]
>  Cuando solo Hola `interval` se especifica, **fijo** se llevan a cabo los reintentos de intervalo.  
>  Cuando solo Hola `interval` y `delta` se especifican, un **lineal** se utiliza el algoritmo de reintento de intervalo, donde el tiempo de espera entre reintentos es calculada Hola correspondiente después fórmula - `interval + (count - 1)*delta`.  
>  Cuando Hola `interval`, `max-interval` y `delta` se especifican, **exponencial** se aplica el algoritmo de reintento de intervalo, donde está creciendo exponencialmente tiempo de espera de hello entre reintentos de hello del valor de Hola de `interval`valor toohello `max-interval` según siguiente toohello forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) . Tenga en cuenta que esta directiva heredará las restricciones de uso de directivas secundarias.  
  
-   **Secciones de la directiva:** entrante, saliente, back-end y en caso de error  
  
-   **Ámbitos de la directiva:** todos los ámbitos  
  
##  <a name="ReturnResponse"></a> Devolución de respuesta  
 Hola `return-response` directiva anula la ejecución de la canalización y devuelve un valor predeterminado o el autor de llamada de respuesta personalizada toohello. La respuesta predeterminada es `200 OK` sin cuerpo. La respuesta personalizada se puede especificar mediante declaraciones de directiva o variable de contexto. Cuando se especifican ambos, respuesta de hello dentro de la variable de contexto de Hola se modifica por las instrucciones de directiva de hello antes de devolverse toohello llamador.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a>Ejemplo  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descripción|Obligatorio|  
|-------------|-----------------|--------------|  
|return-response|Elemento raíz.|Sí|  
|set-header|Una declaración de directiva [set-header](api-management-transformation-policies.md#SetHTTPheader).|No|  
|set-body|Una declaración de directiva [set-body](api-management-transformation-policies.md#SetBody).|No|  
|set-status|Una declaración de directiva [set-status](api-management-advanced-policies.md#SetStatus).|No|  
  
### <a name="attributes"></a>Attributes  
  
|Atributo|Descripción|Obligatorio|  
|---------------|-----------------|--------------|  
|response-variable-name|Hello nombre de variable de contexto de hello hace referencia desde, por ejemplo, un nivel superior [solicitud de envío](api-management-advanced-policies.md#SendRequest) directiva y que contiene un `Response` objeto|Opcional.|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante, saliente, back-end y en caso de error  
  
-   **Ámbitos de la directiva:** todos los ámbitos  
  
##  <a name="SendOneWayRequest"></a> Envío de solicitud unidireccional  
 Hola `send-one-way-request` directiva envía toohello especifica la dirección URL sin tener que esperar una respuesta de solicitud de hello proporcionado.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a>Ejemplo  
 Esta directiva de ejemplo muestra un ejemplo del uso de hello `send-one-way-request` directiva toosend un mensaje tooa demora salón de chat si Hola código de respuesta HTTP es igual o mayor que too500. Para obtener más información acerca de este ejemplo, vea [mediante servicios externos desde el servicio de administración de API de Azure de Hola](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
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
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descripción|Obligatorio|  
|-------------|-----------------|--------------|  
|send-one-way-request|Elemento raíz.|Sí|  
|url|Hola dirección URL de solicitud de saludo.|No si mode=copy; de lo contrario, sí.|  
|estático|método HTTP para la solicitud de Hola Hola.|No si mode=copy; de lo contrario, sí.|  
|encabezado|Encabezado de la solicitud. Utilice varios elementos de encabezado si hay varios encabezados de solicitud.|No|  
|body|cuerpo de la solicitud de saludo.|No|  
  
### <a name="attributes"></a>Attributes  
  
|Atributo|Descripción|Obligatorio|Valor predeterminado|  
|---------------|-----------------|--------------|-------------|  
|mode="cadena"|Determina si se trata de una nueva solicitud o una copia de la solicitud actual Hola. En el modo de salida, modo = copia no inicializa el cuerpo de la solicitud de saludo.|No|Nuevo|  
|name|Especifica el nombre de Hola de hello encabezado toobe conjunto.|Sí|N/D|  
|exists-action|Especifica qué tootake acción cuando ya se ha especificado el encabezado de Hola. Este atributo debe tener uno de hello después de valores.<br /><br /> -invalidar - reemplaza Hola valor del encabezado existente Hola.<br />-skip: no reemplaza el valor del encabezado de hello existente.<br />-append: anexa el valor del encabezado existente Hola valor toohello.<br />-delete: quita el encabezado de saludo de solicitud de Hola.<br /><br /> Cuando se establece demasiado`override` al enumerar varias entradas con hello igual nombre resultados en el encabezado de Hola que se va a entradas correspondiente del conjunto tooall (que aparecerán enumeradas varias veces); solo los valores mostrados se establecerá en el resultado de hello.|No|override|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante, saliente, back-end y en caso de error  
  
-   **Ámbitos de la directiva:** todos los ámbitos  
  
##  <a name="SendRequest"></a> Envío de solicitud  
 Hola `send-request` directiva envía toohello especifica la dirección URL, ya no se espera que Hola establece valor de tiempo de espera de solicitud de hello proporcionado.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a>Ejemplo  
 Este ejemplo muestra una manera de tooverify un token de referencia con un servidor de autorización. Para obtener más información acerca de este ejemplo, vea [mediante servicios externos desde el servicio de administración de API de Azure de Hola](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
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
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descripción|Obligatorio|  
|-------------|-----------------|--------------|  
|send-request|Elemento raíz.|Sí|  
|url|Hola dirección URL de solicitud de saludo.|No si mode=copy; de lo contrario, sí.|  
|estático|método HTTP para la solicitud de Hola Hola.|No si mode=copy; de lo contrario, sí.|  
|encabezado|Encabezado de la solicitud. Utilice varios elementos de encabezado si hay varios encabezados de solicitud.|No|  
|body|cuerpo de la solicitud de saludo.|No|  
  
### <a name="attributes"></a>Attributes  
  
|Atributo|Descripción|Obligatorio|Valor predeterminado|  
|---------------|-----------------|--------------|-------------|  
|mode="cadena"|Determina si se trata de una nueva solicitud o una copia de la solicitud actual Hola. En el modo de salida, modo = copia no inicializa el cuerpo de la solicitud de saludo.|No|Nuevo|  
|response-variable-name="cadena"|Si no está presente, se utiliza `context.Response`.|No|N/D|  
|timeout="entero"|intervalo de tiempo de espera de saludo en segundos antes de la llamada de hello toohello URL se produce un error.|No|60|  
|ignore-error|Si se produce un error de solicitud de hello y true:<br /><br /> -   Si se especificó response-variable-name, contendrá un valor nulo.<br />-   Si no se especificó response-variable-name, no se actualizará context.Request.|No|false|  
|name|Especifica el nombre de Hola de hello encabezado toobe conjunto.|Sí|N/D|  
|exists-action|Especifica qué tootake acción cuando ya se ha especificado el encabezado de Hola. Este atributo debe tener uno de hello después de valores.<br /><br /> -invalidar - reemplaza Hola valor del encabezado existente Hola.<br />-skip: no reemplaza el valor del encabezado de hello existente.<br />-append: anexa el valor del encabezado existente Hola valor toohello.<br />-delete: quita el encabezado de saludo de solicitud de Hola.<br /><br /> Cuando se establece demasiado`override` al enumerar varias entradas con hello igual nombre resultados en el encabezado de Hola que se va a entradas correspondiente del conjunto tooall (que aparecerán enumeradas varias veces); solo los valores mostrados se establecerá en el resultado de hello.|No|override|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante, saliente, back-end y en caso de error  
  
-   **Ámbitos de la directiva:** todos los ámbitos  
  
##  <a name="SetHttpProxy"></a> Establecer proxy HTTP  
 Hola `proxy` directiva permite tooroute toobackends de las solicitudes que se reenvían a través de un proxy HTTP. Se admite solo HTTP (no HTTPS) entre la puerta de enlace de Hola y el proxy de Hola. Solo autenticación básica y NTLM.
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a>Ejemplo  
Tenga en cuenta uso Hola de [propiedades](api-management-howto-properties.md) como valores de hello tooavoid de nombre de usuario y contraseña almacenar información confidencial en el documento de directiva de Hola.  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descripción|Obligatorio|  
|-------------|-----------------|--------------|  
|proxy|Elemento raíz|Sí|  

### <a name="attributes"></a>Attributes  
  
|Atributo|Descripción|Obligatorio|Valor predeterminado|  
|---------------|-----------------|--------------|-------------|  
|url="string"|Dirección URL del proxy en forma de Hola de http://host: Port.|Sí|N/D|  
|username="string"|Toobe de nombre de usuario utilizado para la autenticación con el proxy de Hola.|No|N/D|  
|password="string"|Toobe de contraseña que se usa para la autenticación con el proxy de Hola.|No|N/D|  

### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante  
  
-   **Ámbitos de la directiva:** todos los ámbitos  

##  <a name="SetRequestMethod"></a> Establecimiento de método de solicitud  
 Hola `set-method` directiva permite un método de solicitud de toochange Hola HTTP para una solicitud.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a>Ejemplo  
 Esta directiva de ejemplo que usa hello `set-method` directiva muestra un ejemplo de envío de un salón de chat de mensaje tooa demora si Hola código de respuesta HTTP es mayor que o igual too500. Para obtener más información acerca de este ejemplo, vea [mediante servicios externos desde el servicio de administración de API de Azure de Hola](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
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
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descripción|Obligatorio|  
|-------------|-----------------|--------------|  
|set-method|Elemento raíz. valor de Hola de elemento de Hola especifica método HTTP de hello.|Sí|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante y en caso de error  
  
-   **Ámbitos de la directiva:** todos los ámbitos  
  
##  <a name="SetStatus"></a> Establecimiento de código de estado  
 Hola `set-status` toohello de código de estado de directiva establece Hola HTTP valor especificado.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a>Ejemplo  
 Este ejemplo se muestra cómo tooreturn una respuesta 401 si el token de autorización de hello no es válido. Para obtener más información, vea [mediante servicios externos de hello servicio de administración de API de Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)  
  
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
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descripción|Obligatorio|  
|-------------|-----------------|--------------|  
|set-status|Elemento raíz.|Sí|  
  
### <a name="attributes"></a>Attributes  
  
|Atributo|Descripción|Obligatorio|Valor predeterminado|  
|---------------|-----------------|--------------|-------------|  
|code="entero"|Hola HTTP tooreturn de código de estado.|Sí|N/D|  
|reason="cadena"|Descripción del motivo de Hola para devolver el código de estado de Hola.|Sí|N/D|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** saliente, back-end y en caso de error  
  
-   **Ámbitos de la directiva:** todos los ámbitos  

##  <a name="set-variable"></a> Establecimiento de variable  
 Hola `set-variable` directiva declara un [contexto](api-management-policy-expressions.md#ContextVariables) variable y le asigna un valor especificado a través de un [expresión](api-management-policy-expressions.md) o un literal de cadena. Si expresión de hello contiene un valor literal se convertirán tooa tipo hello y de cadena del valor de hello será `System.String`.  
  
###  <a name="set-variablePolicyStatement"></a> Declaración de la directiva  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <a name="set-variableExample"></a> Ejemplo  
 Hello en el ejemplo siguiente se muestra una directiva de variable establecida en hello sección de entrada. Esta directiva de variable establecida crea una `isMobile` booleano [contexto](api-management-policy-expressions.md#ContextVariables) variable que se establece tootrue si hello `User-Agent` solicitud encabezado contiene texto hello `iPad` o `iPhone`.  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descripción|Obligatorio|  
|-------------|-----------------|--------------|  
|set-variable|Elemento raíz.|Sí|  
  
### <a name="attributes"></a>Attributes  
  
|Atributo|Descripción|Obligatorio|  
|---------------|-----------------|--------------|  
|name|nombre de Hola de variable de saludo.|Sí|  
|value|valor de Hola de variable de saludo. Puede ser una expresión o un valor literal.|Sí|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante, saliente, back-end y en caso de error  
  
-   **Ámbitos de la directiva:** todos los ámbitos  
  
###  <a name="set-variableAllowedTypes"></a> Tipos permitidos  
 Las expresiones usadas en hello `set-variable` directiva debe devolver uno de los siguientes tipos básicos de Hola.  
  
-   System.Boolean  
  
-   System.SByte  
  
-   System.Byte  
  
-   System.UInt16  
  
-   System.UInt32  
  
-   System.UInt64  
  
-   System.Int16  
  
-   System.Int32  
  
-   System.Int64  
  
-   System.Decimal  
  
-   System.Single  
  
-   System.Double  
  
-   System.Guid  
  
-   System.String  
  
-   System.Char  
  
-   System.DateTime  
  
-   System.TimeSpan  
  
-   System.Byte?  
  
-   System.UInt16?  
  
-   System.UInt32?  
  
-   System.UInt64?  
  
-   System.Int16?  
  
-   System.Int32?  
  
-   System.Int64?  
  
-   System.Decimal?  
  
-   System.Single?  
  
-   System.Double?  
  
-   System.Guid?  
  
-   System.String?  
  
-   System.Char?  
  
-   System.DateTime?  

##  <a name="Trace"></a> Seguimiento  
 Hola `trace` directiva agrega una cadena en hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) salida. Hello directiva ejecutará solamente cuando el seguimiento se activa, es decir, `Ocp-Apim-Trace` encabezado de solicitud está presente y establecido demasiado`true` y `Ocp-Apim-Subscription-Key` encabezado de solicitud está presente y contiene una clave válida asociada con la cuenta de administrador de Hola.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descripción|Obligatorio|  
|-------------|-----------------|--------------|  
|trace|Elemento raíz.|Sí|  
  
### <a name="attributes"></a>Attributes  
  
|Atributo|Descripción|Obligatorio|Valor predeterminado|  
|---------------|-----------------|--------------|-------------|  
|de origen|Visor de seguimiento de toohello significativo literal de cadena y especificar origen Hola de mensaje de bienvenida.|Sí|N/D|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .  
  
-   **Secciones de la directiva:** entrante, saliente, back-end y en caso de error  
  
-   **Ámbitos de la directiva:** todos los ámbitos  
  
##  <a name="Wait"></a> Espera  
 Hola `wait` directiva ejecuta sus directivas secundarios inmediatos en paralelo y espera para la totalidad o una de su toocomplete de directivas secundarios inmediatos antes de que finalice. Hello espera directiva puede tener sus directivas secundarios inmediatos [solicitud de envío](api-management-advanced-policies.md#SendRequest), [obtener el valor de caché](api-management-caching-policies.md#GetFromCacheByKey), y [flujo de Control](api-management-advanced-policies.md#choose) directivas.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a>Ejemplo  
 En el siguiente ejemplo de Hola hay dos `choose` directivas como directivas de secundarios inmediatos de hello `wait` directiva. Cada una de estas directivas `choose` se ejecuta en paralelo. Cada `choose` directiva intenta tooretrieve un valor almacenado en caché. Si se produce un error de caché, un servicio back-end se denomina valor de Hola de tooprovide. En este Hola ejemplo `wait` directiva no se completa hasta que se completen todas sus directivas secundarios inmediatos, porque hello `for` atributo está establecido demasiado`all`.   En este variables de contexto de ejemplo Hola (`execute-branch-one`, `value-one`, `execute-branch-two`, y `value-two`) se declaran fuera del ámbito de Hola de esta directiva de ejemplo.  
  
```xml  
<wait for="all">  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-one="])">  
      <cache-lookup-value key="key-one" variable-name="value-one" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-one="))">  
          <send-request mode="new" response-variable-name="value-one">  
            <set-url>https://backend-one</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-two="])">  
      <cache-lookup-value key="key-two" variable-name="value-two" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-two="))">  
          <send-request mode="new" response-variable-name="value-two">  
            <set-url>https://backend-two</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
</wait>  
  
```  
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descripción|Obligatorio|  
|-------------|-----------------|--------------|  
|wait|Elemento raíz. Solo puede contener como elementos secundarios a las directivas `send-request`, `cache-lookup-value` y `choose`.|Sí|  
  
### <a name="attributes"></a>Attributes  
  
|Atributo|Descripción|Obligatorio|Valor predeterminado|  
|---------------|-----------------|--------------|-------------|  
|for|Determina si hello `wait` directiva esperará a que todos los toobe de directivas de secundarios inmediatos completado o solo uno. Los valores permitidos son:<br /><br /> -   `all`-Espere a que todos los secundarios inmediatos directivas toocomplete<br />-- Espere cualquier toocomplete de directiva secundarios inmediatos. Cuando haya completado la primera directiva de secundarios inmediatos de hello, Hola `wait` directiva completa y finaliza la ejecución de cualquier otra directiva secundarios inmediatos.|No|todas|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante, saliente y back-end  
  
-   **Ámbitos de la directiva:** todos los ámbitos  
  
## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre cómo trabajar con directivas, consulte:
-   [Directivas de Administración de API de Azure](api-management-howto-policies.md) 
-   [Policy expressions (Expresiones de directiva)](api-management-policy-expressions.md)
