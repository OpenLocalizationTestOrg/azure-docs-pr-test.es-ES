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
# <a name="api-management-transformation-policies"></a><span data-ttu-id="19863-103">Directivas de transformación de API Management</span><span class="sxs-lookup"><span data-stu-id="19863-103">API Management transformation policies</span></span>
<span data-ttu-id="19863-104">En este tema se proporciona una referencia para hello las siguientes directivas de administración de API.</span><span class="sxs-lookup"><span data-stu-id="19863-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="19863-105">Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="19863-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="19863-106"><a name="TransformationPolicies"></a> Directivas de transformación</span><span class="sxs-lookup"><span data-stu-id="19863-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="19863-107">[Convertir JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) : convierte solicitar o cuerpo de la respuesta de JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="19863-107">[Convert JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON tooXML.</span></span>  
  
-   <span data-ttu-id="19863-108">[Convertir XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) : convierte solicitar o cuerpo de la respuesta de XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="19863-108">[Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML tooJSON.</span></span>  
  
-   <span data-ttu-id="19863-109">[Buscar y reemplazar la cadena en el cuerpo](api-management-transformation-policies.md#Findandreplacestringinbody) : encuentra una subcadena de solicitud o de respuesta y la reemplaza por una subcadena diferente.</span><span class="sxs-lookup"><span data-stu-id="19863-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="19863-110">[Enmascarar direcciones URL en contenido](api-management-transformation-policies.md#MaskURLSContent) -reescribe (enmascara) vínculos en la respuesta de hello cuerpo para que apunten toohello vínculo equivalente a través de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>  
  
-   <span data-ttu-id="19863-111">[Establecer el servicio back-end](api-management-transformation-policies.md#SetBackendService) -cambia el servicio back-end de Hola para una solicitud entrante.</span><span class="sxs-lookup"><span data-stu-id="19863-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes hello backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="19863-112">[Establecer cuerpo](api-management-transformation-policies.md#SetBody) -establece el cuerpo del mensaje de Hola para las solicitudes entrantes y salientes.</span><span class="sxs-lookup"><span data-stu-id="19863-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets hello message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="19863-113">[Definir el encabezado HTTP](api-management-transformation-policies.md#SetHTTPheader) : asigna una respuesta de valor tooan existente o un encabezado de solicitud o agrega un nuevo encabezado de respuesta y/o de solicitud.</span><span class="sxs-lookup"><span data-stu-id="19863-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="19863-114">[Establecer el parámetro de cadena de consulta](api-management-transformation-policies.md#SetQueryStringParameter) : agrega, reemplaza el valor o elimina el parámetro de la cadena de consulta de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="19863-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="19863-115">[Reescribir dirección URL](api-management-transformation-policies.md#RewriteURL) -convierte una dirección URL de solicitud desde su formato de toohello de formato público esperado por el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form toohello form expected by hello web service.</span></span>  
  
-   <span data-ttu-id="19863-116">[Transformar XML mediante una transformación XSLT](api-management-transformation-policies.md#XSLTransform) -se aplica un tooXML de transformación XSL en el cuerpo de solicitud o respuesta Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
##  <span data-ttu-id="19863-117"><a name="ConvertJSONtoXML"></a>Convertir JSON tooXML</span><span class="sxs-lookup"><span data-stu-id="19863-117"><a name="ConvertJSONtoXML"></a> Convert JSON tooXML</span></span>  
 <span data-ttu-id="19863-118">Hola `json-to-xml` directiva convierte un cuerpo de solicitud o respuesta de JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="19863-118">hello `json-to-xml` policy converts a request or response body from JSON tooXML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="19863-119">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="19863-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="19863-120">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="19863-120">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="19863-121">Elementos</span><span class="sxs-lookup"><span data-stu-id="19863-121">Elements</span></span>  
  
|<span data-ttu-id="19863-122">Nombre</span><span class="sxs-lookup"><span data-stu-id="19863-122">Name</span></span>|<span data-ttu-id="19863-123">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-123">Description</span></span>|<span data-ttu-id="19863-124">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="19863-125">json-to-xml</span><span class="sxs-lookup"><span data-stu-id="19863-125">json-to-xml</span></span>|<span data-ttu-id="19863-126">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="19863-126">Root element.</span></span>|<span data-ttu-id="19863-127">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="19863-128">Atributos</span><span class="sxs-lookup"><span data-stu-id="19863-128">Attributes</span></span>  
  
|<span data-ttu-id="19863-129">Nombre</span><span class="sxs-lookup"><span data-stu-id="19863-129">Name</span></span>|<span data-ttu-id="19863-130">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-130">Description</span></span>|<span data-ttu-id="19863-131">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-131">Required</span></span>|<span data-ttu-id="19863-132">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="19863-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="19863-133">apply</span><span class="sxs-lookup"><span data-stu-id="19863-133">apply</span></span>|<span data-ttu-id="19863-134">atributo de Hello debe establecerse tooone de hello después de valores.</span><span class="sxs-lookup"><span data-stu-id="19863-134">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="19863-135">-   always: indica que se debe aplicar la conversión siempre.</span><span class="sxs-lookup"><span data-stu-id="19863-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="19863-136">-   content-type-json: especifica que solo se debe realizar la conversión si el encabezado Content-Type indica la presencia de JSON.</span><span class="sxs-lookup"><span data-stu-id="19863-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="19863-137">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-137">Yes</span></span>|<span data-ttu-id="19863-138">N/D</span><span class="sxs-lookup"><span data-stu-id="19863-138">N/A</span></span>|  
|<span data-ttu-id="19863-139">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="19863-139">consider-accept-header</span></span>|<span data-ttu-id="19863-140">atributo de Hello debe establecerse tooone de hello después de valores.</span><span class="sxs-lookup"><span data-stu-id="19863-140">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="19863-141">-   true: especifica que se debe aplicar la conversión si se solicita JSON en el encabezado de aceptación (Accept) de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="19863-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="19863-142">-   false: indica que se debe aplicar siempre la conversión.</span><span class="sxs-lookup"><span data-stu-id="19863-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="19863-143">No</span><span class="sxs-lookup"><span data-stu-id="19863-143">No</span></span>|<span data-ttu-id="19863-144">true</span><span class="sxs-lookup"><span data-stu-id="19863-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="19863-145">Uso</span><span class="sxs-lookup"><span data-stu-id="19863-145">Usage</span></span>  
 <span data-ttu-id="19863-146">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="19863-146">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="19863-147">**Secciones de la directiva:** entrante, saliente y en caso de error</span><span class="sxs-lookup"><span data-stu-id="19863-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="19863-148">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="19863-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="19863-149"><a name="ConvertXMLtoJSON"></a>Convertir XML tooJSON</span><span class="sxs-lookup"><span data-stu-id="19863-149"><a name="ConvertXMLtoJSON"></a> Convert XML tooJSON</span></span>  
 <span data-ttu-id="19863-150">Hola `xml-to-json` directiva convierte un cuerpo de solicitud o respuesta de XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="19863-150">hello `xml-to-json` policy converts a request or response body from XML tooJSON.</span></span> <span data-ttu-id="19863-151">Esta directiva puede ser toomodernize usa las API basadas en servicios web de back-end solo XML.</span><span class="sxs-lookup"><span data-stu-id="19863-151">This policy can be used toomodernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="19863-152">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="19863-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="19863-153">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="19863-153">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="19863-154">Elementos</span><span class="sxs-lookup"><span data-stu-id="19863-154">Elements</span></span>  
  
|<span data-ttu-id="19863-155">Nombre</span><span class="sxs-lookup"><span data-stu-id="19863-155">Name</span></span>|<span data-ttu-id="19863-156">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-156">Description</span></span>|<span data-ttu-id="19863-157">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="19863-158">xml-to-json</span><span class="sxs-lookup"><span data-stu-id="19863-158">xml-to-json</span></span>|<span data-ttu-id="19863-159">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="19863-159">Root element.</span></span>|<span data-ttu-id="19863-160">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="19863-161">Atributos</span><span class="sxs-lookup"><span data-stu-id="19863-161">Attributes</span></span>  
  
|<span data-ttu-id="19863-162">Nombre</span><span class="sxs-lookup"><span data-stu-id="19863-162">Name</span></span>|<span data-ttu-id="19863-163">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-163">Description</span></span>|<span data-ttu-id="19863-164">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-164">Required</span></span>|<span data-ttu-id="19863-165">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="19863-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="19863-166">kind</span><span class="sxs-lookup"><span data-stu-id="19863-166">kind</span></span>|<span data-ttu-id="19863-167">atributo de Hello debe establecerse tooone de hello después de valores.</span><span class="sxs-lookup"><span data-stu-id="19863-167">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="19863-168">Hola-javascript friendly: convertir JSON tiene un a los desarrolladores de formularios tooJavaScript descriptivo.</span><span class="sxs-lookup"><span data-stu-id="19863-168">-   javascript-friendly - hello converted JSON has a form friendly tooJavaScript developers.</span></span><br /><span data-ttu-id="19863-169">-direct: hello JSON convertido refleja Hola original XML estructura de un documento.</span><span class="sxs-lookup"><span data-stu-id="19863-169">-   direct - hello converted JSON reflects hello original XML document's structure.</span></span>|<span data-ttu-id="19863-170">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-170">Yes</span></span>|<span data-ttu-id="19863-171">N/D</span><span class="sxs-lookup"><span data-stu-id="19863-171">N/A</span></span>|  
|<span data-ttu-id="19863-172">apply</span><span class="sxs-lookup"><span data-stu-id="19863-172">apply</span></span>|<span data-ttu-id="19863-173">atributo de Hello debe establecerse tooone de hello después de valores.</span><span class="sxs-lookup"><span data-stu-id="19863-173">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="19863-174">-   always: indica que se debe realizar la conversión siempre.</span><span class="sxs-lookup"><span data-stu-id="19863-174">-   always - convert always.</span></span><br /><span data-ttu-id="19863-175">-   content-type-XML: especifica que solo se debe realizar la conversión si el encabezado Content-Type indica la presencia de XML.</span><span class="sxs-lookup"><span data-stu-id="19863-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="19863-176">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-176">Yes</span></span>|<span data-ttu-id="19863-177">N/D</span><span class="sxs-lookup"><span data-stu-id="19863-177">N/A</span></span>|  
|<span data-ttu-id="19863-178">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="19863-178">consider-accept-header</span></span>|<span data-ttu-id="19863-179">atributo de Hello debe establecerse tooone de hello después de valores.</span><span class="sxs-lookup"><span data-stu-id="19863-179">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="19863-180">-   true: especifica que se debe aplicar la conversión si se solicita XML en el encabezado de aceptación (Accept) de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="19863-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="19863-181">-   false: indica que se debe aplicar siempre la conversión.</span><span class="sxs-lookup"><span data-stu-id="19863-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="19863-182">No</span><span class="sxs-lookup"><span data-stu-id="19863-182">No</span></span>|<span data-ttu-id="19863-183">true</span><span class="sxs-lookup"><span data-stu-id="19863-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="19863-184">Uso</span><span class="sxs-lookup"><span data-stu-id="19863-184">Usage</span></span>  
 <span data-ttu-id="19863-185">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="19863-185">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="19863-186">**Secciones de la directiva:** entrante, saliente y en caso de error</span><span class="sxs-lookup"><span data-stu-id="19863-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="19863-187">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="19863-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="19863-188"><a name="Findandreplacestringinbody"></a> Buscar y reemplazar la cadena en el cuerpo</span><span class="sxs-lookup"><span data-stu-id="19863-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="19863-189">Hola `find-and-replace` directivas busca una subcadena de solicitud o respuesta y lo reemplaza por una subcadena distinta.</span><span class="sxs-lookup"><span data-stu-id="19863-189">hello `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="19863-190">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="19863-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="19863-191">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="19863-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="19863-192">Elementos</span><span class="sxs-lookup"><span data-stu-id="19863-192">Elements</span></span>  
  
|<span data-ttu-id="19863-193">Nombre</span><span class="sxs-lookup"><span data-stu-id="19863-193">Name</span></span>|<span data-ttu-id="19863-194">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-194">Description</span></span>|<span data-ttu-id="19863-195">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="19863-196">find-and-replace</span><span class="sxs-lookup"><span data-stu-id="19863-196">find-and-replace</span></span>|<span data-ttu-id="19863-197">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="19863-197">Root element.</span></span>|<span data-ttu-id="19863-198">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="19863-199">Atributos</span><span class="sxs-lookup"><span data-stu-id="19863-199">Attributes</span></span>  
  
|<span data-ttu-id="19863-200">Nombre</span><span class="sxs-lookup"><span data-stu-id="19863-200">Name</span></span>|<span data-ttu-id="19863-201">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-201">Description</span></span>|<span data-ttu-id="19863-202">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-202">Required</span></span>|<span data-ttu-id="19863-203">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="19863-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="19863-204">De</span><span class="sxs-lookup"><span data-stu-id="19863-204">from</span></span>|<span data-ttu-id="19863-205">Hola toosearch de cadena para.</span><span class="sxs-lookup"><span data-stu-id="19863-205">hello string toosearch for.</span></span>|<span data-ttu-id="19863-206">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-206">Yes</span></span>|<span data-ttu-id="19863-207">N/D</span><span class="sxs-lookup"><span data-stu-id="19863-207">N/A</span></span>|  
|<span data-ttu-id="19863-208">to</span><span class="sxs-lookup"><span data-stu-id="19863-208">to</span></span>|<span data-ttu-id="19863-209">cadena de reemplazo de Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-209">hello replacement string.</span></span> <span data-ttu-id="19863-210">Especificar una reemplazo cadena tooremove Hola Buscar cadena de longitud cero.</span><span class="sxs-lookup"><span data-stu-id="19863-210">Specify a zero length replacement string tooremove hello search string.</span></span>|<span data-ttu-id="19863-211">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-211">Yes</span></span>|<span data-ttu-id="19863-212">N/D</span><span class="sxs-lookup"><span data-stu-id="19863-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="19863-213">Uso</span><span class="sxs-lookup"><span data-stu-id="19863-213">Usage</span></span>  
 <span data-ttu-id="19863-214">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="19863-214">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="19863-215">**Secciones de la directiva:** entrante, saliente, back-end y en caso de error</span><span class="sxs-lookup"><span data-stu-id="19863-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="19863-216">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="19863-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="19863-217"><a name="MaskURLSContent"></a> Enmascarar URL en el contenido</span><span class="sxs-lookup"><span data-stu-id="19863-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="19863-218">Hola `redirect-content-urls` directiva reescribe (enmascara) vínculos en el cuerpo de la respuesta de Hola para que apunten toohello vínculo equivalente a través de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-218">hello `redirect-content-urls` policy re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span> <span data-ttu-id="19863-219">Utilizarlos en hello sección saliente toore escritura respuesta cuerpo vínculos toomake toohello de punto de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="19863-219">Use in hello outbound section toore-write response body links toomake them point toohello gateway.</span></span> <span data-ttu-id="19863-220">Uso de Hola entrantes sección para obtener el resultado opuesto.</span><span class="sxs-lookup"><span data-stu-id="19863-220">Use in hello inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="19863-221">Esta directiva no cambia los valores de los encabezados, como los `Location`.</span><span class="sxs-lookup"><span data-stu-id="19863-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="19863-222">los valores de encabezado toochange, usar hello [encabezado del conjunto](api-management-transformation-policies.md#SetHTTPheader) directiva.</span><span class="sxs-lookup"><span data-stu-id="19863-222">toochange header values, use hello [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="19863-223">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="19863-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="19863-224">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="19863-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="19863-225">Elementos</span><span class="sxs-lookup"><span data-stu-id="19863-225">Elements</span></span>  
  
|<span data-ttu-id="19863-226">Nombre</span><span class="sxs-lookup"><span data-stu-id="19863-226">Name</span></span>|<span data-ttu-id="19863-227">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-227">Description</span></span>|<span data-ttu-id="19863-228">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="19863-229">redirect-content-urls</span><span class="sxs-lookup"><span data-stu-id="19863-229">redirect-content-urls</span></span>|<span data-ttu-id="19863-230">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="19863-230">Root element.</span></span>|<span data-ttu-id="19863-231">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="19863-232">Uso</span><span class="sxs-lookup"><span data-stu-id="19863-232">Usage</span></span>  
 <span data-ttu-id="19863-233">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="19863-233">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="19863-234">**Secciones de la directiva:** entrante y saliente</span><span class="sxs-lookup"><span data-stu-id="19863-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="19863-235">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="19863-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="19863-236"><a name="SetBackendService"></a> Establecer el servicio back-end</span><span class="sxs-lookup"><span data-stu-id="19863-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="19863-237">Hola de uso `set-backend-service` tooredirect una entrada de directiva de solicitud back-end diferente de tooa de Hola especificada en la configuración de hello API para esa operación.</span><span class="sxs-lookup"><span data-stu-id="19863-237">Use hello `set-backend-service` policy tooredirect an incoming request tooa different backend than hello one specified in hello API settings for that operation.</span></span> <span data-ttu-id="19863-238">Esta directiva cambia Hola back-end base dirección URL del servicio de Hola entrantes solicitud toohello especificada en la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-238">This policy changes hello backend service base URL of hello incoming request toohello one specified in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="19863-239">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="19863-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="19863-240">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="19863-240">Example</span></span>  
  
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
<span data-ttu-id="19863-241">En este Hola de ejemplo establecer la directiva de servicio de back-end enruta las solicitudes según el valor de la versión de Hola pasado Hola consulta cadena tooa diferentes servicio back-end que Hola Hola especificado en una API.</span><span class="sxs-lookup"><span data-stu-id="19863-241">In this example hello set backend service policy routes requests based on hello version value passed in hello query string tooa different backend service than hello one specified in hello API.</span></span>
  
<span data-ttu-id="19863-242">Hola inicialmente la dirección URL base del servicio se deriva de la configuración de la API de Hola de back-end.</span><span class="sxs-lookup"><span data-stu-id="19863-242">Initially hello backend service base URL is derived from hello API settings.</span></span> <span data-ttu-id="19863-243">Hola por lo que la dirección URL de solicitud `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` se convierte en `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` donde `http://contoso.com/api/10.4/` es dirección URL de servicio de back-end Hola especificada en la configuración de hello API.</span><span class="sxs-lookup"><span data-stu-id="19863-243">So hello request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is hello backend service URL specified in hello API settings.</span></span>  
  
<span data-ttu-id="19863-244">Cuando Hola [< elija\> ](api-management-advanced-policies.md#choose) declaración de directiva se aplica URL base del servicio de back-end Hola puede cambiar de nuevo demasiado`http://contoso.com/api/8.2` o `http://contoso.com/api/9.1`, en función de valor Hola Hola versión solicitud del parámetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="19863-244">When hello [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied hello backend service base URL may change again either too`http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on hello value of hello version request query parameter.</span></span> <span data-ttu-id="19863-245">Por ejemplo, si hello valor es `"2013-15"` se convierte en dirección URL de solicitud final hello `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span><span class="sxs-lookup"><span data-stu-id="19863-245">For example, if hello value is `"2013-15"` hello final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="19863-246">Si aún más la transformación de solicitud de hello es deseado, otros [directivas de transformación](api-management-transformation-policies.md#TransformationPolicies) puede utilizarse.</span><span class="sxs-lookup"><span data-stu-id="19863-246">If further transformation of hello request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="19863-247">Por ejemplo, tooremove Hola versión consulta enruta parámetro ahora que hello solicitud se está tooa versión específica back-end, hello [establecer el parámetro de cadena de consulta](api-management-transformation-policies.md#SetQueryStringParameter) directiva puede ser usado tooremove Hola ya es redundante version (atributo).</span><span class="sxs-lookup"><span data-stu-id="19863-247">For example, tooremove hello version query parameter now that hello request is being routed tooa version specific backend, hello  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used tooremove hello now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="19863-248">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="19863-248">Example</span></span>  
  
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
<span data-ttu-id="19863-249">En este ejemplo Hola directiva rutas Hola solicitud tooa service fabric back-end, mediante cadena de consulta de hello userId como clave de partición de Hola y Hola réplica principal de la partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-249">In this example hello policy routes hello request tooa service fabric backend, using hello userId query string as hello partition key and using hello primary replica of hello partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="19863-250">Elementos</span><span class="sxs-lookup"><span data-stu-id="19863-250">Elements</span></span>  
  
|<span data-ttu-id="19863-251">Nombre</span><span class="sxs-lookup"><span data-stu-id="19863-251">Name</span></span>|<span data-ttu-id="19863-252">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-252">Description</span></span>|<span data-ttu-id="19863-253">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="19863-254">set-backend-service</span><span class="sxs-lookup"><span data-stu-id="19863-254">set-backend-service</span></span>|<span data-ttu-id="19863-255">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="19863-255">Root element.</span></span>|<span data-ttu-id="19863-256">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="19863-257">Atributos</span><span class="sxs-lookup"><span data-stu-id="19863-257">Attributes</span></span>  
  
|<span data-ttu-id="19863-258">Nombre</span><span class="sxs-lookup"><span data-stu-id="19863-258">Name</span></span>|<span data-ttu-id="19863-259">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-259">Description</span></span>|<span data-ttu-id="19863-260">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-260">Required</span></span>|<span data-ttu-id="19863-261">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="19863-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="19863-262">base-url</span><span class="sxs-lookup"><span data-stu-id="19863-262">base-url</span></span>|<span data-ttu-id="19863-263">Nueva dirección URL base del servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="19863-263">New backend service base URL.</span></span>|<span data-ttu-id="19863-264">No</span><span class="sxs-lookup"><span data-stu-id="19863-264">No</span></span>|<span data-ttu-id="19863-265">N/D</span><span class="sxs-lookup"><span data-stu-id="19863-265">N/A</span></span>|  
|<span data-ttu-id="19863-266">backend-id</span><span class="sxs-lookup"><span data-stu-id="19863-266">backend-id</span></span>|<span data-ttu-id="19863-267">Identificador de hello tooroute de back-end para.</span><span class="sxs-lookup"><span data-stu-id="19863-267">Identifier of hello backend tooroute to.</span></span>|<span data-ttu-id="19863-268">No</span><span class="sxs-lookup"><span data-stu-id="19863-268">No</span></span>|<span data-ttu-id="19863-269">N/D</span><span class="sxs-lookup"><span data-stu-id="19863-269">N/A</span></span>|  
|<span data-ttu-id="19863-270">sf-partition-key</span><span class="sxs-lookup"><span data-stu-id="19863-270">sf-partition-key</span></span>|<span data-ttu-id="19863-271">Solo se aplica cuando Hola back-end es un servicio de Service Fabric y se especifica mediante el 'Id. de back-end'.</span><span class="sxs-lookup"><span data-stu-id="19863-271">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="19863-272">Usar una partición específica del servicio de resolución de nombres de hello tooresolve.</span><span class="sxs-lookup"><span data-stu-id="19863-272">Used tooresolve a specific partition from hello name resolution service.</span></span>|<span data-ttu-id="19863-273">No</span><span class="sxs-lookup"><span data-stu-id="19863-273">No</span></span>|<span data-ttu-id="19863-274">N/D</span><span class="sxs-lookup"><span data-stu-id="19863-274">N/A</span></span>|  
|<span data-ttu-id="19863-275">sf-replica-type</span><span class="sxs-lookup"><span data-stu-id="19863-275">sf-replica-type</span></span>|<span data-ttu-id="19863-276">Solo se aplica cuando Hola back-end es un servicio de Service Fabric y se especifica mediante el 'Id. de back-end'.</span><span class="sxs-lookup"><span data-stu-id="19863-276">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="19863-277">Controla si la solicitud de hello debe ir toohello réplica principal o secundaria de una partición.</span><span class="sxs-lookup"><span data-stu-id="19863-277">Controls if hello request should go toohello primary or secondary replica of a partition.</span></span> |<span data-ttu-id="19863-278">No</span><span class="sxs-lookup"><span data-stu-id="19863-278">No</span></span>|<span data-ttu-id="19863-279">N/D</span><span class="sxs-lookup"><span data-stu-id="19863-279">N/A</span></span>|    
|<span data-ttu-id="19863-280">sf-resolve-condition</span><span class="sxs-lookup"><span data-stu-id="19863-280">sf-resolve-condition</span></span>|<span data-ttu-id="19863-281">Solo se aplica cuando Hola back-end es un servicio de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="19863-281">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="19863-282">Identificación de condición si Hola llamar a back-end de tooService tejido tiene toobe repetirse con la resolución de nuevo.</span><span class="sxs-lookup"><span data-stu-id="19863-282">Condition identifying if hello call tooService Fabric backend has toobe repeated with new resolution.</span></span>|<span data-ttu-id="19863-283">No</span><span class="sxs-lookup"><span data-stu-id="19863-283">No</span></span>|<span data-ttu-id="19863-284">N/D</span><span class="sxs-lookup"><span data-stu-id="19863-284">N/A</span></span>|    
|<span data-ttu-id="19863-285">sf-service-instance-name</span><span class="sxs-lookup"><span data-stu-id="19863-285">sf-service-instance-name</span></span>|<span data-ttu-id="19863-286">Solo se aplica cuando Hola back-end es un servicio de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="19863-286">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="19863-287">Permite toochange instancias de servicio en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="19863-287">Allows toochange service instances at runtime.</span></span> |<span data-ttu-id="19863-288">No</span><span class="sxs-lookup"><span data-stu-id="19863-288">No</span></span>|<span data-ttu-id="19863-289">N/D</span><span class="sxs-lookup"><span data-stu-id="19863-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="19863-290">Uso</span><span class="sxs-lookup"><span data-stu-id="19863-290">Usage</span></span>  
 <span data-ttu-id="19863-291">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="19863-291">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="19863-292">**Secciones de la directiva:** entrante y back-end</span><span class="sxs-lookup"><span data-stu-id="19863-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="19863-293">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="19863-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="19863-294"><a name="SetBody"></a> Establecer cuerpo</span><span class="sxs-lookup"><span data-stu-id="19863-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="19863-295">Hola de uso `set-body` cuerpo del mensaje Hola directiva tooset para las solicitudes entrantes y salientes.</span><span class="sxs-lookup"><span data-stu-id="19863-295">Use hello `set-body` policy tooset hello message body for incoming and outgoing requests.</span></span> <span data-ttu-id="19863-296">tooaccess Hola cuerpo del mensaje puede usar hello `context.Request.Body` propiedad o hello `context.Response.Body`, dependiendo de si es la directiva de Hola Hola sección entrante o saliente.</span><span class="sxs-lookup"><span data-stu-id="19863-296">tooaccess hello message body you can use hello `context.Request.Body` property or hello `context.Response.Body`, depending on whether hello policy is in hello inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="19863-297">Tenga en cuenta que, de forma predeterminada cuando se tiene acceso Hola cuerpo del mensaje utilizando `context.Request.Body` o `context.Response.Body`, mensaje de Hola original cuerpo se pierde y se debe establecer devolviendo el cuerpo de hello en expresión Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-297">Note that by default when you access hello message body using `context.Request.Body` or `context.Response.Body`, hello original message body is lost and must be set by returning hello body back in hello expression.</span></span> <span data-ttu-id="19863-298">cuerpo de hello toopreserve contenido, establecer hello `preserveContent` parámetro demasiado`true` al tener acceso a mensajes de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="19863-298">toopreserve hello body content, set hello `preserveContent` parameter too`true` when accessing hello message.</span></span> <span data-ttu-id="19863-299">Si `preserveContent` se establece demasiado`true` y un cuerpo diferente se devuelve por expresión de hello, Hola devuelve cuerpo se utiliza.</span><span class="sxs-lookup"><span data-stu-id="19863-299">If `preserveContent` is set too`true` and a different body is returned by hello expression, hello returned body is used.</span></span>  
>   
>  <span data-ttu-id="19863-300">Tenga en cuenta que hello las siguientes consideraciones cuando utilizando hello `set-body` directiva.</span><span class="sxs-lookup"><span data-stu-id="19863-300">Please note hello following considerations when using hello `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="19863-301">Si usas hello `set-body` tooreturn directiva un cuerpo nuevo o actualizado no es necesario tooset `preserveContent` demasiado`true` porque está proporcionando explícitamente el contenido del cuerpo de hello nueva.</span><span class="sxs-lookup"><span data-stu-id="19863-301">If you are using hello `set-body` policy tooreturn a new or updated body you don't need tooset `preserveContent` too`true` because you are explicitly supplying hello new body contents.</span></span>  
> -   <span data-ttu-id="19863-302">Conservar contenido Hola de una respuesta en la canalización de entrada de hello no tiene sentido porque todavía no hay ninguna respuesta.</span><span class="sxs-lookup"><span data-stu-id="19863-302">Preserving hello content of a response in hello inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="19863-303">Conservar contenido Hola de una solicitud en la canalización de salida de hello no tiene sentido porque Hola ya se ha enviado solicitud toohello back-end en este momento.</span><span class="sxs-lookup"><span data-stu-id="19863-303">Preserving hello content of a request in hello outbound pipeline doesn't make sense because hello request has already been sent toohello backend at this point.</span></span>  
> -   <span data-ttu-id="19863-304">Si esta directiva se usa cuando no hay ningún cuerpo de mensaje, por ejemplo, en un GET entrante, se producirá una excepción.</span><span class="sxs-lookup"><span data-stu-id="19863-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="19863-305">Para obtener más información, vea hello `context.Request.Body`, `context.Response.Body`, hello y `IMessage` secciones de hello [variable de contexto](api-management-policy-expressions.md#ContextVariables) tabla.</span><span class="sxs-lookup"><span data-stu-id="19863-305">For more information, see hello `context.Request.Body`, `context.Response.Body`, and hello `IMessage` sections in hello [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="19863-306">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="19863-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="19863-307">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="19863-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="19863-308">Ejemplo de texto literal</span><span class="sxs-lookup"><span data-stu-id="19863-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a><span data-ttu-id="19863-309">Ejemplo de cuerpo de hello como una cadena de acceso.</span><span class="sxs-lookup"><span data-stu-id="19863-309">Example accessing hello body as a string.</span></span> <span data-ttu-id="19863-310">Tenga en cuenta que estamos conservando cuerpo de solicitud original de Hola para que podamos acceder a él más adelante en la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-310">Note that we are preserving hello original request body so that we can access it later in hello pipeline.</span></span>
  
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
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a><span data-ttu-id="19863-311">Ejemplo de cuerpo de Hola como un JObject de acceso.</span><span class="sxs-lookup"><span data-stu-id="19863-311">Example accessing hello body as a JObject.</span></span> <span data-ttu-id="19863-312">Tenga en cuenta que, puesto que no nos estamos reservar Hola original cuerpo de la solicitud, el acceso a él más adelante en la canalización de hello dará como resultado una excepción.</span><span class="sxs-lookup"><span data-stu-id="19863-312">Note that since we are not reserving hello original request body, accesing it later in hello pipeline will result in an exception.</span></span>  
  
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
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="19863-313">Filtro de respuesta según un producto</span><span class="sxs-lookup"><span data-stu-id="19863-313">Filter response based on product</span></span>  
 <span data-ttu-id="19863-314">Este ejemplo muestra cómo tooperform contenido filtrado mediante la eliminación de elementos de datos de respuesta de Hola recibido del servicio de back-end de hello cuando se usa hello `Starter` producto.</span><span class="sxs-lookup"><span data-stu-id="19863-314">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="19863-315">Para ver una demostración de cómo configurar y usar esta directiva, consulte [177 episodio abarcan de nube: más características de administración de API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avancemos too34:30.</span><span class="sxs-lookup"><span data-stu-id="19863-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="19863-316">Iniciar en 31:50 toosee una visión general de [Hola API de previsión de Sky oscuro](https://developer.forecast.io/) utilizada para esta demostración.</span><span class="sxs-lookup"><span data-stu-id="19863-316">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
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

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="19863-317">Uso de plantillas Liquid con la directiva de establecer cuerpo</span><span class="sxs-lookup"><span data-stu-id="19863-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="19863-318">Hola `set-body` directiva puede ser configurado toouse hello [líquido](https://shopify.github.io/liquid/basics/introduction/) plantillas tootransfom Hola cuerpo de lenguaje una solicitud o respuesta.</span><span class="sxs-lookup"><span data-stu-id="19863-318">hello `set-body` policy can be configured toouse hello [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language tootransfom hello body of a request or response.</span></span> <span data-ttu-id="19863-319">Esto puede ser muy eficaces si necesita toocompletely remodelación Hola formato del mensaje.</span><span class="sxs-lookup"><span data-stu-id="19863-319">This can be very effective if you need toocompletely reshape hello format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19863-320">Hola implementación de líquido utilizado en hello `set-body` directiva está configurada en "modo de C#".</span><span class="sxs-lookup"><span data-stu-id="19863-320">hello implementation of Liquid used in hello `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="19863-321">Esto es especialmente importante al realizar tareas como el filtrado.</span><span class="sxs-lookup"><span data-stu-id="19863-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="19863-322">Por ejemplo, mediante un filtro de fecha requiere el uso de Hola de Pascal de mayúsculas y minúsculas y C# fecha formato p. ej.:</span><span class="sxs-lookup"><span data-stu-id="19863-322">As an example, using a date filter requires hello use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="19863-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="19863-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19863-324">En orden toocorrectly enlace tooan XML cuerpo mediante plantilla líquido hello, use un `set-header` directiva tooset Content-Type tooeither aplicación/xml, texto/xml (o cualquier tipo que termine con + xml); para un cuerpo JSON, debe ser application/json, texto/json (o el final de cualquier tipo con + json).</span><span class="sxs-lookup"><span data-stu-id="19863-324">In order toocorrectly bind tooan XML body using hello Liquid template, use a `set-header` policy tooset Content-Type tooeither application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-toosoap-using-a-liquid-template"></a><span data-ttu-id="19863-325">Convertir tooSOAP JSON utilizando una plantilla líquida</span><span class="sxs-lookup"><span data-stu-id="19863-325">Convert JSON tooSOAP using a Liquid template</span></span>
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

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="19863-326">Transformación de JSON mediante una plantilla Liquid</span><span class="sxs-lookup"><span data-stu-id="19863-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="19863-327">Elementos</span><span class="sxs-lookup"><span data-stu-id="19863-327">Elements</span></span>  
  
|<span data-ttu-id="19863-328">Nombre</span><span class="sxs-lookup"><span data-stu-id="19863-328">Name</span></span>|<span data-ttu-id="19863-329">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-329">Description</span></span>|<span data-ttu-id="19863-330">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="19863-331">set-body</span><span class="sxs-lookup"><span data-stu-id="19863-331">set-body</span></span>|<span data-ttu-id="19863-332">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="19863-332">Root element.</span></span> <span data-ttu-id="19863-333">Contiene el texto del cuerpo de Hola o una expresión que devuelve un cuerpo.</span><span class="sxs-lookup"><span data-stu-id="19863-333">Contains hello body text or an expressions that returns a body.</span></span>|<span data-ttu-id="19863-334">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="19863-335">Propiedades</span><span class="sxs-lookup"><span data-stu-id="19863-335">Properties</span></span>  
  
|<span data-ttu-id="19863-336">Nombre</span><span class="sxs-lookup"><span data-stu-id="19863-336">Name</span></span>|<span data-ttu-id="19863-337">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-337">Description</span></span>|<span data-ttu-id="19863-338">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-338">Required</span></span>|<span data-ttu-id="19863-339">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="19863-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="19863-340">template</span><span class="sxs-lookup"><span data-stu-id="19863-340">template</span></span>|<span data-ttu-id="19863-341">Se ejecutará modo de creación de plantillas de Hola toochange usado que Hola establecer la directiva de cuerpo.</span><span class="sxs-lookup"><span data-stu-id="19863-341">Used toochange hello templating mode that hello set body policy will run in.</span></span> <span data-ttu-id="19863-342">Actualmente, el valor de hello solo admitido es:</span><span class="sxs-lookup"><span data-stu-id="19863-342">Currently hello only supported value is:</span></span><br /><br /><span data-ttu-id="19863-343">Hola - líquido - establecer la directiva de cuerpo utilizará el motor de plantillas líquido Hola</span><span class="sxs-lookup"><span data-stu-id="19863-343">- liquid - hello set body policy will use hello liquid templating engine</span></span> |<span data-ttu-id="19863-344">No</span><span class="sxs-lookup"><span data-stu-id="19863-344">No</span></span>|<span data-ttu-id="19863-345">Liquid</span><span class="sxs-lookup"><span data-stu-id="19863-345">liquid</span></span>|  

<span data-ttu-id="19863-346">Para tener acceso a información sobre la solicitud de Hola y respuesta, plantilla líquido Hola puede enlazar el objeto de contexto de tooa con hello propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="19863-346">For accessing information about hello request and response, hello Liquid template can bind tooa context object with hello following properties:</span></span> <br />
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



### <a name="usage"></a><span data-ttu-id="19863-347">Uso</span><span class="sxs-lookup"><span data-stu-id="19863-347">Usage</span></span>  
 <span data-ttu-id="19863-348">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="19863-348">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="19863-349">**Secciones de la directiva:** entrante, saliente y back-end</span><span class="sxs-lookup"><span data-stu-id="19863-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="19863-350">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="19863-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="19863-351"><a name="SetHTTPheader"></a> Establecer encabezado HTTP</span><span class="sxs-lookup"><span data-stu-id="19863-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="19863-352">Hola `set-header` directiva asigna una respuesta de valor tooan existente o un encabezado de solicitud o agrega un nuevo encabezado de respuesta y/o de solicitud.</span><span class="sxs-lookup"><span data-stu-id="19863-352">hello `set-header` policy assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="19863-353">Inserta una lista de encabezados HTTP en un mensaje HTTP.</span><span class="sxs-lookup"><span data-stu-id="19863-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="19863-354">Cuando se coloca en una canalización de entrada, esta directiva establece los encabezados HTTP de Hola para solicitud de Hola que se pasa toohello servicio de destino.</span><span class="sxs-lookup"><span data-stu-id="19863-354">When placed in an inbound pipeline, this policy sets hello HTTP headers for hello request being passed toohello target service.</span></span> <span data-ttu-id="19863-355">Cuando se coloca en una canalización saliente, esta directiva establece los encabezados HTTP de hello para la respuesta de Hola que se envió el cliente de la puerta de enlace de toohello.</span><span class="sxs-lookup"><span data-stu-id="19863-355">When placed in an outbound pipeline, this policy sets hello HTTP headers for hello response being sent toohello gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="19863-356">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="19863-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="19863-357">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="19863-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="19863-358">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="19863-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="19863-359">Reenviar el servicio de back-end de toohello de información de contexto</span><span class="sxs-lookup"><span data-stu-id="19863-359">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="19863-360">Este ejemplo muestra cómo Directiva tooapply en hello API de nivel de servicio de back-end de toohello de información de contexto de toosupply.</span><span class="sxs-lookup"><span data-stu-id="19863-360">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="19863-361">Para ver una demostración de cómo configurar y usar esta directiva, consulte [177 episodio abarcan de nube: más características de administración de API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avancemos too10:30.</span><span class="sxs-lookup"><span data-stu-id="19863-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="19863-362">No hay una demostración de llamar a una operación de portal para desarrolladores de Hola donde puede ver la directiva de hello en el trabajo a las 12:10.</span><span class="sxs-lookup"><span data-stu-id="19863-362">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="19863-363">Para obtener más información, consulte [Policy expressions](api-management-policy-expressions.md) (Expresiones de política) y [Context variable](api-management-policy-expressions.md#ContextVariables) (Variable de contexto).</span><span class="sxs-lookup"><span data-stu-id="19863-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="19863-364">Elementos</span><span class="sxs-lookup"><span data-stu-id="19863-364">Elements</span></span>  
  
|<span data-ttu-id="19863-365">Nombre</span><span class="sxs-lookup"><span data-stu-id="19863-365">Name</span></span>|<span data-ttu-id="19863-366">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-366">Description</span></span>|<span data-ttu-id="19863-367">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="19863-368">set-header</span><span class="sxs-lookup"><span data-stu-id="19863-368">set-header</span></span>|<span data-ttu-id="19863-369">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="19863-369">Root element.</span></span>|<span data-ttu-id="19863-370">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-370">Yes</span></span>|  
|<span data-ttu-id="19863-371">value</span><span class="sxs-lookup"><span data-stu-id="19863-371">value</span></span>|<span data-ttu-id="19863-372">Especifica el valor de Hola de hello encabezado toobe conjunto.</span><span class="sxs-lookup"><span data-stu-id="19863-372">Specifies hello value of hello header toobe set.</span></span> <span data-ttu-id="19863-373">Para varios encabezados con hello homónimas agregar más `value` elementos.</span><span class="sxs-lookup"><span data-stu-id="19863-373">For multiple headers with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="19863-374">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="19863-375">Propiedades</span><span class="sxs-lookup"><span data-stu-id="19863-375">Properties</span></span>  
  
|<span data-ttu-id="19863-376">Nombre</span><span class="sxs-lookup"><span data-stu-id="19863-376">Name</span></span>|<span data-ttu-id="19863-377">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-377">Description</span></span>|<span data-ttu-id="19863-378">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-378">Required</span></span>|<span data-ttu-id="19863-379">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="19863-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="19863-380">exists-action</span><span class="sxs-lookup"><span data-stu-id="19863-380">exists-action</span></span>|<span data-ttu-id="19863-381">Especifica qué tootake acción cuando ya se ha especificado el encabezado de Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-381">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="19863-382">Este atributo debe tener uno de hello después de valores.</span><span class="sxs-lookup"><span data-stu-id="19863-382">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="19863-383">-invalidar - reemplaza Hola valor del encabezado existente Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-383">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="19863-384">-skip: no reemplaza el valor del encabezado de hello existente.</span><span class="sxs-lookup"><span data-stu-id="19863-384">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="19863-385">-append: anexa el valor del encabezado existente Hola valor toohello.</span><span class="sxs-lookup"><span data-stu-id="19863-385">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="19863-386">-delete: quita el encabezado de saludo de solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-386">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="19863-387">Cuando se establece demasiado`override` al enumerar varias entradas con hello igual nombre resultados en el encabezado de Hola que se va a entradas correspondiente del conjunto tooall (que aparecerán enumeradas varias veces); solo los valores mostrados se establecerá en el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="19863-387">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="19863-388">No</span><span class="sxs-lookup"><span data-stu-id="19863-388">No</span></span>|<span data-ttu-id="19863-389">override</span><span class="sxs-lookup"><span data-stu-id="19863-389">override</span></span>|  
|<span data-ttu-id="19863-390">name</span><span class="sxs-lookup"><span data-stu-id="19863-390">name</span></span>|<span data-ttu-id="19863-391">Especifica el nombre del conjunto de toobe de encabezado de Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-391">Specifies name of hello header toobe set.</span></span>|<span data-ttu-id="19863-392">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-392">Yes</span></span>|<span data-ttu-id="19863-393">N/D</span><span class="sxs-lookup"><span data-stu-id="19863-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="19863-394">Uso</span><span class="sxs-lookup"><span data-stu-id="19863-394">Usage</span></span>  
 <span data-ttu-id="19863-395">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="19863-395">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="19863-396">**Secciones de la directiva:** entrante, saliente, back-end y en caso de error</span><span class="sxs-lookup"><span data-stu-id="19863-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="19863-397">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="19863-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="19863-398"><a name="SetQueryStringParameter"></a> Establecimiento del parámetro de cadena de consulta</span><span class="sxs-lookup"><span data-stu-id="19863-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="19863-399">Hola `set-query-parameter` directiva agrega, reemplaza el valor de, o parámetro de cadena de consulta de solicitud de eliminaciones.</span><span class="sxs-lookup"><span data-stu-id="19863-399">hello `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="19863-400">Puede ser toopass usa parámetros de consulta esperados por el servicio de back-end de Hola que son opcionales o no están nunca presenten en la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="19863-400">Can be used toopass query parameters expected by hello backend service which are optional or never present in hello request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="19863-401">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="19863-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="19863-402">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="19863-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="19863-403">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="19863-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="19863-404">Reenviar el servicio de back-end de toohello de información de contexto</span><span class="sxs-lookup"><span data-stu-id="19863-404">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="19863-405">Este ejemplo muestra cómo Directiva tooapply en hello API de nivel de servicio de back-end de toohello de información de contexto de toosupply.</span><span class="sxs-lookup"><span data-stu-id="19863-405">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="19863-406">Para ver una demostración de cómo configurar y usar esta directiva, consulte [177 episodio abarcan de nube: más características de administración de API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avancemos too10:30.</span><span class="sxs-lookup"><span data-stu-id="19863-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="19863-407">No hay una demostración de llamar a una operación de portal para desarrolladores de Hola donde puede ver la directiva de hello en el trabajo a las 12:10.</span><span class="sxs-lookup"><span data-stu-id="19863-407">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="19863-408">Para obtener más información, consulte [Policy expressions](api-management-policy-expressions.md) (Expresiones de política) y [Context variable](api-management-policy-expressions.md#ContextVariables) (Variable de contexto).</span><span class="sxs-lookup"><span data-stu-id="19863-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="19863-409">Elementos</span><span class="sxs-lookup"><span data-stu-id="19863-409">Elements</span></span>  
  
|<span data-ttu-id="19863-410">Nombre</span><span class="sxs-lookup"><span data-stu-id="19863-410">Name</span></span>|<span data-ttu-id="19863-411">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-411">Description</span></span>|<span data-ttu-id="19863-412">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="19863-413">set-query-parameter</span><span class="sxs-lookup"><span data-stu-id="19863-413">set-query-parameter</span></span>|<span data-ttu-id="19863-414">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="19863-414">Root element.</span></span>|<span data-ttu-id="19863-415">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-415">Yes</span></span>|  
|<span data-ttu-id="19863-416">value</span><span class="sxs-lookup"><span data-stu-id="19863-416">value</span></span>|<span data-ttu-id="19863-417">Especifica el valor de Hola Hola parámetro toobe del conjunto de consulta.</span><span class="sxs-lookup"><span data-stu-id="19863-417">Specifies hello value of hello query parameter toobe set.</span></span> <span data-ttu-id="19863-418">Varios parámetros de consulta con hello homónimas agregar más `value` elementos.</span><span class="sxs-lookup"><span data-stu-id="19863-418">For multiple query parameters with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="19863-419">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="19863-420">Propiedades</span><span class="sxs-lookup"><span data-stu-id="19863-420">Properties</span></span>  
  
|<span data-ttu-id="19863-421">Nombre</span><span class="sxs-lookup"><span data-stu-id="19863-421">Name</span></span>|<span data-ttu-id="19863-422">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-422">Description</span></span>|<span data-ttu-id="19863-423">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-423">Required</span></span>|<span data-ttu-id="19863-424">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="19863-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="19863-425">exists-action</span><span class="sxs-lookup"><span data-stu-id="19863-425">exists-action</span></span>|<span data-ttu-id="19863-426">Especifica qué tootake acción cuando ya se ha especificado el parámetro de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-426">Specifies what action tootake when hello query parameter is already specified.</span></span> <span data-ttu-id="19863-427">Este atributo debe tener uno de hello después de valores.</span><span class="sxs-lookup"><span data-stu-id="19863-427">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="19863-428">-invalidar - reemplaza Hola valor de parámetro de hello existente.</span><span class="sxs-lookup"><span data-stu-id="19863-428">-   override - replaces hello value of hello existing parameter.</span></span><br /><span data-ttu-id="19863-429">-skip: no reemplaza el valor del parámetro de consulta existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-429">-   skip - does not replace hello existing query parameter value.</span></span><br /><span data-ttu-id="19863-430">-Anexar - anexa Hola valor toohello parámetro valor de consulta existente.</span><span class="sxs-lookup"><span data-stu-id="19863-430">-   append - appends hello value toohello existing query parameter value.</span></span><br /><span data-ttu-id="19863-431">-delete: quita el parámetro de consulta de Hola de solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-431">-   delete - removes hello query parameter from hello request.</span></span><br /><br /> <span data-ttu-id="19863-432">Cuando se establece demasiado`override` al enumerar varias entradas con hello igual nombre resultados en el parámetro de consulta de Hola que se va a entradas correspondiente del conjunto tooall (que aparecerán enumeradas varias veces); solo los valores mostrados se establecerá en el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="19863-432">When set too`override` enlisting multiple entries with hello same name results in hello query parameter being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="19863-433">No</span><span class="sxs-lookup"><span data-stu-id="19863-433">No</span></span>|<span data-ttu-id="19863-434">override</span><span class="sxs-lookup"><span data-stu-id="19863-434">override</span></span>|  
|<span data-ttu-id="19863-435">name</span><span class="sxs-lookup"><span data-stu-id="19863-435">name</span></span>|<span data-ttu-id="19863-436">Especifica el nombre del conjunto de toobe de parámetros de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-436">Specifies name of hello query parameter toobe set.</span></span>|<span data-ttu-id="19863-437">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-437">Yes</span></span>|<span data-ttu-id="19863-438">N/D</span><span class="sxs-lookup"><span data-stu-id="19863-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="19863-439">Uso</span><span class="sxs-lookup"><span data-stu-id="19863-439">Usage</span></span>  
 <span data-ttu-id="19863-440">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="19863-440">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="19863-441">**Secciones de la directiva:** entrante y back-end</span><span class="sxs-lookup"><span data-stu-id="19863-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="19863-442">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="19863-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="19863-443"><a name="RewriteURL"></a> URL de reescritura</span><span class="sxs-lookup"><span data-stu-id="19863-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="19863-444">Hola `rewrite-uri` directiva convierte una dirección URL de solicitud desde su formato de toohello de formato público esperado por el servicio web de hello, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-444">hello `rewrite-uri` policy converts a request URL from its public form toohello form expected by hello web service, as shown in hello following example.</span></span>  
  
-   <span data-ttu-id="19863-445">URL pública: `http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="19863-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="19863-446">URL de solicitud: `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="19863-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="19863-447">Esta directiva puede usarse cuando una dirección URL humana y/o compatible con el explorador debería transformarse en formato de dirección URL de hello esperado por el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-447">This policy can be used when a human and/or browser-friendly URL should be transformed into hello URL format expected by hello web service.</span></span> <span data-ttu-id="19863-448">Esta directiva solo debe toobe aplicado al exponer un formato de dirección URL alternativo, como direcciones URL limpias, direcciones URL RESTful, direcciones URL descriptivas o direcciones URL descriptivas del SEO que son direcciones URL puramente estructurales que no contienen una cadena de consulta y en su lugar contienen sólo ruta de acceso de Hola de Hola recurso (después de esquema de Hola y la autoridad de hello).</span><span class="sxs-lookup"><span data-stu-id="19863-448">This policy only needs toobe applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only hello path of hello resource (after hello scheme and hello authority).</span></span> <span data-ttu-id="19863-449">Este procedimiento se realiza con fines estéticos, de usabilidad o de optimización del motor de búsqueda (SEO).</span><span class="sxs-lookup"><span data-stu-id="19863-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="19863-450">Solo puede agregar parámetros de cadena de consulta mediante la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="19863-450">You can only add query string parameters using hello policy.</span></span> <span data-ttu-id="19863-451">No se puede agregar parámetros de ruta de acceso de plantilla adicionales en hello reescribir dirección URL.</span><span class="sxs-lookup"><span data-stu-id="19863-451">You cannot add extra template path parameters in hello rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="19863-452">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="19863-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="19863-453">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="19863-453">Example</span></span>  
  
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

### <a name="elements"></a><span data-ttu-id="19863-454">Elementos</span><span class="sxs-lookup"><span data-stu-id="19863-454">Elements</span></span>  
  
|<span data-ttu-id="19863-455">Nombre</span><span class="sxs-lookup"><span data-stu-id="19863-455">Name</span></span>|<span data-ttu-id="19863-456">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-456">Description</span></span>|<span data-ttu-id="19863-457">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="19863-458">rewrite-uri</span><span class="sxs-lookup"><span data-stu-id="19863-458">rewrite-uri</span></span>|<span data-ttu-id="19863-459">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="19863-459">Root element.</span></span>|<span data-ttu-id="19863-460">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="19863-461">Attributes</span><span class="sxs-lookup"><span data-stu-id="19863-461">Attributes</span></span>  
  
|<span data-ttu-id="19863-462">Atributo</span><span class="sxs-lookup"><span data-stu-id="19863-462">Attribute</span></span>|<span data-ttu-id="19863-463">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-463">Description</span></span>|<span data-ttu-id="19863-464">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-464">Required</span></span>|<span data-ttu-id="19863-465">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="19863-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="19863-466">template</span><span class="sxs-lookup"><span data-stu-id="19863-466">template</span></span>|<span data-ttu-id="19863-467">Hola web real dirección URL del servicio con los parámetros de cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="19863-467">hello actual web service URL with any query string parameters.</span></span> <span data-ttu-id="19863-468">Cuando se usan expresiones, el valor completo de hello debe ser una expresión.</span><span class="sxs-lookup"><span data-stu-id="19863-468">When using expressions, hello whole value must be an expression.</span></span>|<span data-ttu-id="19863-469">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-469">Yes</span></span>|<span data-ttu-id="19863-470">N/D</span><span class="sxs-lookup"><span data-stu-id="19863-470">N/A</span></span>|  
|<span data-ttu-id="19863-471">copy-unmatched-params</span><span class="sxs-lookup"><span data-stu-id="19863-471">copy-unmatched-params</span></span>|<span data-ttu-id="19863-472">Especifica si los parámetros de consulta en la solicitud entrante de hello no está presente en la plantilla de dirección URL original de Hola se agregan plantilla volver a escribir la dirección URL de toohello definido por hello</span><span class="sxs-lookup"><span data-stu-id="19863-472">Specifies whether query parameters in hello incoming request not present in hello original URL template are added toohello URL defined by hello re-write template</span></span>|<span data-ttu-id="19863-473">No</span><span class="sxs-lookup"><span data-stu-id="19863-473">No</span></span>|<span data-ttu-id="19863-474">true</span><span class="sxs-lookup"><span data-stu-id="19863-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="19863-475">Uso</span><span class="sxs-lookup"><span data-stu-id="19863-475">Usage</span></span>  
 <span data-ttu-id="19863-476">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="19863-476">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="19863-477">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="19863-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="19863-478">**Ámbitos de la directiva:** producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="19863-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="19863-479"><a name="XSLTransform"></a> Transformar XML mediante una XSLT</span><span class="sxs-lookup"><span data-stu-id="19863-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="19863-480">Hola `Transform XML using an XSLT` un tooXML de transformación XSL en el cuerpo de solicitud o respuesta Hola aplica la directiva.</span><span class="sxs-lookup"><span data-stu-id="19863-480">hello `Transform XML using an XSLT` policy applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="19863-481">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="19863-481">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="19863-482">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="19863-482">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="19863-483">Elementos</span><span class="sxs-lookup"><span data-stu-id="19863-483">Elements</span></span>  
  
|<span data-ttu-id="19863-484">Nombre</span><span class="sxs-lookup"><span data-stu-id="19863-484">Name</span></span>|<span data-ttu-id="19863-485">Descripción</span><span class="sxs-lookup"><span data-stu-id="19863-485">Description</span></span>|<span data-ttu-id="19863-486">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19863-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="19863-487">xsl-transform</span><span class="sxs-lookup"><span data-stu-id="19863-487">xsl-transform</span></span>|<span data-ttu-id="19863-488">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="19863-488">Root element.</span></span>|<span data-ttu-id="19863-489">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-489">Yes</span></span>|  
|<span data-ttu-id="19863-490">Parámetro</span><span class="sxs-lookup"><span data-stu-id="19863-490">parameter</span></span>|<span data-ttu-id="19863-491">Variables de toodefine usado utilizadas en transformación Hola</span><span class="sxs-lookup"><span data-stu-id="19863-491">Used toodefine variables used in hello transform</span></span>|<span data-ttu-id="19863-492">No</span><span class="sxs-lookup"><span data-stu-id="19863-492">No</span></span>|  
|<span data-ttu-id="19863-493">xsl:stylesheet</span><span class="sxs-lookup"><span data-stu-id="19863-493">xsl:stylesheet</span></span>|<span data-ttu-id="19863-494">Elemento raíz de la hoja de estilo.</span><span class="sxs-lookup"><span data-stu-id="19863-494">Root stylesheet element.</span></span> <span data-ttu-id="19863-495">Todos los elementos y atributos definidos dentro de cumplen el estándar de hello [especificación XSLT](http://www.w3.org/TR/xslt)</span><span class="sxs-lookup"><span data-stu-id="19863-495">All elements and attributes defined within follow hello standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="19863-496">Sí</span><span class="sxs-lookup"><span data-stu-id="19863-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="19863-497">Uso</span><span class="sxs-lookup"><span data-stu-id="19863-497">Usage</span></span>  
 <span data-ttu-id="19863-498">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="19863-498">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="19863-499">**Secciones de la directiva:** entrante y saliente</span><span class="sxs-lookup"><span data-stu-id="19863-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="19863-500">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="19863-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="19863-501">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="19863-501">Next steps</span></span>
<span data-ttu-id="19863-502">Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="19863-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
