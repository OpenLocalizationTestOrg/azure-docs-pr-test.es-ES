---
title: "Directivas de transformación de Azure API Management | Microsoft Docs"
description: "Obtenga información sobre las directivas de transformación disponibles para su uso en Azure API Management."
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
ms.openlocfilehash: c2bed904b82c569b28a6e00d0cc9b49107c148dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="c05b9-103">Directivas de transformación de API Management</span><span class="sxs-lookup"><span data-stu-id="c05b9-103">API Management transformation policies</span></span>
<span data-ttu-id="c05b9-104">En este tema se proporciona una referencia para las siguientes directivas de API Management.</span><span class="sxs-lookup"><span data-stu-id="c05b9-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="c05b9-105">Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="c05b9-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="c05b9-106"><a name="TransformationPolicies"></a> Directivas de transformación</span><span class="sxs-lookup"><span data-stu-id="c05b9-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="c05b9-107">[Convertir JSON a XML](api-management-transformation-policies.md#ConvertJSONtoXML) : convierte el cuerpo de solicitud o respuesta de JSON a XML.</span><span class="sxs-lookup"><span data-stu-id="c05b9-107">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
-   <span data-ttu-id="c05b9-108">[Convertir XML a JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) : convierte el cuerpo de solicitud o respuesta de XML a JSON.</span><span class="sxs-lookup"><span data-stu-id="c05b9-108">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
-   <span data-ttu-id="c05b9-109">[Buscar y reemplazar la cadena en el cuerpo](api-management-transformation-policies.md#Findandreplacestringinbody) : encuentra una subcadena de solicitud o de respuesta y la reemplaza por una subcadena diferente.</span><span class="sxs-lookup"><span data-stu-id="c05b9-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="c05b9-110">[Enmascarar URL en el contenido](api-management-transformation-policies.md#MaskURLSContent) : reescribe (enmascara) vínculos en el cuerpo de respuesta para que apunten al vínculo equivalente a través de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c05b9-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
-   <span data-ttu-id="c05b9-111">[Establecer el servicio back-end](api-management-transformation-policies.md#SetBackendService) : cambia el servicio back-end para una solicitud entrante.</span><span class="sxs-lookup"><span data-stu-id="c05b9-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="c05b9-112">[Establecer cuerpo](api-management-transformation-policies.md#SetBody) -establece el cuerpo del mensaje para las solicitudes entrantes y salientes.</span><span class="sxs-lookup"><span data-stu-id="c05b9-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="c05b9-113">[Establecer encabezado HTTP](api-management-transformation-policies.md#SetHTTPheader) : asigna un valor a un encabezado de respuesta o de solicitud existente o agrega un nuevo encabezado de este tipo.</span><span class="sxs-lookup"><span data-stu-id="c05b9-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="c05b9-114">[Establecer el parámetro de cadena de consulta](api-management-transformation-policies.md#SetQueryStringParameter) : agrega, reemplaza el valor o elimina el parámetro de la cadena de consulta de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c05b9-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="c05b9-115">[URL de reescritura](api-management-transformation-policies.md#RewriteURL) : convierte una URL de solicitud de su forma pública a la forma esperada por el servicio web.</span><span class="sxs-lookup"><span data-stu-id="c05b9-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
-   <span data-ttu-id="c05b9-116">[Transformar XML mediante una XSLT](api-management-transformation-policies.md#XSLTransform): aplica una transformación de XSL al XML del cuerpo de la solicitud o respuesta.</span><span class="sxs-lookup"><span data-stu-id="c05b9-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
##  <span data-ttu-id="c05b9-117"><a name="ConvertJSONtoXML"></a> Conversión de JSON a XML</span><span class="sxs-lookup"><span data-stu-id="c05b9-117"><a name="ConvertJSONtoXML"></a> Convert JSON to XML</span></span>  
 <span data-ttu-id="c05b9-118">La directiva `json-to-xml` convierte un cuerpo de solicitud o respuesta de JSON a XML.</span><span class="sxs-lookup"><span data-stu-id="c05b9-118">The `json-to-xml` policy converts a request or response body from JSON to XML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c05b9-119">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="c05b9-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="c05b9-120">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c05b9-120">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="c05b9-121">Elementos</span><span class="sxs-lookup"><span data-stu-id="c05b9-121">Elements</span></span>  
  
|<span data-ttu-id="c05b9-122">Nombre</span><span class="sxs-lookup"><span data-stu-id="c05b9-122">Name</span></span>|<span data-ttu-id="c05b9-123">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-123">Description</span></span>|<span data-ttu-id="c05b9-124">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c05b9-125">json-to-xml</span><span class="sxs-lookup"><span data-stu-id="c05b9-125">json-to-xml</span></span>|<span data-ttu-id="c05b9-126">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="c05b9-126">Root element.</span></span>|<span data-ttu-id="c05b9-127">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c05b9-128">Atributos</span><span class="sxs-lookup"><span data-stu-id="c05b9-128">Attributes</span></span>  
  
|<span data-ttu-id="c05b9-129">Nombre</span><span class="sxs-lookup"><span data-stu-id="c05b9-129">Name</span></span>|<span data-ttu-id="c05b9-130">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-130">Description</span></span>|<span data-ttu-id="c05b9-131">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-131">Required</span></span>|<span data-ttu-id="c05b9-132">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c05b9-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c05b9-133">apply</span><span class="sxs-lookup"><span data-stu-id="c05b9-133">apply</span></span>|<span data-ttu-id="c05b9-134">El atributo debe establecerse en uno de los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="c05b9-134">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="c05b9-135">-   always: indica que se debe aplicar la conversión siempre.</span><span class="sxs-lookup"><span data-stu-id="c05b9-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="c05b9-136">-   content-type-json: especifica que solo se debe realizar la conversión si el encabezado Content-Type indica la presencia de JSON.</span><span class="sxs-lookup"><span data-stu-id="c05b9-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="c05b9-137">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-137">Yes</span></span>|<span data-ttu-id="c05b9-138">N/D</span><span class="sxs-lookup"><span data-stu-id="c05b9-138">N/A</span></span>|  
|<span data-ttu-id="c05b9-139">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="c05b9-139">consider-accept-header</span></span>|<span data-ttu-id="c05b9-140">El atributo debe establecerse en uno de los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="c05b9-140">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="c05b9-141">-   true: especifica que se debe aplicar la conversión si se solicita JSON en el encabezado de aceptación (Accept) de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c05b9-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="c05b9-142">-   false: indica que se debe aplicar siempre la conversión.</span><span class="sxs-lookup"><span data-stu-id="c05b9-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="c05b9-143">No</span><span class="sxs-lookup"><span data-stu-id="c05b9-143">No</span></span>|<span data-ttu-id="c05b9-144">true</span><span class="sxs-lookup"><span data-stu-id="c05b9-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c05b9-145">Uso</span><span class="sxs-lookup"><span data-stu-id="c05b9-145">Usage</span></span>  
 <span data-ttu-id="c05b9-146">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="c05b9-146">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c05b9-147">**Secciones de la directiva:** entrante, saliente y en caso de error</span><span class="sxs-lookup"><span data-stu-id="c05b9-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="c05b9-148">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="c05b9-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c05b9-149"><a name="ConvertXMLtoJSON"></a> Conversión de XML a JSON</span><span class="sxs-lookup"><span data-stu-id="c05b9-149"><a name="ConvertXMLtoJSON"></a> Convert XML to JSON</span></span>  
 <span data-ttu-id="c05b9-150">La directiva `xml-to-json` convierte un cuerpo de solicitud o respuesta de XML a JSON.</span><span class="sxs-lookup"><span data-stu-id="c05b9-150">The `xml-to-json` policy converts a request or response body from XML to JSON.</span></span> <span data-ttu-id="c05b9-151">Esta directiva puede usarse para modernizar API basadas en servicios web de back-end de solo XML.</span><span class="sxs-lookup"><span data-stu-id="c05b9-151">This policy can be used to modernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c05b9-152">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="c05b9-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="c05b9-153">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c05b9-153">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="c05b9-154">Elementos</span><span class="sxs-lookup"><span data-stu-id="c05b9-154">Elements</span></span>  
  
|<span data-ttu-id="c05b9-155">Nombre</span><span class="sxs-lookup"><span data-stu-id="c05b9-155">Name</span></span>|<span data-ttu-id="c05b9-156">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-156">Description</span></span>|<span data-ttu-id="c05b9-157">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c05b9-158">xml-to-json</span><span class="sxs-lookup"><span data-stu-id="c05b9-158">xml-to-json</span></span>|<span data-ttu-id="c05b9-159">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="c05b9-159">Root element.</span></span>|<span data-ttu-id="c05b9-160">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c05b9-161">Atributos</span><span class="sxs-lookup"><span data-stu-id="c05b9-161">Attributes</span></span>  
  
|<span data-ttu-id="c05b9-162">Nombre</span><span class="sxs-lookup"><span data-stu-id="c05b9-162">Name</span></span>|<span data-ttu-id="c05b9-163">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-163">Description</span></span>|<span data-ttu-id="c05b9-164">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-164">Required</span></span>|<span data-ttu-id="c05b9-165">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c05b9-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c05b9-166">kind</span><span class="sxs-lookup"><span data-stu-id="c05b9-166">kind</span></span>|<span data-ttu-id="c05b9-167">El atributo debe establecerse en uno de los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="c05b9-167">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="c05b9-168">-   javascript-friendly: el código JSON convertido presenta un formato intuitivo para los desarrolladores de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c05b9-168">-   javascript-friendly - the converted JSON has a form friendly to JavaScript developers.</span></span><br /><span data-ttu-id="c05b9-169">-   direct: el código JSON convertido refleja la estructura del documento XML original.</span><span class="sxs-lookup"><span data-stu-id="c05b9-169">-   direct - the converted JSON reflects the original XML document's structure.</span></span>|<span data-ttu-id="c05b9-170">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-170">Yes</span></span>|<span data-ttu-id="c05b9-171">N/D</span><span class="sxs-lookup"><span data-stu-id="c05b9-171">N/A</span></span>|  
|<span data-ttu-id="c05b9-172">apply</span><span class="sxs-lookup"><span data-stu-id="c05b9-172">apply</span></span>|<span data-ttu-id="c05b9-173">El atributo debe establecerse en uno de los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="c05b9-173">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="c05b9-174">-   always: indica que se debe realizar la conversión siempre.</span><span class="sxs-lookup"><span data-stu-id="c05b9-174">-   always - convert always.</span></span><br /><span data-ttu-id="c05b9-175">-   content-type-XML: especifica que solo se debe realizar la conversión si el encabezado Content-Type indica la presencia de XML.</span><span class="sxs-lookup"><span data-stu-id="c05b9-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="c05b9-176">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-176">Yes</span></span>|<span data-ttu-id="c05b9-177">N/D</span><span class="sxs-lookup"><span data-stu-id="c05b9-177">N/A</span></span>|  
|<span data-ttu-id="c05b9-178">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="c05b9-178">consider-accept-header</span></span>|<span data-ttu-id="c05b9-179">El atributo debe establecerse en uno de los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="c05b9-179">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="c05b9-180">-   true: especifica que se debe aplicar la conversión si se solicita XML en el encabezado de aceptación (Accept) de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c05b9-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="c05b9-181">-   false: indica que se debe aplicar siempre la conversión.</span><span class="sxs-lookup"><span data-stu-id="c05b9-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="c05b9-182">No</span><span class="sxs-lookup"><span data-stu-id="c05b9-182">No</span></span>|<span data-ttu-id="c05b9-183">true</span><span class="sxs-lookup"><span data-stu-id="c05b9-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c05b9-184">Uso</span><span class="sxs-lookup"><span data-stu-id="c05b9-184">Usage</span></span>  
 <span data-ttu-id="c05b9-185">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="c05b9-185">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c05b9-186">**Secciones de la directiva:** entrante, saliente y en caso de error</span><span class="sxs-lookup"><span data-stu-id="c05b9-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="c05b9-187">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="c05b9-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c05b9-188"><a name="Findandreplacestringinbody"></a> Buscar y reemplazar la cadena en el cuerpo</span><span class="sxs-lookup"><span data-stu-id="c05b9-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="c05b9-189">La política `find-and-replace` busca una subcadena de solicitud o de respuesta y la sustituye por otra distinta.</span><span class="sxs-lookup"><span data-stu-id="c05b9-189">The `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c05b9-190">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="c05b9-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what to replace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="c05b9-191">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c05b9-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="c05b9-192">Elementos</span><span class="sxs-lookup"><span data-stu-id="c05b9-192">Elements</span></span>  
  
|<span data-ttu-id="c05b9-193">Nombre</span><span class="sxs-lookup"><span data-stu-id="c05b9-193">Name</span></span>|<span data-ttu-id="c05b9-194">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-194">Description</span></span>|<span data-ttu-id="c05b9-195">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c05b9-196">find-and-replace</span><span class="sxs-lookup"><span data-stu-id="c05b9-196">find-and-replace</span></span>|<span data-ttu-id="c05b9-197">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="c05b9-197">Root element.</span></span>|<span data-ttu-id="c05b9-198">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c05b9-199">Atributos</span><span class="sxs-lookup"><span data-stu-id="c05b9-199">Attributes</span></span>  
  
|<span data-ttu-id="c05b9-200">Nombre</span><span class="sxs-lookup"><span data-stu-id="c05b9-200">Name</span></span>|<span data-ttu-id="c05b9-201">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-201">Description</span></span>|<span data-ttu-id="c05b9-202">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-202">Required</span></span>|<span data-ttu-id="c05b9-203">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c05b9-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c05b9-204">De</span><span class="sxs-lookup"><span data-stu-id="c05b9-204">from</span></span>|<span data-ttu-id="c05b9-205">La cadena que se va a buscar.</span><span class="sxs-lookup"><span data-stu-id="c05b9-205">The string to search for.</span></span>|<span data-ttu-id="c05b9-206">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-206">Yes</span></span>|<span data-ttu-id="c05b9-207">N/D</span><span class="sxs-lookup"><span data-stu-id="c05b9-207">N/A</span></span>|  
|<span data-ttu-id="c05b9-208">Para</span><span class="sxs-lookup"><span data-stu-id="c05b9-208">to</span></span>|<span data-ttu-id="c05b9-209">La cadena de sustitución.</span><span class="sxs-lookup"><span data-stu-id="c05b9-209">The replacement string.</span></span> <span data-ttu-id="c05b9-210">Especifique una cadena de reemplazo de longitud cero para quitar la cadena de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="c05b9-210">Specify a zero length replacement string to remove the search string.</span></span>|<span data-ttu-id="c05b9-211">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-211">Yes</span></span>|<span data-ttu-id="c05b9-212">N/D</span><span class="sxs-lookup"><span data-stu-id="c05b9-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c05b9-213">Uso</span><span class="sxs-lookup"><span data-stu-id="c05b9-213">Usage</span></span>  
 <span data-ttu-id="c05b9-214">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="c05b9-214">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c05b9-215">**Secciones de la directiva:** entrante, saliente, back-end y en caso de error</span><span class="sxs-lookup"><span data-stu-id="c05b9-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="c05b9-216">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="c05b9-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c05b9-217"><a name="MaskURLSContent"></a> Enmascarar URL en el contenido</span><span class="sxs-lookup"><span data-stu-id="c05b9-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="c05b9-218">La directiva `redirect-content-urls` reescribe (enmascara) los vínculos del cuerpo de la respuesta para que apunten al vinculo equivalente a través de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c05b9-218">The `redirect-content-urls` policy re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span> <span data-ttu-id="c05b9-219">Utilícela en la sección saliente a fin de rescribir los vínculos del cuerpo de la respuesta para hacer que apunten a la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c05b9-219">Use in the outbound section to re-write response body links to make them point to the gateway.</span></span> <span data-ttu-id="c05b9-220">Úsela en la sección entrante para obtener el resultado opuesto.</span><span class="sxs-lookup"><span data-stu-id="c05b9-220">Use in the inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="c05b9-221">Esta directiva no cambia los valores de los encabezados, como los `Location`.</span><span class="sxs-lookup"><span data-stu-id="c05b9-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="c05b9-222">Para cambiar los valores del encabezado, use la directiva [set-header](api-management-transformation-policies.md#SetHTTPheader).</span><span class="sxs-lookup"><span data-stu-id="c05b9-222">To change header values, use the [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c05b9-223">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="c05b9-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="c05b9-224">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c05b9-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="c05b9-225">Elementos</span><span class="sxs-lookup"><span data-stu-id="c05b9-225">Elements</span></span>  
  
|<span data-ttu-id="c05b9-226">Nombre</span><span class="sxs-lookup"><span data-stu-id="c05b9-226">Name</span></span>|<span data-ttu-id="c05b9-227">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-227">Description</span></span>|<span data-ttu-id="c05b9-228">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c05b9-229">redirect-content-urls</span><span class="sxs-lookup"><span data-stu-id="c05b9-229">redirect-content-urls</span></span>|<span data-ttu-id="c05b9-230">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="c05b9-230">Root element.</span></span>|<span data-ttu-id="c05b9-231">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c05b9-232">Uso</span><span class="sxs-lookup"><span data-stu-id="c05b9-232">Usage</span></span>  
 <span data-ttu-id="c05b9-233">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="c05b9-233">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c05b9-234">**Secciones de la directiva:** entrante y saliente</span><span class="sxs-lookup"><span data-stu-id="c05b9-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="c05b9-235">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="c05b9-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c05b9-236"><a name="SetBackendService"></a> Establecer el servicio back-end</span><span class="sxs-lookup"><span data-stu-id="c05b9-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="c05b9-237">Use la directiva `set-backend-service` a fin de redirigir una solicitud entrante a un back-end distinto al especificado en la configuración de la API para esa operación.</span><span class="sxs-lookup"><span data-stu-id="c05b9-237">Use the `set-backend-service` policy to redirect an incoming request to a different backend than the one specified in the API settings for that operation.</span></span> <span data-ttu-id="c05b9-238">Esta directiva cambia la dirección URL base del servicio back-end de la solicitud entrante a la especificada en la directiva.</span><span class="sxs-lookup"><span data-stu-id="c05b9-238">This policy changes the backend service base URL of the incoming request to the one specified in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c05b9-239">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="c05b9-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of the backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="c05b9-240">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c05b9-240">Example</span></span>  
  
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
<span data-ttu-id="c05b9-241">En este ejemplo, la directiva del servicio back-end establecida enruta las solicitudes según el valor de versión pasado en la cadena de consulta a un servicio back-end distinto del especificado en la API.</span><span class="sxs-lookup"><span data-stu-id="c05b9-241">In this example the set backend service policy routes requests based on the version value passed in the query string to a different backend service than the one specified in the API.</span></span>
  
<span data-ttu-id="c05b9-242">Inicialmente, la dirección URL base del servicio back-end se obtiene a partir de la configuración de la API.</span><span class="sxs-lookup"><span data-stu-id="c05b9-242">Initially the backend service base URL is derived from the API settings.</span></span> <span data-ttu-id="c05b9-243">Por ello, la dirección URL de solicitud `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` se convierte en `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef`, donde `http://contoso.com/api/10.4/` se corresponde con la dirección URL del servicio back-end especificada en la configuración de la API.</span><span class="sxs-lookup"><span data-stu-id="c05b9-243">So the request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is the backend service URL specified in the API settings.</span></span>  
  
<span data-ttu-id="c05b9-244">Cuando se aplica la instrucción de la directiva [<choose\>](api-management-advanced-policies.md#choose), la dirección URL base del servicio back-end puede volver a cambiar a `http://contoso.com/api/8.2` o `http://contoso.com/api/9.1`, en función del valor del parámetro de consulta de la solicitud de la versión.</span><span class="sxs-lookup"><span data-stu-id="c05b9-244">When the [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied the backend service base URL may change again either to `http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on the value of the version request query parameter.</span></span> <span data-ttu-id="c05b9-245">Por ejemplo, si el valor es `"2013-15"`, la dirección URL final de la solicitud se convierte en `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span><span class="sxs-lookup"><span data-stu-id="c05b9-245">For example, if the value is `"2013-15"` the final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="c05b9-246">Si se desea aplicar más transformaciones a la solicitud, es posible usar otras [directivas de transformación](api-management-transformation-policies.md#TransformationPolicies).</span><span class="sxs-lookup"><span data-stu-id="c05b9-246">If further transformation of the request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="c05b9-247">Por ejemplo, para quitar el parámetro de consulta de la versión ahora que la solicitud se está enrutando a un back-end específico de la versión, se puede usar la directiva de [establecimiento del parámetro de cadena de consulta](api-management-transformation-policies.md#SetQueryStringParameter) para quitar el atributo de versión, que ahora presenta un carácter redundante.</span><span class="sxs-lookup"><span data-stu-id="c05b9-247">For example, to remove the version query parameter now that the request is being routed to a version specific backend, the  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used to remove the now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="c05b9-248">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c05b9-248">Example</span></span>  
  
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
<span data-ttu-id="c05b9-249">En este ejemplo, la directiva enruta la solicitud a un back-end de Service Fabric, con la cadena de consulta userId como la clave de partición y con la réplica principal de la partición.</span><span class="sxs-lookup"><span data-stu-id="c05b9-249">In this example the policy routes the request to a service fabric backend, using the userId query string as the partition key and using the primary replica of the partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="c05b9-250">Elementos</span><span class="sxs-lookup"><span data-stu-id="c05b9-250">Elements</span></span>  
  
|<span data-ttu-id="c05b9-251">Nombre</span><span class="sxs-lookup"><span data-stu-id="c05b9-251">Name</span></span>|<span data-ttu-id="c05b9-252">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-252">Description</span></span>|<span data-ttu-id="c05b9-253">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c05b9-254">set-backend-service</span><span class="sxs-lookup"><span data-stu-id="c05b9-254">set-backend-service</span></span>|<span data-ttu-id="c05b9-255">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="c05b9-255">Root element.</span></span>|<span data-ttu-id="c05b9-256">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c05b9-257">Atributos</span><span class="sxs-lookup"><span data-stu-id="c05b9-257">Attributes</span></span>  
  
|<span data-ttu-id="c05b9-258">Nombre</span><span class="sxs-lookup"><span data-stu-id="c05b9-258">Name</span></span>|<span data-ttu-id="c05b9-259">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-259">Description</span></span>|<span data-ttu-id="c05b9-260">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-260">Required</span></span>|<span data-ttu-id="c05b9-261">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c05b9-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c05b9-262">base-url</span><span class="sxs-lookup"><span data-stu-id="c05b9-262">base-url</span></span>|<span data-ttu-id="c05b9-263">Nueva dirección URL base del servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="c05b9-263">New backend service base URL.</span></span>|<span data-ttu-id="c05b9-264">No</span><span class="sxs-lookup"><span data-stu-id="c05b9-264">No</span></span>|<span data-ttu-id="c05b9-265">N/D</span><span class="sxs-lookup"><span data-stu-id="c05b9-265">N/A</span></span>|  
|<span data-ttu-id="c05b9-266">backend-id</span><span class="sxs-lookup"><span data-stu-id="c05b9-266">backend-id</span></span>|<span data-ttu-id="c05b9-267">Identificador del back-end al que se va a enrutar.</span><span class="sxs-lookup"><span data-stu-id="c05b9-267">Identifier of the backend to route to.</span></span>|<span data-ttu-id="c05b9-268">No</span><span class="sxs-lookup"><span data-stu-id="c05b9-268">No</span></span>|<span data-ttu-id="c05b9-269">N/D</span><span class="sxs-lookup"><span data-stu-id="c05b9-269">N/A</span></span>|  
|<span data-ttu-id="c05b9-270">sf-partition-key</span><span class="sxs-lookup"><span data-stu-id="c05b9-270">sf-partition-key</span></span>|<span data-ttu-id="c05b9-271">Solo se aplica cuando el back-end es un servicio de Service Fabric y se especifica con "backend-id".</span><span class="sxs-lookup"><span data-stu-id="c05b9-271">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="c05b9-272">Se usa para resolver una partición específica desde el servicio de resolución de nombres.</span><span class="sxs-lookup"><span data-stu-id="c05b9-272">Used to resolve a specific partition from the name resolution service.</span></span>|<span data-ttu-id="c05b9-273">No</span><span class="sxs-lookup"><span data-stu-id="c05b9-273">No</span></span>|<span data-ttu-id="c05b9-274">N/D</span><span class="sxs-lookup"><span data-stu-id="c05b9-274">N/A</span></span>|  
|<span data-ttu-id="c05b9-275">sf-replica-type</span><span class="sxs-lookup"><span data-stu-id="c05b9-275">sf-replica-type</span></span>|<span data-ttu-id="c05b9-276">Solo se aplica cuando el back-end es un servicio de Service Fabric y se especifica con "backend-id".</span><span class="sxs-lookup"><span data-stu-id="c05b9-276">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="c05b9-277">Controla si la solicitud debe ir a la réplica principal o secundaria de una partición.</span><span class="sxs-lookup"><span data-stu-id="c05b9-277">Controls if the request should go to the primary or secondary replica of a partition.</span></span> |<span data-ttu-id="c05b9-278">No</span><span class="sxs-lookup"><span data-stu-id="c05b9-278">No</span></span>|<span data-ttu-id="c05b9-279">N/D</span><span class="sxs-lookup"><span data-stu-id="c05b9-279">N/A</span></span>|    
|<span data-ttu-id="c05b9-280">sf-resolve-condition</span><span class="sxs-lookup"><span data-stu-id="c05b9-280">sf-resolve-condition</span></span>|<span data-ttu-id="c05b9-281">Solo se aplica cuando el back-end es un servicio de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c05b9-281">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="c05b9-282">Condición que identifica si la llamada al back-end de Service Fabric tiene que repetirse con la nueva resolución.</span><span class="sxs-lookup"><span data-stu-id="c05b9-282">Condition identifying if the call to Service Fabric backend has to be repeated with new resolution.</span></span>|<span data-ttu-id="c05b9-283">No</span><span class="sxs-lookup"><span data-stu-id="c05b9-283">No</span></span>|<span data-ttu-id="c05b9-284">N/D</span><span class="sxs-lookup"><span data-stu-id="c05b9-284">N/A</span></span>|    
|<span data-ttu-id="c05b9-285">sf-service-instance-name</span><span class="sxs-lookup"><span data-stu-id="c05b9-285">sf-service-instance-name</span></span>|<span data-ttu-id="c05b9-286">Solo se aplica cuando el back-end es un servicio de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c05b9-286">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="c05b9-287">Permite cambiar instancias de servicio en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c05b9-287">Allows to change service instances at runtime.</span></span> |<span data-ttu-id="c05b9-288">No</span><span class="sxs-lookup"><span data-stu-id="c05b9-288">No</span></span>|<span data-ttu-id="c05b9-289">N/D</span><span class="sxs-lookup"><span data-stu-id="c05b9-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="c05b9-290">Uso</span><span class="sxs-lookup"><span data-stu-id="c05b9-290">Usage</span></span>  
 <span data-ttu-id="c05b9-291">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="c05b9-291">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c05b9-292">**Secciones de la directiva:** entrante y back-end</span><span class="sxs-lookup"><span data-stu-id="c05b9-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="c05b9-293">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="c05b9-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c05b9-294"><a name="SetBody"></a> Establecer cuerpo</span><span class="sxs-lookup"><span data-stu-id="c05b9-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="c05b9-295">Utilice la directiva `set-body` con la finalidad de establecer el cuerpo del mensaje para las solicitudes entrantes y salientes.</span><span class="sxs-lookup"><span data-stu-id="c05b9-295">Use the `set-body` policy to set the message body for incoming and outgoing requests.</span></span> <span data-ttu-id="c05b9-296">Para acceder al cuerpo del mensaje, puede utilizar las propiedades `context.Request.Body` o `context.Response.Body`, según si la directiva se encuentra en la sección entrante o saliente.</span><span class="sxs-lookup"><span data-stu-id="c05b9-296">To access the message body you can use the `context.Request.Body` property or the `context.Response.Body`, depending on whether the policy is in the inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="c05b9-297">Tenga en cuenta que, de forma predeterminada, al acceder al cuerpo del mensaje mediante `context.Request.Body` o `context.Response.Body`, se pierde el cuerpo del mensaje original y se debe establecer devolviendo el cuerpo en la expresión.</span><span class="sxs-lookup"><span data-stu-id="c05b9-297">Note that by default when you access the message body using `context.Request.Body` or `context.Response.Body`, the original message body is lost and must be set by returning the body back in the expression.</span></span> <span data-ttu-id="c05b9-298">Para conservar el contenido del cuerpo, establezca el parámetro `preserveContent` en `true` al acceder al mensaje.</span><span class="sxs-lookup"><span data-stu-id="c05b9-298">To preserve the body content, set the `preserveContent` parameter to `true` when accessing the message.</span></span> <span data-ttu-id="c05b9-299">Si `preserveContent` está establecido en `true` y la expresión devuelve un cuerpo distinto, se utiliza el que se devuelva.</span><span class="sxs-lookup"><span data-stu-id="c05b9-299">If `preserveContent` is set to `true` and a different body is returned by the expression, the returned body is used.</span></span>  
>   
>  <span data-ttu-id="c05b9-300">Tenga en cuenta las siguientes consideraciones al utilizar la directiva `set-body`.</span><span class="sxs-lookup"><span data-stu-id="c05b9-300">Please note the following considerations when using the `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="c05b9-301">Si usa la directiva `set-body` para devolver un cuerpo nuevo o actualizado, no hay que establecer `preserveContent` en `true` porque estará especificando explícitamente el nuevo contenido del cuerpo.</span><span class="sxs-lookup"><span data-stu-id="c05b9-301">If you are using the `set-body` policy to return a new or updated body you don't need to set `preserveContent` to `true` because you are explicitly supplying the new body contents.</span></span>  
> -   <span data-ttu-id="c05b9-302">No tiene sentido conservar el contenido de una respuesta en la canalización de entrada porque todavía no hay ninguna respuesta.</span><span class="sxs-lookup"><span data-stu-id="c05b9-302">Preserving the content of a response in the inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="c05b9-303">De igual modo, no tiene sentido conservar el contenido de una solicitud en la canalización de salida porque la solicitud ya se ha enviado al servidor en este momento.</span><span class="sxs-lookup"><span data-stu-id="c05b9-303">Preserving the content of a request in the outbound pipeline doesn't make sense because the request has already been sent to the backend at this point.</span></span>  
> -   <span data-ttu-id="c05b9-304">Si esta directiva se usa cuando no hay ningún cuerpo de mensaje, por ejemplo, en un GET entrante, se producirá una excepción.</span><span class="sxs-lookup"><span data-stu-id="c05b9-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="c05b9-305">Para obtener más información, consulte las secciones `context.Request.Body`, `context.Response.Body` y `IMessage` de la tabla [Context variable](api-management-policy-expressions.md#ContextVariables) (Variable de contexto).</span><span class="sxs-lookup"><span data-stu-id="c05b9-305">For more information, see the `context.Request.Body`, `context.Response.Body`, and the `IMessage` sections in the [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c05b9-306">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="c05b9-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="c05b9-307">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c05b9-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="c05b9-308">Ejemplo de texto literal</span><span class="sxs-lookup"><span data-stu-id="c05b9-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-the-body-as-a-string-note-that-we-are-preserving-the-original-request-body-so-that-we-can-access-it-later-in-the-pipeline"></a><span data-ttu-id="c05b9-309">Ejemplo de acceso al cuerpo como una cadena.</span><span class="sxs-lookup"><span data-stu-id="c05b9-309">Example accessing the body as a string.</span></span> <span data-ttu-id="c05b9-310">Tenga en cuenta que estamos conservando el cuerpo de la solicitud original para que resulte accesible más adelante en la canalización.</span><span class="sxs-lookup"><span data-stu-id="c05b9-310">Note that we are preserving the original request body so that we can access it later in the pipeline.</span></span>
  
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
  
#### <a name="example-accessing-the-body-as-a-jobject-note-that-since-we-are-not-reserving-the-original-request-body-accesing-it-later-in-the-pipeline-will-result-in-an-exception"></a><span data-ttu-id="c05b9-311">Ejemplo de acceso al cuerpo como un elemento JObject.</span><span class="sxs-lookup"><span data-stu-id="c05b9-311">Example accessing the body as a JObject.</span></span> <span data-ttu-id="c05b9-312">Tenga en cuenta que, al no estar conservando el cuerpo de la solicitud original, el acceso posterior a él en la canalización producirá una excepción.</span><span class="sxs-lookup"><span data-stu-id="c05b9-312">Note that since we are not reserving the original request body, accesing it later in the pipeline will result in an exception.</span></span>  
  
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
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="c05b9-313">Filtro de respuesta según un producto</span><span class="sxs-lookup"><span data-stu-id="c05b9-313">Filter response based on product</span></span>  
 <span data-ttu-id="c05b9-314">En este ejemplo se muestra cómo filtrar contenido quitando elementos de datos de la respuesta recibida del servicio back-end al usar el producto `Starter`.</span><span class="sxs-lookup"><span data-stu-id="c05b9-314">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="c05b9-315">Para ver una demostración de la configuración y el uso de esta directiva, vea [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Episodio 177 de Cloud Cover: más características API Management con Vlad Vinogradsky) y avance al minuto 34:30.</span><span class="sxs-lookup"><span data-stu-id="c05b9-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="c05b9-316">Empiece en el minuto 31:50 para ver una introducción a la [API de previsión de Dark Sky](https://developer.forecast.io/) empleada en esta demostración.</span><span class="sxs-lookup"><span data-stu-id="c05b9-316">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into the outbound section to remove a number of data elements from the response received from the backend service based on the name of the api product -->  
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

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="c05b9-317">Uso de plantillas Liquid con la directiva de establecer cuerpo</span><span class="sxs-lookup"><span data-stu-id="c05b9-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="c05b9-318">La directiva `set-body` se puede configurar para usar el lenguaje de plantillas [Liquid](https://shopify.github.io/liquid/basics/introduction/) que transforman el cuerpo de una solicitud o respuesta.</span><span class="sxs-lookup"><span data-stu-id="c05b9-318">The `set-body` policy can be configured to use the [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language to transfom the body of a request or response.</span></span> <span data-ttu-id="c05b9-319">Esto puede resultar muy eficaz si necesita cambiar completamente el formato del mensaje.</span><span class="sxs-lookup"><span data-stu-id="c05b9-319">This can be very effective if you need to completely reshape the format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c05b9-320">La implementación de Liquid que se utiliza en la directiva `set-body` está configurada en el modo de C#.</span><span class="sxs-lookup"><span data-stu-id="c05b9-320">The implementation of Liquid used in the `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="c05b9-321">Esto es especialmente importante al realizar tareas como el filtrado.</span><span class="sxs-lookup"><span data-stu-id="c05b9-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="c05b9-322">Por ejemplo, para usar un filtro de fecha se requiere usar las mayúsculas y minúsculas de Pascal y el formato de fecha de C#; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c05b9-322">As an example, using a date filter requires the use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="c05b9-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="c05b9-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c05b9-324">Para enlazar correctamente con un cuerpo XML mediante la plantilla Liquid, use una directiva `set-header` para establecer que Content-Type sea application/xml, text/xml (o cualquier tipo que termine en +xml); para un cuerpo JSON, debe ser application/json, texto/json (o cualquier tipo que termine en +json).</span><span class="sxs-lookup"><span data-stu-id="c05b9-324">In order to correctly bind to an XML body using the Liquid template, use a `set-header` policy to set Content-Type to either application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-to-soap-using-a-liquid-template"></a><span data-ttu-id="c05b9-325">Conversión de JSON en SOAP mediante una plantilla Liquid</span><span class="sxs-lookup"><span data-stu-id="c05b9-325">Convert JSON to SOAP using a Liquid template</span></span>
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

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="c05b9-326">Transformación de JSON mediante una plantilla Liquid</span><span class="sxs-lookup"><span data-stu-id="c05b9-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="c05b9-327">Elementos</span><span class="sxs-lookup"><span data-stu-id="c05b9-327">Elements</span></span>  
  
|<span data-ttu-id="c05b9-328">Nombre</span><span class="sxs-lookup"><span data-stu-id="c05b9-328">Name</span></span>|<span data-ttu-id="c05b9-329">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-329">Description</span></span>|<span data-ttu-id="c05b9-330">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c05b9-331">set-body</span><span class="sxs-lookup"><span data-stu-id="c05b9-331">set-body</span></span>|<span data-ttu-id="c05b9-332">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="c05b9-332">Root element.</span></span> <span data-ttu-id="c05b9-333">Contiene el cuerpo del texto o una expresión que devuelve un cuerpo.</span><span class="sxs-lookup"><span data-stu-id="c05b9-333">Contains the body text or an expressions that returns a body.</span></span>|<span data-ttu-id="c05b9-334">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="c05b9-335">Propiedades</span><span class="sxs-lookup"><span data-stu-id="c05b9-335">Properties</span></span>  
  
|<span data-ttu-id="c05b9-336">Nombre</span><span class="sxs-lookup"><span data-stu-id="c05b9-336">Name</span></span>|<span data-ttu-id="c05b9-337">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-337">Description</span></span>|<span data-ttu-id="c05b9-338">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-338">Required</span></span>|<span data-ttu-id="c05b9-339">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c05b9-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c05b9-340">template</span><span class="sxs-lookup"><span data-stu-id="c05b9-340">template</span></span>|<span data-ttu-id="c05b9-341">Se utiliza para cambiar el modo de creación de plantillas que ejecutará la directiva de establecer cuerpo.</span><span class="sxs-lookup"><span data-stu-id="c05b9-341">Used to change the templating mode that the set body policy will run in.</span></span> <span data-ttu-id="c05b9-342">Actualmente, el único valor admitido es:</span><span class="sxs-lookup"><span data-stu-id="c05b9-342">Currently the only supported value is:</span></span><br /><br /><span data-ttu-id="c05b9-343">- liquid: la directiva de establecer cuerpo usará el motor de plantillas Liquid</span><span class="sxs-lookup"><span data-stu-id="c05b9-343">- liquid - the set body policy will use the liquid templating engine</span></span> |<span data-ttu-id="c05b9-344">No</span><span class="sxs-lookup"><span data-stu-id="c05b9-344">No</span></span>|<span data-ttu-id="c05b9-345">Liquid</span><span class="sxs-lookup"><span data-stu-id="c05b9-345">liquid</span></span>|  

<span data-ttu-id="c05b9-346">Para acceder a información sobre solicitud y respuesta, la plantilla Liquid puede enlazar a un objeto de contexto con las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="c05b9-346">For accessing information about the request and response, the Liquid template can bind to a context object with the following properties:</span></span> <br />
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



### <a name="usage"></a><span data-ttu-id="c05b9-347">Uso</span><span class="sxs-lookup"><span data-stu-id="c05b9-347">Usage</span></span>  
 <span data-ttu-id="c05b9-348">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="c05b9-348">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c05b9-349">**Secciones de la directiva:** entrante, saliente y back-end</span><span class="sxs-lookup"><span data-stu-id="c05b9-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="c05b9-350">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="c05b9-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c05b9-351"><a name="SetHTTPheader"></a> Establecer encabezado HTTP</span><span class="sxs-lookup"><span data-stu-id="c05b9-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="c05b9-352">La directiva `set-header` asigna un valor a un encabezado de respuesta o de solicitud existente o agrega un nuevo encabezado de este tipo.</span><span class="sxs-lookup"><span data-stu-id="c05b9-352">The `set-header` policy assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="c05b9-353">Inserta una lista de encabezados HTTP en un mensaje HTTP.</span><span class="sxs-lookup"><span data-stu-id="c05b9-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="c05b9-354">Cuando se coloca en un proceso entrante, esta directiva establece los encabezados HTTP para la solicitud que se pasa al servicio de destino.</span><span class="sxs-lookup"><span data-stu-id="c05b9-354">When placed in an inbound pipeline, this policy sets the HTTP headers for the request being passed to the target service.</span></span> <span data-ttu-id="c05b9-355">Cuando se coloca en una canalización saliente, esta directiva establece los encabezados HTTP para la respuesta que se está enviando al cliente de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c05b9-355">When placed in an outbound pipeline, this policy sets the HTTP headers for the response being sent to the gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c05b9-356">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="c05b9-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with the same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="c05b9-357">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c05b9-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="c05b9-358">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c05b9-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="c05b9-359">Reenvío de información contextual al servicio back-end</span><span class="sxs-lookup"><span data-stu-id="c05b9-359">Forward context information to the backend service</span></span>  
 <span data-ttu-id="c05b9-360">En este ejemplo se muestra cómo aplicar directivas en el nivel de API para proporcionar información contextual al servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="c05b9-360">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="c05b9-361">Para ver una demostración de la configuración y el uso de esta directiva, vea [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Episodio 177 de Cloud Cover: más características API Management con Vlad Vinogradsky) y avance al minuto 10:30.</span><span class="sxs-lookup"><span data-stu-id="c05b9-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="c05b9-362">En el minuto 12:10 se realiza una demostración del llamamiento de una operación en el portal para desarrolladores donde podrá ver la directiva en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="c05b9-362">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward some context information, user id and the region the gateway is hosted in, to the backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="c05b9-363">Para obtener más información, consulte [Policy expressions](api-management-policy-expressions.md) (Expresiones de política) y [Context variable](api-management-policy-expressions.md#ContextVariables) (Variable de contexto).</span><span class="sxs-lookup"><span data-stu-id="c05b9-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="c05b9-364">Elementos</span><span class="sxs-lookup"><span data-stu-id="c05b9-364">Elements</span></span>  
  
|<span data-ttu-id="c05b9-365">Nombre</span><span class="sxs-lookup"><span data-stu-id="c05b9-365">Name</span></span>|<span data-ttu-id="c05b9-366">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-366">Description</span></span>|<span data-ttu-id="c05b9-367">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c05b9-368">set-header</span><span class="sxs-lookup"><span data-stu-id="c05b9-368">set-header</span></span>|<span data-ttu-id="c05b9-369">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="c05b9-369">Root element.</span></span>|<span data-ttu-id="c05b9-370">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-370">Yes</span></span>|  
|<span data-ttu-id="c05b9-371">value</span><span class="sxs-lookup"><span data-stu-id="c05b9-371">value</span></span>|<span data-ttu-id="c05b9-372">Especifica el valor del encabezado que se va a establecer.</span><span class="sxs-lookup"><span data-stu-id="c05b9-372">Specifies the value of the header to be set.</span></span> <span data-ttu-id="c05b9-373">Para varios encabezados con el mismo nombre, agregue más elementos `value`.</span><span class="sxs-lookup"><span data-stu-id="c05b9-373">For multiple headers with the same name add additional `value` elements.</span></span>|<span data-ttu-id="c05b9-374">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="c05b9-375">Propiedades</span><span class="sxs-lookup"><span data-stu-id="c05b9-375">Properties</span></span>  
  
|<span data-ttu-id="c05b9-376">Nombre</span><span class="sxs-lookup"><span data-stu-id="c05b9-376">Name</span></span>|<span data-ttu-id="c05b9-377">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-377">Description</span></span>|<span data-ttu-id="c05b9-378">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-378">Required</span></span>|<span data-ttu-id="c05b9-379">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c05b9-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c05b9-380">exists-action</span><span class="sxs-lookup"><span data-stu-id="c05b9-380">exists-action</span></span>|<span data-ttu-id="c05b9-381">Especifica la acción que se debe realizar cuando ya se ha especificado un encabezado.</span><span class="sxs-lookup"><span data-stu-id="c05b9-381">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="c05b9-382">Este atributo debe tener uno de los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="c05b9-382">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="c05b9-383">-   override: sustituye el valor del encabezado existente.</span><span class="sxs-lookup"><span data-stu-id="c05b9-383">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="c05b9-384">-   skip: no sustituye el valor del encabezado existente.</span><span class="sxs-lookup"><span data-stu-id="c05b9-384">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="c05b9-385">-   append: anexa el valor al encabezado existente.</span><span class="sxs-lookup"><span data-stu-id="c05b9-385">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="c05b9-386">-   delete: quita el encabezado de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c05b9-386">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="c05b9-387">Cuando se establece en `override`, si se inscriben varias entradas con el mismo nombre, se establece el encabezado de acuerdo con todas ellas (que se inscribirán varias veces); solo los valores mostrados se establecerán en el resultado.</span><span class="sxs-lookup"><span data-stu-id="c05b9-387">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="c05b9-388">No</span><span class="sxs-lookup"><span data-stu-id="c05b9-388">No</span></span>|<span data-ttu-id="c05b9-389">override</span><span class="sxs-lookup"><span data-stu-id="c05b9-389">override</span></span>|  
|<span data-ttu-id="c05b9-390">name</span><span class="sxs-lookup"><span data-stu-id="c05b9-390">name</span></span>|<span data-ttu-id="c05b9-391">Especifica el nombre del encabezado que se va a establecer.</span><span class="sxs-lookup"><span data-stu-id="c05b9-391">Specifies name of the header to be set.</span></span>|<span data-ttu-id="c05b9-392">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-392">Yes</span></span>|<span data-ttu-id="c05b9-393">N/D</span><span class="sxs-lookup"><span data-stu-id="c05b9-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c05b9-394">Uso</span><span class="sxs-lookup"><span data-stu-id="c05b9-394">Usage</span></span>  
 <span data-ttu-id="c05b9-395">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="c05b9-395">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c05b9-396">**Secciones de la directiva:** entrante, saliente, back-end y en caso de error</span><span class="sxs-lookup"><span data-stu-id="c05b9-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="c05b9-397">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="c05b9-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c05b9-398"><a name="SetQueryStringParameter"></a> Establecimiento del parámetro de cadena de consulta</span><span class="sxs-lookup"><span data-stu-id="c05b9-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="c05b9-399">La directiva `set-query-parameter` agrega o elimina el parámetro de cadena de consulta de la solicitud, o bien sustituye su valor.</span><span class="sxs-lookup"><span data-stu-id="c05b9-399">The `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="c05b9-400">Se puede utilizar para pasar parámetros de consulta previstos por el servicio back-end que tienen carácter opcional o que nunca están presentes en la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c05b9-400">Can be used to pass query parameters expected by the backend service which are optional or never present in the request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c05b9-401">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="c05b9-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with the same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="c05b9-402">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c05b9-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="c05b9-403">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c05b9-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with the same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="c05b9-404">Reenvío de información contextual al servicio back-end</span><span class="sxs-lookup"><span data-stu-id="c05b9-404">Forward context information to the backend service</span></span>  
 <span data-ttu-id="c05b9-405">En este ejemplo se muestra cómo aplicar directivas en el nivel de API para proporcionar información contextual al servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="c05b9-405">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="c05b9-406">Para ver una demostración de la configuración y el uso de esta directiva, vea [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Episodio 177 de Cloud Cover: más características API Management con Vlad Vinogradsky) y avance al minuto 10:30.</span><span class="sxs-lookup"><span data-stu-id="c05b9-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="c05b9-407">En el minuto 12:10 se realiza una demostración del llamamiento de una operación en el portal para desarrolladores donde podrá ver la directiva en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="c05b9-407">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward a piece of context, product name in this example, to the backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="c05b9-408">Para obtener más información, consulte [Policy expressions](api-management-policy-expressions.md) (Expresiones de política) y [Context variable](api-management-policy-expressions.md#ContextVariables) (Variable de contexto).</span><span class="sxs-lookup"><span data-stu-id="c05b9-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="c05b9-409">Elementos</span><span class="sxs-lookup"><span data-stu-id="c05b9-409">Elements</span></span>  
  
|<span data-ttu-id="c05b9-410">Nombre</span><span class="sxs-lookup"><span data-stu-id="c05b9-410">Name</span></span>|<span data-ttu-id="c05b9-411">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-411">Description</span></span>|<span data-ttu-id="c05b9-412">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c05b9-413">set-query-parameter</span><span class="sxs-lookup"><span data-stu-id="c05b9-413">set-query-parameter</span></span>|<span data-ttu-id="c05b9-414">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="c05b9-414">Root element.</span></span>|<span data-ttu-id="c05b9-415">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-415">Yes</span></span>|  
|<span data-ttu-id="c05b9-416">value</span><span class="sxs-lookup"><span data-stu-id="c05b9-416">value</span></span>|<span data-ttu-id="c05b9-417">Especifica el valor del parámetro de consulta que se debe establecer.</span><span class="sxs-lookup"><span data-stu-id="c05b9-417">Specifies the value of the query parameter to be set.</span></span> <span data-ttu-id="c05b9-418">Para varios parámetros de consulta con el mismo nombre, agregue más elementos `value`.</span><span class="sxs-lookup"><span data-stu-id="c05b9-418">For multiple query parameters with the same name add additional `value` elements.</span></span>|<span data-ttu-id="c05b9-419">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="c05b9-420">Propiedades</span><span class="sxs-lookup"><span data-stu-id="c05b9-420">Properties</span></span>  
  
|<span data-ttu-id="c05b9-421">Nombre</span><span class="sxs-lookup"><span data-stu-id="c05b9-421">Name</span></span>|<span data-ttu-id="c05b9-422">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-422">Description</span></span>|<span data-ttu-id="c05b9-423">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-423">Required</span></span>|<span data-ttu-id="c05b9-424">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c05b9-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c05b9-425">exists-action</span><span class="sxs-lookup"><span data-stu-id="c05b9-425">exists-action</span></span>|<span data-ttu-id="c05b9-426">Especifica la acción que se debe realizar cuando ya se especifica un parámetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="c05b9-426">Specifies what action to take when the query parameter is already specified.</span></span> <span data-ttu-id="c05b9-427">Este atributo debe tener uno de los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="c05b9-427">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="c05b9-428">-   override: sustituye el valor del parámetro de consulta existente.</span><span class="sxs-lookup"><span data-stu-id="c05b9-428">-   override - replaces the value of the existing parameter.</span></span><br /><span data-ttu-id="c05b9-429">-   skip: no sustituye el valor del parámetro de consulta existente.</span><span class="sxs-lookup"><span data-stu-id="c05b9-429">-   skip - does not replace the existing query parameter value.</span></span><br /><span data-ttu-id="c05b9-430">-   append: anexa el valor al del parámetro de consulta existente.</span><span class="sxs-lookup"><span data-stu-id="c05b9-430">-   append - appends the value to the existing query parameter value.</span></span><br /><span data-ttu-id="c05b9-431">-   delete: quita el parámetro de consulta de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c05b9-431">-   delete - removes the query parameter from the request.</span></span><br /><br /> <span data-ttu-id="c05b9-432">Cuando se establece en `override`, se inscriben varias entradas con los resultados del mismo nombre del parámetro de consulta que se están estableciendo de acuerdo con todas las entradas (que se inscribirán varias veces); solo los valores mostrados se establecerán en el resultado.</span><span class="sxs-lookup"><span data-stu-id="c05b9-432">When set to `override` enlisting multiple entries with the same name results in the query parameter being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="c05b9-433">No</span><span class="sxs-lookup"><span data-stu-id="c05b9-433">No</span></span>|<span data-ttu-id="c05b9-434">override</span><span class="sxs-lookup"><span data-stu-id="c05b9-434">override</span></span>|  
|<span data-ttu-id="c05b9-435">name</span><span class="sxs-lookup"><span data-stu-id="c05b9-435">name</span></span>|<span data-ttu-id="c05b9-436">Especifica el nombre del parámetro de consulta que se debe establecer.</span><span class="sxs-lookup"><span data-stu-id="c05b9-436">Specifies name of the query parameter to be set.</span></span>|<span data-ttu-id="c05b9-437">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-437">Yes</span></span>|<span data-ttu-id="c05b9-438">N/D</span><span class="sxs-lookup"><span data-stu-id="c05b9-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c05b9-439">Uso</span><span class="sxs-lookup"><span data-stu-id="c05b9-439">Usage</span></span>  
 <span data-ttu-id="c05b9-440">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="c05b9-440">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c05b9-441">**Secciones de la directiva:** entrante y back-end</span><span class="sxs-lookup"><span data-stu-id="c05b9-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="c05b9-442">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="c05b9-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c05b9-443"><a name="RewriteURL"></a> URL de reescritura</span><span class="sxs-lookup"><span data-stu-id="c05b9-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="c05b9-444">La directiva `rewrite-uri` convierte una dirección URL de solicitud de su forma pública a la que espera recibir el servicio web, como se muestra en el siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c05b9-444">The `rewrite-uri` policy converts a request URL from its public form to the form expected by the web service, as shown in the following example.</span></span>  
  
-   <span data-ttu-id="c05b9-445">URL pública: `http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="c05b9-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="c05b9-446">URL de solicitud: `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="c05b9-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="c05b9-447">Esta directiva se puede utilizar cuando una URL apta para el explorador o para individuos debe transformarse en el formato de URL que espera el servicio web.</span><span class="sxs-lookup"><span data-stu-id="c05b9-447">This policy can be used when a human and/or browser-friendly URL should be transformed into the URL format expected by the web service.</span></span> <span data-ttu-id="c05b9-448">Esta directiva solo debe aplicarse al exponer un formato de URL alternativo, como URL limpias, direcciones URL RESTful y direcciones URL sencillas o aptas para optimización del motor de búsqueda que son URL puramente estructurales que no contienen una cadena de consulta, sino solo la ruta del recurso (después del esquema y la autoridad).</span><span class="sxs-lookup"><span data-stu-id="c05b9-448">This policy only needs to be applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only the path of the resource (after the scheme and the authority).</span></span> <span data-ttu-id="c05b9-449">Este procedimiento se realiza con fines estéticos, de usabilidad o de optimización del motor de búsqueda (SEO).</span><span class="sxs-lookup"><span data-stu-id="c05b9-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="c05b9-450">Solo puede agregar parámetros de cadena de consulta mediante esta directiva.</span><span class="sxs-lookup"><span data-stu-id="c05b9-450">You can only add query string parameters using the policy.</span></span> <span data-ttu-id="c05b9-451">No puede agregar ningún parámetro de ruta de plantilla adicional en la URL de reescritura.</span><span class="sxs-lookup"><span data-stu-id="c05b9-451">You cannot add extra template path parameters in the rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="c05b9-452">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="c05b9-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="c05b9-453">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c05b9-453">Example</span></span>  
  
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
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

### <a name="elements"></a><span data-ttu-id="c05b9-454">Elementos</span><span class="sxs-lookup"><span data-stu-id="c05b9-454">Elements</span></span>  
  
|<span data-ttu-id="c05b9-455">Nombre</span><span class="sxs-lookup"><span data-stu-id="c05b9-455">Name</span></span>|<span data-ttu-id="c05b9-456">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-456">Description</span></span>|<span data-ttu-id="c05b9-457">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c05b9-458">rewrite-uri</span><span class="sxs-lookup"><span data-stu-id="c05b9-458">rewrite-uri</span></span>|<span data-ttu-id="c05b9-459">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="c05b9-459">Root element.</span></span>|<span data-ttu-id="c05b9-460">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c05b9-461">Attributes</span><span class="sxs-lookup"><span data-stu-id="c05b9-461">Attributes</span></span>  
  
|<span data-ttu-id="c05b9-462">Atributo</span><span class="sxs-lookup"><span data-stu-id="c05b9-462">Attribute</span></span>|<span data-ttu-id="c05b9-463">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-463">Description</span></span>|<span data-ttu-id="c05b9-464">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-464">Required</span></span>|<span data-ttu-id="c05b9-465">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c05b9-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="c05b9-466">template</span><span class="sxs-lookup"><span data-stu-id="c05b9-466">template</span></span>|<span data-ttu-id="c05b9-467">La dirección URL del servicio web real con cualquier parámetro de cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="c05b9-467">The actual web service URL with any query string parameters.</span></span> <span data-ttu-id="c05b9-468">Cuando se usan expresiones, todo el valor debe ser una expresión.</span><span class="sxs-lookup"><span data-stu-id="c05b9-468">When using expressions, the whole value must be an expression.</span></span>|<span data-ttu-id="c05b9-469">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-469">Yes</span></span>|<span data-ttu-id="c05b9-470">N/D</span><span class="sxs-lookup"><span data-stu-id="c05b9-470">N/A</span></span>|  
|<span data-ttu-id="c05b9-471">copy-unmatched-params</span><span class="sxs-lookup"><span data-stu-id="c05b9-471">copy-unmatched-params</span></span>|<span data-ttu-id="c05b9-472">Especifica si los parámetros de consulta de la solicitud entrante no presentes en la plantilla de la dirección URL original se agregan en la dirección URL definida por la plantilla de reescritura</span><span class="sxs-lookup"><span data-stu-id="c05b9-472">Specifies whether query parameters in the incoming request not present in the original URL template are added to the URL defined by the re-write template</span></span>|<span data-ttu-id="c05b9-473">No</span><span class="sxs-lookup"><span data-stu-id="c05b9-473">No</span></span>|<span data-ttu-id="c05b9-474">true</span><span class="sxs-lookup"><span data-stu-id="c05b9-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c05b9-475">Uso</span><span class="sxs-lookup"><span data-stu-id="c05b9-475">Usage</span></span>  
 <span data-ttu-id="c05b9-476">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="c05b9-476">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c05b9-477">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="c05b9-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="c05b9-478">**Ámbitos de la directiva:** producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="c05b9-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="c05b9-479"><a name="XSLTransform"></a> Transformar XML mediante una XSLT</span><span class="sxs-lookup"><span data-stu-id="c05b9-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="c05b9-480">La directiva `Transform XML using an XSLT` aplica una transformación XSL al XML del cuerpo de la solicitud o la respuesta.</span><span class="sxs-lookup"><span data-stu-id="c05b9-480">The `Transform XML using an XSLT` policy applies an XSL transformation to XML in the request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c05b9-481">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="c05b9-481">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="c05b9-482">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c05b9-482">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="c05b9-483">Elementos</span><span class="sxs-lookup"><span data-stu-id="c05b9-483">Elements</span></span>  
  
|<span data-ttu-id="c05b9-484">Nombre</span><span class="sxs-lookup"><span data-stu-id="c05b9-484">Name</span></span>|<span data-ttu-id="c05b9-485">Descripción</span><span class="sxs-lookup"><span data-stu-id="c05b9-485">Description</span></span>|<span data-ttu-id="c05b9-486">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c05b9-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c05b9-487">xsl-transform</span><span class="sxs-lookup"><span data-stu-id="c05b9-487">xsl-transform</span></span>|<span data-ttu-id="c05b9-488">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="c05b9-488">Root element.</span></span>|<span data-ttu-id="c05b9-489">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-489">Yes</span></span>|  
|<span data-ttu-id="c05b9-490">Parámetro</span><span class="sxs-lookup"><span data-stu-id="c05b9-490">parameter</span></span>|<span data-ttu-id="c05b9-491">Permite definir las variables utilizadas en la transformación.</span><span class="sxs-lookup"><span data-stu-id="c05b9-491">Used to define variables used in the transform</span></span>|<span data-ttu-id="c05b9-492">No</span><span class="sxs-lookup"><span data-stu-id="c05b9-492">No</span></span>|  
|<span data-ttu-id="c05b9-493">xsl:stylesheet</span><span class="sxs-lookup"><span data-stu-id="c05b9-493">xsl:stylesheet</span></span>|<span data-ttu-id="c05b9-494">Elemento raíz de la hoja de estilo.</span><span class="sxs-lookup"><span data-stu-id="c05b9-494">Root stylesheet element.</span></span> <span data-ttu-id="c05b9-495">Todos los elementos y atributos definidos dentro de él cumplen la [especificación XSLT](http://www.w3.org/TR/xslt) estándar.</span><span class="sxs-lookup"><span data-stu-id="c05b9-495">All elements and attributes defined within follow the standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="c05b9-496">Sí</span><span class="sxs-lookup"><span data-stu-id="c05b9-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c05b9-497">Uso</span><span class="sxs-lookup"><span data-stu-id="c05b9-497">Usage</span></span>  
 <span data-ttu-id="c05b9-498">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="c05b9-498">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c05b9-499">**Secciones de la directiva:** entrante y saliente</span><span class="sxs-lookup"><span data-stu-id="c05b9-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="c05b9-500">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="c05b9-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="c05b9-501">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c05b9-501">Next steps</span></span>
<span data-ttu-id="c05b9-502">Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c05b9-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
