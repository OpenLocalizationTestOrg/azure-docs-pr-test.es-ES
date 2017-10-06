---
title: "directivas de almacenamiento en caché de administración de API aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de hello almacenamiento en caché de directivas disponibles para su uso en la administración de API de Azure."
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
ms.openlocfilehash: bd6b0721945609b28dbf6e7ef0631979c08c8c65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="da362-103">Directivas de almacenamiento en caché de API Management</span><span class="sxs-lookup"><span data-stu-id="da362-103">API Management caching policies</span></span>
<span data-ttu-id="da362-104">En este tema se proporciona una referencia para hello las siguientes directivas de administración de API.</span><span class="sxs-lookup"><span data-stu-id="da362-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="da362-105">Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="da362-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="da362-106"><a name="CachingPolicies"></a> Directivas de almacenamiento en caché</span><span class="sxs-lookup"><span data-stu-id="da362-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="da362-107">Directivas de almacenamiento en caché de respuesta</span><span class="sxs-lookup"><span data-stu-id="da362-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="da362-108">[Get from cache](api-management-caching-policies.md#GetFromCache): realiza una búsqueda en caché y devuelve una respuesta en caché válida cuando está disponible.</span><span class="sxs-lookup"><span data-stu-id="da362-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="da362-109">[Almacenar toocache](api-management-caching-policies.md#StoreToCache) : las respuestas de las memorias caché según la configuración de control de caché especificado toohello.</span><span class="sxs-lookup"><span data-stu-id="da362-109">[Store toocache](api-management-caching-policies.md#StoreToCache) - Caches responses according toohello specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="da362-110">Directivas de almacenamiento en caché de valores</span><span class="sxs-lookup"><span data-stu-id="da362-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="da362-111">[Obtener valor de caché](#GetFromCacheByKey) : recupere un elemento almacenado en caché por clave.</span><span class="sxs-lookup"><span data-stu-id="da362-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="da362-112">[Valor de almacenar en caché](#StoreToCacheByKey) -almacenar un elemento en caché de Hola por clave.</span><span class="sxs-lookup"><span data-stu-id="da362-112">[Store value in cache](#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>  
  
    -   <span data-ttu-id="da362-113">[Quitar el valor de la caché](#RemoveCacheByKey) -quitar un elemento en caché de Hola por clave.</span><span class="sxs-lookup"><span data-stu-id="da362-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>  
  
##  <span data-ttu-id="da362-114"><a name="GetFromCache"></a> Get from cache</span><span class="sxs-lookup"><span data-stu-id="da362-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="da362-115">Hola de uso `cache-lookup` caché de directiva tooperform buscar y devolver una respuesta almacenada en caché válida si está disponible.</span><span class="sxs-lookup"><span data-stu-id="da362-115">Use hello `cache-lookup` policy tooperform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="da362-116">Esta directiva se puede aplicar en aquellos casos en los que el contenido de respuesta permanezca estático durante un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="da362-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="da362-117">Las respuestas en caché reducen el ancho de banda y los requisitos de procesamiento impuesta en hello back-end web server y reduce la latencia percibida por los consumidores de API.</span><span class="sxs-lookup"><span data-stu-id="da362-117">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="da362-118">Esta directiva debe tener su correspondiente [toocache almacén](api-management-caching-policies.md#StoreToCache) directiva.</span><span class="sxs-lookup"><span data-stu-id="da362-118">This policy must have a corresponding [Store toocache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="da362-119">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="da362-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression tooevaluate)">  
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
  
### <a name="examples"></a><span data-ttu-id="da362-120">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="da362-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="da362-121">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="da362-121">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="da362-122">Ejemplo de uso de expresiones de directiva</span><span class="sxs-lookup"><span data-stu-id="da362-122">Example using policy expressions</span></span>  
 <span data-ttu-id="da362-123">Este ejemplo muestra cómo hacer las respuesta de administración de API tootooconfigure almacenamiento en caché de duración que coincidencias hello las respuestas en caché del servicio de back-end de hello según lo especificado por Hola de seguridad del servicio `Cache-Control` directiva.</span><span class="sxs-lookup"><span data-stu-id="da362-123">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="da362-124">Para ver una demostración de cómo configurar y usar esta directiva, consulte [177 episodio abarcan de nube: más características de administración de API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avancemos too25:25.</span><span class="sxs-lookup"><span data-stu-id="da362-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="da362-125">Para obtener más información, consulte [Policy expressions](api-management-policy-expressions.md) (Expresiones de política) y [Context variable](api-management-policy-expressions.md#ContextVariables) (Variable de contexto).</span><span class="sxs-lookup"><span data-stu-id="da362-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="da362-126">Elementos</span><span class="sxs-lookup"><span data-stu-id="da362-126">Elements</span></span>  
  
|<span data-ttu-id="da362-127">Nombre</span><span class="sxs-lookup"><span data-stu-id="da362-127">Name</span></span>|<span data-ttu-id="da362-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="da362-128">Description</span></span>|<span data-ttu-id="da362-129">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="da362-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="da362-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="da362-130">cache-lookup</span></span>|<span data-ttu-id="da362-131">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="da362-131">Root element.</span></span>|<span data-ttu-id="da362-132">Sí</span><span class="sxs-lookup"><span data-stu-id="da362-132">Yes</span></span>|  
|<span data-ttu-id="da362-133">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="da362-133">vary-by-header</span></span>|<span data-ttu-id="da362-134">Inicia el almacenamiento en caché de respuestas por valor del encabezado especificado, por ejemplo, Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span><span class="sxs-lookup"><span data-stu-id="da362-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="da362-135">No</span><span class="sxs-lookup"><span data-stu-id="da362-135">No</span></span>|  
|<span data-ttu-id="da362-136">vary-by-query-parameter</span><span class="sxs-lookup"><span data-stu-id="da362-136">vary-by-query-parameter</span></span>|<span data-ttu-id="da362-137">Inicia el almacenamiento en caché de las respuestas por valor de los parámetros de consulta especificados.</span><span class="sxs-lookup"><span data-stu-id="da362-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="da362-138">Permite introducir uno o varios parámetros.</span><span class="sxs-lookup"><span data-stu-id="da362-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="da362-139">Utilice el punto y coma como separador.</span><span class="sxs-lookup"><span data-stu-id="da362-139">Use semicolon as a separator.</span></span> <span data-ttu-id="da362-140">Si no se especifica ninguno, se usan todos los parámetros de consulta.</span><span class="sxs-lookup"><span data-stu-id="da362-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="da362-141">No</span><span class="sxs-lookup"><span data-stu-id="da362-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="da362-142">Attributes</span><span class="sxs-lookup"><span data-stu-id="da362-142">Attributes</span></span>  
  
|<span data-ttu-id="da362-143">Nombre</span><span class="sxs-lookup"><span data-stu-id="da362-143">Name</span></span>|<span data-ttu-id="da362-144">Descripción</span><span class="sxs-lookup"><span data-stu-id="da362-144">Description</span></span>|<span data-ttu-id="da362-145">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="da362-145">Required</span></span>|<span data-ttu-id="da362-146">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="da362-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="da362-147">allow-private-response-caching</span><span class="sxs-lookup"><span data-stu-id="da362-147">allow-private-response-caching</span></span>|<span data-ttu-id="da362-148">Cuando se establece demasiado`true`, permite el almacenamiento en caché de las solicitudes que contienen un encabezado de autorización.</span><span class="sxs-lookup"><span data-stu-id="da362-148">When set too`true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="da362-149">No</span><span class="sxs-lookup"><span data-stu-id="da362-149">No</span></span>|<span data-ttu-id="da362-150">false</span><span class="sxs-lookup"><span data-stu-id="da362-150">false</span></span>|  
|<span data-ttu-id="da362-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="da362-151">downstream-caching-type</span></span>|<span data-ttu-id="da362-152">Este atributo debe establecerse tooone de hello después de valores.</span><span class="sxs-lookup"><span data-stu-id="da362-152">This attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="da362-153">-   none: no se permite el almacenamiento en caché de bajada.</span><span class="sxs-lookup"><span data-stu-id="da362-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="da362-154">-   private: se permite el almacenamiento en caché de bajada privado.</span><span class="sxs-lookup"><span data-stu-id="da362-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="da362-155">-   public: se permite el almacenamiento en caché de bajada privado y compartido.</span><span class="sxs-lookup"><span data-stu-id="da362-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="da362-156">No</span><span class="sxs-lookup"><span data-stu-id="da362-156">No</span></span>|<span data-ttu-id="da362-157">Ninguna</span><span class="sxs-lookup"><span data-stu-id="da362-157">none</span></span>|  
|<span data-ttu-id="da362-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="da362-158">must-revalidate</span></span>|<span data-ttu-id="da362-159">Cuando se habilita el almacenamiento en caché descendente este atributo activa o desactiva hello `must-revalidate` directiva de control de caché en las respuestas de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="da362-159">When downstream caching is enabled this attribute turns on or off  hello `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="da362-160">No</span><span class="sxs-lookup"><span data-stu-id="da362-160">No</span></span>|<span data-ttu-id="da362-161">true</span><span class="sxs-lookup"><span data-stu-id="da362-161">true</span></span>|  
|<span data-ttu-id="da362-162">vary-by-developer</span><span class="sxs-lookup"><span data-stu-id="da362-162">vary-by-developer</span></span>|<span data-ttu-id="da362-163">Establecer demasiado`true` toocache respuestas por clave de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="da362-163">Set too`true` toocache responses per developer key.</span></span>|<span data-ttu-id="da362-164">No</span><span class="sxs-lookup"><span data-stu-id="da362-164">No</span></span>|<span data-ttu-id="da362-165">false</span><span class="sxs-lookup"><span data-stu-id="da362-165">false</span></span>|  
|<span data-ttu-id="da362-166">vary-by-developer-groups</span><span class="sxs-lookup"><span data-stu-id="da362-166">vary-by-developer-groups</span></span>|<span data-ttu-id="da362-167">Establecer demasiado`true` toocache respuestas por función de usuario.</span><span class="sxs-lookup"><span data-stu-id="da362-167">Set too`true` toocache responses per user role.</span></span>|<span data-ttu-id="da362-168">No</span><span class="sxs-lookup"><span data-stu-id="da362-168">No</span></span>|<span data-ttu-id="da362-169">false</span><span class="sxs-lookup"><span data-stu-id="da362-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="da362-170">Uso</span><span class="sxs-lookup"><span data-stu-id="da362-170">Usage</span></span>  
 <span data-ttu-id="da362-171">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="da362-171">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="da362-172">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="da362-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="da362-173">**Ámbitos de directiva:** API, operation, product</span><span class="sxs-lookup"><span data-stu-id="da362-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="da362-174"><a name="StoreToCache"></a>Toocache almacén</span><span class="sxs-lookup"><span data-stu-id="da362-174"><a name="StoreToCache"></a> Store toocache</span></span>  
 <span data-ttu-id="da362-175">Hola `cache-store` según toohello las respuestas de las memorias caché de directiva especifica la configuración de la caché.</span><span class="sxs-lookup"><span data-stu-id="da362-175">hello `cache-store` policy caches responses according toohello specified cache settings.</span></span> <span data-ttu-id="da362-176">Esta directiva se puede aplicar en aquellos casos en los que el contenido de respuesta permanezca estático durante un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="da362-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="da362-177">Las respuestas en caché reducen el ancho de banda y los requisitos de procesamiento impuesta en hello back-end web server y reduce la latencia percibida por los consumidores de API.</span><span class="sxs-lookup"><span data-stu-id="da362-177">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="da362-178">Esta directiva debe tener una directiva [Get from cache](api-management-caching-policies.md#GetFromCache) correspondiente.</span><span class="sxs-lookup"><span data-stu-id="da362-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="da362-179">Declaración de directiva</span><span class="sxs-lookup"><span data-stu-id="da362-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="da362-180">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="da362-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="da362-181">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="da362-181">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="da362-182">Ejemplo de uso de expresiones de directiva</span><span class="sxs-lookup"><span data-stu-id="da362-182">Example using policy expressions</span></span>  
 <span data-ttu-id="da362-183">Este ejemplo muestra cómo hacer las respuesta de administración de API tootooconfigure almacenamiento en caché de duración que coincidencias hello las respuestas en caché del servicio de back-end de hello según lo especificado por Hola de seguridad del servicio `Cache-Control` directiva.</span><span class="sxs-lookup"><span data-stu-id="da362-183">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="da362-184">Para ver una demostración de cómo configurar y usar esta directiva, consulte [177 episodio abarcan de nube: más características de administración de API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avancemos too25:25.</span><span class="sxs-lookup"><span data-stu-id="da362-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="da362-185">Para obtener más información, consulte [Policy expressions](api-management-policy-expressions.md) (Expresiones de política) y [Context variable](api-management-policy-expressions.md#ContextVariables) (Variable de contexto).</span><span class="sxs-lookup"><span data-stu-id="da362-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="da362-186">Elementos</span><span class="sxs-lookup"><span data-stu-id="da362-186">Elements</span></span>  
  
|<span data-ttu-id="da362-187">Nombre</span><span class="sxs-lookup"><span data-stu-id="da362-187">Name</span></span>|<span data-ttu-id="da362-188">Descripción</span><span class="sxs-lookup"><span data-stu-id="da362-188">Description</span></span>|<span data-ttu-id="da362-189">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="da362-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="da362-190">cache-store</span><span class="sxs-lookup"><span data-stu-id="da362-190">cache-store</span></span>|<span data-ttu-id="da362-191">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="da362-191">Root element.</span></span>|<span data-ttu-id="da362-192">Sí</span><span class="sxs-lookup"><span data-stu-id="da362-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="da362-193">Atributos</span><span class="sxs-lookup"><span data-stu-id="da362-193">Attributes</span></span>  
  
|<span data-ttu-id="da362-194">Nombre</span><span class="sxs-lookup"><span data-stu-id="da362-194">Name</span></span>|<span data-ttu-id="da362-195">Descripción</span><span class="sxs-lookup"><span data-stu-id="da362-195">Description</span></span>|<span data-ttu-id="da362-196">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="da362-196">Required</span></span>|<span data-ttu-id="da362-197">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="da362-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="da362-198">duration</span><span class="sxs-lookup"><span data-stu-id="da362-198">duration</span></span>|<span data-ttu-id="da362-199">Tiempo de vida del programa Hola a almacenar en caché las entradas, especificadas en segundos.</span><span class="sxs-lookup"><span data-stu-id="da362-199">Time-to-live of hello cached entries, specified in seconds.</span></span>|<span data-ttu-id="da362-200">Sí</span><span class="sxs-lookup"><span data-stu-id="da362-200">Yes</span></span>|<span data-ttu-id="da362-201">N/D</span><span class="sxs-lookup"><span data-stu-id="da362-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="da362-202">Uso</span><span class="sxs-lookup"><span data-stu-id="da362-202">Usage</span></span>  
 <span data-ttu-id="da362-203">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="da362-203">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="da362-204">**Secciones de la directiva:** outbound</span><span class="sxs-lookup"><span data-stu-id="da362-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="da362-205">**Ámbitos de directiva:** API, operation, product</span><span class="sxs-lookup"><span data-stu-id="da362-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="da362-206"><a name="GetFromCacheByKey"></a> Get value from cache (Obtener valor de la caché)</span><span class="sxs-lookup"><span data-stu-id="da362-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="da362-207">Hola de uso `cache-lookup-value` tooperform directiva caché búsqueda por clave y devolver un valor almacenado en caché.</span><span class="sxs-lookup"><span data-stu-id="da362-207">Use hello `cache-lookup-value` policy tooperform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="da362-208">clave de Hello puede tener un valor de cadena arbitraria y se proporciona normalmente mediante una expresión de directiva.</span><span class="sxs-lookup"><span data-stu-id="da362-208">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="da362-209">Esta directiva debe tener una directiva [Store value in cache](#StoreToCacheByKey) (Almacenar valor en la caché) correspondiente.</span><span class="sxs-lookup"><span data-stu-id="da362-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="da362-210">Declaración de directiva</span><span class="sxs-lookup"><span data-stu-id="da362-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="da362-211">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="da362-211">Example</span></span>  
 <span data-ttu-id="da362-212">Para más información y ver ejemplos de esta directiva, consulte [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/) (Almacenamiento en caché personalizado en Azure API Management).</span><span class="sxs-lookup"><span data-stu-id="da362-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="da362-213">Elementos</span><span class="sxs-lookup"><span data-stu-id="da362-213">Elements</span></span>  
  
|<span data-ttu-id="da362-214">Nombre</span><span class="sxs-lookup"><span data-stu-id="da362-214">Name</span></span>|<span data-ttu-id="da362-215">Descripción</span><span class="sxs-lookup"><span data-stu-id="da362-215">Description</span></span>|<span data-ttu-id="da362-216">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="da362-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="da362-217">cache-lookup-value</span><span class="sxs-lookup"><span data-stu-id="da362-217">cache-lookup-value</span></span>|<span data-ttu-id="da362-218">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="da362-218">Root element.</span></span>|<span data-ttu-id="da362-219">Sí</span><span class="sxs-lookup"><span data-stu-id="da362-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="da362-220">Atributos</span><span class="sxs-lookup"><span data-stu-id="da362-220">Attributes</span></span>  
  
|<span data-ttu-id="da362-221">Nombre</span><span class="sxs-lookup"><span data-stu-id="da362-221">Name</span></span>|<span data-ttu-id="da362-222">Descripción</span><span class="sxs-lookup"><span data-stu-id="da362-222">Description</span></span>|<span data-ttu-id="da362-223">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="da362-223">Required</span></span>|<span data-ttu-id="da362-224">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="da362-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="da362-225">default-value</span><span class="sxs-lookup"><span data-stu-id="da362-225">default-value</span></span>|<span data-ttu-id="da362-226">Un valor que se va a asignar toohello variable si generó un error de búsqueda de claves de caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="da362-226">A value that will be assigned toohello variable if hello cache key lookup resulted in a miss.</span></span> <span data-ttu-id="da362-227">Si no se especifica este atributo, se asigna `null`.</span><span class="sxs-lookup"><span data-stu-id="da362-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="da362-228">No</span><span class="sxs-lookup"><span data-stu-id="da362-228">No</span></span>|`null`|  
|<span data-ttu-id="da362-229">key</span><span class="sxs-lookup"><span data-stu-id="da362-229">key</span></span>|<span data-ttu-id="da362-230">Almacenar en caché toouse de valor de clave en la búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="da362-230">Cache key value toouse in hello lookup.</span></span>|<span data-ttu-id="da362-231">Sí</span><span class="sxs-lookup"><span data-stu-id="da362-231">Yes</span></span>|<span data-ttu-id="da362-232">N/D</span><span class="sxs-lookup"><span data-stu-id="da362-232">N/A</span></span>|  
|<span data-ttu-id="da362-233">variable-name</span><span class="sxs-lookup"><span data-stu-id="da362-233">variable-name</span></span>|<span data-ttu-id="da362-234">Nombre del programa Hola a [variable de contexto](api-management-policy-expressions.md#ContextVariables) Hola buscado valor se asignará a, si la búsqueda es correcta.</span><span class="sxs-lookup"><span data-stu-id="da362-234">Name of hello [context variable](api-management-policy-expressions.md#ContextVariables) hello looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="da362-235">Si se produce un error de búsqueda, se asignará variable Hola valor Hola de hello `default-value` atributo o `null`, si hello `default-value` se omite el atributo.</span><span class="sxs-lookup"><span data-stu-id="da362-235">If lookup results in a miss, hello variable will be assigned hello value of hello `default-value` attribute or `null`, if hello `default-value` attribute is omitted.</span></span>|<span data-ttu-id="da362-236">Sí</span><span class="sxs-lookup"><span data-stu-id="da362-236">Yes</span></span>|<span data-ttu-id="da362-237">N/D</span><span class="sxs-lookup"><span data-stu-id="da362-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="da362-238">Uso</span><span class="sxs-lookup"><span data-stu-id="da362-238">Usage</span></span>  
 <span data-ttu-id="da362-239">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="da362-239">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="da362-240">**Secciones de la directiva:** entrante, saliente, back-end y en caso de error</span><span class="sxs-lookup"><span data-stu-id="da362-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="da362-241">**Ámbitos de la directiva:** global, API, operación, producto</span><span class="sxs-lookup"><span data-stu-id="da362-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="da362-242"><a name="StoreToCacheByKey"></a> Store value in cache (Almacenar valor en la caché)</span><span class="sxs-lookup"><span data-stu-id="da362-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="da362-243">Hola `cache-store-value` realiza el almacenamiento en caché por clave.</span><span class="sxs-lookup"><span data-stu-id="da362-243">hello `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="da362-244">clave de Hello puede tener un valor de cadena arbitraria y se proporciona normalmente mediante una expresión de directiva.</span><span class="sxs-lookup"><span data-stu-id="da362-244">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="da362-245">Esta directiva debe tener una directiva [Get from cache](#GetFromCacheByKey) (Obtener de la caché) correspondiente.</span><span class="sxs-lookup"><span data-stu-id="da362-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="da362-246">Declaración de directiva</span><span class="sxs-lookup"><span data-stu-id="da362-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="da362-247">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="da362-247">Example</span></span>  
 <span data-ttu-id="da362-248">Para más información y ver ejemplos de esta directiva, consulte [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/) (Almacenamiento en caché personalizado en Azure API Management).</span><span class="sxs-lookup"><span data-stu-id="da362-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="da362-249">Elementos</span><span class="sxs-lookup"><span data-stu-id="da362-249">Elements</span></span>  
  
|<span data-ttu-id="da362-250">Nombre</span><span class="sxs-lookup"><span data-stu-id="da362-250">Name</span></span>|<span data-ttu-id="da362-251">Descripción</span><span class="sxs-lookup"><span data-stu-id="da362-251">Description</span></span>|<span data-ttu-id="da362-252">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="da362-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="da362-253">cache-store-value</span><span class="sxs-lookup"><span data-stu-id="da362-253">cache-store-value</span></span>|<span data-ttu-id="da362-254">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="da362-254">Root element.</span></span>|<span data-ttu-id="da362-255">Sí</span><span class="sxs-lookup"><span data-stu-id="da362-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="da362-256">Atributos</span><span class="sxs-lookup"><span data-stu-id="da362-256">Attributes</span></span>  
  
|<span data-ttu-id="da362-257">Nombre</span><span class="sxs-lookup"><span data-stu-id="da362-257">Name</span></span>|<span data-ttu-id="da362-258">Descripción</span><span class="sxs-lookup"><span data-stu-id="da362-258">Description</span></span>|<span data-ttu-id="da362-259">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="da362-259">Required</span></span>|<span data-ttu-id="da362-260">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="da362-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="da362-261">duration</span><span class="sxs-lookup"><span data-stu-id="da362-261">duration</span></span>|<span data-ttu-id="da362-262">Valor se almacenarán en caché para hello proporcionada el valor de duración, especificado en segundos.</span><span class="sxs-lookup"><span data-stu-id="da362-262">Value will be cached for hello provided duration value, specified in seconds.</span></span>|<span data-ttu-id="da362-263">Sí</span><span class="sxs-lookup"><span data-stu-id="da362-263">Yes</span></span>|<span data-ttu-id="da362-264">N/D</span><span class="sxs-lookup"><span data-stu-id="da362-264">N/A</span></span>|  
|<span data-ttu-id="da362-265">key</span><span class="sxs-lookup"><span data-stu-id="da362-265">key</span></span>|<span data-ttu-id="da362-266">Valor de clave Hola de caché se almacenarán en.</span><span class="sxs-lookup"><span data-stu-id="da362-266">Cache key hello value will be stored under.</span></span>|<span data-ttu-id="da362-267">Sí</span><span class="sxs-lookup"><span data-stu-id="da362-267">Yes</span></span>|<span data-ttu-id="da362-268">N/D</span><span class="sxs-lookup"><span data-stu-id="da362-268">N/A</span></span>|  
|<span data-ttu-id="da362-269">value</span><span class="sxs-lookup"><span data-stu-id="da362-269">value</span></span>|<span data-ttu-id="da362-270">Hola toobe de valor almacenado en memoria caché.</span><span class="sxs-lookup"><span data-stu-id="da362-270">hello value toobe cached.</span></span>|<span data-ttu-id="da362-271">Sí</span><span class="sxs-lookup"><span data-stu-id="da362-271">Yes</span></span>|<span data-ttu-id="da362-272">N/D</span><span class="sxs-lookup"><span data-stu-id="da362-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="da362-273">Uso</span><span class="sxs-lookup"><span data-stu-id="da362-273">Usage</span></span>  
 <span data-ttu-id="da362-274">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="da362-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="da362-275">**Secciones de la directiva:** entrante, saliente, back-end y en caso de error</span><span class="sxs-lookup"><span data-stu-id="da362-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="da362-276">**Ámbitos de la directiva:** global, API, operación, producto</span><span class="sxs-lookup"><span data-stu-id="da362-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="da362-277"><a name="RemoveCacheByKey"></a> Remove value from cache (Quitar valor de la caché)</span><span class="sxs-lookup"><span data-stu-id="da362-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="da362-278">Hola `cache-remove-value` elimina un elemento almacenado en caché identificado por su clave.</span><span class="sxs-lookup"><span data-stu-id="da362-278">hello             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="da362-279">clave de Hello puede tener un valor de cadena arbitraria y se proporciona normalmente mediante una expresión de directiva.</span><span class="sxs-lookup"><span data-stu-id="da362-279">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="da362-280">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="da362-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="da362-281">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="da362-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="da362-282">Elementos</span><span class="sxs-lookup"><span data-stu-id="da362-282">Elements</span></span>  
  
|<span data-ttu-id="da362-283">Nombre</span><span class="sxs-lookup"><span data-stu-id="da362-283">Name</span></span>|<span data-ttu-id="da362-284">Descripción</span><span class="sxs-lookup"><span data-stu-id="da362-284">Description</span></span>|<span data-ttu-id="da362-285">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="da362-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="da362-286">cache-remove-value</span><span class="sxs-lookup"><span data-stu-id="da362-286">cache-remove-value</span></span>|<span data-ttu-id="da362-287">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="da362-287">Root element.</span></span>|<span data-ttu-id="da362-288">Sí</span><span class="sxs-lookup"><span data-stu-id="da362-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="da362-289">Atributos</span><span class="sxs-lookup"><span data-stu-id="da362-289">Attributes</span></span>  
  
|<span data-ttu-id="da362-290">Nombre</span><span class="sxs-lookup"><span data-stu-id="da362-290">Name</span></span>|<span data-ttu-id="da362-291">Descripción</span><span class="sxs-lookup"><span data-stu-id="da362-291">Description</span></span>|<span data-ttu-id="da362-292">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="da362-292">Required</span></span>|<span data-ttu-id="da362-293">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="da362-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="da362-294">key</span><span class="sxs-lookup"><span data-stu-id="da362-294">key</span></span>|<span data-ttu-id="da362-295">clave de Hola de hello previamente en caché toobe valor quitado de la memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="da362-295">hello key of hello previously cached value toobe removed from hello cache.</span></span>|<span data-ttu-id="da362-296">Sí</span><span class="sxs-lookup"><span data-stu-id="da362-296">Yes</span></span>|<span data-ttu-id="da362-297">N/D</span><span class="sxs-lookup"><span data-stu-id="da362-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="da362-298">Uso</span><span class="sxs-lookup"><span data-stu-id="da362-298">Usage</span></span>  
 <span data-ttu-id="da362-299">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="da362-299">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="da362-300">**Secciones de la directiva:** entrante, saliente, back-end y en caso de error</span><span class="sxs-lookup"><span data-stu-id="da362-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="da362-301">**Ámbitos de la directiva:** global, API, operación, producto</span><span class="sxs-lookup"><span data-stu-id="da362-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="da362-302">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="da362-302">Next steps</span></span>
<span data-ttu-id="da362-303">Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="da362-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  