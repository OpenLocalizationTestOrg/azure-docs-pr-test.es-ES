---
title: Directivas entre dominios de Azure API Management | Microsoft Docs
description: Aprenda sobre las directivas entre dominios disponibles para su uso en Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7689d277-8abe-472a-a78c-e6d4bd43455d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ddca9e35b44a21294abbb5eaa4418bcdb85494cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="cad8d-103">Directivas entre dominios de Administración de API</span><span class="sxs-lookup"><span data-stu-id="cad8d-103">API Management cross domain policies</span></span>
<span data-ttu-id="cad8d-104">En este tema se proporciona una referencia para las siguientes directivas de API Management.</span><span class="sxs-lookup"><span data-stu-id="cad8d-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="cad8d-105">Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="cad8d-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="cad8d-106"><a name="CrossDomainPolicies"></a> Directivas entre dominios</span><span class="sxs-lookup"><span data-stu-id="cad8d-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="cad8d-107">[Permitir llamadas entre dominios](api-management-cross-domain-policies.md#AllowCrossDomainCalls) : permite que la API sea accesible desde los clientes basados en explorador de Adobe Flash y Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="cad8d-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="cad8d-108">[CORS](api-management-cross-domain-policies.md#CORS) : agrega soporte de uso compartido de recursos entre orígenes (CORS) a una operación o a una API para permitir llamadas entre dominios desde clientes basados en explorador.</span><span class="sxs-lookup"><span data-stu-id="cad8d-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="cad8d-109">[JSONP](api-management-cross-domain-policies.md#JSONP) : agrega JSON con soporte de relleno (JSONP) a una operación o a una API para permitir llamadas entre dominios desde clientes basados en explorador de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="cad8d-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="cad8d-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls (Permitir llamadas entre dominios)</span><span class="sxs-lookup"><span data-stu-id="cad8d-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="cad8d-111">Use la directiva `cross-domain` para que la API sea accesible desde Adobe Flash y clientes basados en explorador de Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="cad8d-111">Use the `cross-domain` policy to make the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="cad8d-112">Declaración de directiva</span><span class="sxs-lookup"><span data-stu-id="cad8d-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in the Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="cad8d-113">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="cad8d-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="cad8d-114">Elementos</span><span class="sxs-lookup"><span data-stu-id="cad8d-114">Elements</span></span>  
  
|<span data-ttu-id="cad8d-115">Nombre</span><span class="sxs-lookup"><span data-stu-id="cad8d-115">Name</span></span>|<span data-ttu-id="cad8d-116">Descripción</span><span class="sxs-lookup"><span data-stu-id="cad8d-116">Description</span></span>|<span data-ttu-id="cad8d-117">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="cad8d-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="cad8d-118">entre dominios</span><span class="sxs-lookup"><span data-stu-id="cad8d-118">cross-domain</span></span>|<span data-ttu-id="cad8d-119">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="cad8d-119">Root element.</span></span> <span data-ttu-id="cad8d-120">Los elementos secundarios deben ajustarse a la [especificación de archivos de directivas entre dominios de Adobe](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span><span class="sxs-lookup"><span data-stu-id="cad8d-120">Child elements must conform to the [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="cad8d-121">Sí</span><span class="sxs-lookup"><span data-stu-id="cad8d-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="cad8d-122">Uso</span><span class="sxs-lookup"><span data-stu-id="cad8d-122">Usage</span></span>  
 <span data-ttu-id="cad8d-123">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="cad8d-123">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cad8d-124">**Secciones de la directiva:** inbound</span><span class="sxs-lookup"><span data-stu-id="cad8d-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="cad8d-125">**Ámbitos de la directiva:** global</span><span class="sxs-lookup"><span data-stu-id="cad8d-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="cad8d-126"><a name="CORS"></a> CORS</span><span class="sxs-lookup"><span data-stu-id="cad8d-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="cad8d-127">La directiva `cors` agrega compatibilidad con el uso compartido de recursos entre orígenes (CORS) a una operación o a una API para permitir llamadas entre dominios desde clientes basados en explorador.</span><span class="sxs-lookup"><span data-stu-id="cad8d-127">The `cors` policy adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="cad8d-128">CORS permite a un explorador y a un servidor interactuar y determinar si se permiten o no solicitudes específicas entre orígenes (por ejemplo, llamadas XMLHttpRequests realizadas desde JavaScript en una página web a otros dominios).</span><span class="sxs-lookup"><span data-stu-id="cad8d-128">CORS allows a browser and a server to interact and determine whether or not to allow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page to other domains).</span></span> <span data-ttu-id="cad8d-129">Esto permite más flexibilidad que si solo se permiten solicitudes del mismo origen, pero es más seguro que permitir todas las solicitudes entre orígenes.</span><span class="sxs-lookup"><span data-stu-id="cad8d-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="cad8d-130">Declaración de directiva</span><span class="sxs-lookup"><span data-stu-id="cad8d-130">Policy statement</span></span>  
  
