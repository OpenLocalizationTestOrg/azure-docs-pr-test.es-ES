---
title: "Administración de API de aaaAzure directivas entre dominios | Documentos de Microsoft"
description: "Obtenga información acerca de hello directivas entre dominios disponibles para su uso en la administración de API de Azure."
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
ms.openlocfilehash: dd5ebfd65b92ebd0c1f589a2bac669a3928d40b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="8210a-103">Directivas entre dominios de Administración de API</span><span class="sxs-lookup"><span data-stu-id="8210a-103">API Management cross domain policies</span></span>
<span data-ttu-id="8210a-104">En este tema se proporciona una referencia para hello las siguientes directivas de administración de API.</span><span class="sxs-lookup"><span data-stu-id="8210a-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="8210a-105">Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="8210a-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="8210a-106"><a name="CrossDomainPolicies"></a> Directivas entre dominios</span><span class="sxs-lookup"><span data-stu-id="8210a-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="8210a-107">[Permitir llamadas entre dominios](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -hace Hola API sea accesible desde clientes basados en exploradores de Adobe Flash y Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="8210a-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="8210a-108">[CORS](api-management-cross-domain-policies.md#CORS) -agrega recursos entre orígenes (CORS) de uso compartido admite la operación de tooan o llama a una API tooallow dominios desde clientes basados en explorador.</span><span class="sxs-lookup"><span data-stu-id="8210a-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="8210a-109">[JSONP](api-management-cross-domain-policies.md#JSONP) : agrega JSON con relleno (JSONP) soporte tooan operación o llama a una API tooallow dominios desde clientes basados en exploradores de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8210a-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="8210a-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls (Permitir llamadas entre dominios)</span><span class="sxs-lookup"><span data-stu-id="8210a-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="8210a-111">Hola de uso `cross-domain` Hola de toomake directiva API que sea accesible desde clientes basados en exploradores de Adobe Flash y Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="8210a-111">Use hello `cross-domain` policy toomake hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8210a-112">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="8210a-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="8210a-113">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8210a-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="8210a-114">Elementos</span><span class="sxs-lookup"><span data-stu-id="8210a-114">Elements</span></span>  
  
|<span data-ttu-id="8210a-115">Nombre</span><span class="sxs-lookup"><span data-stu-id="8210a-115">Name</span></span>|<span data-ttu-id="8210a-116">Descripción</span><span class="sxs-lookup"><span data-stu-id="8210a-116">Description</span></span>|<span data-ttu-id="8210a-117">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8210a-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8210a-118">entre dominios</span><span class="sxs-lookup"><span data-stu-id="8210a-118">cross-domain</span></span>|<span data-ttu-id="8210a-119">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="8210a-119">Root element.</span></span> <span data-ttu-id="8210a-120">Elementos secundarios deben ajustarse toohello [especificación de archivo de directivas entre dominios de Adobe](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span><span class="sxs-lookup"><span data-stu-id="8210a-120">Child elements must conform toohello [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="8210a-121">Sí</span><span class="sxs-lookup"><span data-stu-id="8210a-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8210a-122">Uso</span><span class="sxs-lookup"><span data-stu-id="8210a-122">Usage</span></span>  
 <span data-ttu-id="8210a-123">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="8210a-123">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8210a-124">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="8210a-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="8210a-125">**Ámbitos de la directiva:** global</span><span class="sxs-lookup"><span data-stu-id="8210a-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="8210a-126"><a name="CORS"></a> CORS</span><span class="sxs-lookup"><span data-stu-id="8210a-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="8210a-127">Hola `cors` directiva agrega recursos entre orígenes (CORS) de uso compartido admite la operación de tooan o llama a una API tooallow dominios desde clientes basados en explorador.</span><span class="sxs-lookup"><span data-stu-id="8210a-127">hello `cors` policy adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="8210a-128">CORS permite que un explorador y un servidor toointeract y determinar si se permite o no tooallow específicas entre orígenes las solicitudes (es decir, llamadas XMLHttpRequests realizadas desde JavaScript en una página web tooother los dominios).</span><span class="sxs-lookup"><span data-stu-id="8210a-128">CORS allows a browser and a server toointeract and determine whether or not tooallow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page tooother domains).</span></span> <span data-ttu-id="8210a-129">Esto permite más flexibilidad que si solo se permiten solicitudes del mismo origen, pero es más seguro que permitir todas las solicitudes entre orígenes.</span><span class="sxs-lookup"><span data-stu-id="8210a-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8210a-130">Declaración de directiva</span><span class="sxs-lookup"><span data-stu-id="8210a-130">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="8210a-131">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8210a-131">Example</span></span>  
 <span data-ttu-id="8210a-132">En este ejemplo se muestra cómo las solicitudes preparatorias toosupport, como aquellos con encabezados personalizados o métodos distintos de GET y POST.</span><span class="sxs-lookup"><span data-stu-id="8210a-132">This example demonstrates how toosupport pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="8210a-133">encabezados personalizados toosupport y verbos HTTP adicionales, use hello `allowed-methods` y `allowed-headers` secciones tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8210a-133">toosupport custom headers and additional HTTP verbs, use hello `allowed-methods` and `allowed-headers` sections as shown in hello following example.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="8210a-134">Elementos</span><span class="sxs-lookup"><span data-stu-id="8210a-134">Elements</span></span>  
  
