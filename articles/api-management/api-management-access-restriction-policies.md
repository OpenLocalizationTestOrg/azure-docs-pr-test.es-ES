---
title: "Directivas de restricción de acceso de Azure API Management | Microsoft Docs"
description: "Aprenda sobre las directivas de restricción de acceso disponibles para su uso en Azure API Management."
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
ms.openlocfilehash: 4c9991baf3fbcf3b8ea01f8dd573e2336db88b68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="f3397-103">Directivas de restricción de acceso de API Management</span><span class="sxs-lookup"><span data-stu-id="f3397-103">API Management access restriction policies</span></span>
<span data-ttu-id="f3397-104">En este tema se proporciona una referencia para las siguientes directivas de API Management.</span><span class="sxs-lookup"><span data-stu-id="f3397-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="f3397-105">Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="f3397-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="f3397-106"><a name="AccessRestrictionPolicies"></a> Directivas de restricción de acceso</span><span class="sxs-lookup"><span data-stu-id="f3397-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="f3397-107">[Activar encabezado HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) : aplica la existencia o el valor de un encabezado HTTP.</span><span class="sxs-lookup"><span data-stu-id="f3397-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="f3397-108">[Limitar la frecuencia de llamadas por suscripción](api-management-access-restriction-policies.md#LimitCallRate) : evita los picos de uso de la API limitando la frecuencia de llamadas, por suscripción.</span><span class="sxs-lookup"><span data-stu-id="f3397-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="f3397-109">[Limitar la frecuencia de llamadas por clave](#LimitCallRateByKey) : evita los picos de uso de la API limitando la frecuencia de llamadas, por clave.</span><span class="sxs-lookup"><span data-stu-id="f3397-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="f3397-110">[Restringir IP de autor de llamada](api-management-access-restriction-policies.md#RestrictCallerIPs) : filtra (permite/deniega) las llamadas de direcciones IP específicas o de intervalos de direcciones.</span><span class="sxs-lookup"><span data-stu-id="f3397-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="f3397-111">[Establecer cuota de uso por suscripción](api-management-access-restriction-policies.md#SetUsageQuota) : le permite aplicar un volumen de llamadas renovables o permanentes o una cuota de ancho de banda por suscripción.</span><span class="sxs-lookup"><span data-stu-id="f3397-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="f3397-112">[Establecer cuota de uso por clave](#SetUsageQuotaByKey) : le permite aplicar un volumen de llamadas renovables o permanentes o una cuota de ancho de banda por clave.</span><span class="sxs-lookup"><span data-stu-id="f3397-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="f3397-113">[Validar JWT](api-management-access-restriction-policies.md#ValidateJWT) : aplica la existencia y la validez de un JWT extraído de un encabezado HTTP especificado o un parámetro de consulta especificado.</span><span class="sxs-lookup"><span data-stu-id="f3397-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="f3397-114"><a name="CheckHTTPHeader"></a> Activar encabezado HTTP</span><span class="sxs-lookup"><span data-stu-id="f3397-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="f3397-115">Usa la directiva `check-header` para exigir que una solicitud tenga un encabezado HTTP especificado.</span><span class="sxs-lookup"><span data-stu-id="f3397-115">Use the `check-header` policy to enforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="f3397-116">Si lo desea, puede comprobar si el encabezado tiene un valor específico o un intervalo de valores permitidos.</span><span class="sxs-lookup"><span data-stu-id="f3397-116">You can optionally check to see if the header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="f3397-117">Si el resultado de la comprobación es negativo, la directiva finaliza el procesamiento de la solicitud y devuelve el mensaje de error y el código de estado HTTP que especifica.</span><span class="sxs-lookup"><span data-stu-id="f3397-117">If the check fails, the policy terminates request processing and returns the HTTP status code and error message specified by the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f3397-118">Declaración de la directiva</span><span class="sxs-lookup"><span data-stu-id="f3397-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="f3397-119">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="f3397-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="f3397-120">Elementos</span><span class="sxs-lookup"><span data-stu-id="f3397-120">Elements</span></span>  
  
|<span data-ttu-id="f3397-121">Nombre</span><span class="sxs-lookup"><span data-stu-id="f3397-121">Name</span></span>|<span data-ttu-id="f3397-122">Descripción</span><span class="sxs-lookup"><span data-stu-id="f3397-122">Description</span></span>|<span data-ttu-id="f3397-123">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f3397-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f3397-124">check-header</span><span class="sxs-lookup"><span data-stu-id="f3397-124">check-header</span></span>|<span data-ttu-id="f3397-125">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="f3397-125">Root element.</span></span>|<span data-ttu-id="f3397-126">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-126">Yes</span></span>|  
|<span data-ttu-id="f3397-127">value</span><span class="sxs-lookup"><span data-stu-id="f3397-127">value</span></span>|<span data-ttu-id="f3397-128">Valor del encabezado HTTP permitido.</span><span class="sxs-lookup"><span data-stu-id="f3397-128">Allowed HTTP header value.</span></span> <span data-ttu-id="f3397-129">Cuando se especifican varios elementos de valor, el resultado de la comprobación se considera positivo en caso de coincidencia con cualquiera de los valores.</span><span class="sxs-lookup"><span data-stu-id="f3397-129">When multiple value elements are specified, the check is considered a success if any one of the values is a match.</span></span>|<span data-ttu-id="f3397-130">No</span><span class="sxs-lookup"><span data-stu-id="f3397-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f3397-131">Attributes</span><span class="sxs-lookup"><span data-stu-id="f3397-131">Attributes</span></span>  
  
|<span data-ttu-id="f3397-132">Nombre</span><span class="sxs-lookup"><span data-stu-id="f3397-132">Name</span></span>|<span data-ttu-id="f3397-133">Descripción</span><span class="sxs-lookup"><span data-stu-id="f3397-133">Description</span></span>|<span data-ttu-id="f3397-134">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f3397-134">Required</span></span>|<span data-ttu-id="f3397-135">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="f3397-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f3397-136">failed-check-error-message</span><span class="sxs-lookup"><span data-stu-id="f3397-136">failed-check-error-message</span></span>|<span data-ttu-id="f3397-137">Mensaje de error que se devuelve en el cuerpo de la respuesta HTTP si el encabezado no existe o tiene un valor no válido.</span><span class="sxs-lookup"><span data-stu-id="f3397-137">Error message to return in the HTTP response body if the header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="f3397-138">Los caracteres especiales de este mensaje deben incluir los caracteres de escape correctos.</span><span class="sxs-lookup"><span data-stu-id="f3397-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="f3397-139">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-139">Yes</span></span>|<span data-ttu-id="f3397-140">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-140">N/A</span></span>|  
|<span data-ttu-id="f3397-141">failed-check-httpcode</span><span class="sxs-lookup"><span data-stu-id="f3397-141">failed-check-httpcode</span></span>|<span data-ttu-id="f3397-142">Código de estado HTTP que se devuelve si el encabezado no existe o tiene un valor no válido.</span><span class="sxs-lookup"><span data-stu-id="f3397-142">HTTP Status code to return if the header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="f3397-143">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-143">Yes</span></span>|<span data-ttu-id="f3397-144">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-144">N/A</span></span>|  
|<span data-ttu-id="f3397-145">header-name</span><span class="sxs-lookup"><span data-stu-id="f3397-145">header-name</span></span>|<span data-ttu-id="f3397-146">Nombre del encabezado HTTP que hay que comprobar.</span><span class="sxs-lookup"><span data-stu-id="f3397-146">The name of the HTTP Header to check.</span></span>|<span data-ttu-id="f3397-147">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-147">Yes</span></span>|<span data-ttu-id="f3397-148">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-148">N/A</span></span>|  
|<span data-ttu-id="f3397-149">ignore-case</span><span class="sxs-lookup"><span data-stu-id="f3397-149">ignore-case</span></span>|<span data-ttu-id="f3397-150">Puede establecerse en True o False.</span><span class="sxs-lookup"><span data-stu-id="f3397-150">Can be set to True or False.</span></span> <span data-ttu-id="f3397-151">Si se establece en True, se omite la presencia de mayúsculas/minúsculas cuando el valor del encabezado se compara con el conjunto de valores aceptables.</span><span class="sxs-lookup"><span data-stu-id="f3397-151">If set to True case is ignored when the header value is compared against the set of acceptable values.</span></span>|<span data-ttu-id="f3397-152">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-152">Yes</span></span>|<span data-ttu-id="f3397-153">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f3397-154">Uso</span><span class="sxs-lookup"><span data-stu-id="f3397-154">Usage</span></span>  
 <span data-ttu-id="f3397-155">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="f3397-155">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f3397-156">**Secciones de la directiva:** entrante y saliente</span><span class="sxs-lookup"><span data-stu-id="f3397-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="f3397-157">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="f3397-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="f3397-158"><a name="LimitCallRate"></a> Limitar la tasa de llamadas por suscripción</span><span class="sxs-lookup"><span data-stu-id="f3397-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="f3397-159">La directiva `rate-limit` evita los picos de uso de la API según suscripción limitando la tasa de llamadas a un número especificado por un período de tiempo establecido.</span><span class="sxs-lookup"><span data-stu-id="f3397-159">The `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="f3397-160">Cuando se desencadena esta directiva, el autor de la llamada recibe un código de estado de respuesta `429 Too Many Requests`.</span><span class="sxs-lookup"><span data-stu-id="f3397-160">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="f3397-161">Esta directiva se puede usar una sola vez por documento de directiva.</span><span class="sxs-lookup"><span data-stu-id="f3397-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="f3397-162">Las [expresiones de directiva](api-management-policy-expressions.md) no se pueden usar en ninguno de los atributos de esta directiva.</span><span class="sxs-lookup"><span data-stu-id="f3397-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f3397-163">Declaración de la directiva</span><span class="sxs-lookup"><span data-stu-id="f3397-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="f3397-164">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="f3397-164">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="f3397-165">Elementos</span><span class="sxs-lookup"><span data-stu-id="f3397-165">Elements</span></span>  
  
|<span data-ttu-id="f3397-166">Nombre</span><span class="sxs-lookup"><span data-stu-id="f3397-166">Name</span></span>|<span data-ttu-id="f3397-167">Descripción</span><span class="sxs-lookup"><span data-stu-id="f3397-167">Description</span></span>|<span data-ttu-id="f3397-168">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f3397-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f3397-169">set-limit</span><span class="sxs-lookup"><span data-stu-id="f3397-169">set-limit</span></span>|<span data-ttu-id="f3397-170">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="f3397-170">Root element.</span></span>|<span data-ttu-id="f3397-171">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-171">Yes</span></span>|  
|<span data-ttu-id="f3397-172">api</span><span class="sxs-lookup"><span data-stu-id="f3397-172">api</span></span>|<span data-ttu-id="f3397-173">Agregue uno o varios de estos elementos para imponer un límite de tasa de llamadas a las API del producto.</span><span class="sxs-lookup"><span data-stu-id="f3397-173">Add one  or more of these elements to impose a call rate limit on APIs within the product.</span></span> <span data-ttu-id="f3397-174">Los límites de tasa de llamadas a la API y al producto se aplican de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="f3397-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="f3397-175">No</span><span class="sxs-lookup"><span data-stu-id="f3397-175">No</span></span>|  
|<span data-ttu-id="f3397-176">operación</span><span class="sxs-lookup"><span data-stu-id="f3397-176">operation</span></span>|<span data-ttu-id="f3397-177">Agregue uno o varios de estos elementos para imponer un límite de tasa de llamadas a las operaciones de una API.</span><span class="sxs-lookup"><span data-stu-id="f3397-177">Add one  or more of these elements to impose a call rate limit on operations within an API.</span></span> <span data-ttu-id="f3397-178">Los límites de tasa de llamadas se aplican de forma independiente a la API, a la operación y al producto.</span><span class="sxs-lookup"><span data-stu-id="f3397-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="f3397-179">No</span><span class="sxs-lookup"><span data-stu-id="f3397-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f3397-180">Attributes</span><span class="sxs-lookup"><span data-stu-id="f3397-180">Attributes</span></span>  
  
|<span data-ttu-id="f3397-181">Nombre</span><span class="sxs-lookup"><span data-stu-id="f3397-181">Name</span></span>|<span data-ttu-id="f3397-182">Descripción</span><span class="sxs-lookup"><span data-stu-id="f3397-182">Description</span></span>|<span data-ttu-id="f3397-183">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f3397-183">Required</span></span>|<span data-ttu-id="f3397-184">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="f3397-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f3397-185">name</span><span class="sxs-lookup"><span data-stu-id="f3397-185">name</span></span>|<span data-ttu-id="f3397-186">Nombre de la API a la que se va a aplicar un límite de tasa.</span><span class="sxs-lookup"><span data-stu-id="f3397-186">The name of the API for which to apply the rate limit.</span></span>|<span data-ttu-id="f3397-187">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-187">Yes</span></span>|<span data-ttu-id="f3397-188">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-188">N/A</span></span>|  
|<span data-ttu-id="f3397-189">calls</span><span class="sxs-lookup"><span data-stu-id="f3397-189">calls</span></span>|<span data-ttu-id="f3397-190">Número total máximo de llamadas permitidas durante el intervalo de tiempo especificado en `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="f3397-190">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="f3397-191">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-191">Yes</span></span>|<span data-ttu-id="f3397-192">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-192">N/A</span></span>|  
|<span data-ttu-id="f3397-193">renewal-period</span><span class="sxs-lookup"><span data-stu-id="f3397-193">renewal-period</span></span>|<span data-ttu-id="f3397-194">Período de tiempo en segundos tras el cual se restablece la cuota.</span><span class="sxs-lookup"><span data-stu-id="f3397-194">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="f3397-195">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-195">Yes</span></span>|<span data-ttu-id="f3397-196">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f3397-197">Uso</span><span class="sxs-lookup"><span data-stu-id="f3397-197">Usage</span></span>  
 <span data-ttu-id="f3397-198">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="f3397-198">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f3397-199">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="f3397-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="f3397-200">**Ámbitos de la directiva:** producto</span><span class="sxs-lookup"><span data-stu-id="f3397-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="f3397-201"><a name="LimitCallRateByKey"></a> Limitar la tasa de llamadas por clave</span><span class="sxs-lookup"><span data-stu-id="f3397-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="f3397-202">La directiva `rate-limit-by-key` evita los picos de uso de la API según clave limitando la tasa de llamadas a un número especificado por un período de tiempo establecido.</span><span class="sxs-lookup"><span data-stu-id="f3397-202">The `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="f3397-203">La clave puede tener un valor de cadena arbitrario y normalmente se proporciona mediante una expresión de directiva.</span><span class="sxs-lookup"><span data-stu-id="f3397-203">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="f3397-204">Puede agregarse una condición de incremento opcional para especificar qué solicitudes se deben contar para este límite.</span><span class="sxs-lookup"><span data-stu-id="f3397-204">Optional increment condition can be added to specify which requests should be counted towards the limit.</span></span> <span data-ttu-id="f3397-205">Cuando se desencadena esta directiva, el autor de la llamada recibe un código de estado de respuesta `429 Too Many Requests`.</span><span class="sxs-lookup"><span data-stu-id="f3397-205">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="f3397-206">Para obtener más información y ver ejemplos de esta directiva, consulte [Limitación avanzada de solicitudes con Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="f3397-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="f3397-207">Esta directiva se puede usar una sola vez por documento de directiva.</span><span class="sxs-lookup"><span data-stu-id="f3397-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f3397-208">Declaración de la directiva</span><span class="sxs-lookup"><span data-stu-id="f3397-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="f3397-209">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="f3397-209">Example</span></span>  
 <span data-ttu-id="f3397-210">En el ejemplo siguiente, la clave del límite de velocidad se establece según la dirección IP del autor de la llamada.</span><span class="sxs-lookup"><span data-stu-id="f3397-210">In the following example, the rate limit is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="f3397-211">Elementos</span><span class="sxs-lookup"><span data-stu-id="f3397-211">Elements</span></span>  
  
|<span data-ttu-id="f3397-212">Nombre</span><span class="sxs-lookup"><span data-stu-id="f3397-212">Name</span></span>|<span data-ttu-id="f3397-213">Descripción</span><span class="sxs-lookup"><span data-stu-id="f3397-213">Description</span></span>|<span data-ttu-id="f3397-214">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f3397-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f3397-215">set-limit</span><span class="sxs-lookup"><span data-stu-id="f3397-215">set-limit</span></span>|<span data-ttu-id="f3397-216">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="f3397-216">Root element.</span></span>|<span data-ttu-id="f3397-217">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f3397-218">Atributos</span><span class="sxs-lookup"><span data-stu-id="f3397-218">Attributes</span></span>  
  
|<span data-ttu-id="f3397-219">Nombre</span><span class="sxs-lookup"><span data-stu-id="f3397-219">Name</span></span>|<span data-ttu-id="f3397-220">Descripción</span><span class="sxs-lookup"><span data-stu-id="f3397-220">Description</span></span>|<span data-ttu-id="f3397-221">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f3397-221">Required</span></span>|<span data-ttu-id="f3397-222">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="f3397-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f3397-223">calls</span><span class="sxs-lookup"><span data-stu-id="f3397-223">calls</span></span>|<span data-ttu-id="f3397-224">Número total máximo de llamadas permitidas durante el intervalo de tiempo especificado en `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="f3397-224">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="f3397-225">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-225">Yes</span></span>|<span data-ttu-id="f3397-226">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-226">N/A</span></span>|  
|<span data-ttu-id="f3397-227">counter-key</span><span class="sxs-lookup"><span data-stu-id="f3397-227">counter-key</span></span>|<span data-ttu-id="f3397-228">Clave que se usa para la directiva de límite de tasa.</span><span class="sxs-lookup"><span data-stu-id="f3397-228">The key to use for the rate limit policy.</span></span>|<span data-ttu-id="f3397-229">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-229">Yes</span></span>|<span data-ttu-id="f3397-230">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-230">N/A</span></span>|  
|<span data-ttu-id="f3397-231">increment-condition</span><span class="sxs-lookup"><span data-stu-id="f3397-231">increment-condition</span></span>|<span data-ttu-id="f3397-232">Expresión booleana que especifica si la solicitud se debe contar para la cuota (`true`).</span><span class="sxs-lookup"><span data-stu-id="f3397-232">The boolean expression specifying if the request should be counted towards the quota (`true`).</span></span>|<span data-ttu-id="f3397-233">No</span><span class="sxs-lookup"><span data-stu-id="f3397-233">No</span></span>|<span data-ttu-id="f3397-234">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-234">N/A</span></span>|  
|<span data-ttu-id="f3397-235">renewal-period</span><span class="sxs-lookup"><span data-stu-id="f3397-235">renewal-period</span></span>|<span data-ttu-id="f3397-236">Período de tiempo en segundos tras el cual se restablece la cuota.</span><span class="sxs-lookup"><span data-stu-id="f3397-236">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="f3397-237">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-237">Yes</span></span>|<span data-ttu-id="f3397-238">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f3397-239">Uso</span><span class="sxs-lookup"><span data-stu-id="f3397-239">Usage</span></span>  
 <span data-ttu-id="f3397-240">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="f3397-240">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f3397-241">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="f3397-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="f3397-242">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="f3397-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="f3397-243"><a name="RestrictCallerIPs"></a> Restringir IP de autor de llamada</span><span class="sxs-lookup"><span data-stu-id="f3397-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="f3397-244">La directiva `ip-filter` filtra (permite/deniega) llamadas de direcciones IP específicas o de intervalos de direcciones.</span><span class="sxs-lookup"><span data-stu-id="f3397-244">The `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f3397-245">Declaración de la directiva</span><span class="sxs-lookup"><span data-stu-id="f3397-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="f3397-246">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="f3397-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="f3397-247">Elementos</span><span class="sxs-lookup"><span data-stu-id="f3397-247">Elements</span></span>  
  
|<span data-ttu-id="f3397-248">Nombre</span><span class="sxs-lookup"><span data-stu-id="f3397-248">Name</span></span>|<span data-ttu-id="f3397-249">Descripción</span><span class="sxs-lookup"><span data-stu-id="f3397-249">Description</span></span>|<span data-ttu-id="f3397-250">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f3397-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f3397-251">ip-filter</span><span class="sxs-lookup"><span data-stu-id="f3397-251">ip-filter</span></span>|<span data-ttu-id="f3397-252">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="f3397-252">Root element.</span></span>|<span data-ttu-id="f3397-253">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-253">Yes</span></span>|  
|<span data-ttu-id="f3397-254">address</span><span class="sxs-lookup"><span data-stu-id="f3397-254">address</span></span>|<span data-ttu-id="f3397-255">Especifica la dirección IP única por la que filtrar.</span><span class="sxs-lookup"><span data-stu-id="f3397-255">Specifies a single IP address on which to filter.</span></span>|<span data-ttu-id="f3397-256">Es necesario al menos un elemento `address` o `address-range`.</span><span class="sxs-lookup"><span data-stu-id="f3397-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="f3397-257">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="f3397-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="f3397-258">Especifica un intervalo de direcciones IP por el que filtrar.</span><span class="sxs-lookup"><span data-stu-id="f3397-258">Specifies a range of IP address on which to filter.</span></span>|<span data-ttu-id="f3397-259">Es necesario al menos un elemento `address` o `address-range`.</span><span class="sxs-lookup"><span data-stu-id="f3397-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f3397-260">Attributes</span><span class="sxs-lookup"><span data-stu-id="f3397-260">Attributes</span></span>  
  
|<span data-ttu-id="f3397-261">Nombre</span><span class="sxs-lookup"><span data-stu-id="f3397-261">Name</span></span>|<span data-ttu-id="f3397-262">Descripción</span><span class="sxs-lookup"><span data-stu-id="f3397-262">Description</span></span>|<span data-ttu-id="f3397-263">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f3397-263">Required</span></span>|<span data-ttu-id="f3397-264">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="f3397-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f3397-265">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="f3397-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="f3397-266">Un intervalo de direcciones IP a las que permitir o denegar el acceso.</span><span class="sxs-lookup"><span data-stu-id="f3397-266">A range of IP addresses to allow or deny access for.</span></span>|<span data-ttu-id="f3397-267">Obligatorio cuando se utiliza el elemento `address-range`.</span><span class="sxs-lookup"><span data-stu-id="f3397-267">Required when the `address-range` element is used.</span></span>|<span data-ttu-id="f3397-268">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-268">N/A</span></span>|  
|<span data-ttu-id="f3397-269">ip-filter action="allow &#124; forbid"</span><span class="sxs-lookup"><span data-stu-id="f3397-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="f3397-270">Especifica si se deben permitir o no las llamadas para los intervalos y direcciones IP especificados.</span><span class="sxs-lookup"><span data-stu-id="f3397-270">Specifies whether calls should be allowed or not for the specified IP addresses and ranges.</span></span>|<span data-ttu-id="f3397-271">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-271">Yes</span></span>|<span data-ttu-id="f3397-272">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f3397-273">Uso</span><span class="sxs-lookup"><span data-stu-id="f3397-273">Usage</span></span>  
 <span data-ttu-id="f3397-274">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="f3397-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f3397-275">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="f3397-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="f3397-276">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="f3397-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="f3397-277"><a name="SetUsageQuota"></a> Establecer cuota de uso por suscripción</span><span class="sxs-lookup"><span data-stu-id="f3397-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="f3397-278">La directiva `quota` aplica un volumen de llamadas o una cuota de ancho de banda renovables o permanentes por suscripción.</span><span class="sxs-lookup"><span data-stu-id="f3397-278">The `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="f3397-279">Esta directiva se puede usar una sola vez por documento de directiva.</span><span class="sxs-lookup"><span data-stu-id="f3397-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="f3397-280">Las [expresiones de directiva](api-management-policy-expressions.md) no se pueden usar en ninguno de los atributos de esta directiva.</span><span class="sxs-lookup"><span data-stu-id="f3397-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f3397-281">Declaración de la directiva</span><span class="sxs-lookup"><span data-stu-id="f3397-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="f3397-282">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="f3397-282">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="f3397-283">Elementos</span><span class="sxs-lookup"><span data-stu-id="f3397-283">Elements</span></span>  
  
|<span data-ttu-id="f3397-284">Nombre</span><span class="sxs-lookup"><span data-stu-id="f3397-284">Name</span></span>|<span data-ttu-id="f3397-285">Descripción</span><span class="sxs-lookup"><span data-stu-id="f3397-285">Description</span></span>|<span data-ttu-id="f3397-286">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f3397-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f3397-287">quota</span><span class="sxs-lookup"><span data-stu-id="f3397-287">quota</span></span>|<span data-ttu-id="f3397-288">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="f3397-288">Root element.</span></span>|<span data-ttu-id="f3397-289">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-289">Yes</span></span>|  
|<span data-ttu-id="f3397-290">api</span><span class="sxs-lookup"><span data-stu-id="f3397-290">api</span></span>|<span data-ttu-id="f3397-291">Agregue uno o varios de estos elementos para imponer una cuota a las API del producto.</span><span class="sxs-lookup"><span data-stu-id="f3397-291">Add one  or more of these elements to impose a quota on APIs within the product.</span></span> <span data-ttu-id="f3397-292">Las cuotas de API y de producto se aplican de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="f3397-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="f3397-293">No</span><span class="sxs-lookup"><span data-stu-id="f3397-293">No</span></span>|  
|<span data-ttu-id="f3397-294">operación</span><span class="sxs-lookup"><span data-stu-id="f3397-294">operation</span></span>|<span data-ttu-id="f3397-295">Agregue uno o varios de estos elementos para imponer una cuota a las operaciones de una API.</span><span class="sxs-lookup"><span data-stu-id="f3397-295">Add one  or more of these elements to impose a quota on operations within an API.</span></span> <span data-ttu-id="f3397-296">Las cuotas de API, operación y producto se aplican de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="f3397-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="f3397-297">No</span><span class="sxs-lookup"><span data-stu-id="f3397-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f3397-298">Attributes</span><span class="sxs-lookup"><span data-stu-id="f3397-298">Attributes</span></span>  
  
|<span data-ttu-id="f3397-299">Nombre</span><span class="sxs-lookup"><span data-stu-id="f3397-299">Name</span></span>|<span data-ttu-id="f3397-300">Descripción</span><span class="sxs-lookup"><span data-stu-id="f3397-300">Description</span></span>|<span data-ttu-id="f3397-301">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f3397-301">Required</span></span>|<span data-ttu-id="f3397-302">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="f3397-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f3397-303">name</span><span class="sxs-lookup"><span data-stu-id="f3397-303">name</span></span>|<span data-ttu-id="f3397-304">Nombre de la API u operación a la que se aplica la cuota.</span><span class="sxs-lookup"><span data-stu-id="f3397-304">The name of the API or operation for which the quota applies.</span></span>|<span data-ttu-id="f3397-305">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-305">Yes</span></span>|<span data-ttu-id="f3397-306">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-306">N/A</span></span>|  
|<span data-ttu-id="f3397-307">bandwidth</span><span class="sxs-lookup"><span data-stu-id="f3397-307">bandwidth</span></span>|<span data-ttu-id="f3397-308">Número total máximo de kilobytes permitidos durante el intervalo de tiempo especificado en `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="f3397-308">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="f3397-309">Debe especificarse `calls`, `bandwidth` o ambos.</span><span class="sxs-lookup"><span data-stu-id="f3397-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="f3397-310">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-310">N/A</span></span>|  
|<span data-ttu-id="f3397-311">calls</span><span class="sxs-lookup"><span data-stu-id="f3397-311">calls</span></span>|<span data-ttu-id="f3397-312">Número total máximo de llamadas permitidas durante el intervalo de tiempo especificado en `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="f3397-312">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="f3397-313">Debe especificarse `calls`, `bandwidth` o ambos.</span><span class="sxs-lookup"><span data-stu-id="f3397-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="f3397-314">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-314">N/A</span></span>|  
|<span data-ttu-id="f3397-315">renewal-period</span><span class="sxs-lookup"><span data-stu-id="f3397-315">renewal-period</span></span>|<span data-ttu-id="f3397-316">Período de tiempo en segundos tras el cual se restablece la cuota.</span><span class="sxs-lookup"><span data-stu-id="f3397-316">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="f3397-317">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-317">Yes</span></span>|<span data-ttu-id="f3397-318">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f3397-319">Uso</span><span class="sxs-lookup"><span data-stu-id="f3397-319">Usage</span></span>  
 <span data-ttu-id="f3397-320">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="f3397-320">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f3397-321">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="f3397-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="f3397-322">**Ámbitos de la directiva:** producto</span><span class="sxs-lookup"><span data-stu-id="f3397-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="f3397-323"><a name="SetUsageQuotaByKey"></a>Establecer cuota de uso por clave</span><span class="sxs-lookup"><span data-stu-id="f3397-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="f3397-324">La directiva `quota-by-key` aplica un volumen de llamadas o una cuota de ancho de banda por clave renovables o permanentes.</span><span class="sxs-lookup"><span data-stu-id="f3397-324">The `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="f3397-325">La clave puede tener un valor de cadena arbitrario y normalmente se proporciona mediante una expresión de directiva.</span><span class="sxs-lookup"><span data-stu-id="f3397-325">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="f3397-326">Puede agregarse una condición de incremento opcional para especificar qué solicitudes se cuentan para esta cuota.</span><span class="sxs-lookup"><span data-stu-id="f3397-326">Optional increment condition can be added to specify which requests should be counted towards the quota.</span></span>  
  
 <span data-ttu-id="f3397-327">Para obtener más información y ver ejemplos de esta directiva, consulte [Limitación avanzada de solicitudes con Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="f3397-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="f3397-328">Esta directiva se puede usar una sola vez por documento de directiva.</span><span class="sxs-lookup"><span data-stu-id="f3397-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="f3397-329">Las [expresiones de directiva](api-management-policy-expressions.md) no se pueden usar en ninguno de los atributos de esta directiva.</span><span class="sxs-lookup"><span data-stu-id="f3397-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f3397-330">Declaración de la directiva</span><span class="sxs-lookup"><span data-stu-id="f3397-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="f3397-331">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="f3397-331">Example</span></span>  
 <span data-ttu-id="f3397-332">En el ejemplo siguiente, la clave de la cuota se establece según la dirección IP del autor de la llamada.</span><span class="sxs-lookup"><span data-stu-id="f3397-332">In the following example, the quota is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="f3397-333">Elementos</span><span class="sxs-lookup"><span data-stu-id="f3397-333">Elements</span></span>  
  
|<span data-ttu-id="f3397-334">Nombre</span><span class="sxs-lookup"><span data-stu-id="f3397-334">Name</span></span>|<span data-ttu-id="f3397-335">Descripción</span><span class="sxs-lookup"><span data-stu-id="f3397-335">Description</span></span>|<span data-ttu-id="f3397-336">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f3397-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f3397-337">quota</span><span class="sxs-lookup"><span data-stu-id="f3397-337">quota</span></span>|<span data-ttu-id="f3397-338">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="f3397-338">Root element.</span></span>|<span data-ttu-id="f3397-339">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f3397-340">Atributos</span><span class="sxs-lookup"><span data-stu-id="f3397-340">Attributes</span></span>  
  
|<span data-ttu-id="f3397-341">Nombre</span><span class="sxs-lookup"><span data-stu-id="f3397-341">Name</span></span>|<span data-ttu-id="f3397-342">Descripción</span><span class="sxs-lookup"><span data-stu-id="f3397-342">Description</span></span>|<span data-ttu-id="f3397-343">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f3397-343">Required</span></span>|<span data-ttu-id="f3397-344">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="f3397-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f3397-345">bandwidth</span><span class="sxs-lookup"><span data-stu-id="f3397-345">bandwidth</span></span>|<span data-ttu-id="f3397-346">Número total máximo de kilobytes permitidos durante el intervalo de tiempo especificado en `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="f3397-346">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="f3397-347">Debe especificarse `calls`, `bandwidth` o ambos.</span><span class="sxs-lookup"><span data-stu-id="f3397-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="f3397-348">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-348">N/A</span></span>|  
|<span data-ttu-id="f3397-349">calls</span><span class="sxs-lookup"><span data-stu-id="f3397-349">calls</span></span>|<span data-ttu-id="f3397-350">Número total máximo de llamadas permitidas durante el intervalo de tiempo especificado en `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="f3397-350">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="f3397-351">Debe especificarse `calls`, `bandwidth` o ambos.</span><span class="sxs-lookup"><span data-stu-id="f3397-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="f3397-352">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-352">N/A</span></span>|  
|<span data-ttu-id="f3397-353">counter-key</span><span class="sxs-lookup"><span data-stu-id="f3397-353">counter-key</span></span>|<span data-ttu-id="f3397-354">Clave que se usa para la directiva de cuota.</span><span class="sxs-lookup"><span data-stu-id="f3397-354">The key to use for the quota policy.</span></span>|<span data-ttu-id="f3397-355">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-355">Yes</span></span>|<span data-ttu-id="f3397-356">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-356">N/A</span></span>|  
|<span data-ttu-id="f3397-357">increment-condition</span><span class="sxs-lookup"><span data-stu-id="f3397-357">increment-condition</span></span>|<span data-ttu-id="f3397-358">Expresión booleana que especifica si la solicitud se debe contar para la cuota (`true`).</span><span class="sxs-lookup"><span data-stu-id="f3397-358">The boolean expression specifying if the request should be counted towards the quota (`true`)</span></span>|<span data-ttu-id="f3397-359">No</span><span class="sxs-lookup"><span data-stu-id="f3397-359">No</span></span>|<span data-ttu-id="f3397-360">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-360">N/A</span></span>|  
|<span data-ttu-id="f3397-361">renewal-period</span><span class="sxs-lookup"><span data-stu-id="f3397-361">renewal-period</span></span>|<span data-ttu-id="f3397-362">Período de tiempo en segundos tras el cual se restablece la cuota.</span><span class="sxs-lookup"><span data-stu-id="f3397-362">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="f3397-363">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-363">Yes</span></span>|<span data-ttu-id="f3397-364">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f3397-365">Uso</span><span class="sxs-lookup"><span data-stu-id="f3397-365">Usage</span></span>  
 <span data-ttu-id="f3397-366">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="f3397-366">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f3397-367">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="f3397-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="f3397-368">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="f3397-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="f3397-369"><a name="ValidateJWT"></a> Validación de JWT</span><span class="sxs-lookup"><span data-stu-id="f3397-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="f3397-370">La directiva `validate-jwt` aplica la existencia y la validez de un JWT extraído de un encabezado HTTP o un parámetro de consulta especificados.</span><span class="sxs-lookup"><span data-stu-id="f3397-370">The `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="f3397-371">La directiva `validate-jwt` requiere que la notificación registrada `exp` se incluya en el token de JWT, a menos que se especifique el atributo `require-expiration-time` y se establezca en `false`.</span><span class="sxs-lookup"><span data-stu-id="f3397-371">The `validate-jwt` policy requires that the `exp` registered claim is inlcuded in the JWT token, unless `require-expiration-time` attribute is specified and set to `false`.</span></span>  
> <span data-ttu-id="f3397-372">La directiva `validate-jwt` es compatible con los algoritmos de firma HS256 y RS256.</span><span class="sxs-lookup"><span data-stu-id="f3397-372">The `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="f3397-373">En el caso de HS256, la clave debe proporcionarse en línea dentro de la directiva con el formato de codificación Base64.</span><span class="sxs-lookup"><span data-stu-id="f3397-373">For HS256 the key must be provided inline within the policy in the base64 encoded form.</span></span> <span data-ttu-id="f3397-374">En el caso de RS256, la clave debe proporcionarse a través de un punto de conexión de configuración OpenID.</span><span class="sxs-lookup"><span data-stu-id="f3397-374">For RS256 the key has to be provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f3397-375">Declaración de la directiva</span><span class="sxs-lookup"><span data-stu-id="f3397-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing the token (use query-parameter-name attribute if the token is passed in the URL)"   
    failed-validation-httpcode="http status code to return on failure"   
    failed-validation-error-message="error message to return on failure"   
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
    <claim name="name of the claim as it appears in the token" match="all|any">  
      <value>claim value as it is expected to appear in the token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of the configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="f3397-376">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="f3397-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="f3397-377">Validación de tokens de Azure Mobile Services</span><span class="sxs-lookup"><span data-stu-id="f3397-377">Azure Mobile Services token validation</span></span>  
  
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
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="f3397-378">Validación de tokens de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3397-378">Azure Active Directory token validation</span></span>  
  
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

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="f3397-379">Validación de tokens de Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="f3397-379">Azure Active Directory B2C token validation</span></span>  
  
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
  
#### <a name="authorize-access-to-operations-based-on-token-claims"></a><span data-ttu-id="f3397-380">Autorización de acceso a las operaciones según las notificaciones de tokens</span><span class="sxs-lookup"><span data-stu-id="f3397-380">Authorize access to operations based on token claims</span></span>  
 <span data-ttu-id="f3397-381">Este ejemplo muestra cómo utilizar la directiva de [validación de JWT](api-management-access-restriction-policies.md#ValidateJWT) para preautorizar el acceso a operaciones según notificaciones de token.</span><span class="sxs-lookup"><span data-stu-id="f3397-381">This example shows how to use the [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy to pre-authorize access to operations based on token claims.</span></span> <span data-ttu-id="f3397-382">Para ver una demostración de la configuración y el uso de esta directiva, vea [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Episodio 177 de Cloud Cover: más características API Management con Vlad Vinogradsky) y avance al minuto 13:50.</span><span class="sxs-lookup"><span data-stu-id="f3397-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="f3397-383">Avance rápidamente hasta 15:00 para ver las directivas configuradas en el editor de directivas y hasta 18:50 para ver una demostración de llamada de una operación desde el portal para desarrolladores tanto con y sin el token de autorización necesario.</span><span class="sxs-lookup"><span data-stu-id="f3397-383">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>  
  
```xml  
<!-- Copy the following snippet into the inbound section at the api (or higher) level to pre-authorize access to operations based on token claims -->  
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
  
### <a name="elements"></a><span data-ttu-id="f3397-384">Elementos</span><span class="sxs-lookup"><span data-stu-id="f3397-384">Elements</span></span>  
  
|<span data-ttu-id="f3397-385">Elemento</span><span class="sxs-lookup"><span data-stu-id="f3397-385">Element</span></span>|<span data-ttu-id="f3397-386">Descripción</span><span class="sxs-lookup"><span data-stu-id="f3397-386">Description</span></span>|<span data-ttu-id="f3397-387">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f3397-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="f3397-388">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="f3397-388">validate-jwt</span></span>|<span data-ttu-id="f3397-389">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="f3397-389">Root element.</span></span>|<span data-ttu-id="f3397-390">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-390">Yes</span></span>|  
|<span data-ttu-id="f3397-391">audiences</span><span class="sxs-lookup"><span data-stu-id="f3397-391">audiences</span></span>|<span data-ttu-id="f3397-392">Contiene una lista de notificaciones de audiencia aceptables que pueden estar presentes en el token.</span><span class="sxs-lookup"><span data-stu-id="f3397-392">Contains a list of acceptable audience claims that can be present on the token.</span></span> <span data-ttu-id="f3397-393">Si existen varios valores de audiencia, se prueban los valores uno a uno hasta que se agoten todos (en cuyo caso no se superará la validación) o hasta que se obtenga un resultado positivo con alguno.</span><span class="sxs-lookup"><span data-stu-id="f3397-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="f3397-394">Debe especificarse al menos una audiencia.</span><span class="sxs-lookup"><span data-stu-id="f3397-394">At least one audience must be specified.</span></span>|<span data-ttu-id="f3397-395">No</span><span class="sxs-lookup"><span data-stu-id="f3397-395">No</span></span>|  
|<span data-ttu-id="f3397-396">issuer-signing-keys</span><span class="sxs-lookup"><span data-stu-id="f3397-396">issuer-signing-keys</span></span>|<span data-ttu-id="f3397-397">Lista de las claves de seguridad con codificación Base64 que se utilizan para validar los tokens firmados.</span><span class="sxs-lookup"><span data-stu-id="f3397-397">A list of Base64-encoded security keys used to validate signed tokens.</span></span> <span data-ttu-id="f3397-398">Si existen varias claves de seguridad, se prueban las claves una a una hasta que se agoten todas (en cuyo caso no se superará la validación) o hasta que una sea correcta (lo que es útil para la sustitución de tokens).</span><span class="sxs-lookup"><span data-stu-id="f3397-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="f3397-399">Los elementos de clave tienen un atributo `id` opcional que se utiliza para compararlo con la notificación `kid`.</span><span class="sxs-lookup"><span data-stu-id="f3397-399">Key elements have an optional `id` attribute used to match against `kid` claim.</span></span>|<span data-ttu-id="f3397-400">No</span><span class="sxs-lookup"><span data-stu-id="f3397-400">No</span></span>|  
|<span data-ttu-id="f3397-401">issuers</span><span class="sxs-lookup"><span data-stu-id="f3397-401">issuers</span></span>|<span data-ttu-id="f3397-402">Lista de entidades de seguridad aceptables que emitieron el token.</span><span class="sxs-lookup"><span data-stu-id="f3397-402">A list of acceptable principals that issued the token.</span></span> <span data-ttu-id="f3397-403">Si existen varios valores de emisor, se prueban los valores uno a uno hasta que se agoten todos (en cuyo caso no se superará la validación) o hasta que se obtenga un resultado positivo con alguno.</span><span class="sxs-lookup"><span data-stu-id="f3397-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="f3397-404">No</span><span class="sxs-lookup"><span data-stu-id="f3397-404">No</span></span>|  
|<span data-ttu-id="f3397-405">openid-config</span><span class="sxs-lookup"><span data-stu-id="f3397-405">openid-config</span></span>|<span data-ttu-id="f3397-406">Elemento que se usa para especificar un punto de conexión de configuración OpenID compatible desde el que se puedan obtener las claves y el emisor de la firma.</span><span class="sxs-lookup"><span data-stu-id="f3397-406">The element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="f3397-407">No</span><span class="sxs-lookup"><span data-stu-id="f3397-407">No</span></span>|  
|<span data-ttu-id="f3397-408">required-claims</span><span class="sxs-lookup"><span data-stu-id="f3397-408">required-claims</span></span>|<span data-ttu-id="f3397-409">Contiene una lista de las notificaciones que se espera que estén presentes en el token para que se considere válido.</span><span class="sxs-lookup"><span data-stu-id="f3397-409">Contains a list of claims expected to be present on the token for it to be considered valid.</span></span> <span data-ttu-id="f3397-410">Cuando el atributo `match` está establecido en `all`, todos los valores de notificación de la directiva deben estar presentes en el token para que la validación se efectúe correctamente.</span><span class="sxs-lookup"><span data-stu-id="f3397-410">When the `match` attribute is set to `all` every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="f3397-411">Cuando el atributo `match` está establecido en `any`, debe haber al menos una notificación en el token para que la validación se efectúe correctamente.</span><span class="sxs-lookup"><span data-stu-id="f3397-411">When the `match` attribute is set to `any` at least one claim must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="f3397-412">No</span><span class="sxs-lookup"><span data-stu-id="f3397-412">No</span></span>|  
|<span data-ttu-id="f3397-413">zumo-master-key</span><span class="sxs-lookup"><span data-stu-id="f3397-413">zumo-master-key</span></span>|<span data-ttu-id="f3397-414">Clave maestra para los tokens que emite Azure Mobile Services.</span><span class="sxs-lookup"><span data-stu-id="f3397-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="f3397-415">No</span><span class="sxs-lookup"><span data-stu-id="f3397-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f3397-416">Attributes</span><span class="sxs-lookup"><span data-stu-id="f3397-416">Attributes</span></span>  
  
|<span data-ttu-id="f3397-417">Nombre</span><span class="sxs-lookup"><span data-stu-id="f3397-417">Name</span></span>|<span data-ttu-id="f3397-418">Descripción</span><span class="sxs-lookup"><span data-stu-id="f3397-418">Description</span></span>|<span data-ttu-id="f3397-419">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f3397-419">Required</span></span>|<span data-ttu-id="f3397-420">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="f3397-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f3397-421">clock-skew</span><span class="sxs-lookup"><span data-stu-id="f3397-421">clock-skew</span></span>|<span data-ttu-id="f3397-422">Intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="f3397-422">Timespan.</span></span> <span data-ttu-id="f3397-423">Proporciona un pequeño margen de tiempo en caso de que la notificación de expiración del token esté presente en este último y sea posterior a la fecha/hora actuales.</span><span class="sxs-lookup"><span data-stu-id="f3397-423">Provides some small leeway in case the token's expiration claim is present in the token and is past the current date / time.</span></span>|<span data-ttu-id="f3397-424">No</span><span class="sxs-lookup"><span data-stu-id="f3397-424">No</span></span>|<span data-ttu-id="f3397-425">0 segundos</span><span class="sxs-lookup"><span data-stu-id="f3397-425">0 seconds</span></span>|  
|<span data-ttu-id="f3397-426">failed-validation-error-message</span><span class="sxs-lookup"><span data-stu-id="f3397-426">failed-validation-error-message</span></span>|<span data-ttu-id="f3397-427">Mensaje de error que se devuelve en el cuerpo de respuesta HTTP si el elemento JWT no pasa la validación.</span><span class="sxs-lookup"><span data-stu-id="f3397-427">Error message to return in the HTTP response body if the JWT does not pass validation.</span></span> <span data-ttu-id="f3397-428">Los caracteres especiales de este mensaje deben incluir los caracteres de escape correctos.</span><span class="sxs-lookup"><span data-stu-id="f3397-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="f3397-429">No</span><span class="sxs-lookup"><span data-stu-id="f3397-429">No</span></span>|<span data-ttu-id="f3397-430">El mensaje de error predeterminado depende del problema de validación, por ejemplo, la notificación de la ausencia del elemento JWT.</span><span class="sxs-lookup"><span data-stu-id="f3397-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="f3397-431">failed-validation-httpcode</span><span class="sxs-lookup"><span data-stu-id="f3397-431">failed-validation-httpcode</span></span>|<span data-ttu-id="f3397-432">Código de estado HTTP que se devuelve si el elemento JWT no pasa la validación.</span><span class="sxs-lookup"><span data-stu-id="f3397-432">HTTP Status code to return if the JWT doesn't pass validation.</span></span>|<span data-ttu-id="f3397-433">No</span><span class="sxs-lookup"><span data-stu-id="f3397-433">No</span></span>|<span data-ttu-id="f3397-434">401</span><span class="sxs-lookup"><span data-stu-id="f3397-434">401</span></span>|  
|<span data-ttu-id="f3397-435">header-name</span><span class="sxs-lookup"><span data-stu-id="f3397-435">header-name</span></span>|<span data-ttu-id="f3397-436">El nombre del encabezado HTTP que contiene el token.</span><span class="sxs-lookup"><span data-stu-id="f3397-436">The name of the HTTP header holding the token.</span></span>|<span data-ttu-id="f3397-437">Se debe especificar `header-name` o `query-paremeter-name`, pero no ambos.</span><span class="sxs-lookup"><span data-stu-id="f3397-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="f3397-438">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-438">N/A</span></span>|  
|<span data-ttu-id="f3397-439">id</span><span class="sxs-lookup"><span data-stu-id="f3397-439">id</span></span>|<span data-ttu-id="f3397-440">El atributo `id` del elemento `key` le permite especificar la cadena que se comparará con la notificación `kid` del token (si existe) para averiguar qué clave debe usarse para validar la firma.</span><span class="sxs-lookup"><span data-stu-id="f3397-440">The `id` attribute on the `key` element allows you to specify the string that will be matched against `kid` claim in the token (if present) to find out the appropriate key to use for signature validation.</span></span>|<span data-ttu-id="f3397-441">No</span><span class="sxs-lookup"><span data-stu-id="f3397-441">No</span></span>|<span data-ttu-id="f3397-442">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-442">N/A</span></span>|  
|<span data-ttu-id="f3397-443">match</span><span class="sxs-lookup"><span data-stu-id="f3397-443">match</span></span>|<span data-ttu-id="f3397-444">El atributo `match` del elemento `claim` especifica si todos los valores de notificación de la directiva deben estar presentes en el token para que la validación se efectúe correctamente.</span><span class="sxs-lookup"><span data-stu-id="f3397-444">The `match` attribute on the `claim` element specifies whether every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="f3397-445">Los valores posibles son:</span><span class="sxs-lookup"><span data-stu-id="f3397-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="f3397-446">-                          `all`: todos los valores de notificación de la directiva deben estar presentes en el token para que la validación se efectúe correctamente.</span><span class="sxs-lookup"><span data-stu-id="f3397-446">-                          `all` - every claim value in the policy must be present in the token for validation to succeed.</span></span><br /><br /> <span data-ttu-id="f3397-447">-                          `any`: al menos un valor de notificación debe estar presente en el token para que la validación se efectúe correctamente.</span><span class="sxs-lookup"><span data-stu-id="f3397-447">-                          `any` - at least one claim value must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="f3397-448">No</span><span class="sxs-lookup"><span data-stu-id="f3397-448">No</span></span>|<span data-ttu-id="f3397-449">todas</span><span class="sxs-lookup"><span data-stu-id="f3397-449">all</span></span>|  
|<span data-ttu-id="f3397-450">query-paremeter-name</span><span class="sxs-lookup"><span data-stu-id="f3397-450">query-paremeter-name</span></span>|<span data-ttu-id="f3397-451">Nombre del parámetro de consulta que contiene el token.</span><span class="sxs-lookup"><span data-stu-id="f3397-451">The name of the the query parameter holding the token.</span></span>|<span data-ttu-id="f3397-452">Se debe especificar `header-name` o `query-paremeter-name`, pero no ambos.</span><span class="sxs-lookup"><span data-stu-id="f3397-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="f3397-453">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-453">N/A</span></span>|  
|<span data-ttu-id="f3397-454">require-expiration-time</span><span class="sxs-lookup"><span data-stu-id="f3397-454">require-expiration-time</span></span>|<span data-ttu-id="f3397-455">Booleano.</span><span class="sxs-lookup"><span data-stu-id="f3397-455">Boolean.</span></span> <span data-ttu-id="f3397-456">Especifica si es necesaria una notificación de expiración en el token.</span><span class="sxs-lookup"><span data-stu-id="f3397-456">Specifies whether an expiration claim is required in the token.</span></span>|<span data-ttu-id="f3397-457">No</span><span class="sxs-lookup"><span data-stu-id="f3397-457">No</span></span>|<span data-ttu-id="f3397-458">true</span><span class="sxs-lookup"><span data-stu-id="f3397-458">true</span></span>|
|<span data-ttu-id="f3397-459">require-scheme</span><span class="sxs-lookup"><span data-stu-id="f3397-459">require-scheme</span></span>|<span data-ttu-id="f3397-460">El nombre del token de esquema; por ejemplo, "Bearer".</span><span class="sxs-lookup"><span data-stu-id="f3397-460">The name of the token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="f3397-461">Cuando se establece este atributo, la directiva se asegurará de que ese esquema especificado esté presente en el valor del encabezado de la autorización.</span><span class="sxs-lookup"><span data-stu-id="f3397-461">When this attribute is set, the policy will ensure that specified scheme is present in the Authorization header value.</span></span>|<span data-ttu-id="f3397-462">No</span><span class="sxs-lookup"><span data-stu-id="f3397-462">No</span></span>|<span data-ttu-id="f3397-463">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-463">N/A</span></span>|
|<span data-ttu-id="f3397-464">require-signed-tokens</span><span class="sxs-lookup"><span data-stu-id="f3397-464">require-signed-tokens</span></span>|<span data-ttu-id="f3397-465">Booleano.</span><span class="sxs-lookup"><span data-stu-id="f3397-465">Boolean.</span></span> <span data-ttu-id="f3397-466">Especifica si un token debe estar firmado.</span><span class="sxs-lookup"><span data-stu-id="f3397-466">Specifies whether a token is required to be signed.</span></span>|<span data-ttu-id="f3397-467">No</span><span class="sxs-lookup"><span data-stu-id="f3397-467">No</span></span>|<span data-ttu-id="f3397-468">true</span><span class="sxs-lookup"><span data-stu-id="f3397-468">true</span></span>|  
|<span data-ttu-id="f3397-469">url</span><span class="sxs-lookup"><span data-stu-id="f3397-469">url</span></span>|<span data-ttu-id="f3397-470">Dirección URL de punto de conexión de configuración de OpenID desde donde se pueden obtener los metadatos de configuración de OpenID.</span><span class="sxs-lookup"><span data-stu-id="f3397-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="f3397-471">En Azure Active Directory, utilice la dirección URL `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` y sustituya tenant-name por el nombre del inquilino de directorio, por ejemplo, `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="f3397-471">For Azure Active Directory use the following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="f3397-472">Sí</span><span class="sxs-lookup"><span data-stu-id="f3397-472">Yes</span></span>|<span data-ttu-id="f3397-473">N/D</span><span class="sxs-lookup"><span data-stu-id="f3397-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f3397-474">Uso</span><span class="sxs-lookup"><span data-stu-id="f3397-474">Usage</span></span>  
 <span data-ttu-id="f3397-475">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="f3397-475">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f3397-476">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="f3397-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="f3397-477">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="f3397-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="f3397-478">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f3397-478">Next steps</span></span>
<span data-ttu-id="f3397-479">Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f3397-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
