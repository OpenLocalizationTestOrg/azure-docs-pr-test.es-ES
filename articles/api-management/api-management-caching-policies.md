---
title: "Directivas de almacenamiento en caché de Azure API Management | Microsoft Docs"
description: "Aprenda sobre las directivas de almacenamiento en caché disponibles para su uso en Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2a8f012e7e223ef5c1683c8a6c5ecf2f3e96bed8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="778fc-103">Directivas de almacenamiento en caché de API Management</span><span class="sxs-lookup"><span data-stu-id="778fc-103">API Management caching policies</span></span>
<span data-ttu-id="778fc-104">En este tema se proporciona una referencia para las siguientes directivas de API Management.</span><span class="sxs-lookup"><span data-stu-id="778fc-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="778fc-105">Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="778fc-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="778fc-106"><a name="CachingPolicies"></a> Directivas de almacenamiento en caché</span><span class="sxs-lookup"><span data-stu-id="778fc-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="778fc-107">Directivas de almacenamiento en caché de respuesta</span><span class="sxs-lookup"><span data-stu-id="778fc-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="778fc-108">[Get from cache](api-management-caching-policies.md#GetFromCache): realiza una búsqueda en caché y devuelve una respuesta en caché válida cuando está disponible.</span><span class="sxs-lookup"><span data-stu-id="778fc-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="778fc-109">[Store to cache](api-management-caching-policies.md#StoreToCache) (Almacenar en la caché): almacena en caché la respuesta de acuerdo con la configuración de control de caché especificada.</span><span class="sxs-lookup"><span data-stu-id="778fc-109">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches responses according to the specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="778fc-110">Directivas de almacenamiento en caché de valores</span><span class="sxs-lookup"><span data-stu-id="778fc-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="778fc-111">[Obtener valor de caché](#GetFromCacheByKey) : recupere un elemento almacenado en caché por clave.</span><span class="sxs-lookup"><span data-stu-id="778fc-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="778fc-112">[Almacenar valor en caché](#StoreToCacheByKey) : almacene un elemento en la memoria caché por clave.</span><span class="sxs-lookup"><span data-stu-id="778fc-112">[Store value in cache](#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="778fc-113">[Quitar valor de caché](#RemoveCacheByKey); quita un elemento de la memoria caché por clave.</span><span class="sxs-lookup"><span data-stu-id="778fc-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
##  <span data-ttu-id="778fc-114"><a name="GetFromCache"></a> Get from cache</span><span class="sxs-lookup"><span data-stu-id="778fc-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="778fc-115">Use la directiva `cache-lookup` para realizar una consulta en la caché y devolver una respuesta en caché válida cuando esté disponible.</span><span class="sxs-lookup"><span data-stu-id="778fc-115">Use the `cache-lookup` policy to perform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="778fc-116">Esta directiva se puede aplicar en aquellos casos en los que el contenido de respuesta permanezca estático durante un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="778fc-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="778fc-117">El almacenamiento en caché de respuesta reduce el ancho de banda y los requisitos de procesamiento impuestos sobre el servidor web de back-end y disminuye la latencia percibida por los consumidores de API.</span><span class="sxs-lookup"><span data-stu-id="778fc-117">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="778fc-118">Esta directiva debe tener una directiva [Store to cache](api-management-caching-policies.md#StoreToCache) (Almacenar en la caché) correspondiente.</span><span class="sxs-lookup"><span data-stu-id="778fc-118">This policy must have a corresponding [Store to cache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="778fc-119">Declaración de directiva</span><span class="sxs-lookup"><span data-stu-id="778fc-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression to evaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-authorized-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a><span data-ttu-id="778fc-120">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="778fc-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="778fc-121">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="778fc-121">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="none" must-revalidate="true">  
            <vary-by-query-parameter>version</vary-by-query-parameter>  
        </cache-lookup>           
    </inbound>  
    <outbound>  
        <cache-store duration="seconds" />  
        <base />          
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="778fc-122">Ejemplo de uso de expresiones de directiva</span><span class="sxs-lookup"><span data-stu-id="778fc-122">Example using policy expressions</span></span>  
 <span data-ttu-id="778fc-123">En este ejemplo se muestra cómo configurar la duración del almacenamiento en caché de respuesta de API Management para que coincida con el almacenamiento en caché de respuesta del servicio de back-end especificado por la directiva `Cache-Control` del servicio de back-end.</span><span class="sxs-lookup"><span data-stu-id="778fc-123">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="778fc-124">Para ver una demostración de la configuración y el uso de esta directiva, consulte [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Episodio 177 de Cloud Cover: más características de API Management con Vlad Vinogradsky) y avance al minuto 25:25.</span><span class="sxs-lookup"><span data-stu-id="778fc-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="778fc-125">Para más información, consulte [Expresiones de directiva](api-management-policy-expressions.md) y [Variable de contexto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="778fc-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="778fc-126">Elementos</span><span class="sxs-lookup"><span data-stu-id="778fc-126">Elements</span></span>  
  
|<span data-ttu-id="778fc-127">Nombre</span><span class="sxs-lookup"><span data-stu-id="778fc-127">Name</span></span>|<span data-ttu-id="778fc-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="778fc-128">Description</span></span>|<span data-ttu-id="778fc-129">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="778fc-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="778fc-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="778fc-130">cache-lookup</span></span>|<span data-ttu-id="778fc-131">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="778fc-131">Root element.</span></span>|<span data-ttu-id="778fc-132">Sí</span><span class="sxs-lookup"><span data-stu-id="778fc-132">Yes</span></span>|  
|<span data-ttu-id="778fc-133">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="778fc-133">vary-by-header</span></span>|<span data-ttu-id="778fc-134">Inicia el almacenamiento en caché de respuestas por valor del encabezado especificado, por ejemplo, Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span><span class="sxs-lookup"><span data-stu-id="778fc-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="778fc-135">No</span><span class="sxs-lookup"><span data-stu-id="778fc-135">No</span></span>|  
|<span data-ttu-id="778fc-136">vary-by-query-parameter</span><span class="sxs-lookup"><span data-stu-id="778fc-136">vary-by-query-parameter</span></span>|<span data-ttu-id="778fc-137">Inicia el almacenamiento en caché de las respuestas por valor de los parámetros de consulta especificados.</span><span class="sxs-lookup"><span data-stu-id="778fc-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="778fc-138">Permite introducir uno o varios parámetros.</span><span class="sxs-lookup"><span data-stu-id="778fc-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="778fc-139">Utilice el punto y coma como separador.</span><span class="sxs-lookup"><span data-stu-id="778fc-139">Use semicolon as a separator.</span></span> <span data-ttu-id="778fc-140">Si no se especifica ninguno, se usan todos los parámetros de consulta.</span><span class="sxs-lookup"><span data-stu-id="778fc-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="778fc-141">No</span><span class="sxs-lookup"><span data-stu-id="778fc-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="778fc-142">Attributes</span><span class="sxs-lookup"><span data-stu-id="778fc-142">Attributes</span></span>  
  
|<span data-ttu-id="778fc-143">Nombre</span><span class="sxs-lookup"><span data-stu-id="778fc-143">Name</span></span>|<span data-ttu-id="778fc-144">Descripción</span><span class="sxs-lookup"><span data-stu-id="778fc-144">Description</span></span>|<span data-ttu-id="778fc-145">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="778fc-145">Required</span></span>|<span data-ttu-id="778fc-146">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="778fc-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="778fc-147">allow-private-response-caching</span><span class="sxs-lookup"><span data-stu-id="778fc-147">allow-private-response-caching</span></span>|<span data-ttu-id="778fc-148">Cuando se establece en `true`, permite el almacenamiento en caché de las solicitudes que contienen un encabezado de autorización.</span><span class="sxs-lookup"><span data-stu-id="778fc-148">When set to `true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="778fc-149">No</span><span class="sxs-lookup"><span data-stu-id="778fc-149">No</span></span>|<span data-ttu-id="778fc-150">false</span><span class="sxs-lookup"><span data-stu-id="778fc-150">false</span></span>|  
|<span data-ttu-id="778fc-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="778fc-151">downstream-caching-type</span></span>|<span data-ttu-id="778fc-152">Este atributo debe establecerse en uno de los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="778fc-152">This attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="778fc-153">-   none: no se permite el almacenamiento en caché de bajada.</span><span class="sxs-lookup"><span data-stu-id="778fc-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="778fc-154">-   private: se permite el almacenamiento en caché de bajada privado.</span><span class="sxs-lookup"><span data-stu-id="778fc-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="778fc-155">-   public: se permite el almacenamiento en caché de bajada privado y compartido.</span><span class="sxs-lookup"><span data-stu-id="778fc-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="778fc-156">No</span><span class="sxs-lookup"><span data-stu-id="778fc-156">No</span></span>|<span data-ttu-id="778fc-157">Ninguna</span><span class="sxs-lookup"><span data-stu-id="778fc-157">none</span></span>|  
|<span data-ttu-id="778fc-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="778fc-158">must-revalidate</span></span>|<span data-ttu-id="778fc-159">Cuando el almacenamiento en caché de bajada está habilitado, este atributo activa o desactiva la directiva de control de caché `must-revalidate` en las respuestas de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="778fc-159">When downstream caching is enabled this attribute turns on or off  the `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="778fc-160">No</span><span class="sxs-lookup"><span data-stu-id="778fc-160">No</span></span>|<span data-ttu-id="778fc-161">true</span><span class="sxs-lookup"><span data-stu-id="778fc-161">true</span></span>|  
|<span data-ttu-id="778fc-162">vary-by-developer</span><span class="sxs-lookup"><span data-stu-id="778fc-162">vary-by-developer</span></span>|<span data-ttu-id="778fc-163">Se establece en `true` para almacenar en caché las respuestas por clave de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="778fc-163">Set to `true` to cache responses per developer key.</span></span>|<span data-ttu-id="778fc-164">No</span><span class="sxs-lookup"><span data-stu-id="778fc-164">No</span></span>|<span data-ttu-id="778fc-165">false</span><span class="sxs-lookup"><span data-stu-id="778fc-165">false</span></span>|  
|<span data-ttu-id="778fc-166">vary-by-developer-groups</span><span class="sxs-lookup"><span data-stu-id="778fc-166">vary-by-developer-groups</span></span>|<span data-ttu-id="778fc-167">Se establece en `true` para almacenar en caché las respuestas por rol de usuario.</span><span class="sxs-lookup"><span data-stu-id="778fc-167">Set to `true` to cache responses per user role.</span></span>|<span data-ttu-id="778fc-168">No</span><span class="sxs-lookup"><span data-stu-id="778fc-168">No</span></span>|<span data-ttu-id="778fc-169">false</span><span class="sxs-lookup"><span data-stu-id="778fc-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="778fc-170">Uso</span><span class="sxs-lookup"><span data-stu-id="778fc-170">Usage</span></span>  
 <span data-ttu-id="778fc-171">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="778fc-171">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="778fc-172">**Secciones de la directiva:** inbound</span><span class="sxs-lookup"><span data-stu-id="778fc-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="778fc-173">**Ámbitos de directiva:** API, operation, product</span><span class="sxs-lookup"><span data-stu-id="778fc-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="778fc-174"><a name="StoreToCache"></a> Store to cache (Almacenar en la caché)</span><span class="sxs-lookup"><span data-stu-id="778fc-174"><a name="StoreToCache"></a> Store to cache</span></span>  
 <span data-ttu-id="778fc-175">La directiva `cache-store` almacena en caché las respuestas según la configuración de caché especificada.</span><span class="sxs-lookup"><span data-stu-id="778fc-175">The `cache-store` policy caches responses according to the specified cache settings.</span></span> <span data-ttu-id="778fc-176">Esta directiva se puede aplicar en aquellos casos en los que el contenido de respuesta permanezca estático durante un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="778fc-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="778fc-177">El almacenamiento en caché de respuesta reduce el ancho de banda y los requisitos de procesamiento impuestos sobre el servidor web de back-end y disminuye la latencia percibida por los consumidores de API.</span><span class="sxs-lookup"><span data-stu-id="778fc-177">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="778fc-178">Esta directiva debe tener una directiva [Get from cache](api-management-caching-policies.md#GetFromCache) correspondiente.</span><span class="sxs-lookup"><span data-stu-id="778fc-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="778fc-179">Declaración de directiva</span><span class="sxs-lookup"><span data-stu-id="778fc-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="778fc-180">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="778fc-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="778fc-181">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="778fc-181">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
          <cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false">  
                <vary-by-query-parameter>parameter name</vary-by-query-parameter> <!-- optional, can repeated several times -->  
        </cache-lookup>  
    </inbound>  
    <outbound>  
        <base />  
            <cache-store duration="3600" />  
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="778fc-182">Ejemplo de uso de expresiones de directiva</span><span class="sxs-lookup"><span data-stu-id="778fc-182">Example using policy expressions</span></span>  
 <span data-ttu-id="778fc-183">En este ejemplo se muestra cómo configurar la duración del almacenamiento en caché de respuesta de API Management para que coincida con el almacenamiento en caché de respuesta del servicio de back-end especificado por la directiva `Cache-Control` del servicio de back-end.</span><span class="sxs-lookup"><span data-stu-id="778fc-183">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="778fc-184">Para ver una demostración de la configuración y el uso de esta directiva, consulte [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Episodio 177 de Cloud Cover: más características de API Management con Vlad Vinogradsky) y avance al minuto 25:25.</span><span class="sxs-lookup"><span data-stu-id="778fc-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="778fc-185">Para más información, consulte [Expresiones de directiva](api-management-policy-expressions.md) y [Variable de contexto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="778fc-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="778fc-186">Elementos</span><span class="sxs-lookup"><span data-stu-id="778fc-186">Elements</span></span>  
  
|<span data-ttu-id="778fc-187">Nombre</span><span class="sxs-lookup"><span data-stu-id="778fc-187">Name</span></span>|<span data-ttu-id="778fc-188">Descripción</span><span class="sxs-lookup"><span data-stu-id="778fc-188">Description</span></span>|<span data-ttu-id="778fc-189">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="778fc-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="778fc-190">cache-store</span><span class="sxs-lookup"><span data-stu-id="778fc-190">cache-store</span></span>|<span data-ttu-id="778fc-191">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="778fc-191">Root element.</span></span>|<span data-ttu-id="778fc-192">Sí</span><span class="sxs-lookup"><span data-stu-id="778fc-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="778fc-193">Atributos</span><span class="sxs-lookup"><span data-stu-id="778fc-193">Attributes</span></span>  
  
|<span data-ttu-id="778fc-194">Nombre</span><span class="sxs-lookup"><span data-stu-id="778fc-194">Name</span></span>|<span data-ttu-id="778fc-195">Descripción</span><span class="sxs-lookup"><span data-stu-id="778fc-195">Description</span></span>|<span data-ttu-id="778fc-196">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="778fc-196">Required</span></span>|<span data-ttu-id="778fc-197">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="778fc-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="778fc-198">duration</span><span class="sxs-lookup"><span data-stu-id="778fc-198">duration</span></span>|<span data-ttu-id="778fc-199">Período de vida de las entradas almacenadas en caché, especificado en segundos.</span><span class="sxs-lookup"><span data-stu-id="778fc-199">Time-to-live of the cached entries, specified in seconds.</span></span>|<span data-ttu-id="778fc-200">Sí</span><span class="sxs-lookup"><span data-stu-id="778fc-200">Yes</span></span>|<span data-ttu-id="778fc-201">N/D</span><span class="sxs-lookup"><span data-stu-id="778fc-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="778fc-202">Uso</span><span class="sxs-lookup"><span data-stu-id="778fc-202">Usage</span></span>  
 <span data-ttu-id="778fc-203">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de las directivas.</span><span class="sxs-lookup"><span data-stu-id="778fc-203">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="778fc-204">**Secciones de la directiva:** outbound</span><span class="sxs-lookup"><span data-stu-id="778fc-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="778fc-205">**Ámbitos de directiva:** API, operation, product</span><span class="sxs-lookup"><span data-stu-id="778fc-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="778fc-206"><a name="GetFromCacheByKey"></a> Get value from cache (Obtener valor de la caché)</span><span class="sxs-lookup"><span data-stu-id="778fc-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="778fc-207">Use la directiva `cache-lookup-value` para realizar la búsqueda en la caché por clave y devolver un valor almacenado en caché.</span><span class="sxs-lookup"><span data-stu-id="778fc-207">Use the `cache-lookup-value` policy to perform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="778fc-208">La clave puede tener un valor de cadena arbitrario y normalmente se proporciona mediante una expresión de directiva.</span><span class="sxs-lookup"><span data-stu-id="778fc-208">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="778fc-209">Esta directiva debe tener una directiva [Store value in cache](#StoreToCacheByKey) (Almacenar valor en la caché) correspondiente.</span><span class="sxs-lookup"><span data-stu-id="778fc-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="778fc-210">Declaración de directiva</span><span class="sxs-lookup"><span data-stu-id="778fc-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value to use if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="778fc-211">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="778fc-211">Example</span></span>  
 <span data-ttu-id="778fc-212">Para más información y ver ejemplos de esta directiva, consulte [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/) (Almacenamiento en caché personalizado en Azure API Management).</span><span class="sxs-lookup"><span data-stu-id="778fc-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="778fc-213">Elementos</span><span class="sxs-lookup"><span data-stu-id="778fc-213">Elements</span></span>  
  
|<span data-ttu-id="778fc-214">Nombre</span><span class="sxs-lookup"><span data-stu-id="778fc-214">Name</span></span>|<span data-ttu-id="778fc-215">Descripción</span><span class="sxs-lookup"><span data-stu-id="778fc-215">Description</span></span>|<span data-ttu-id="778fc-216">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="778fc-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="778fc-217">cache-lookup-value</span><span class="sxs-lookup"><span data-stu-id="778fc-217">cache-lookup-value</span></span>|<span data-ttu-id="778fc-218">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="778fc-218">Root element.</span></span>|<span data-ttu-id="778fc-219">Sí</span><span class="sxs-lookup"><span data-stu-id="778fc-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="778fc-220">Atributos</span><span class="sxs-lookup"><span data-stu-id="778fc-220">Attributes</span></span>  
  
|<span data-ttu-id="778fc-221">Nombre</span><span class="sxs-lookup"><span data-stu-id="778fc-221">Name</span></span>|<span data-ttu-id="778fc-222">Descripción</span><span class="sxs-lookup"><span data-stu-id="778fc-222">Description</span></span>|<span data-ttu-id="778fc-223">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="778fc-223">Required</span></span>|<span data-ttu-id="778fc-224">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="778fc-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="778fc-225">default-value</span><span class="sxs-lookup"><span data-stu-id="778fc-225">default-value</span></span>|<span data-ttu-id="778fc-226">Un valor que se asignará a la variable si la búsqueda de la clave de caché da lugar a un error.</span><span class="sxs-lookup"><span data-stu-id="778fc-226">A value that will be assigned to the variable if the cache key lookup resulted in a miss.</span></span> <span data-ttu-id="778fc-227">Si no se especifica este atributo, se asigna `null`.</span><span class="sxs-lookup"><span data-stu-id="778fc-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="778fc-228">No</span><span class="sxs-lookup"><span data-stu-id="778fc-228">No</span></span>|`null`|  
|<span data-ttu-id="778fc-229">key</span><span class="sxs-lookup"><span data-stu-id="778fc-229">key</span></span>|<span data-ttu-id="778fc-230">Valor de clave de caché para usar en la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="778fc-230">Cache key value to use in the lookup.</span></span>|<span data-ttu-id="778fc-231">Sí</span><span class="sxs-lookup"><span data-stu-id="778fc-231">Yes</span></span>|<span data-ttu-id="778fc-232">N/D</span><span class="sxs-lookup"><span data-stu-id="778fc-232">N/A</span></span>|  
|<span data-ttu-id="778fc-233">variable-name</span><span class="sxs-lookup"><span data-stu-id="778fc-233">variable-name</span></span>|<span data-ttu-id="778fc-234">Nombre de la [variable de contexto](api-management-policy-expressions.md#ContextVariables) a la que se asignará el valor buscado si la búsqueda tiene éxito.</span><span class="sxs-lookup"><span data-stu-id="778fc-234">Name of the [context variable](api-management-policy-expressions.md#ContextVariables) the looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="778fc-235">Si se produce un error de búsqueda, se asignará a la variable el valor del atributo `default-value` o `null`, si se omite el atributo `default-value`.</span><span class="sxs-lookup"><span data-stu-id="778fc-235">If lookup results in a miss, the variable will be assigned the value of the `default-value` attribute or `null`, if the `default-value` attribute is omitted.</span></span>|<span data-ttu-id="778fc-236">Sí</span><span class="sxs-lookup"><span data-stu-id="778fc-236">Yes</span></span>|<span data-ttu-id="778fc-237">N/D</span><span class="sxs-lookup"><span data-stu-id="778fc-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="778fc-238">Uso</span><span class="sxs-lookup"><span data-stu-id="778fc-238">Usage</span></span>  
 <span data-ttu-id="778fc-239">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="778fc-239">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="778fc-240">**Secciones de la directiva:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="778fc-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="778fc-241">**Ámbitos de la directiva:** global, API, operación, producto</span><span class="sxs-lookup"><span data-stu-id="778fc-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="778fc-242"><a name="StoreToCacheByKey"></a> Store value in cache (Almacenar valor en la caché)</span><span class="sxs-lookup"><span data-stu-id="778fc-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="778fc-243">La directiva `cache-store-value` realiza el almacenamiento en caché mediante una clave.</span><span class="sxs-lookup"><span data-stu-id="778fc-243">The `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="778fc-244">La clave puede tener un valor de cadena arbitrario y normalmente se proporciona mediante una expresión de directiva.</span><span class="sxs-lookup"><span data-stu-id="778fc-244">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="778fc-245">Esta directiva debe tener una directiva [Get from cache](#GetFromCacheByKey) (Obtener de la caché) correspondiente.</span><span class="sxs-lookup"><span data-stu-id="778fc-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="778fc-246">Declaración de directiva</span><span class="sxs-lookup"><span data-stu-id="778fc-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value to cache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="778fc-247">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="778fc-247">Example</span></span>  
 <span data-ttu-id="778fc-248">Para más información y ver ejemplos de esta directiva, consulte [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/) (Almacenamiento en caché personalizado en Azure API Management).</span><span class="sxs-lookup"><span data-stu-id="778fc-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="778fc-249">Elementos</span><span class="sxs-lookup"><span data-stu-id="778fc-249">Elements</span></span>  
  
|<span data-ttu-id="778fc-250">Nombre</span><span class="sxs-lookup"><span data-stu-id="778fc-250">Name</span></span>|<span data-ttu-id="778fc-251">Descripción</span><span class="sxs-lookup"><span data-stu-id="778fc-251">Description</span></span>|<span data-ttu-id="778fc-252">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="778fc-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="778fc-253">cache-store-value</span><span class="sxs-lookup"><span data-stu-id="778fc-253">cache-store-value</span></span>|<span data-ttu-id="778fc-254">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="778fc-254">Root element.</span></span>|<span data-ttu-id="778fc-255">Sí</span><span class="sxs-lookup"><span data-stu-id="778fc-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="778fc-256">Atributos</span><span class="sxs-lookup"><span data-stu-id="778fc-256">Attributes</span></span>  
  
|<span data-ttu-id="778fc-257">Nombre</span><span class="sxs-lookup"><span data-stu-id="778fc-257">Name</span></span>|<span data-ttu-id="778fc-258">Descripción</span><span class="sxs-lookup"><span data-stu-id="778fc-258">Description</span></span>|<span data-ttu-id="778fc-259">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="778fc-259">Required</span></span>|<span data-ttu-id="778fc-260">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="778fc-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="778fc-261">duration</span><span class="sxs-lookup"><span data-stu-id="778fc-261">duration</span></span>|<span data-ttu-id="778fc-262">El valor se almacenará en la caché según el valor de duración proporcionado, especificado en segundos.</span><span class="sxs-lookup"><span data-stu-id="778fc-262">Value will be cached for the provided duration value, specified in seconds.</span></span>|<span data-ttu-id="778fc-263">Sí</span><span class="sxs-lookup"><span data-stu-id="778fc-263">Yes</span></span>|<span data-ttu-id="778fc-264">N/D</span><span class="sxs-lookup"><span data-stu-id="778fc-264">N/A</span></span>|  
|<span data-ttu-id="778fc-265">key</span><span class="sxs-lookup"><span data-stu-id="778fc-265">key</span></span>|<span data-ttu-id="778fc-266">La clave de caché con la que se almacenará el valor.</span><span class="sxs-lookup"><span data-stu-id="778fc-266">Cache key the value will be stored under.</span></span>|<span data-ttu-id="778fc-267">Sí</span><span class="sxs-lookup"><span data-stu-id="778fc-267">Yes</span></span>|<span data-ttu-id="778fc-268">N/D</span><span class="sxs-lookup"><span data-stu-id="778fc-268">N/A</span></span>|  
|<span data-ttu-id="778fc-269">value</span><span class="sxs-lookup"><span data-stu-id="778fc-269">value</span></span>|<span data-ttu-id="778fc-270">El valor que se almacenará en la caché.</span><span class="sxs-lookup"><span data-stu-id="778fc-270">The value to be cached.</span></span>|<span data-ttu-id="778fc-271">Sí</span><span class="sxs-lookup"><span data-stu-id="778fc-271">Yes</span></span>|<span data-ttu-id="778fc-272">N/D</span><span class="sxs-lookup"><span data-stu-id="778fc-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="778fc-273">Uso</span><span class="sxs-lookup"><span data-stu-id="778fc-273">Usage</span></span>  
 <span data-ttu-id="778fc-274">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="778fc-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="778fc-275">**Secciones de la directiva:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="778fc-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="778fc-276">**Ámbitos de la directiva:** global, API, operación, producto</span><span class="sxs-lookup"><span data-stu-id="778fc-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="778fc-277"><a name="RemoveCacheByKey"></a> Remove value from cache (Quitar valor de la caché)</span><span class="sxs-lookup"><span data-stu-id="778fc-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="778fc-278">La directiva `cache-remove-value` elimina un elemento almacenado en caché identificado por su clave.</span><span class="sxs-lookup"><span data-stu-id="778fc-278">The             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="778fc-279">La clave puede tener un valor de cadena arbitrario y normalmente se proporciona mediante una expresión de directiva.</span><span class="sxs-lookup"><span data-stu-id="778fc-279">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="778fc-280">Declaración de directiva</span><span class="sxs-lookup"><span data-stu-id="778fc-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="778fc-281">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="778fc-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="778fc-282">Elementos</span><span class="sxs-lookup"><span data-stu-id="778fc-282">Elements</span></span>  
  
|<span data-ttu-id="778fc-283">Nombre</span><span class="sxs-lookup"><span data-stu-id="778fc-283">Name</span></span>|<span data-ttu-id="778fc-284">Descripción</span><span class="sxs-lookup"><span data-stu-id="778fc-284">Description</span></span>|<span data-ttu-id="778fc-285">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="778fc-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="778fc-286">cache-remove-value</span><span class="sxs-lookup"><span data-stu-id="778fc-286">cache-remove-value</span></span>|<span data-ttu-id="778fc-287">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="778fc-287">Root element.</span></span>|<span data-ttu-id="778fc-288">Sí</span><span class="sxs-lookup"><span data-stu-id="778fc-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="778fc-289">Atributos</span><span class="sxs-lookup"><span data-stu-id="778fc-289">Attributes</span></span>  
  
|<span data-ttu-id="778fc-290">Nombre</span><span class="sxs-lookup"><span data-stu-id="778fc-290">Name</span></span>|<span data-ttu-id="778fc-291">Descripción</span><span class="sxs-lookup"><span data-stu-id="778fc-291">Description</span></span>|<span data-ttu-id="778fc-292">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="778fc-292">Required</span></span>|<span data-ttu-id="778fc-293">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="778fc-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="778fc-294">key</span><span class="sxs-lookup"><span data-stu-id="778fc-294">key</span></span>|<span data-ttu-id="778fc-295">La clave del valor anteriormente almacenado en caché que se quitará de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="778fc-295">The key of the previously cached value to be removed from the cache.</span></span>|<span data-ttu-id="778fc-296">Sí</span><span class="sxs-lookup"><span data-stu-id="778fc-296">Yes</span></span>|<span data-ttu-id="778fc-297">N/D</span><span class="sxs-lookup"><span data-stu-id="778fc-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="778fc-298">Uso</span><span class="sxs-lookup"><span data-stu-id="778fc-298">Usage</span></span>  
 <span data-ttu-id="778fc-299">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="778fc-299">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="778fc-300">**Secciones de la directiva:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="778fc-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="778fc-301">**Ámbitos de la directiva:** global, API, operación, producto</span><span class="sxs-lookup"><span data-stu-id="778fc-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="778fc-302">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="778fc-302">Next steps</span></span>
<span data-ttu-id="778fc-303">Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="778fc-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  