|<span data-ttu-id="8210a-135">Nombre</span><span class="sxs-lookup"><span data-stu-id="8210a-135">Name</span></span>|<span data-ttu-id="8210a-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="8210a-136">Description</span></span>|<span data-ttu-id="8210a-137">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8210a-137">Required</span></span>|<span data-ttu-id="8210a-138">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="8210a-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8210a-139">cors</span><span class="sxs-lookup"><span data-stu-id="8210a-139">cors</span></span>|<span data-ttu-id="8210a-140">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="8210a-140">Root element.</span></span>|<span data-ttu-id="8210a-141">Sí</span><span class="sxs-lookup"><span data-stu-id="8210a-141">Yes</span></span>|<span data-ttu-id="8210a-142">N/D</span><span class="sxs-lookup"><span data-stu-id="8210a-142">N/A</span></span>|  
|<span data-ttu-id="8210a-143">allowed-origins</span><span class="sxs-lookup"><span data-stu-id="8210a-143">allowed-origins</span></span>|<span data-ttu-id="8210a-144">Contiene `origin` elementos que describen la Hola permitida orígenes para las solicitudes entre dominios.</span><span class="sxs-lookup"><span data-stu-id="8210a-144">Contains `origin` elements that describe hello allowed origins for cross-domain requests.</span></span> <span data-ttu-id="8210a-145">`allowed-origins`puede contener un único `origin` elemento que especifica `*` tooallow cualquier origen, o uno o varios `origin` elementos que contienen un identificador URI.</span><span class="sxs-lookup"><span data-stu-id="8210a-145">`allowed-origins` can contain either a single `origin` element that specifies `*` tooallow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="8210a-146">Sí</span><span class="sxs-lookup"><span data-stu-id="8210a-146">Yes</span></span>|<span data-ttu-id="8210a-147">N/D</span><span class="sxs-lookup"><span data-stu-id="8210a-147">N/A</span></span>|  
|<span data-ttu-id="8210a-148">origin</span><span class="sxs-lookup"><span data-stu-id="8210a-148">origin</span></span>|<span data-ttu-id="8210a-149">Hello valor puede ser `*` tooallow todos los orígenes o un URI que especifica un único origen.</span><span class="sxs-lookup"><span data-stu-id="8210a-149">hello value can be either `*` tooallow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="8210a-150">Hola URI debe incluir un esquema, host y puerto.</span><span class="sxs-lookup"><span data-stu-id="8210a-150">hello URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="8210a-151">Sí</span><span class="sxs-lookup"><span data-stu-id="8210a-151">Yes</span></span>|<span data-ttu-id="8210a-152">Si se omite el puerto de hello en un URI, usa el puerto 80 para HTTP y se utiliza el puerto 443 para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8210a-152">If hello port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="8210a-153">allowed-methods</span><span class="sxs-lookup"><span data-stu-id="8210a-153">allowed-methods</span></span>|<span data-ttu-id="8210a-154">Este elemento es necesario si se permiten métodos distintos de GET o POST.</span><span class="sxs-lookup"><span data-stu-id="8210a-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="8210a-155">Contiene `method` elementos que especifican Hola admite verbos HTTP.</span><span class="sxs-lookup"><span data-stu-id="8210a-155">Contains `method` elements that specify hello supported HTTP verbs.</span></span>|<span data-ttu-id="8210a-156">No</span><span class="sxs-lookup"><span data-stu-id="8210a-156">No</span></span>|<span data-ttu-id="8210a-157">Si esta sección no está presente, se admiten GET y POST.</span><span class="sxs-lookup"><span data-stu-id="8210a-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="8210a-158">estático</span><span class="sxs-lookup"><span data-stu-id="8210a-158">method</span></span>|<span data-ttu-id="8210a-159">Especifica un verbo HTTP.</span><span class="sxs-lookup"><span data-stu-id="8210a-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="8210a-160">Al menos un `method` elemento es necesario si hello `allowed-methods` sección está presente.</span><span class="sxs-lookup"><span data-stu-id="8210a-160">At least one `method` element is required if hello `allowed-methods` section is present.</span></span>|<span data-ttu-id="8210a-161">N/D</span><span class="sxs-lookup"><span data-stu-id="8210a-161">N/A</span></span>|  
|<span data-ttu-id="8210a-162">allowed-headers</span><span class="sxs-lookup"><span data-stu-id="8210a-162">allowed-headers</span></span>|<span data-ttu-id="8210a-163">Este elemento contiene `header` elementos especifican nombres de encabezados de Hola que pueden incluirse en la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="8210a-163">This element contains `header` elements specifying names of hello headers that can be included in hello request.</span></span>|<span data-ttu-id="8210a-164">No</span><span class="sxs-lookup"><span data-stu-id="8210a-164">No</span></span>|<span data-ttu-id="8210a-165">N/D</span><span class="sxs-lookup"><span data-stu-id="8210a-165">N/A</span></span>|  
|<span data-ttu-id="8210a-166">expose-headers</span><span class="sxs-lookup"><span data-stu-id="8210a-166">expose-headers</span></span>|<span data-ttu-id="8210a-167">Este elemento contiene `header` elementos especifican nombres de encabezados de Hola que estarán accesibles por cliente Hola.</span><span class="sxs-lookup"><span data-stu-id="8210a-167">This element contains `header` elements specifying names of hello headers that will be accessible by hello client.</span></span>|<span data-ttu-id="8210a-168">No</span><span class="sxs-lookup"><span data-stu-id="8210a-168">No</span></span>|<span data-ttu-id="8210a-169">N/D</span><span class="sxs-lookup"><span data-stu-id="8210a-169">N/A</span></span>|  
|<span data-ttu-id="8210a-170">encabezado</span><span class="sxs-lookup"><span data-stu-id="8210a-170">header</span></span>|<span data-ttu-id="8210a-171">Especifica un nombre de encabezado.</span><span class="sxs-lookup"><span data-stu-id="8210a-171">Specifies a header name.</span></span>|<span data-ttu-id="8210a-172">Al menos un `header` elemento es necesario en `allowed-headers` o `expose-headers` si Hola sección está presente.</span><span class="sxs-lookup"><span data-stu-id="8210a-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if hello section is present.</span></span>|<span data-ttu-id="8210a-173">N/D</span><span class="sxs-lookup"><span data-stu-id="8210a-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8210a-174">Attributes</span><span class="sxs-lookup"><span data-stu-id="8210a-174">Attributes</span></span>  
  
