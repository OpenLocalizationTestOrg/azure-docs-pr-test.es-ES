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
# <a name="api-management-advanced-policies"></a><span data-ttu-id="2599b-103">Directivas avanzadas de API Management</span><span class="sxs-lookup"><span data-stu-id="2599b-103">API Management advanced policies</span></span>
<span data-ttu-id="2599b-104">En este tema se proporciona una referencia para hello las siguientes directivas de administración de API.</span><span class="sxs-lookup"><span data-stu-id="2599b-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="2599b-105">Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="2599b-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="2599b-106"><a name="AdvancedPolicies"></a> Directivas avanzadas</span><span class="sxs-lookup"><span data-stu-id="2599b-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="2599b-107">[Flujo de control](api-management-advanced-policies.md#choose) - condicionalmente aplica las instrucciones de directiva en función de los resultados de Hola de evaluación de Hola de tipo Boolean [expresiones](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="2599b-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="2599b-108">[Reenviar la solicitud](#ForwardRequest) -reenvía el servicio back-end de hello solicitud toohello.</span><span class="sxs-lookup"><span data-stu-id="2599b-108">[Forward request](#ForwardRequest) - Forwards hello request toohello backend service.</span></span>

-   <span data-ttu-id="2599b-109">[Limitar la simultaneidad](#LimitConcurrency) -evita entre las directivas de ejecución más Hola cantidad especificada de solicitudes a la vez.</span><span class="sxs-lookup"><span data-stu-id="2599b-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than hello specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="2599b-110">[Inicie sesión tooEvent concentrador](#log-to-eventhub) -envía los mensajes de Hola especificado tooan formato concentrador de eventos definido por una entidad de registrador.</span><span class="sxs-lookup"><span data-stu-id="2599b-110">[Log tooEvent Hub](#log-to-eventhub) - Sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="2599b-111">[Simular respuesta](#mock-response) -ejecución de canalización de anulaciones y devuelve una respuesta simulada directamente toohello autor de la llamada.</span><span class="sxs-lookup"><span data-stu-id="2599b-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly toohello caller.</span></span>
  
-   <span data-ttu-id="2599b-112">[Vuelva a intentar](#Retry) -ejecución de reintentos de hello entre las instrucciones de directiva, si y hasta que se cumpla la condición de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-112">[Retry](#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="2599b-113">Ejecución se repetirá en intervalos de tiempo especificados de Hola y seguridad toohello especificada el número de reintentos.</span><span class="sxs-lookup"><span data-stu-id="2599b-113">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>  
  
-   <span data-ttu-id="2599b-114">[Devolver la respuesta](#ReturnResponse) -Hola de ejecución y devuelve de la canalización de anulaciones especificado respuesta directamente toohello autor de la llamada.</span><span class="sxs-lookup"><span data-stu-id="2599b-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span> 
  
-   <span data-ttu-id="2599b-115">[Enviar solicitud unidireccionales](#SendOneWayRequest) -envía una solicitud toohello especificó la dirección URL sin tener que esperar una respuesta.</span><span class="sxs-lookup"><span data-stu-id="2599b-115">[Send one way request](#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="2599b-116">[Enviar solicitud](#SendRequest) -envía una solicitud toohello URL especificada.</span><span class="sxs-lookup"><span data-stu-id="2599b-116">[Send request](#SendRequest) - Sends a request toohello specified URL.</span></span>  

-   <span data-ttu-id="2599b-117">[Establecer el proxy HTTP](#SetHttpProxy) -permite tooroute reenviar solicitudes a través de un proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="2599b-117">[Set HTTP proxy](#SetHttpProxy) - Allows you tooroute forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="2599b-118">[Establecer el método de solicitud](#SetRequestMethod) -permite toochange método de hello HTTP para una solicitud.</span><span class="sxs-lookup"><span data-stu-id="2599b-118">[Set request method](#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="2599b-119">[Código de estado del conjunto de](#SetStatus) -toohello de código de estado HTTP de Hola de cambios de valor especificado.</span><span class="sxs-lookup"><span data-stu-id="2599b-119">[Set status code](#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>  
  
-   <span data-ttu-id="2599b-120">[Establecimiento de variable](api-management-advanced-policies.md#set-variable): conserva un valor en una variable [context](api-management-policy-expressions.md#ContextVariables) con nombre para su posterior acceso.</span><span class="sxs-lookup"><span data-stu-id="2599b-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="2599b-121">[Seguimiento](#Trace) -agrega una cadena en hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) salida.</span><span class="sxs-lookup"><span data-stu-id="2599b-121">[Trace](#Trace) - Adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="2599b-122">[Espere](#Wait) -espera entre [solicitud de envío](api-management-advanced-policies.md#SendRequest), [obtener el valor de caché](api-management-caching-policies.md#GetFromCacheByKey), o [flujo de Control](api-management-advanced-policies.md#choose) toocomplete directivas antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="2599b-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies toocomplete before proceeding.</span></span>  
  
##  <span data-ttu-id="2599b-123"><a name="choose"></a> Flujo de control</span><span class="sxs-lookup"><span data-stu-id="2599b-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="2599b-124">Hola `choose` directiva aplica a instrucciones en función de resultado de hello de la evaluación de expresiones booleanas, similar tooan if-then-else o un conmutador que se construyen en un lenguaje de programación de directiva adjuntas.</span><span class="sxs-lookup"><span data-stu-id="2599b-124">hello `choose` policy applies enclosed policy statements based on hello outcome of evaluation of Boolean expressions, similar tooan if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="2599b-125"><a name="ChoosePolicyStatement"></a> Declaración de la directiva</span><span class="sxs-lookup"><span data-stu-id="2599b-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
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
  
 <span data-ttu-id="2599b-126">Hello directiva de flujo de control debe contener al menos un `<when/>` elemento.</span><span class="sxs-lookup"><span data-stu-id="2599b-126">hello control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="2599b-127">Hola `<otherwise/>` elemento es opcional.</span><span class="sxs-lookup"><span data-stu-id="2599b-127">hello `<otherwise/>` element is optional.</span></span> <span data-ttu-id="2599b-128">Las condiciones en `<when/>` elementos se evalúan en orden de aparición dentro de la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-128">Conditions in `<when/>` elements are evaluated in order of their appearance within hello policy.</span></span> <span data-ttu-id="2599b-129">Directivas adjuntas en hello primero `<when/>` elemento con el atributo de condición es igual a `true` se aplicarán.</span><span class="sxs-lookup"><span data-stu-id="2599b-129">Policy statement(s) enclosed within hello first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="2599b-130">Directivas delimitadas hello `<otherwise/>` elemento, si está presente, se aplicará si todas las de hello `<when/>` los atributos de condición de elemento son `false`.</span><span class="sxs-lookup"><span data-stu-id="2599b-130">Policies enclosed within hello `<otherwise/>` element, if present, will be applied if all of hello `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="2599b-131">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2599b-131">Examples</span></span>  
  
####  <span data-ttu-id="2599b-132"><a name="ChooseExample"></a> Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2599b-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="2599b-133">Hello en el ejemplo siguiente se muestra cómo un [set-variable](api-management-advanced-policies.md#set-variable) directiva y dos directivas de flujo de control.</span><span class="sxs-lookup"><span data-stu-id="2599b-133">hello following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="2599b-134">Hola establecer la variable directiva está en Hola sección de entrada y crea un `isMobile` booleano [contexto](api-management-policy-expressions.md#ContextVariables) variable que se establece tootrue si hello `User-Agent` solicitud encabezado contiene texto hello `iPad` o `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="2599b-134">hello set variable policy is in hello inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="2599b-135">Hola primera directiva de flujo de control también está en Hola sección de entrada y aplica condicionalmente uno de dos [establecer el parámetro de cadena de consulta](api-management-transformation-policies.md#SetQueryStringParameter) directivas según valor Hola de hello `isMobile` variable de contexto.</span><span class="sxs-lookup"><span data-stu-id="2599b-135">hello first control flow policy is also in hello inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on hello value of hello `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="2599b-136">segunda directiva de flujo de control Hello en la sección de salida de hello y aplica condicionalmente hello [convertir XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) directiva cuando `isMobile` se establece demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="2599b-136">hello second control flow policy is in hello outbound section and conditionally applies hello [Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set too`true`.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="2599b-137">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2599b-137">Example</span></span>  
 <span data-ttu-id="2599b-138">Este ejemplo muestra cómo tooperform contenido filtrado mediante la eliminación de elementos de datos de respuesta de Hola recibido del servicio de back-end de hello cuando se usa hello `Starter` producto.</span><span class="sxs-lookup"><span data-stu-id="2599b-138">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="2599b-139">Para ver una demostración de cómo configurar y usar esta directiva, consulte [177 episodio abarcan de nube: más características de administración de API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avancemos too34:30.</span><span class="sxs-lookup"><span data-stu-id="2599b-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="2599b-140">Iniciar en 31:50 toosee una visión general de [Hola API de previsión de Sky oscuro](https://developer.forecast.io/) utilizada para esta demostración.</span><span class="sxs-lookup"><span data-stu-id="2599b-140">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="2599b-141">Elementos</span><span class="sxs-lookup"><span data-stu-id="2599b-141">Elements</span></span>  
  
|<span data-ttu-id="2599b-142">Elemento</span><span class="sxs-lookup"><span data-stu-id="2599b-142">Element</span></span>|<span data-ttu-id="2599b-143">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-143">Description</span></span>|<span data-ttu-id="2599b-144">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2599b-145">choose</span><span class="sxs-lookup"><span data-stu-id="2599b-145">choose</span></span>|<span data-ttu-id="2599b-146">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="2599b-146">Root element.</span></span>|<span data-ttu-id="2599b-147">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-147">Yes</span></span>|  
|<span data-ttu-id="2599b-148">when</span><span class="sxs-lookup"><span data-stu-id="2599b-148">when</span></span>|<span data-ttu-id="2599b-149">Hola toouse de condición para hello `if` o `ifelse` partes de hello `choose` directiva.</span><span class="sxs-lookup"><span data-stu-id="2599b-149">hello condition toouse for hello `if` or `ifelse` parts of hello `choose` policy.</span></span> <span data-ttu-id="2599b-150">Si hello `choose` directiva tenga varias `when` secciones, se evalúan de forma secuencial.</span><span class="sxs-lookup"><span data-stu-id="2599b-150">If hello `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="2599b-151">Una vez Hola `condition` de cuando el elemento se evalúa demasiado`true`, ningún otro `when` se evalúan las condiciones.</span><span class="sxs-lookup"><span data-stu-id="2599b-151">Once hello `condition` of a when element evaluates too`true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="2599b-152">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-152">Yes</span></span>|  
|<span data-ttu-id="2599b-153">otherwise</span><span class="sxs-lookup"><span data-stu-id="2599b-153">otherwise</span></span>|<span data-ttu-id="2599b-154">Contiene toobe de fragmento de código de directiva de Hola utilizado si ninguna de hello `when` condiciones se evalúan demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="2599b-154">Contains hello policy snippet toobe used if none of hello `when` conditions evaluate too`true`.</span></span>|<span data-ttu-id="2599b-155">No</span><span class="sxs-lookup"><span data-stu-id="2599b-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2599b-156">Attributes</span><span class="sxs-lookup"><span data-stu-id="2599b-156">Attributes</span></span>  
  
|<span data-ttu-id="2599b-157">Atributo</span><span class="sxs-lookup"><span data-stu-id="2599b-157">Attribute</span></span>|<span data-ttu-id="2599b-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-158">Description</span></span>|<span data-ttu-id="2599b-159">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="2599b-160">condition="Constante booleana &#124; Constante booleana"</span><span class="sxs-lookup"><span data-stu-id="2599b-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="2599b-161">expresión booleana de Hola o constante tooevaluated cuando Hola que contiene `when` se evalúa la instrucción de directiva.</span><span class="sxs-lookup"><span data-stu-id="2599b-161">hello Boolean expression or constant tooevaluated when hello containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="2599b-162">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-162">Yes</span></span>|  
  
###  <span data-ttu-id="2599b-163"><a name="ChooseUsage"></a> Uso</span><span class="sxs-lookup"><span data-stu-id="2599b-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="2599b-164">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="2599b-164">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2599b-165">**Secciones de la directiva:** entrante, saliente, back-end y en caso de error</span><span class="sxs-lookup"><span data-stu-id="2599b-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2599b-166">**Ámbitos de la directiva:** todos los ámbitos</span><span class="sxs-lookup"><span data-stu-id="2599b-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="2599b-167"><a name="ForwardRequest"></a> Reenvío de solicitud</span><span class="sxs-lookup"><span data-stu-id="2599b-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="2599b-168">Hola `forward-request` directiva reenvía Hola entrantes solicitud toohello servicio back-end especificado en la solicitud de hello [contexto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="2599b-168">hello `forward-request` policy forwards hello incoming request toohello backend service specified in hello request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="2599b-169">dirección URL del servicio back-end Hello se especifica una API de Hola [configuración](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) y se puede cambiar mediante hello [establecer el servicio back-end](api-management-transformation-policies.md) directiva.</span><span class="sxs-lookup"><span data-stu-id="2599b-169">hello backend service URL is specified in hello API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using hello [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="2599b-170">Quitar este resultados de directivas de solicitud de hello no se reenvían las directivas de hello y servicio del back-end de toohello en la sección de salida de hello se evalúan inmediatamente tras la finalización correcta de Hola de directivas de Hola Hola sección de entrada.</span><span class="sxs-lookup"><span data-stu-id="2599b-170">Removing this policy results in hello request not being forwarded toohello backend service and hello policies in hello outbound section are evaluated immediately upon hello successful completion of hello policies in hello inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2599b-171">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="2599b-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="2599b-172">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2599b-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="2599b-173">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2599b-173">Example</span></span>  
 <span data-ttu-id="2599b-174">Hello siguientes directivas de nivel de API reenvía todas las solicitudes de servicio de back-end de toohello con un intervalo de tiempo de espera de 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="2599b-174">hello following API level policy forwards all requests toohello backend service with a timeout interval of 60 seconds.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="2599b-175">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2599b-175">Example</span></span>  
 <span data-ttu-id="2599b-176">Esta directiva de nivel de operación utiliza hello `base` directiva de elemento tooinherit Hola back-end de ámbito de nivel de elemento primario API Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-176">This operation level policy uses hello `base` element tooinherit hello backend policy from hello parent API level scope.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="2599b-177">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2599b-177">Example</span></span>  
 <span data-ttu-id="2599b-178">Esta directiva de nivel de operación explícitamente reenvía todas las solicitudes back-end de toohello de servicio con un tiempo de espera de 120 y no hereda a primario Hola directiva de nivel de back-end de API.</span><span class="sxs-lookup"><span data-stu-id="2599b-178">This operation level policy explicitly forwards all requests toohello backend service with a timeout of 120 and does not inherit hello parent API level backend policy.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="2599b-179">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2599b-179">Example</span></span>  
 <span data-ttu-id="2599b-180">Esta directiva de nivel de operación no reenvía las solicitudes de servicio de back-end de toohello.</span><span class="sxs-lookup"><span data-stu-id="2599b-180">This operation level policy does not forward requests toohello backend service.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="2599b-181">Elementos</span><span class="sxs-lookup"><span data-stu-id="2599b-181">Elements</span></span>  
  
|<span data-ttu-id="2599b-182">Elemento</span><span class="sxs-lookup"><span data-stu-id="2599b-182">Element</span></span>|<span data-ttu-id="2599b-183">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-183">Description</span></span>|<span data-ttu-id="2599b-184">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2599b-185">forward-request</span><span class="sxs-lookup"><span data-stu-id="2599b-185">forward-request</span></span>|<span data-ttu-id="2599b-186">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="2599b-186">Root element.</span></span>|<span data-ttu-id="2599b-187">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2599b-188">Attributes</span><span class="sxs-lookup"><span data-stu-id="2599b-188">Attributes</span></span>  
  
|<span data-ttu-id="2599b-189">Atributo</span><span class="sxs-lookup"><span data-stu-id="2599b-189">Attribute</span></span>|<span data-ttu-id="2599b-190">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-190">Description</span></span>|<span data-ttu-id="2599b-191">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-191">Required</span></span>|<span data-ttu-id="2599b-192">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="2599b-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="2599b-193">timeout="entero"</span><span class="sxs-lookup"><span data-stu-id="2599b-193">timeout="integer"</span></span>|<span data-ttu-id="2599b-194">intervalo de tiempo de espera de saludo en segundos antes de que se produce un error en el servicio de back-end de hello llamada toohello.</span><span class="sxs-lookup"><span data-stu-id="2599b-194">hello timeout interval in seconds before hello call toohello backend service fails.</span></span>|<span data-ttu-id="2599b-195">No</span><span class="sxs-lookup"><span data-stu-id="2599b-195">No</span></span>|<span data-ttu-id="2599b-196">Sin tiempo de espera</span><span class="sxs-lookup"><span data-stu-id="2599b-196">No timeout</span></span>|  
|<span data-ttu-id="2599b-197">follow-redirects="true &#124; false"</span><span class="sxs-lookup"><span data-stu-id="2599b-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="2599b-198">Especifica si redirecciones desde el servicio de back-end de Hola se seguido de puerta de enlace de Hola o devuelve toohello autor de la llamada.</span><span class="sxs-lookup"><span data-stu-id="2599b-198">Specifies whether redirects from hello backend service are followed by hello gateway or returned toohello caller.</span></span>|<span data-ttu-id="2599b-199">No</span><span class="sxs-lookup"><span data-stu-id="2599b-199">No</span></span>|<span data-ttu-id="2599b-200">false</span><span class="sxs-lookup"><span data-stu-id="2599b-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2599b-201">Uso</span><span class="sxs-lookup"><span data-stu-id="2599b-201">Usage</span></span>  
 <span data-ttu-id="2599b-202">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="2599b-202">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2599b-203">**Secciones de la directiva:** back-end</span><span class="sxs-lookup"><span data-stu-id="2599b-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="2599b-204">**Ámbitos de la directiva:** todos los ámbitos</span><span class="sxs-lookup"><span data-stu-id="2599b-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="2599b-205"><a name="LimitConcurrency"></a> Limitar la simultaneidad</span><span class="sxs-lookup"><span data-stu-id="2599b-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="2599b-206">Hola `limit-concurrency` directiva impide que las directivas entre ejecutar más de Hola cantidad especificada de solicitudes en un momento dado.</span><span class="sxs-lookup"><span data-stu-id="2599b-206">hello `limit-concurrency` policy prevents enclosed policies from executing by more than hello specified number of requests at a given time.</span></span> <span data-ttu-id="2599b-207">Al superar el umbral de hello, las nuevas solicitudes se agregan tooa cola, hasta que se logra la longitud máxima de la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-207">Upon exceeding hello threshold, new requests are added tooa queue, until hello maximum queue length is achieved.</span></span> <span data-ttu-id="2599b-208">Cuando la cola se agota, al intentar agregar nuevas solicitudes se produce un error inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="2599b-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="2599b-209"><a name="LimitConcurrencyStatement"></a> Declaración de la directiva</span><span class="sxs-lookup"><span data-stu-id="2599b-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="2599b-210">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2599b-210">Examples</span></span>  
  
####  <span data-ttu-id="2599b-211"><a name="ChooseExample"></a> Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2599b-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="2599b-212">Hello en el ejemplo siguiente se muestra cómo toolimit número de solicitudes reenviados tooa back-end basado en valor de Hola de una variable de contexto.</span><span class="sxs-lookup"><span data-stu-id="2599b-212">hello following example demonstrates how toolimit number of requests forwarded tooa backend based on hello value of a context variable.</span></span>
 
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

### <a name="elements"></a><span data-ttu-id="2599b-213">Elementos</span><span class="sxs-lookup"><span data-stu-id="2599b-213">Elements</span></span>  
  
|<span data-ttu-id="2599b-214">Elemento</span><span class="sxs-lookup"><span data-stu-id="2599b-214">Element</span></span>|<span data-ttu-id="2599b-215">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-215">Description</span></span>|<span data-ttu-id="2599b-216">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="2599b-217">límite de simultaneidad</span><span class="sxs-lookup"><span data-stu-id="2599b-217">limit-concurrency</span></span>|<span data-ttu-id="2599b-218">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="2599b-218">Root element.</span></span>|<span data-ttu-id="2599b-219">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2599b-220">Attributes</span><span class="sxs-lookup"><span data-stu-id="2599b-220">Attributes</span></span>  
  
|<span data-ttu-id="2599b-221">Atributo</span><span class="sxs-lookup"><span data-stu-id="2599b-221">Attribute</span></span>|<span data-ttu-id="2599b-222">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-222">Description</span></span>|<span data-ttu-id="2599b-223">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-223">Required</span></span>|<span data-ttu-id="2599b-224">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="2599b-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="2599b-225">key</span><span class="sxs-lookup"><span data-stu-id="2599b-225">key</span></span>|<span data-ttu-id="2599b-226">Una cadena.</span><span class="sxs-lookup"><span data-stu-id="2599b-226">A string.</span></span> <span data-ttu-id="2599b-227">Expresión que se permite.</span><span class="sxs-lookup"><span data-stu-id="2599b-227">Expression allowed.</span></span> <span data-ttu-id="2599b-228">Especifica el ámbito de la simultaneidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-228">Specifies hello concurrency scope.</span></span> <span data-ttu-id="2599b-229">Puede compartirse entre varias directivas.</span><span class="sxs-lookup"><span data-stu-id="2599b-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="2599b-230">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-230">Yes</span></span>|<span data-ttu-id="2599b-231">N/D</span><span class="sxs-lookup"><span data-stu-id="2599b-231">N/A</span></span>|  
|<span data-ttu-id="2599b-232">número máximo</span><span class="sxs-lookup"><span data-stu-id="2599b-232">max-count</span></span>|<span data-ttu-id="2599b-233">Un entero.</span><span class="sxs-lookup"><span data-stu-id="2599b-233">An integer.</span></span> <span data-ttu-id="2599b-234">Especifica un número máximo de solicitudes que se permiten la directiva de hello tooenter.</span><span class="sxs-lookup"><span data-stu-id="2599b-234">Specifies a maximum number of requests that are allowed tooenter hello policy.</span></span>|<span data-ttu-id="2599b-235">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-235">Yes</span></span>|<span data-ttu-id="2599b-236">N/D</span><span class="sxs-lookup"><span data-stu-id="2599b-236">N/A</span></span>|  
|<span data-ttu-id="2599b-237">timeout</span><span class="sxs-lookup"><span data-stu-id="2599b-237">timeout</span></span>|<span data-ttu-id="2599b-238">Un entero.</span><span class="sxs-lookup"><span data-stu-id="2599b-238">An integer.</span></span> <span data-ttu-id="2599b-239">Expresión que se permite.</span><span class="sxs-lookup"><span data-stu-id="2599b-239">Expression allowed.</span></span> <span data-ttu-id="2599b-240">Especifica el número de Hola de segundos que una solicitud debe esperar tooenter un ámbito antes de generar "403 demasiados muchas solicitudes"</span><span class="sxs-lookup"><span data-stu-id="2599b-240">Specifies hello number of seconds a request should wait tooenter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="2599b-241">No</span><span class="sxs-lookup"><span data-stu-id="2599b-241">No</span></span>|<span data-ttu-id="2599b-242">Infinity</span><span class="sxs-lookup"><span data-stu-id="2599b-242">Infinity</span></span>|  
|<span data-ttu-id="2599b-243">longitud máxima de cola</span><span class="sxs-lookup"><span data-stu-id="2599b-243">max-queue-length</span></span>|<span data-ttu-id="2599b-244">Un entero.</span><span class="sxs-lookup"><span data-stu-id="2599b-244">An integer.</span></span> <span data-ttu-id="2599b-245">Expresión que se permite.</span><span class="sxs-lookup"><span data-stu-id="2599b-245">Expression allowed.</span></span> <span data-ttu-id="2599b-246">Especifica la longitud máxima de la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-246">Specifies hello maximum queue length.</span></span> <span data-ttu-id="2599b-247">Las solicitudes entrantes intentar tooenter esta directiva se terminará con "403 demasiados muchas solicitudes" inmediatamente cuando se agota la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-247">Incoming requests trying tooenter this policy will be terminated with “403 Too Many Requests” immediately when hello queue is exhausted.</span></span>|<span data-ttu-id="2599b-248">No</span><span class="sxs-lookup"><span data-stu-id="2599b-248">No</span></span>|<span data-ttu-id="2599b-249">Infinity</span><span class="sxs-lookup"><span data-stu-id="2599b-249">Infinity</span></span>|  
  
###  <span data-ttu-id="2599b-250"><a name="ChooseUsage"></a> Uso</span><span class="sxs-lookup"><span data-stu-id="2599b-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="2599b-251">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="2599b-251">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2599b-252">**Secciones de la directiva:** entrante, saliente, back-end y en caso de error</span><span class="sxs-lookup"><span data-stu-id="2599b-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2599b-253">**Ámbitos de la directiva:** todos los ámbitos</span><span class="sxs-lookup"><span data-stu-id="2599b-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="2599b-254"><a name="log-to-eventhub"></a>Registro tooEvent concentrador</span><span class="sxs-lookup"><span data-stu-id="2599b-254"><a name="log-to-eventhub"></a> Log tooEvent Hub</span></span>  
 <span data-ttu-id="2599b-255">Hola `log-to-eventhub` envía directiva mensajes de Hola especificado formato tooan concentrador de eventos definidos por una entidad de registrador.</span><span class="sxs-lookup"><span data-stu-id="2599b-255">hello `log-to-eventhub` policy sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="2599b-256">Como su nombre implica, directiva de Hola se usa para guardar información de contexto seleccionada de solicitud o respuesta para un análisis en línea o sin conexión.</span><span class="sxs-lookup"><span data-stu-id="2599b-256">As its name implies, hello policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="2599b-257">Para obtener una guía paso a paso acerca de cómo configurar un concentrador de eventos y eventos de registro, consulte [cómo toolog eventos de administración de API con concentradores de eventos de Azure](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="2599b-257">For a step-by-step guide on configuring an event hub and logging events, see [How toolog API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2599b-258">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="2599b-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="2599b-259">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2599b-259">Example</span></span>  
 <span data-ttu-id="2599b-260">Puede utilizar cualquier cadena como Hola valor toobe registrado en los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="2599b-260">Any string can be used as hello value toobe logged in Event Hubs.</span></span> <span data-ttu-id="2599b-261">En este ejemplo Hola fecha y hora, el nombre del servicio de implementación, Id. de solicitud, dirección ip y nombre de la operación para todas las llamadas entrantes son concentrador de eventos registrados toohello registrador registrado con hello `contoso-logger` id.</span><span class="sxs-lookup"><span data-stu-id="2599b-261">In this example hello date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged toohello event hub Logger registered with hello `contoso-logger` id.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="2599b-262">Elementos</span><span class="sxs-lookup"><span data-stu-id="2599b-262">Elements</span></span>  
  
|<span data-ttu-id="2599b-263">Elemento</span><span class="sxs-lookup"><span data-stu-id="2599b-263">Element</span></span>|<span data-ttu-id="2599b-264">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-264">Description</span></span>|<span data-ttu-id="2599b-265">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2599b-266">log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="2599b-266">log-to-eventhub</span></span>|<span data-ttu-id="2599b-267">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="2599b-267">Root element.</span></span> <span data-ttu-id="2599b-268">valor Hola de este elemento es el concentrador de eventos de hello cadena toolog tooyour.</span><span class="sxs-lookup"><span data-stu-id="2599b-268">hello value of this element is hello string toolog tooyour event hub.</span></span>|<span data-ttu-id="2599b-269">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2599b-270">Attributes</span><span class="sxs-lookup"><span data-stu-id="2599b-270">Attributes</span></span>  
  
|<span data-ttu-id="2599b-271">Atributo</span><span class="sxs-lookup"><span data-stu-id="2599b-271">Attribute</span></span>|<span data-ttu-id="2599b-272">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-272">Description</span></span>|<span data-ttu-id="2599b-273">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="2599b-274">logger-id</span><span class="sxs-lookup"><span data-stu-id="2599b-274">logger-id</span></span>|<span data-ttu-id="2599b-275">Id. de Hola de hello registrador registrados con el servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="2599b-275">hello id of hello Logger registered with your API Management service.</span></span>|<span data-ttu-id="2599b-276">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-276">Yes</span></span>|  
|<span data-ttu-id="2599b-277">partition-id</span><span class="sxs-lookup"><span data-stu-id="2599b-277">partition-id</span></span>|<span data-ttu-id="2599b-278">Especifica el índice de Hola de partición de Hola dónde se envían los mensajes.</span><span class="sxs-lookup"><span data-stu-id="2599b-278">Specifies hello index of hello partition where messages are sent.</span></span>|<span data-ttu-id="2599b-279">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2599b-279">Optional.</span></span> <span data-ttu-id="2599b-280">Este atributo no se puede utilizar cuando se usa `partition-key`.</span><span class="sxs-lookup"><span data-stu-id="2599b-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="2599b-281">partition-key</span><span class="sxs-lookup"><span data-stu-id="2599b-281">partition-key</span></span>|<span data-ttu-id="2599b-282">Especifica el valor de Hola que se usa para la asignación de partición cuando se envían mensajes.</span><span class="sxs-lookup"><span data-stu-id="2599b-282">Specifies hello value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="2599b-283">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2599b-283">Optional.</span></span> <span data-ttu-id="2599b-284">Este atributo no se puede utilizar cuando se usa `partition-id`.</span><span class="sxs-lookup"><span data-stu-id="2599b-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2599b-285">Uso</span><span class="sxs-lookup"><span data-stu-id="2599b-285">Usage</span></span>  
 <span data-ttu-id="2599b-286">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="2599b-286">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2599b-287">**Secciones de la directiva:** entrante, saliente, back-end y en caso de error</span><span class="sxs-lookup"><span data-stu-id="2599b-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2599b-288">**Ámbitos de la directiva:** todos los ámbitos</span><span class="sxs-lookup"><span data-stu-id="2599b-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="2599b-289"><a name="mock-response"></a> Similar respuesta</span><span class="sxs-lookup"><span data-stu-id="2599b-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="2599b-290">Hola `mock-response`, como nombre de hello implica, se utiliza toomock API y operaciones.</span><span class="sxs-lookup"><span data-stu-id="2599b-290">hello `mock-response`, as hello name implies, is used toomock APIs and operations.</span></span> <span data-ttu-id="2599b-291">Se anula la ejecución de la canalización normal y devuelve un autor de llamada de respuesta simuladas toohello.</span><span class="sxs-lookup"><span data-stu-id="2599b-291">It aborts normal pipeline execution and returns a mocked response toohello caller.</span></span> <span data-ttu-id="2599b-292">Directiva de Hello siempre intenta tooreturn respuestas de mayor fidelidad.</span><span class="sxs-lookup"><span data-stu-id="2599b-292">hello policy always tries tooreturn responses of highest fidelity.</span></span> <span data-ttu-id="2599b-293">Prefiere ejemplos de contenido de respuesta, siempre que estén disponibles.</span><span class="sxs-lookup"><span data-stu-id="2599b-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="2599b-294">Genera las respuestas de ejemplo a partir de esquemas, cuando se proporcionan esquemas y no ejemplos.</span><span class="sxs-lookup"><span data-stu-id="2599b-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="2599b-295">Si no se encuentran ni ejemplos ni esquemas, se devuelven las respuestas sin contenido.</span><span class="sxs-lookup"><span data-stu-id="2599b-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="2599b-296">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="2599b-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="2599b-297">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2599b-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="2599b-298">Elementos</span><span class="sxs-lookup"><span data-stu-id="2599b-298">Elements</span></span>  
  
|<span data-ttu-id="2599b-299">Elemento</span><span class="sxs-lookup"><span data-stu-id="2599b-299">Element</span></span>|<span data-ttu-id="2599b-300">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-300">Description</span></span>|<span data-ttu-id="2599b-301">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2599b-302">mock-response</span><span class="sxs-lookup"><span data-stu-id="2599b-302">mock-response</span></span>|<span data-ttu-id="2599b-303">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="2599b-303">Root element.</span></span>|<span data-ttu-id="2599b-304">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2599b-305">Attributes</span><span class="sxs-lookup"><span data-stu-id="2599b-305">Attributes</span></span>  
  
|<span data-ttu-id="2599b-306">Atributo</span><span class="sxs-lookup"><span data-stu-id="2599b-306">Attribute</span></span>|<span data-ttu-id="2599b-307">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-307">Description</span></span>|<span data-ttu-id="2599b-308">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-308">Required</span></span>|<span data-ttu-id="2599b-309">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="2599b-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="2599b-310">status-code</span><span class="sxs-lookup"><span data-stu-id="2599b-310">status-code</span></span>|<span data-ttu-id="2599b-311">Especifica el código de estado de respuesta y tooselect utilizados correspondiente en el ejemplo se o un esquema.</span><span class="sxs-lookup"><span data-stu-id="2599b-311">Specifies response status code and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="2599b-312">No</span><span class="sxs-lookup"><span data-stu-id="2599b-312">No</span></span>|<span data-ttu-id="2599b-313">200</span><span class="sxs-lookup"><span data-stu-id="2599b-313">200</span></span>|  
|<span data-ttu-id="2599b-314">content-type</span><span class="sxs-lookup"><span data-stu-id="2599b-314">content-type</span></span>|<span data-ttu-id="2599b-315">Especifica `Content-Type` el valor del encabezado de respuesta y tooselect usados correspondientes en el ejemplo se o un esquema.</span><span class="sxs-lookup"><span data-stu-id="2599b-315">Specifies `Content-Type` response header value and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="2599b-316">No</span><span class="sxs-lookup"><span data-stu-id="2599b-316">No</span></span>|<span data-ttu-id="2599b-317">None</span><span class="sxs-lookup"><span data-stu-id="2599b-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2599b-318">Uso</span><span class="sxs-lookup"><span data-stu-id="2599b-318">Usage</span></span>  
 <span data-ttu-id="2599b-319">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="2599b-319">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2599b-320">**Secciones de la directiva:** entrante, saliente y en caso de error</span><span class="sxs-lookup"><span data-stu-id="2599b-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="2599b-321">**Ámbitos de la directiva:** todos los ámbitos</span><span class="sxs-lookup"><span data-stu-id="2599b-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="2599b-322"><a name="Retry"></a> Reintento</span><span class="sxs-lookup"><span data-stu-id="2599b-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="2599b-323">Hola `retry` directiva ejecuta sus directivas secundario una vez y, a continuación, vuelve a intentar su ejecución hasta el reintento de hello `condition` se convierte en `false` o vuelva a intentar `count` está agotada.</span><span class="sxs-lookup"><span data-stu-id="2599b-323">hello             `retry` policy executes its child policies once and then retries their execution until hello retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2599b-324">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="2599b-324">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="2599b-325">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2599b-325">Example</span></span>  
 <span data-ttu-id="2599b-326">Hola después forewarding de solicitud de ejemplo se vuelve a intentar la tooten veces mediante el algoritmo de reintento exponencial.</span><span class="sxs-lookup"><span data-stu-id="2599b-326">In hello following example request forewarding is retried up tooten times using exponential retry algorithm.</span></span> <span data-ttu-id="2599b-327">Puesto que `first-fast-retry` se establece toofalse, todos los intentos de reintento son el algoritmo de reintento de asunto toohello exponsntial.</span><span class="sxs-lookup"><span data-stu-id="2599b-327">Since                    `first-fast-retry` is set toofalse, all retry attempts are subject toohello exponsntial retry algorithm.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="2599b-328">Elementos</span><span class="sxs-lookup"><span data-stu-id="2599b-328">Elements</span></span>  
  
|<span data-ttu-id="2599b-329">Elemento</span><span class="sxs-lookup"><span data-stu-id="2599b-329">Element</span></span>|<span data-ttu-id="2599b-330">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-330">Description</span></span>|<span data-ttu-id="2599b-331">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2599b-332">retry</span><span class="sxs-lookup"><span data-stu-id="2599b-332">retry</span></span>|<span data-ttu-id="2599b-333">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="2599b-333">Root element.</span></span> <span data-ttu-id="2599b-334">Puede contener cualquier otra directiva como elemento secundario.</span><span class="sxs-lookup"><span data-stu-id="2599b-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="2599b-335">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2599b-336">Attributes</span><span class="sxs-lookup"><span data-stu-id="2599b-336">Attributes</span></span>  
  
|<span data-ttu-id="2599b-337">Atributo</span><span class="sxs-lookup"><span data-stu-id="2599b-337">Attribute</span></span>|<span data-ttu-id="2599b-338">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-338">Description</span></span>|<span data-ttu-id="2599b-339">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-339">Required</span></span>|<span data-ttu-id="2599b-340">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="2599b-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="2599b-341">condition</span><span class="sxs-lookup"><span data-stu-id="2599b-341">condition</span></span>|<span data-ttu-id="2599b-342">[Expresión](api-management-policy-expressions.md) o literal booleanos que especifican si los reintentos se deben detener (`false`) o continuar (`true`).</span><span class="sxs-lookup"><span data-stu-id="2599b-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="2599b-343">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-343">Yes</span></span>|<span data-ttu-id="2599b-344">N/D</span><span class="sxs-lookup"><span data-stu-id="2599b-344">N/A</span></span>|  
|<span data-ttu-id="2599b-345">count</span><span class="sxs-lookup"><span data-stu-id="2599b-345">count</span></span>|<span data-ttu-id="2599b-346">Un número positivo que especifica el número máximo de Hola de reintentos tooattempt.</span><span class="sxs-lookup"><span data-stu-id="2599b-346">A positive number specifying hello maximum number of retries tooattempt.</span></span>|<span data-ttu-id="2599b-347">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-347">Yes</span></span>|<span data-ttu-id="2599b-348">N/D</span><span class="sxs-lookup"><span data-stu-id="2599b-348">N/A</span></span>|  
|<span data-ttu-id="2599b-349">interval</span><span class="sxs-lookup"><span data-stu-id="2599b-349">interval</span></span>|<span data-ttu-id="2599b-350">Un número positivo en segundos que especifica el intervalo de espera de hello entre los reintentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-350">A positive number in seconds specifying hello wait interval between hello retry attempts.</span></span>|<span data-ttu-id="2599b-351">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-351">Yes</span></span>|<span data-ttu-id="2599b-352">N/D</span><span class="sxs-lookup"><span data-stu-id="2599b-352">N/A</span></span>|  
|<span data-ttu-id="2599b-353">max-interval</span><span class="sxs-lookup"><span data-stu-id="2599b-353">max-interval</span></span>|<span data-ttu-id="2599b-354">Un número positivo en segundos que especifica el intervalo de espera máximo de saludo entre los reintentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-354">A positive number in seconds specifying hello maximum wait interval between hello retry attempts.</span></span> <span data-ttu-id="2599b-355">Es tooimplement usa un algoritmo exponencial de reintentos.</span><span class="sxs-lookup"><span data-stu-id="2599b-355">It is used tooimplement an exponential retry algorithm.</span></span>|<span data-ttu-id="2599b-356">No</span><span class="sxs-lookup"><span data-stu-id="2599b-356">No</span></span>|<span data-ttu-id="2599b-357">N/D</span><span class="sxs-lookup"><span data-stu-id="2599b-357">N/A</span></span>|  
|<span data-ttu-id="2599b-358">delta</span><span class="sxs-lookup"><span data-stu-id="2599b-358">delta</span></span>|<span data-ttu-id="2599b-359">Un número positivo en segundos que especifica el incremento de intervalo de espera de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-359">A positive number in seconds specifying hello wait interval increment.</span></span> <span data-ttu-id="2599b-360">Es algoritmos de reintento lineal y exponencial de hello tooimplement usado.</span><span class="sxs-lookup"><span data-stu-id="2599b-360">It is used tooimplement hello linear and exponential retry algorithms.</span></span>|<span data-ttu-id="2599b-361">No</span><span class="sxs-lookup"><span data-stu-id="2599b-361">No</span></span>|<span data-ttu-id="2599b-362">N/D</span><span class="sxs-lookup"><span data-stu-id="2599b-362">N/A</span></span>|  
|<span data-ttu-id="2599b-363">first-fast-retry</span><span class="sxs-lookup"><span data-stu-id="2599b-363">first-fast-retry</span></span>|<span data-ttu-id="2599b-364">Si establece demasiado `true` , Hola primer intento de reintento se lleva a cabo inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="2599b-364">If set too                                   `true` , hello first retry attempt is performed immediately.</span></span>|<span data-ttu-id="2599b-365">No</span><span class="sxs-lookup"><span data-stu-id="2599b-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="2599b-366">Cuando solo Hola `interval` se especifica, **fijo** se llevan a cabo los reintentos de intervalo.</span><span class="sxs-lookup"><span data-stu-id="2599b-366">When only hello `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="2599b-367">Cuando solo Hola `interval` y `delta` se especifican, un **lineal** se utiliza el algoritmo de reintento de intervalo, donde el tiempo de espera entre reintentos es calculada Hola correspondiente después fórmula - `interval + (count - 1)*delta`.</span><span class="sxs-lookup"><span data-stu-id="2599b-367">When only hello `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according hello following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="2599b-368">Cuando Hola `interval`, `max-interval` y `delta` se especifican, **exponencial** se aplica el algoritmo de reintento de intervalo, donde está creciendo exponencialmente tiempo de espera de hello entre reintentos de hello del valor de Hola de `interval`valor toohello `max-interval` según siguiente toohello forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span><span class="sxs-lookup"><span data-stu-id="2599b-368">When hello `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where hello wait time between hello retries is growing exponentially from hello value of `interval` toohello value `max-interval` according toohello following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="2599b-369">Uso</span><span class="sxs-lookup"><span data-stu-id="2599b-369">Usage</span></span>  
 <span data-ttu-id="2599b-370">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="2599b-370">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="2599b-371">Tenga en cuenta que esta directiva heredará las restricciones de uso de directivas secundarias.</span><span class="sxs-lookup"><span data-stu-id="2599b-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="2599b-372">**Secciones de la directiva:** entrante, saliente, back-end y en caso de error</span><span class="sxs-lookup"><span data-stu-id="2599b-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2599b-373">**Ámbitos de la directiva:** todos los ámbitos</span><span class="sxs-lookup"><span data-stu-id="2599b-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="2599b-374"><a name="ReturnResponse"></a> Devolución de respuesta</span><span class="sxs-lookup"><span data-stu-id="2599b-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="2599b-375">Hola `return-response` directiva anula la ejecución de la canalización y devuelve un valor predeterminado o el autor de llamada de respuesta personalizada toohello.</span><span class="sxs-lookup"><span data-stu-id="2599b-375">hello `return-response` policy aborts pipeline execution and returns either a default or custom response toohello caller.</span></span> <span data-ttu-id="2599b-376">La respuesta predeterminada es `200 OK` sin cuerpo.</span><span class="sxs-lookup"><span data-stu-id="2599b-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="2599b-377">La respuesta personalizada se puede especificar mediante declaraciones de directiva o variable de contexto.</span><span class="sxs-lookup"><span data-stu-id="2599b-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="2599b-378">Cuando se especifican ambos, respuesta de hello dentro de la variable de contexto de Hola se modifica por las instrucciones de directiva de hello antes de devolverse toohello llamador.</span><span class="sxs-lookup"><span data-stu-id="2599b-378">When both are provided, hello response contained within hello context variable is modified by hello policy statements before being returned toohello caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2599b-379">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="2599b-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="2599b-380">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2599b-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="2599b-381">Elementos</span><span class="sxs-lookup"><span data-stu-id="2599b-381">Elements</span></span>  
  
|<span data-ttu-id="2599b-382">Elemento</span><span class="sxs-lookup"><span data-stu-id="2599b-382">Element</span></span>|<span data-ttu-id="2599b-383">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-383">Description</span></span>|<span data-ttu-id="2599b-384">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2599b-385">return-response</span><span class="sxs-lookup"><span data-stu-id="2599b-385">return-response</span></span>|<span data-ttu-id="2599b-386">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="2599b-386">Root element.</span></span>|<span data-ttu-id="2599b-387">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-387">Yes</span></span>|  
|<span data-ttu-id="2599b-388">set-header</span><span class="sxs-lookup"><span data-stu-id="2599b-388">set-header</span></span>|<span data-ttu-id="2599b-389">Una declaración de directiva [set-header](api-management-transformation-policies.md#SetHTTPheader).</span><span class="sxs-lookup"><span data-stu-id="2599b-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="2599b-390">No</span><span class="sxs-lookup"><span data-stu-id="2599b-390">No</span></span>|  
|<span data-ttu-id="2599b-391">set-body</span><span class="sxs-lookup"><span data-stu-id="2599b-391">set-body</span></span>|<span data-ttu-id="2599b-392">Una declaración de directiva [set-body](api-management-transformation-policies.md#SetBody).</span><span class="sxs-lookup"><span data-stu-id="2599b-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="2599b-393">No</span><span class="sxs-lookup"><span data-stu-id="2599b-393">No</span></span>|  
|<span data-ttu-id="2599b-394">set-status</span><span class="sxs-lookup"><span data-stu-id="2599b-394">set-status</span></span>|<span data-ttu-id="2599b-395">Una declaración de directiva [set-status](api-management-advanced-policies.md#SetStatus).</span><span class="sxs-lookup"><span data-stu-id="2599b-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="2599b-396">No</span><span class="sxs-lookup"><span data-stu-id="2599b-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2599b-397">Attributes</span><span class="sxs-lookup"><span data-stu-id="2599b-397">Attributes</span></span>  
  
|<span data-ttu-id="2599b-398">Atributo</span><span class="sxs-lookup"><span data-stu-id="2599b-398">Attribute</span></span>|<span data-ttu-id="2599b-399">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-399">Description</span></span>|<span data-ttu-id="2599b-400">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="2599b-401">response-variable-name</span><span class="sxs-lookup"><span data-stu-id="2599b-401">response-variable-name</span></span>|<span data-ttu-id="2599b-402">Hello nombre de variable de contexto de hello hace referencia desde, por ejemplo, un nivel superior [solicitud de envío](api-management-advanced-policies.md#SendRequest) directiva y que contiene un `Response` objeto</span><span class="sxs-lookup"><span data-stu-id="2599b-402">hello name of hello context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="2599b-403">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2599b-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2599b-404">Uso</span><span class="sxs-lookup"><span data-stu-id="2599b-404">Usage</span></span>  
 <span data-ttu-id="2599b-405">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="2599b-405">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2599b-406">**Secciones de la directiva:** entrante, saliente, back-end y en caso de error</span><span class="sxs-lookup"><span data-stu-id="2599b-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2599b-407">**Ámbitos de la directiva:** todos los ámbitos</span><span class="sxs-lookup"><span data-stu-id="2599b-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="2599b-408"><a name="SendOneWayRequest"></a> Envío de solicitud unidireccional</span><span class="sxs-lookup"><span data-stu-id="2599b-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="2599b-409">Hola `send-one-way-request` directiva envía toohello especifica la dirección URL sin tener que esperar una respuesta de solicitud de hello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="2599b-409">hello `send-one-way-request` policy sends hello provided request toohello specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2599b-410">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="2599b-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="2599b-411">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2599b-411">Example</span></span>  
 <span data-ttu-id="2599b-412">Esta directiva de ejemplo muestra un ejemplo del uso de hello `send-one-way-request` directiva toosend un mensaje tooa demora salón de chat si Hola código de respuesta HTTP es igual o mayor que too500.</span><span class="sxs-lookup"><span data-stu-id="2599b-412">This sample policy shows an example of using hello `send-one-way-request` policy toosend a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="2599b-413">Para obtener más información acerca de este ejemplo, vea [mediante servicios externos desde el servicio de administración de API de Azure de Hola](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="2599b-413">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="2599b-414">Elementos</span><span class="sxs-lookup"><span data-stu-id="2599b-414">Elements</span></span>  
  
|<span data-ttu-id="2599b-415">Elemento</span><span class="sxs-lookup"><span data-stu-id="2599b-415">Element</span></span>|<span data-ttu-id="2599b-416">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-416">Description</span></span>|<span data-ttu-id="2599b-417">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2599b-418">send-one-way-request</span><span class="sxs-lookup"><span data-stu-id="2599b-418">send-one-way-request</span></span>|<span data-ttu-id="2599b-419">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="2599b-419">Root element.</span></span>|<span data-ttu-id="2599b-420">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-420">Yes</span></span>|  
|<span data-ttu-id="2599b-421">url</span><span class="sxs-lookup"><span data-stu-id="2599b-421">url</span></span>|<span data-ttu-id="2599b-422">Hola dirección URL de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="2599b-422">hello URL of hello request.</span></span>|<span data-ttu-id="2599b-423">No si mode=copy; de lo contrario, sí.</span><span class="sxs-lookup"><span data-stu-id="2599b-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="2599b-424">estático</span><span class="sxs-lookup"><span data-stu-id="2599b-424">method</span></span>|<span data-ttu-id="2599b-425">método HTTP para la solicitud de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-425">hello HTTP method for hello request.</span></span>|<span data-ttu-id="2599b-426">No si mode=copy; de lo contrario, sí.</span><span class="sxs-lookup"><span data-stu-id="2599b-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="2599b-427">encabezado</span><span class="sxs-lookup"><span data-stu-id="2599b-427">header</span></span>|<span data-ttu-id="2599b-428">Encabezado de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="2599b-428">Request header.</span></span> <span data-ttu-id="2599b-429">Utilice varios elementos de encabezado si hay varios encabezados de solicitud.</span><span class="sxs-lookup"><span data-stu-id="2599b-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="2599b-430">No</span><span class="sxs-lookup"><span data-stu-id="2599b-430">No</span></span>|  
|<span data-ttu-id="2599b-431">body</span><span class="sxs-lookup"><span data-stu-id="2599b-431">body</span></span>|<span data-ttu-id="2599b-432">cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="2599b-432">hello request body.</span></span>|<span data-ttu-id="2599b-433">No</span><span class="sxs-lookup"><span data-stu-id="2599b-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2599b-434">Attributes</span><span class="sxs-lookup"><span data-stu-id="2599b-434">Attributes</span></span>  
  
|<span data-ttu-id="2599b-435">Atributo</span><span class="sxs-lookup"><span data-stu-id="2599b-435">Attribute</span></span>|<span data-ttu-id="2599b-436">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-436">Description</span></span>|<span data-ttu-id="2599b-437">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-437">Required</span></span>|<span data-ttu-id="2599b-438">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="2599b-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="2599b-439">mode="cadena"</span><span class="sxs-lookup"><span data-stu-id="2599b-439">mode="string"</span></span>|<span data-ttu-id="2599b-440">Determina si se trata de una nueva solicitud o una copia de la solicitud actual Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-440">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="2599b-441">En el modo de salida, modo = copia no inicializa el cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="2599b-441">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="2599b-442">No</span><span class="sxs-lookup"><span data-stu-id="2599b-442">No</span></span>|<span data-ttu-id="2599b-443">Nuevo</span><span class="sxs-lookup"><span data-stu-id="2599b-443">New</span></span>|  
|<span data-ttu-id="2599b-444">name</span><span class="sxs-lookup"><span data-stu-id="2599b-444">name</span></span>|<span data-ttu-id="2599b-445">Especifica el nombre de Hola de hello encabezado toobe conjunto.</span><span class="sxs-lookup"><span data-stu-id="2599b-445">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="2599b-446">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-446">Yes</span></span>|<span data-ttu-id="2599b-447">N/D</span><span class="sxs-lookup"><span data-stu-id="2599b-447">N/A</span></span>|  
|<span data-ttu-id="2599b-448">exists-action</span><span class="sxs-lookup"><span data-stu-id="2599b-448">exists-action</span></span>|<span data-ttu-id="2599b-449">Especifica qué tootake acción cuando ya se ha especificado el encabezado de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-449">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="2599b-450">Este atributo debe tener uno de hello después de valores.</span><span class="sxs-lookup"><span data-stu-id="2599b-450">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="2599b-451">-invalidar - reemplaza Hola valor del encabezado existente Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-451">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="2599b-452">-skip: no reemplaza el valor del encabezado de hello existente.</span><span class="sxs-lookup"><span data-stu-id="2599b-452">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="2599b-453">-append: anexa el valor del encabezado existente Hola valor toohello.</span><span class="sxs-lookup"><span data-stu-id="2599b-453">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="2599b-454">-delete: quita el encabezado de saludo de solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-454">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="2599b-455">Cuando se establece demasiado`override` al enumerar varias entradas con hello igual nombre resultados en el encabezado de Hola que se va a entradas correspondiente del conjunto tooall (que aparecerán enumeradas varias veces); solo los valores mostrados se establecerá en el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="2599b-455">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="2599b-456">No</span><span class="sxs-lookup"><span data-stu-id="2599b-456">No</span></span>|<span data-ttu-id="2599b-457">override</span><span class="sxs-lookup"><span data-stu-id="2599b-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2599b-458">Uso</span><span class="sxs-lookup"><span data-stu-id="2599b-458">Usage</span></span>  
 <span data-ttu-id="2599b-459">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="2599b-459">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2599b-460">**Secciones de la directiva:** entrante, saliente, back-end y en caso de error</span><span class="sxs-lookup"><span data-stu-id="2599b-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2599b-461">**Ámbitos de la directiva:** todos los ámbitos</span><span class="sxs-lookup"><span data-stu-id="2599b-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="2599b-462"><a name="SendRequest"></a> Envío de solicitud</span><span class="sxs-lookup"><span data-stu-id="2599b-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="2599b-463">Hola `send-request` directiva envía toohello especifica la dirección URL, ya no se espera que Hola establece valor de tiempo de espera de solicitud de hello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="2599b-463">hello `send-request` policy sends hello provided request toohello specified URL, waiting no longer than hello set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2599b-464">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="2599b-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="2599b-465">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2599b-465">Example</span></span>  
 <span data-ttu-id="2599b-466">Este ejemplo muestra una manera de tooverify un token de referencia con un servidor de autorización.</span><span class="sxs-lookup"><span data-stu-id="2599b-466">This example shows one way tooverify a reference token with an authorization server.</span></span> <span data-ttu-id="2599b-467">Para obtener más información acerca de este ejemplo, vea [mediante servicios externos desde el servicio de administración de API de Azure de Hola](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="2599b-467">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="2599b-468">Elementos</span><span class="sxs-lookup"><span data-stu-id="2599b-468">Elements</span></span>  
  
|<span data-ttu-id="2599b-469">Elemento</span><span class="sxs-lookup"><span data-stu-id="2599b-469">Element</span></span>|<span data-ttu-id="2599b-470">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-470">Description</span></span>|<span data-ttu-id="2599b-471">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2599b-472">send-request</span><span class="sxs-lookup"><span data-stu-id="2599b-472">send-request</span></span>|<span data-ttu-id="2599b-473">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="2599b-473">Root element.</span></span>|<span data-ttu-id="2599b-474">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-474">Yes</span></span>|  
|<span data-ttu-id="2599b-475">url</span><span class="sxs-lookup"><span data-stu-id="2599b-475">url</span></span>|<span data-ttu-id="2599b-476">Hola dirección URL de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="2599b-476">hello URL of hello request.</span></span>|<span data-ttu-id="2599b-477">No si mode=copy; de lo contrario, sí.</span><span class="sxs-lookup"><span data-stu-id="2599b-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="2599b-478">estático</span><span class="sxs-lookup"><span data-stu-id="2599b-478">method</span></span>|<span data-ttu-id="2599b-479">método HTTP para la solicitud de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-479">hello HTTP method for hello request.</span></span>|<span data-ttu-id="2599b-480">No si mode=copy; de lo contrario, sí.</span><span class="sxs-lookup"><span data-stu-id="2599b-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="2599b-481">encabezado</span><span class="sxs-lookup"><span data-stu-id="2599b-481">header</span></span>|<span data-ttu-id="2599b-482">Encabezado de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="2599b-482">Request header.</span></span> <span data-ttu-id="2599b-483">Utilice varios elementos de encabezado si hay varios encabezados de solicitud.</span><span class="sxs-lookup"><span data-stu-id="2599b-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="2599b-484">No</span><span class="sxs-lookup"><span data-stu-id="2599b-484">No</span></span>|  
|<span data-ttu-id="2599b-485">body</span><span class="sxs-lookup"><span data-stu-id="2599b-485">body</span></span>|<span data-ttu-id="2599b-486">cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="2599b-486">hello request body.</span></span>|<span data-ttu-id="2599b-487">No</span><span class="sxs-lookup"><span data-stu-id="2599b-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2599b-488">Attributes</span><span class="sxs-lookup"><span data-stu-id="2599b-488">Attributes</span></span>  
  
|<span data-ttu-id="2599b-489">Atributo</span><span class="sxs-lookup"><span data-stu-id="2599b-489">Attribute</span></span>|<span data-ttu-id="2599b-490">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-490">Description</span></span>|<span data-ttu-id="2599b-491">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-491">Required</span></span>|<span data-ttu-id="2599b-492">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="2599b-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="2599b-493">mode="cadena"</span><span class="sxs-lookup"><span data-stu-id="2599b-493">mode="string"</span></span>|<span data-ttu-id="2599b-494">Determina si se trata de una nueva solicitud o una copia de la solicitud actual Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-494">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="2599b-495">En el modo de salida, modo = copia no inicializa el cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="2599b-495">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="2599b-496">No</span><span class="sxs-lookup"><span data-stu-id="2599b-496">No</span></span>|<span data-ttu-id="2599b-497">Nuevo</span><span class="sxs-lookup"><span data-stu-id="2599b-497">New</span></span>|  
|<span data-ttu-id="2599b-498">response-variable-name="cadena"</span><span class="sxs-lookup"><span data-stu-id="2599b-498">response-variable-name="string"</span></span>|<span data-ttu-id="2599b-499">Si no está presente, se utiliza `context.Response`.</span><span class="sxs-lookup"><span data-stu-id="2599b-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="2599b-500">No</span><span class="sxs-lookup"><span data-stu-id="2599b-500">No</span></span>|<span data-ttu-id="2599b-501">N/D</span><span class="sxs-lookup"><span data-stu-id="2599b-501">N/A</span></span>|  
|<span data-ttu-id="2599b-502">timeout="entero"</span><span class="sxs-lookup"><span data-stu-id="2599b-502">timeout="integer"</span></span>|<span data-ttu-id="2599b-503">intervalo de tiempo de espera de saludo en segundos antes de la llamada de hello toohello URL se produce un error.</span><span class="sxs-lookup"><span data-stu-id="2599b-503">hello timeout interval in seconds before hello call toohello URL fails.</span></span>|<span data-ttu-id="2599b-504">No</span><span class="sxs-lookup"><span data-stu-id="2599b-504">No</span></span>|<span data-ttu-id="2599b-505">60</span><span class="sxs-lookup"><span data-stu-id="2599b-505">60</span></span>|  
|<span data-ttu-id="2599b-506">ignore-error</span><span class="sxs-lookup"><span data-stu-id="2599b-506">ignore-error</span></span>|<span data-ttu-id="2599b-507">Si se produce un error de solicitud de hello y true:</span><span class="sxs-lookup"><span data-stu-id="2599b-507">If true and hello request results in an error:</span></span><br /><br /> <span data-ttu-id="2599b-508">-   Si se especificó response-variable-name, contendrá un valor nulo.</span><span class="sxs-lookup"><span data-stu-id="2599b-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="2599b-509">-   Si no se especificó response-variable-name, no se actualizará context.Request.</span><span class="sxs-lookup"><span data-stu-id="2599b-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="2599b-510">No</span><span class="sxs-lookup"><span data-stu-id="2599b-510">No</span></span>|<span data-ttu-id="2599b-511">false</span><span class="sxs-lookup"><span data-stu-id="2599b-511">false</span></span>|  
|<span data-ttu-id="2599b-512">name</span><span class="sxs-lookup"><span data-stu-id="2599b-512">name</span></span>|<span data-ttu-id="2599b-513">Especifica el nombre de Hola de hello encabezado toobe conjunto.</span><span class="sxs-lookup"><span data-stu-id="2599b-513">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="2599b-514">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-514">Yes</span></span>|<span data-ttu-id="2599b-515">N/D</span><span class="sxs-lookup"><span data-stu-id="2599b-515">N/A</span></span>|  
|<span data-ttu-id="2599b-516">exists-action</span><span class="sxs-lookup"><span data-stu-id="2599b-516">exists-action</span></span>|<span data-ttu-id="2599b-517">Especifica qué tootake acción cuando ya se ha especificado el encabezado de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-517">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="2599b-518">Este atributo debe tener uno de hello después de valores.</span><span class="sxs-lookup"><span data-stu-id="2599b-518">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="2599b-519">-invalidar - reemplaza Hola valor del encabezado existente Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-519">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="2599b-520">-skip: no reemplaza el valor del encabezado de hello existente.</span><span class="sxs-lookup"><span data-stu-id="2599b-520">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="2599b-521">-append: anexa el valor del encabezado existente Hola valor toohello.</span><span class="sxs-lookup"><span data-stu-id="2599b-521">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="2599b-522">-delete: quita el encabezado de saludo de solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-522">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="2599b-523">Cuando se establece demasiado`override` al enumerar varias entradas con hello igual nombre resultados en el encabezado de Hola que se va a entradas correspondiente del conjunto tooall (que aparecerán enumeradas varias veces); solo los valores mostrados se establecerá en el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="2599b-523">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="2599b-524">No</span><span class="sxs-lookup"><span data-stu-id="2599b-524">No</span></span>|<span data-ttu-id="2599b-525">override</span><span class="sxs-lookup"><span data-stu-id="2599b-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2599b-526">Uso</span><span class="sxs-lookup"><span data-stu-id="2599b-526">Usage</span></span>  
 <span data-ttu-id="2599b-527">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="2599b-527">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2599b-528">**Secciones de la directiva:** entrante, saliente, back-end y en caso de error</span><span class="sxs-lookup"><span data-stu-id="2599b-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2599b-529">**Ámbitos de la directiva:** todos los ámbitos</span><span class="sxs-lookup"><span data-stu-id="2599b-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="2599b-530"><a name="SetHttpProxy"></a> Establecer proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="2599b-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="2599b-531">Hola `proxy` directiva permite tooroute toobackends de las solicitudes que se reenvían a través de un proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="2599b-531">hello `proxy` policy allows you tooroute requests forwarded toobackends via an HTTP proxy.</span></span> <span data-ttu-id="2599b-532">Se admite solo HTTP (no HTTPS) entre la puerta de enlace de Hola y el proxy de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-532">Only HTTP (not HTTPS) is supported between hello gateway and hello proxy.</span></span> <span data-ttu-id="2599b-533">Solo autenticación básica y NTLM.</span><span class="sxs-lookup"><span data-stu-id="2599b-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="2599b-534">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="2599b-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="2599b-535">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2599b-535">Example</span></span>  
<span data-ttu-id="2599b-536">Tenga en cuenta uso Hola de [propiedades](api-management-howto-properties.md) como valores de hello tooavoid de nombre de usuario y contraseña almacenar información confidencial en el documento de directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-536">Note hello use of [properties](api-management-howto-properties.md) as values of hello username and password tooavoid storing sensitive information in hello policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="2599b-537">Elementos</span><span class="sxs-lookup"><span data-stu-id="2599b-537">Elements</span></span>  
  
|<span data-ttu-id="2599b-538">Elemento</span><span class="sxs-lookup"><span data-stu-id="2599b-538">Element</span></span>|<span data-ttu-id="2599b-539">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-539">Description</span></span>|<span data-ttu-id="2599b-540">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2599b-541">proxy</span><span class="sxs-lookup"><span data-stu-id="2599b-541">proxy</span></span>|<span data-ttu-id="2599b-542">Elemento raíz</span><span class="sxs-lookup"><span data-stu-id="2599b-542">Root element</span></span>|<span data-ttu-id="2599b-543">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="2599b-544">Attributes</span><span class="sxs-lookup"><span data-stu-id="2599b-544">Attributes</span></span>  
  
|<span data-ttu-id="2599b-545">Atributo</span><span class="sxs-lookup"><span data-stu-id="2599b-545">Attribute</span></span>|<span data-ttu-id="2599b-546">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-546">Description</span></span>|<span data-ttu-id="2599b-547">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-547">Required</span></span>|<span data-ttu-id="2599b-548">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="2599b-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="2599b-549">url="string"</span><span class="sxs-lookup"><span data-stu-id="2599b-549">url="string"</span></span>|<span data-ttu-id="2599b-550">Dirección URL del proxy en forma de Hola de http://host: Port.</span><span class="sxs-lookup"><span data-stu-id="2599b-550">Proxy URL in hello form of http://host:port.</span></span>|<span data-ttu-id="2599b-551">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-551">Yes</span></span>|<span data-ttu-id="2599b-552">N/D</span><span class="sxs-lookup"><span data-stu-id="2599b-552">N/A</span></span>|  
|<span data-ttu-id="2599b-553">username="string"</span><span class="sxs-lookup"><span data-stu-id="2599b-553">username="string"</span></span>|<span data-ttu-id="2599b-554">Toobe de nombre de usuario utilizado para la autenticación con el proxy de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-554">Username toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="2599b-555">No</span><span class="sxs-lookup"><span data-stu-id="2599b-555">No</span></span>|<span data-ttu-id="2599b-556">N/D</span><span class="sxs-lookup"><span data-stu-id="2599b-556">N/A</span></span>|  
|<span data-ttu-id="2599b-557">password="string"</span><span class="sxs-lookup"><span data-stu-id="2599b-557">password="string"</span></span>|<span data-ttu-id="2599b-558">Toobe de contraseña que se usa para la autenticación con el proxy de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-558">Password toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="2599b-559">No</span><span class="sxs-lookup"><span data-stu-id="2599b-559">No</span></span>|<span data-ttu-id="2599b-560">N/D</span><span class="sxs-lookup"><span data-stu-id="2599b-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="2599b-561">Uso</span><span class="sxs-lookup"><span data-stu-id="2599b-561">Usage</span></span>  
 <span data-ttu-id="2599b-562">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="2599b-562">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2599b-563">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="2599b-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="2599b-564">**Ámbitos de la directiva:** todos los ámbitos</span><span class="sxs-lookup"><span data-stu-id="2599b-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="2599b-565"><a name="SetRequestMethod"></a> Establecimiento de método de solicitud</span><span class="sxs-lookup"><span data-stu-id="2599b-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="2599b-566">Hola `set-method` directiva permite un método de solicitud de toochange Hola HTTP para una solicitud.</span><span class="sxs-lookup"><span data-stu-id="2599b-566">hello `set-method` policy allows you toochange hello HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2599b-567">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="2599b-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="2599b-568">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2599b-568">Example</span></span>  
 <span data-ttu-id="2599b-569">Esta directiva de ejemplo que usa hello `set-method` directiva muestra un ejemplo de envío de un salón de chat de mensaje tooa demora si Hola código de respuesta HTTP es mayor que o igual too500.</span><span class="sxs-lookup"><span data-stu-id="2599b-569">This sample policy that uses hello `set-method` policy shows an example of sending a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="2599b-570">Para obtener más información acerca de este ejemplo, vea [mediante servicios externos desde el servicio de administración de API de Azure de Hola](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="2599b-570">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="2599b-571">Elementos</span><span class="sxs-lookup"><span data-stu-id="2599b-571">Elements</span></span>  
  
|<span data-ttu-id="2599b-572">Elemento</span><span class="sxs-lookup"><span data-stu-id="2599b-572">Element</span></span>|<span data-ttu-id="2599b-573">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-573">Description</span></span>|<span data-ttu-id="2599b-574">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2599b-575">set-method</span><span class="sxs-lookup"><span data-stu-id="2599b-575">set-method</span></span>|<span data-ttu-id="2599b-576">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="2599b-576">Root element.</span></span> <span data-ttu-id="2599b-577">valor de Hola de elemento de Hola especifica método HTTP de hello.</span><span class="sxs-lookup"><span data-stu-id="2599b-577">hello value of hello element specifies hello HTTP method.</span></span>|<span data-ttu-id="2599b-578">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2599b-579">Uso</span><span class="sxs-lookup"><span data-stu-id="2599b-579">Usage</span></span>  
 <span data-ttu-id="2599b-580">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="2599b-580">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2599b-581">**Secciones de la directiva:** entrante y en caso de error</span><span class="sxs-lookup"><span data-stu-id="2599b-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="2599b-582">**Ámbitos de la directiva:** todos los ámbitos</span><span class="sxs-lookup"><span data-stu-id="2599b-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="2599b-583"><a name="SetStatus"></a> Establecimiento de código de estado</span><span class="sxs-lookup"><span data-stu-id="2599b-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="2599b-584">Hola `set-status` toohello de código de estado de directiva establece Hola HTTP valor especificado.</span><span class="sxs-lookup"><span data-stu-id="2599b-584">hello `set-status` policy sets hello HTTP status code toohello specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2599b-585">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="2599b-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="2599b-586">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2599b-586">Example</span></span>  
 <span data-ttu-id="2599b-587">Este ejemplo se muestra cómo tooreturn una respuesta 401 si el token de autorización de hello no es válido.</span><span class="sxs-lookup"><span data-stu-id="2599b-587">This example shows how tooreturn a 401 response if hello authorization token is invalid.</span></span> <span data-ttu-id="2599b-588">Para obtener más información, vea [mediante servicios externos de hello servicio de administración de API de Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span><span class="sxs-lookup"><span data-stu-id="2599b-588">For more information, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="2599b-589">Elementos</span><span class="sxs-lookup"><span data-stu-id="2599b-589">Elements</span></span>  
  
|<span data-ttu-id="2599b-590">Elemento</span><span class="sxs-lookup"><span data-stu-id="2599b-590">Element</span></span>|<span data-ttu-id="2599b-591">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-591">Description</span></span>|<span data-ttu-id="2599b-592">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2599b-593">set-status</span><span class="sxs-lookup"><span data-stu-id="2599b-593">set-status</span></span>|<span data-ttu-id="2599b-594">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="2599b-594">Root element.</span></span>|<span data-ttu-id="2599b-595">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2599b-596">Attributes</span><span class="sxs-lookup"><span data-stu-id="2599b-596">Attributes</span></span>  
  
|<span data-ttu-id="2599b-597">Atributo</span><span class="sxs-lookup"><span data-stu-id="2599b-597">Attribute</span></span>|<span data-ttu-id="2599b-598">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-598">Description</span></span>|<span data-ttu-id="2599b-599">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-599">Required</span></span>|<span data-ttu-id="2599b-600">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="2599b-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="2599b-601">code="entero"</span><span class="sxs-lookup"><span data-stu-id="2599b-601">code="integer"</span></span>|<span data-ttu-id="2599b-602">Hola HTTP tooreturn de código de estado.</span><span class="sxs-lookup"><span data-stu-id="2599b-602">hello HTTP status code tooreturn.</span></span>|<span data-ttu-id="2599b-603">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-603">Yes</span></span>|<span data-ttu-id="2599b-604">N/D</span><span class="sxs-lookup"><span data-stu-id="2599b-604">N/A</span></span>|  
|<span data-ttu-id="2599b-605">reason="cadena"</span><span class="sxs-lookup"><span data-stu-id="2599b-605">reason="string"</span></span>|<span data-ttu-id="2599b-606">Descripción del motivo de Hola para devolver el código de estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-606">A description of hello reason for returning hello status code.</span></span>|<span data-ttu-id="2599b-607">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-607">Yes</span></span>|<span data-ttu-id="2599b-608">N/D</span><span class="sxs-lookup"><span data-stu-id="2599b-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2599b-609">Uso</span><span class="sxs-lookup"><span data-stu-id="2599b-609">Usage</span></span>  
 <span data-ttu-id="2599b-610">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="2599b-610">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2599b-611">**Secciones de la directiva:** saliente, back-end y en caso de error</span><span class="sxs-lookup"><span data-stu-id="2599b-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2599b-612">**Ámbitos de la directiva:** todos los ámbitos</span><span class="sxs-lookup"><span data-stu-id="2599b-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="2599b-613"><a name="set-variable"></a> Establecimiento de variable</span><span class="sxs-lookup"><span data-stu-id="2599b-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="2599b-614">Hola `set-variable` directiva declara un [contexto](api-management-policy-expressions.md#ContextVariables) variable y le asigna un valor especificado a través de un [expresión](api-management-policy-expressions.md) o un literal de cadena.</span><span class="sxs-lookup"><span data-stu-id="2599b-614">hello `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="2599b-615">Si expresión de hello contiene un valor literal se convertirán tooa tipo hello y de cadena del valor de hello será `System.String`.</span><span class="sxs-lookup"><span data-stu-id="2599b-615">if hello expression contains a literal it will be converted tooa string and hello type of hello value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="2599b-616"><a name="set-variablePolicyStatement"></a> Declaración de la directiva</span><span class="sxs-lookup"><span data-stu-id="2599b-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="2599b-617"><a name="set-variableExample"></a> Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2599b-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="2599b-618">Hello en el ejemplo siguiente se muestra una directiva de variable establecida en hello sección de entrada.</span><span class="sxs-lookup"><span data-stu-id="2599b-618">hello following example demonstrates a set variable policy in hello inbound section.</span></span> <span data-ttu-id="2599b-619">Esta directiva de variable establecida crea una `isMobile` booleano [contexto](api-management-policy-expressions.md#ContextVariables) variable que se establece tootrue si hello `User-Agent` solicitud encabezado contiene texto hello `iPad` o `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="2599b-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="2599b-620">Elementos</span><span class="sxs-lookup"><span data-stu-id="2599b-620">Elements</span></span>  
  
|<span data-ttu-id="2599b-621">Elemento</span><span class="sxs-lookup"><span data-stu-id="2599b-621">Element</span></span>|<span data-ttu-id="2599b-622">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-622">Description</span></span>|<span data-ttu-id="2599b-623">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2599b-624">set-variable</span><span class="sxs-lookup"><span data-stu-id="2599b-624">set-variable</span></span>|<span data-ttu-id="2599b-625">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="2599b-625">Root element.</span></span>|<span data-ttu-id="2599b-626">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2599b-627">Attributes</span><span class="sxs-lookup"><span data-stu-id="2599b-627">Attributes</span></span>  
  
|<span data-ttu-id="2599b-628">Atributo</span><span class="sxs-lookup"><span data-stu-id="2599b-628">Attribute</span></span>|<span data-ttu-id="2599b-629">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-629">Description</span></span>|<span data-ttu-id="2599b-630">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="2599b-631">name</span><span class="sxs-lookup"><span data-stu-id="2599b-631">name</span></span>|<span data-ttu-id="2599b-632">nombre de Hola de variable de saludo.</span><span class="sxs-lookup"><span data-stu-id="2599b-632">hello name of hello variable.</span></span>|<span data-ttu-id="2599b-633">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-633">Yes</span></span>|  
|<span data-ttu-id="2599b-634">value</span><span class="sxs-lookup"><span data-stu-id="2599b-634">value</span></span>|<span data-ttu-id="2599b-635">valor de Hola de variable de saludo.</span><span class="sxs-lookup"><span data-stu-id="2599b-635">hello value of hello variable.</span></span> <span data-ttu-id="2599b-636">Puede ser una expresión o un valor literal.</span><span class="sxs-lookup"><span data-stu-id="2599b-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="2599b-637">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2599b-638">Uso</span><span class="sxs-lookup"><span data-stu-id="2599b-638">Usage</span></span>  
 <span data-ttu-id="2599b-639">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="2599b-639">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2599b-640">**Secciones de la directiva:** entrante, saliente, back-end y en caso de error</span><span class="sxs-lookup"><span data-stu-id="2599b-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2599b-641">**Ámbitos de la directiva:** todos los ámbitos</span><span class="sxs-lookup"><span data-stu-id="2599b-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="2599b-642"><a name="set-variableAllowedTypes"></a> Tipos permitidos</span><span class="sxs-lookup"><span data-stu-id="2599b-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="2599b-643">Las expresiones usadas en hello `set-variable` directiva debe devolver uno de los siguientes tipos básicos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-643">Expressions used in hello `set-variable` policy must return one of hello following basic types.</span></span>  
  
-   <span data-ttu-id="2599b-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="2599b-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="2599b-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="2599b-645">System.SByte</span></span>  
  
-   <span data-ttu-id="2599b-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="2599b-646">System.Byte</span></span>  
  
-   <span data-ttu-id="2599b-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="2599b-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="2599b-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="2599b-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="2599b-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="2599b-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="2599b-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="2599b-650">System.Int16</span></span>  
  
-   <span data-ttu-id="2599b-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="2599b-651">System.Int32</span></span>  
  
-   <span data-ttu-id="2599b-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="2599b-652">System.Int64</span></span>  
  
-   <span data-ttu-id="2599b-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="2599b-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="2599b-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="2599b-654">System.Single</span></span>  
  
-   <span data-ttu-id="2599b-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="2599b-655">System.Double</span></span>  
  
-   <span data-ttu-id="2599b-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="2599b-656">System.Guid</span></span>  
  
-   <span data-ttu-id="2599b-657">System.String</span><span class="sxs-lookup"><span data-stu-id="2599b-657">System.String</span></span>  
  
-   <span data-ttu-id="2599b-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="2599b-658">System.Char</span></span>  
  
-   <span data-ttu-id="2599b-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="2599b-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="2599b-660">System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2599b-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="2599b-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="2599b-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="2599b-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="2599b-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="2599b-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="2599b-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="2599b-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="2599b-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="2599b-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="2599b-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="2599b-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="2599b-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="2599b-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="2599b-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="2599b-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="2599b-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="2599b-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="2599b-669">System.Single?</span></span>  
  
-   <span data-ttu-id="2599b-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="2599b-670">System.Double?</span></span>  
  
-   <span data-ttu-id="2599b-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="2599b-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="2599b-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="2599b-672">System.String?</span></span>  
  
-   <span data-ttu-id="2599b-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="2599b-673">System.Char?</span></span>  
  
-   <span data-ttu-id="2599b-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="2599b-674">System.DateTime?</span></span>  

##  <span data-ttu-id="2599b-675"><a name="Trace"></a> Seguimiento</span><span class="sxs-lookup"><span data-stu-id="2599b-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="2599b-676">Hola `trace` directiva agrega una cadena en hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) salida.</span><span class="sxs-lookup"><span data-stu-id="2599b-676">hello             `trace` policy adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="2599b-677">Hello directiva ejecutará solamente cuando el seguimiento se activa, es decir, `Ocp-Apim-Trace` encabezado de solicitud está presente y establecido demasiado`true` y `Ocp-Apim-Subscription-Key` encabezado de solicitud está presente y contiene una clave válida asociada con la cuenta de administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="2599b-677">hello policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set too`true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with hello admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2599b-678">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="2599b-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="2599b-679">Elementos</span><span class="sxs-lookup"><span data-stu-id="2599b-679">Elements</span></span>  
  
|<span data-ttu-id="2599b-680">Elemento</span><span class="sxs-lookup"><span data-stu-id="2599b-680">Element</span></span>|<span data-ttu-id="2599b-681">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-681">Description</span></span>|<span data-ttu-id="2599b-682">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2599b-683">trace</span><span class="sxs-lookup"><span data-stu-id="2599b-683">trace</span></span>|<span data-ttu-id="2599b-684">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="2599b-684">Root element.</span></span>|<span data-ttu-id="2599b-685">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2599b-686">Attributes</span><span class="sxs-lookup"><span data-stu-id="2599b-686">Attributes</span></span>  
  
|<span data-ttu-id="2599b-687">Atributo</span><span class="sxs-lookup"><span data-stu-id="2599b-687">Attribute</span></span>|<span data-ttu-id="2599b-688">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-688">Description</span></span>|<span data-ttu-id="2599b-689">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-689">Required</span></span>|<span data-ttu-id="2599b-690">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="2599b-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="2599b-691">de origen</span><span class="sxs-lookup"><span data-stu-id="2599b-691">source</span></span>|<span data-ttu-id="2599b-692">Visor de seguimiento de toohello significativo literal de cadena y especificar origen Hola de mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="2599b-692">String literal meaningful toohello trace viewer and specifying hello source of hello message.</span></span>|<span data-ttu-id="2599b-693">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-693">Yes</span></span>|<span data-ttu-id="2599b-694">N/D</span><span class="sxs-lookup"><span data-stu-id="2599b-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2599b-695">Uso</span><span class="sxs-lookup"><span data-stu-id="2599b-695">Usage</span></span>  
 <span data-ttu-id="2599b-696">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="2599b-696">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="2599b-697">**Secciones de la directiva:** entrante, saliente, back-end y en caso de error</span><span class="sxs-lookup"><span data-stu-id="2599b-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2599b-698">**Ámbitos de la directiva:** todos los ámbitos</span><span class="sxs-lookup"><span data-stu-id="2599b-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="2599b-699"><a name="Wait"></a> Espera</span><span class="sxs-lookup"><span data-stu-id="2599b-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="2599b-700">Hola `wait` directiva ejecuta sus directivas secundarios inmediatos en paralelo y espera para la totalidad o una de su toocomplete de directivas secundarios inmediatos antes de que finalice.</span><span class="sxs-lookup"><span data-stu-id="2599b-700">hello `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies toocomplete before it completes.</span></span> <span data-ttu-id="2599b-701">Hello espera directiva puede tener sus directivas secundarios inmediatos [solicitud de envío](api-management-advanced-policies.md#SendRequest), [obtener el valor de caché](api-management-caching-policies.md#GetFromCacheByKey), y [flujo de Control](api-management-advanced-policies.md#choose) directivas.</span><span class="sxs-lookup"><span data-stu-id="2599b-701">hello wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2599b-702">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="2599b-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="2599b-703">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2599b-703">Example</span></span>  
 <span data-ttu-id="2599b-704">En el siguiente ejemplo de Hola hay dos `choose` directivas como directivas de secundarios inmediatos de hello `wait` directiva.</span><span class="sxs-lookup"><span data-stu-id="2599b-704">In hello following example there are two `choose` policies as immediate child policies of hello `wait` policy.</span></span> <span data-ttu-id="2599b-705">Cada una de estas directivas `choose` se ejecuta en paralelo.</span><span class="sxs-lookup"><span data-stu-id="2599b-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="2599b-706">Cada `choose` directiva intenta tooretrieve un valor almacenado en caché.</span><span class="sxs-lookup"><span data-stu-id="2599b-706">Each `choose` policy attempts tooretrieve a cached value.</span></span> <span data-ttu-id="2599b-707">Si se produce un error de caché, un servicio back-end se denomina valor de Hola de tooprovide.</span><span class="sxs-lookup"><span data-stu-id="2599b-707">If there is a cache miss, a backend service is called tooprovide hello value.</span></span> <span data-ttu-id="2599b-708">En este Hola ejemplo `wait` directiva no se completa hasta que se completen todas sus directivas secundarios inmediatos, porque hello `for` atributo está establecido demasiado`all`.</span><span class="sxs-lookup"><span data-stu-id="2599b-708">In this example hello `wait` policy does not complete until all of its immediate child policies complete, because hello `for` attribute is set too`all`.</span></span>   <span data-ttu-id="2599b-709">En este variables de contexto de ejemplo Hola (`execute-branch-one`, `value-one`, `execute-branch-two`, y `value-two`) se declaran fuera del ámbito de Hola de esta directiva de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2599b-709">In this example hello context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of hello scope of this example policy.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="2599b-710">Elementos</span><span class="sxs-lookup"><span data-stu-id="2599b-710">Elements</span></span>  
  
|<span data-ttu-id="2599b-711">Elemento</span><span class="sxs-lookup"><span data-stu-id="2599b-711">Element</span></span>|<span data-ttu-id="2599b-712">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-712">Description</span></span>|<span data-ttu-id="2599b-713">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2599b-714">wait</span><span class="sxs-lookup"><span data-stu-id="2599b-714">wait</span></span>|<span data-ttu-id="2599b-715">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="2599b-715">Root element.</span></span> <span data-ttu-id="2599b-716">Solo puede contener como elementos secundarios a las directivas `send-request`, `cache-lookup-value` y `choose`.</span><span class="sxs-lookup"><span data-stu-id="2599b-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="2599b-717">Sí</span><span class="sxs-lookup"><span data-stu-id="2599b-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2599b-718">Attributes</span><span class="sxs-lookup"><span data-stu-id="2599b-718">Attributes</span></span>  
  
|<span data-ttu-id="2599b-719">Atributo</span><span class="sxs-lookup"><span data-stu-id="2599b-719">Attribute</span></span>|<span data-ttu-id="2599b-720">Descripción</span><span class="sxs-lookup"><span data-stu-id="2599b-720">Description</span></span>|<span data-ttu-id="2599b-721">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2599b-721">Required</span></span>|<span data-ttu-id="2599b-722">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="2599b-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="2599b-723">for</span><span class="sxs-lookup"><span data-stu-id="2599b-723">for</span></span>|<span data-ttu-id="2599b-724">Determina si hello `wait` directiva esperará a que todos los toobe de directivas de secundarios inmediatos completado o solo uno.</span><span class="sxs-lookup"><span data-stu-id="2599b-724">Determines whether hello `wait` policy waits for all immediate child policies toobe completed or just one.</span></span> <span data-ttu-id="2599b-725">Los valores permitidos son:</span><span class="sxs-lookup"><span data-stu-id="2599b-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="2599b-726">-   `all`-Espere a que todos los secundarios inmediatos directivas toocomplete</span><span class="sxs-lookup"><span data-stu-id="2599b-726">-   `all` - wait for all immediate child policies toocomplete</span></span><br /><span data-ttu-id="2599b-727">-- Espere cualquier toocomplete de directiva secundarios inmediatos.</span><span class="sxs-lookup"><span data-stu-id="2599b-727">-   any - wait for any immediate child policy toocomplete.</span></span> <span data-ttu-id="2599b-728">Cuando haya completado la primera directiva de secundarios inmediatos de hello, Hola `wait` directiva completa y finaliza la ejecución de cualquier otra directiva secundarios inmediatos.</span><span class="sxs-lookup"><span data-stu-id="2599b-728">Once hello first immediate child policy has completed, hello `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="2599b-729">No</span><span class="sxs-lookup"><span data-stu-id="2599b-729">No</span></span>|<span data-ttu-id="2599b-730">todas</span><span class="sxs-lookup"><span data-stu-id="2599b-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2599b-731">Uso</span><span class="sxs-lookup"><span data-stu-id="2599b-731">Usage</span></span>  
 <span data-ttu-id="2599b-732">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="2599b-732">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2599b-733">**Secciones de la directiva:** entrante, saliente y back-end</span><span class="sxs-lookup"><span data-stu-id="2599b-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="2599b-734">**Ámbitos de la directiva:** todos los ámbitos</span><span class="sxs-lookup"><span data-stu-id="2599b-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="2599b-735">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2599b-735">Next steps</span></span>
<span data-ttu-id="2599b-736">Para obtener más información sobre cómo trabajar con directivas, consulte:</span><span class="sxs-lookup"><span data-stu-id="2599b-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="2599b-737">Directivas de Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="2599b-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="2599b-738">Policy expressions (Expresiones de directiva)</span><span class="sxs-lookup"><span data-stu-id="2599b-738">Policy expressions</span></span>](api-management-policy-expressions.md)