```xml  
<cors allow-credentials="false|true">  
    <allowed-origins>  
        <origin>origin uri</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="number of seconds">  
        <method>http verb</method>  
    </allowed-methods>  
    <allowed-headers>  
        <header>header name</header>  
    </allowed-headers>  
    <expose-headers>  
        <header>header name</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="example"></a><span data-ttu-id="cad8d-131">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="cad8d-131">Example</span></span>  
 <span data-ttu-id="cad8d-132">En este ejemplo se muestra cómo admitir solicitudes preparatorias, como aquellas con encabezados o métodos personalizados distintos de GET y POST.</span><span class="sxs-lookup"><span data-stu-id="cad8d-132">This example demonstrates how to support pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="cad8d-133">Para admitir encabezados personalizados y verbos HTTP adicionales, use las secciones `allowed-methods` y `allowed-headers` tal como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="cad8d-133">To support custom headers and additional HTTP verbs, use the `allowed-methods` and `allowed-headers` sections as shown in the following example.</span></span>  
  
```xml  
<cors allow-credentials="true">  
    <allowed-origins>  
        <!-- Localhost useful for development -->  
        <origin>http://localhost:8080/</origin>  
        <origin>http://example.com/</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="300">  
        <method>GET</method>  
        <method>POST</method>  
        <method>PATCH</method>  
        <method>DELETE</method>  
    </allowed-methods>  
    <allowed-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
        <header>x-zumo-version</header>  
        <header>x-zumo-auth</header>  
        <header>content-type</header>  
        <header>accept</header>  
    </allowed-headers>  
    <expose-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="elements"></a><span data-ttu-id="cad8d-134">Elementos</span><span class="sxs-lookup"><span data-stu-id="cad8d-134">Elements</span></span>  
  