|<span data-ttu-id="8210a-175">Nombre</span><span class="sxs-lookup"><span data-stu-id="8210a-175">Name</span></span>|<span data-ttu-id="8210a-176">Descripción</span><span class="sxs-lookup"><span data-stu-id="8210a-176">Description</span></span>|<span data-ttu-id="8210a-177">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8210a-177">Required</span></span>|<span data-ttu-id="8210a-178">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="8210a-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8210a-179">allow-credentials</span><span class="sxs-lookup"><span data-stu-id="8210a-179">allow-credentials</span></span>|<span data-ttu-id="8210a-180">Hola `Access-Control-Allow-Credentials` encabezado de respuesta preparatoria Hola se establezca el valor de este atributo toohello y afecta a credenciales de toosubmit de capacidad del cliente de hello en solicitudes entre dominios.</span><span class="sxs-lookup"><span data-stu-id="8210a-180">hello `Access-Control-Allow-Credentials` header in hello preflight response will be set toohello value of this attribute and affect hello client’s ability toosubmit credentials in cross-domain requests.</span></span>|<span data-ttu-id="8210a-181">No</span><span class="sxs-lookup"><span data-stu-id="8210a-181">No</span></span>|<span data-ttu-id="8210a-182">false</span><span class="sxs-lookup"><span data-stu-id="8210a-182">false</span></span>|  
|<span data-ttu-id="8210a-183">preflight-result-max-age</span><span class="sxs-lookup"><span data-stu-id="8210a-183">preflight-result-max-age</span></span>|<span data-ttu-id="8210a-184">Hola `Access-Control-Max-Age` encabezado de respuesta preparatoria Hola se establezca el valor de este atributo toohello y afectan a la respuesta preparatoria del agente de usuario de hello capacidad toocache.</span><span class="sxs-lookup"><span data-stu-id="8210a-184">hello `Access-Control-Max-Age` header in hello preflight response will be set toohello value of this attribute and affect hello user agent’s ability toocache pre-flight response.</span></span>|<span data-ttu-id="8210a-185">No</span><span class="sxs-lookup"><span data-stu-id="8210a-185">No</span></span>|<span data-ttu-id="8210a-186">0</span><span class="sxs-lookup"><span data-stu-id="8210a-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8210a-187">Uso</span><span class="sxs-lookup"><span data-stu-id="8210a-187">Usage</span></span>  
 <span data-ttu-id="8210a-188">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="8210a-188">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8210a-189">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="8210a-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="8210a-190">**Ámbitos de la directiva:** API, operación</span><span class="sxs-lookup"><span data-stu-id="8210a-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="8210a-191"><a name="JSONP"></a> JSONP</span><span class="sxs-lookup"><span data-stu-id="8210a-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="8210a-192">Hola `jsonp` directiva agrega JSON con relleno de la operación de tooan de soporte (JSONP) o un llamadas a API tooallow entre dominios desde clientes basados en exploradores de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8210a-192">hello `jsonp` policy adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="8210a-193">JSONP es un método utilizado en los datos de toorequest de programas de JavaScript de un servidor en un dominio diferente.</span><span class="sxs-lookup"><span data-stu-id="8210a-193">JSONP is a method used in JavaScript programs toorequest data from a server in a different domain.</span></span> <span data-ttu-id="8210a-194">JSONP omite la limitación de hello aplicada por la mayoría de los exploradores web que las páginas de tooweb de acceso deben tener Hola mismo dominio.</span><span class="sxs-lookup"><span data-stu-id="8210a-194">JSONP bypasses hello limitation enforced by most web browsers where access tooweb pages must be in hello same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8210a-195">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="8210a-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="8210a-196">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8210a-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="8210a-197">Si llama al método hello sin el parámetro de devolución de llamada de hello? cb = XXX, devolverá JSON sin formato (sin un contenedor de llamadas de función).</span><span class="sxs-lookup"><span data-stu-id="8210a-197">If you call hello method without hello callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="8210a-198">Si agrega el parámetro de devolución de llamada de hello `?cb=XXX` devolverá un resultado JSONP, ajuste resultados JSON originales de hello alrededor de la función de devolución de llamada de hello como`XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="8210a-198">If you add hello callback parameter `?cb=XXX` it will return a JSONP result, wrapping hello original JSON results around hello callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="8210a-199">Elementos</span><span class="sxs-lookup"><span data-stu-id="8210a-199">Elements</span></span>  
  
|<span data-ttu-id="8210a-200">Nombre</span><span class="sxs-lookup"><span data-stu-id="8210a-200">Name</span></span>|<span data-ttu-id="8210a-201">Descripción</span><span class="sxs-lookup"><span data-stu-id="8210a-201">Description</span></span>|<span data-ttu-id="8210a-202">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8210a-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8210a-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="8210a-203">jsonp</span></span>|<span data-ttu-id="8210a-204">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="8210a-204">Root element.</span></span>|<span data-ttu-id="8210a-205">Sí</span><span class="sxs-lookup"><span data-stu-id="8210a-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8210a-206">Atributos</span><span class="sxs-lookup"><span data-stu-id="8210a-206">Attributes</span></span>  
  
|<span data-ttu-id="8210a-207">Nombre</span><span class="sxs-lookup"><span data-stu-id="8210a-207">Name</span></span>|<span data-ttu-id="8210a-208">Descripción</span><span class="sxs-lookup"><span data-stu-id="8210a-208">Description</span></span>|<span data-ttu-id="8210a-209">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8210a-209">Required</span></span>|<span data-ttu-id="8210a-210">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="8210a-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8210a-211">callback-parameter-name</span><span class="sxs-lookup"><span data-stu-id="8210a-211">callback-parameter-name</span></span>|<span data-ttu-id="8210a-212">Hello llamada de función de JavaScript entre dominios como prefijo con el nombre de dominio completo de Hola donde hello función reside.</span><span class="sxs-lookup"><span data-stu-id="8210a-212">hello cross-domain JavaScript function call prefixed with hello fully qualified domain name where hello function resides.</span></span>|<span data-ttu-id="8210a-213">Sí</span><span class="sxs-lookup"><span data-stu-id="8210a-213">Yes</span></span>|<span data-ttu-id="8210a-214">N/D</span><span class="sxs-lookup"><span data-stu-id="8210a-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8210a-215">Uso</span><span class="sxs-lookup"><span data-stu-id="8210a-215">Usage</span></span>  
 <span data-ttu-id="8210a-216">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="8210a-216">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8210a-217">**Secciones de la directiva:** outbound</span><span class="sxs-lookup"><span data-stu-id="8210a-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="8210a-218">**Ámbitos de la directiva:** global, producto, API, operación</span><span class="sxs-lookup"><span data-stu-id="8210a-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="8210a-219">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8210a-219">Next steps</span></span>
<span data-ttu-id="8210a-220">Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="8210a-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  