|<span data-ttu-id="cad8d-135">Nombre</span><span class="sxs-lookup"><span data-stu-id="cad8d-135">Name</span></span>|<span data-ttu-id="cad8d-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="cad8d-136">Description</span></span>|<span data-ttu-id="cad8d-137">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="cad8d-137">Required</span></span>|<span data-ttu-id="cad8d-138">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="cad8d-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="cad8d-139">cors</span><span class="sxs-lookup"><span data-stu-id="cad8d-139">cors</span></span>|<span data-ttu-id="cad8d-140">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="cad8d-140">Root element.</span></span>|<span data-ttu-id="cad8d-141">Sí</span><span class="sxs-lookup"><span data-stu-id="cad8d-141">Yes</span></span>|<span data-ttu-id="cad8d-142">N/D</span><span class="sxs-lookup"><span data-stu-id="cad8d-142">N/A</span></span>|  
|<span data-ttu-id="cad8d-143">allowed-origins</span><span class="sxs-lookup"><span data-stu-id="cad8d-143">allowed-origins</span></span>|<span data-ttu-id="cad8d-144">Contiene elementos `origin` que describen los orígenes permitidos para las solicitudes entre dominios.</span><span class="sxs-lookup"><span data-stu-id="cad8d-144">Contains `origin` elements that describe the allowed origins for cross-domain requests.</span></span> <span data-ttu-id="cad8d-145">`allowed-origins` puede contener un único elemento `origin` que especifica `*` para permitir cualquier origen, o uno o varios elementos `origin` que contienen un identificador URI.</span><span class="sxs-lookup"><span data-stu-id="cad8d-145">`allowed-origins` can contain either a single `origin` element that specifies `*` to allow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="cad8d-146">Sí</span><span class="sxs-lookup"><span data-stu-id="cad8d-146">Yes</span></span>|<span data-ttu-id="cad8d-147">N/D</span><span class="sxs-lookup"><span data-stu-id="cad8d-147">N/A</span></span>|  
|<span data-ttu-id="cad8d-148">origin</span><span class="sxs-lookup"><span data-stu-id="cad8d-148">origin</span></span>|<span data-ttu-id="cad8d-149">El valor puede ser `*` para permitir todos los orígenes o un identificador URI que especifica un único origen.</span><span class="sxs-lookup"><span data-stu-id="cad8d-149">The value can be either `*` to allow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="cad8d-150">El URI debe incluir un esquema, un host y un puerto.</span><span class="sxs-lookup"><span data-stu-id="cad8d-150">The URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="cad8d-151">Sí</span><span class="sxs-lookup"><span data-stu-id="cad8d-151">Yes</span></span>|<span data-ttu-id="cad8d-152">Si se omite el puerto en un identificador URI, se usa el puerto 80 para HTTP y el puerto 443 para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="cad8d-152">If the port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="cad8d-153">allowed-methods</span><span class="sxs-lookup"><span data-stu-id="cad8d-153">allowed-methods</span></span>|<span data-ttu-id="cad8d-154">Este elemento es necesario si se permiten métodos distintos de GET o POST.</span><span class="sxs-lookup"><span data-stu-id="cad8d-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="cad8d-155">Contiene elementos `method` que especifican los verbos HTTP admitidos.</span><span class="sxs-lookup"><span data-stu-id="cad8d-155">Contains `method` elements that specify the supported HTTP verbs.</span></span>|<span data-ttu-id="cad8d-156">No</span><span class="sxs-lookup"><span data-stu-id="cad8d-156">No</span></span>|<span data-ttu-id="cad8d-157">Si esta sección no está presente, se admiten GET y POST.</span><span class="sxs-lookup"><span data-stu-id="cad8d-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="cad8d-158">estático</span><span class="sxs-lookup"><span data-stu-id="cad8d-158">method</span></span>|<span data-ttu-id="cad8d-159">Especifica un verbo HTTP.</span><span class="sxs-lookup"><span data-stu-id="cad8d-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="cad8d-160">Al menos un elemento `method` es necesario si la sección `allowed-methods` está presente.</span><span class="sxs-lookup"><span data-stu-id="cad8d-160">At least one `method` element is required if the `allowed-methods` section is present.</span></span>|<span data-ttu-id="cad8d-161">N/D</span><span class="sxs-lookup"><span data-stu-id="cad8d-161">N/A</span></span>|  
|<span data-ttu-id="cad8d-162">allowed-headers</span><span class="sxs-lookup"><span data-stu-id="cad8d-162">allowed-headers</span></span>|<span data-ttu-id="cad8d-163">Este elemento contiene elementos `header` que especifican los nombres de los encabezados que pueden incluirse en la solicitud.</span><span class="sxs-lookup"><span data-stu-id="cad8d-163">This element contains `header` elements specifying names of the headers that can be included in the request.</span></span>|<span data-ttu-id="cad8d-164">No</span><span class="sxs-lookup"><span data-stu-id="cad8d-164">No</span></span>|<span data-ttu-id="cad8d-165">N/D</span><span class="sxs-lookup"><span data-stu-id="cad8d-165">N/A</span></span>|  
|<span data-ttu-id="cad8d-166">expose-headers</span><span class="sxs-lookup"><span data-stu-id="cad8d-166">expose-headers</span></span>|<span data-ttu-id="cad8d-167">Este elemento contiene elementos `header` que especifican los nombres de los encabezados a los que tendrá acceso el cliente.</span><span class="sxs-lookup"><span data-stu-id="cad8d-167">This element contains `header` elements specifying names of the headers that will be accessible by the client.</span></span>|<span data-ttu-id="cad8d-168">No</span><span class="sxs-lookup"><span data-stu-id="cad8d-168">No</span></span>|<span data-ttu-id="cad8d-169">N/D</span><span class="sxs-lookup"><span data-stu-id="cad8d-169">N/A</span></span>|  
|<span data-ttu-id="cad8d-170">encabezado</span><span class="sxs-lookup"><span data-stu-id="cad8d-170">header</span></span>|<span data-ttu-id="cad8d-171">Especifica un nombre de encabezado.</span><span class="sxs-lookup"><span data-stu-id="cad8d-171">Specifies a header name.</span></span>|<span data-ttu-id="cad8d-172">Al menos un elemento `header` es necesario en `allowed-headers` o `expose-headers` si está presente la sección.</span><span class="sxs-lookup"><span data-stu-id="cad8d-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if the section is present.</span></span>|<span data-ttu-id="cad8d-173">N/D</span><span class="sxs-lookup"><span data-stu-id="cad8d-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="cad8d-174">Attributes</span><span class="sxs-lookup"><span data-stu-id="cad8d-174">Attributes</span></span>  
  
|<span data-ttu-id="cad8d-175">Nombre</span><span class="sxs-lookup"><span data-stu-id="cad8d-175">Name</span></span>|<span data-ttu-id="cad8d-176">Descripción</span><span class="sxs-lookup"><span data-stu-id="cad8d-176">Description</span></span>|<span data-ttu-id="cad8d-177">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="cad8d-177">Required</span></span>|<span data-ttu-id="cad8d-178">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="cad8d-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="cad8d-179">allow-credentials</span><span class="sxs-lookup"><span data-stu-id="cad8d-179">allow-credentials</span></span>|<span data-ttu-id="cad8d-180">El encabezado `Access-Control-Allow-Credentials` de la respuesta preparatoria se establecerá en el valor de este atributo e influirá en la posibilidad de que el cliente pueda enviar credenciales en solicitudes entre dominios.</span><span class="sxs-lookup"><span data-stu-id="cad8d-180">The `Access-Control-Allow-Credentials` header in the preflight response will be set to the value of this attribute and affect the client’s ability to submit credentials in cross-domain requests.</span></span>|<span data-ttu-id="cad8d-181">No</span><span class="sxs-lookup"><span data-stu-id="cad8d-181">No</span></span>|<span data-ttu-id="cad8d-182">false</span><span class="sxs-lookup"><span data-stu-id="cad8d-182">false</span></span>|  
|<span data-ttu-id="cad8d-183">preflight-result-max-age</span><span class="sxs-lookup"><span data-stu-id="cad8d-183">preflight-result-max-age</span></span>|<span data-ttu-id="cad8d-184">El encabezado `Access-Control-Max-Age` de la respuesta preparatoria se establecerá en el valor de este atributo e influirá en la posibilidad de que el agente del usuario pueda almacenar en caché la respuesta preparatoria.</span><span class="sxs-lookup"><span data-stu-id="cad8d-184">The `Access-Control-Max-Age` header in the preflight response will be set to the value of this attribute and affect the user agent’s ability to cache pre-flight response.</span></span>|<span data-ttu-id="cad8d-185">No</span><span class="sxs-lookup"><span data-stu-id="cad8d-185">No</span></span>|<span data-ttu-id="cad8d-186">0</span><span class="sxs-lookup"><span data-stu-id="cad8d-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="cad8d-187">Uso</span><span class="sxs-lookup"><span data-stu-id="cad8d-187">Usage</span></span>  
 <span data-ttu-id="cad8d-188">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="cad8d-188">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cad8d-189">**Secciones de la directiva:** inbound</span><span class="sxs-lookup"><span data-stu-id="cad8d-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="cad8d-190">**Ámbitos de la directiva:** API, operación</span><span class="sxs-lookup"><span data-stu-id="cad8d-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="cad8d-191"><a name="JSONP"></a> JSONP</span><span class="sxs-lookup"><span data-stu-id="cad8d-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="cad8d-192">La directiva `jsonp` agrega JSON con compatibilidad con relleno (JSONP) a una operación o a una API para permitir llamadas entre dominios desde clientes basados en explorador de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="cad8d-192">The `jsonp` policy adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="cad8d-193">JSONP es un método utilizado en los programas JavaScript para solicitar datos desde un servidor en un dominio diferente.</span><span class="sxs-lookup"><span data-stu-id="cad8d-193">JSONP is a method used in JavaScript programs to request data from a server in a different domain.</span></span> <span data-ttu-id="cad8d-194">JSONP sortea la limitación exigida por la mayoría de los exploradores web donde el acceso a las páginas web debe estar en el mismo dominio.</span><span class="sxs-lookup"><span data-stu-id="cad8d-194">JSONP bypasses the limitation enforced by most web browsers where access to web pages must be in the same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="cad8d-195">Declaración de directiva</span><span class="sxs-lookup"><span data-stu-id="cad8d-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="cad8d-196">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="cad8d-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="cad8d-197">Si llama al método sin el parámetro de devolución de llamada ?cb=XXX, devolverá JSON sin formato (sin un envoltorio de llamada de función).</span><span class="sxs-lookup"><span data-stu-id="cad8d-197">If you call the method without the callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="cad8d-198">Si agrega el parámetro de devolución de llamada `?cb=XXX`, devolverá un resultado JSONP, envolviendo los resultados JSON originales en torno a la función de devolución de llamada como `XYZ('<json result goes here>');`.</span><span class="sxs-lookup"><span data-stu-id="cad8d-198">If you add the callback parameter `?cb=XXX` it will return a JSONP result, wrapping the original JSON results around the callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="cad8d-199">Elementos</span><span class="sxs-lookup"><span data-stu-id="cad8d-199">Elements</span></span>  
  
|<span data-ttu-id="cad8d-200">Nombre</span><span class="sxs-lookup"><span data-stu-id="cad8d-200">Name</span></span>|<span data-ttu-id="cad8d-201">Descripción</span><span class="sxs-lookup"><span data-stu-id="cad8d-201">Description</span></span>|<span data-ttu-id="cad8d-202">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="cad8d-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="cad8d-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="cad8d-203">jsonp</span></span>|<span data-ttu-id="cad8d-204">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="cad8d-204">Root element.</span></span>|<span data-ttu-id="cad8d-205">Sí</span><span class="sxs-lookup"><span data-stu-id="cad8d-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="cad8d-206">Atributos</span><span class="sxs-lookup"><span data-stu-id="cad8d-206">Attributes</span></span>  
  
|<span data-ttu-id="cad8d-207">Nombre</span><span class="sxs-lookup"><span data-stu-id="cad8d-207">Name</span></span>|<span data-ttu-id="cad8d-208">Descripción</span><span class="sxs-lookup"><span data-stu-id="cad8d-208">Description</span></span>|<span data-ttu-id="cad8d-209">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="cad8d-209">Required</span></span>|<span data-ttu-id="cad8d-210">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="cad8d-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="cad8d-211">callback-parameter-name</span><span class="sxs-lookup"><span data-stu-id="cad8d-211">callback-parameter-name</span></span>|<span data-ttu-id="cad8d-212">La llamada de función de JavaScript entre dominios prefijada con el nombre de dominio completo en donde reside la función.</span><span class="sxs-lookup"><span data-stu-id="cad8d-212">The cross-domain JavaScript function call prefixed with the fully qualified domain name where the function resides.</span></span>|<span data-ttu-id="cad8d-213">Sí</span><span class="sxs-lookup"><span data-stu-id="cad8d-213">Yes</span></span>|<span data-ttu-id="cad8d-214">N/D</span><span class="sxs-lookup"><span data-stu-id="cad8d-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="cad8d-215">Uso</span><span class="sxs-lookup"><span data-stu-id="cad8d-215">Usage</span></span>  
 <span data-ttu-id="cad8d-216">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de las directivas.</span><span class="sxs-lookup"><span data-stu-id="cad8d-216">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cad8d-217">**Secciones de la directiva:** outbound</span><span class="sxs-lookup"><span data-stu-id="cad8d-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="cad8d-218">**Ámbitos de la directiva:** global, producto, API, operación</span><span class="sxs-lookup"><span data-stu-id="cad8d-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="cad8d-219">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cad8d-219">Next steps</span></span>
<span data-ttu-id="cad8d-220">Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="cad8d-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  