---
title: "directivas de restricción de acceso de administración de API aaaAzure | Documentos de Microsoft"
description: "Obtenga información sobre directivas de restricción de acceso de hello disponibles para su uso en la administración de API de Azure."
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
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="ed947-103">Directivas de restricción de acceso de API Management</span><span class="sxs-lookup"><span data-stu-id="ed947-103">API Management access restriction policies</span></span>
<span data-ttu-id="ed947-104">En este tema se proporciona una referencia para hello las siguientes directivas de administración de API.</span><span class="sxs-lookup"><span data-stu-id="ed947-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="ed947-105">Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="ed947-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="ed947-106"><a name="AccessRestrictionPolicies"></a> Directivas de restricción de acceso</span><span class="sxs-lookup"><span data-stu-id="ed947-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="ed947-107">[Activar encabezado HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) : aplica la existencia o el valor de un encabezado HTTP.</span><span class="sxs-lookup"><span data-stu-id="ed947-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="ed947-108">[Limitar la frecuencia de llamadas por suscripción](api-management-access-restriction-policies.md#LimitCallRate) : evita los picos de uso de la API limitando la frecuencia de llamadas, por suscripción.</span><span class="sxs-lookup"><span data-stu-id="ed947-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="ed947-109">[Limitar la frecuencia de llamadas por clave](#LimitCallRateByKey) : evita los picos de uso de la API limitando la frecuencia de llamadas, por clave.</span><span class="sxs-lookup"><span data-stu-id="ed947-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="ed947-110">[Restringir IP de autor de llamada](api-management-access-restriction-policies.md#RestrictCallerIPs) : filtra (permite/deniega) las llamadas de direcciones IP específicas o de intervalos de direcciones.</span><span class="sxs-lookup"><span data-stu-id="ed947-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="ed947-111">[Establecer la cuota de uso por suscripción](api-management-access-restriction-policies.md#SetUsageQuota) -permite tooenforce un llamadas renovable o duración volumen o ancho de banda de cuota, por suscripción.</span><span class="sxs-lookup"><span data-stu-id="ed947-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="ed947-112">[Establecer la cuota de uso clave](#SetUsageQuotaByKey) -permite tooenforce un llamadas renovable o duración volumen o ancho de banda de cuota, de forma por clave.</span><span class="sxs-lookup"><span data-stu-id="ed947-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="ed947-113">[Validar JWT](api-management-access-restriction-policies.md#ValidateJWT) : aplica la existencia y la validez de un JWT extraído de un encabezado HTTP especificado o un parámetro de consulta especificado.</span><span class="sxs-lookup"><span data-stu-id="ed947-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="ed947-114"><a name="CheckHTTPHeader"></a> Activar encabezado HTTP</span><span class="sxs-lookup"><span data-stu-id="ed947-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="ed947-115">Hola de uso `check-header` tooenforce de directiva que una solicitud tiene un encabezado HTTP especificado.</span><span class="sxs-lookup"><span data-stu-id="ed947-115">Use hello `check-header` policy tooenforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="ed947-116">Si lo desea, puede comprobar toosee si el encabezado de hello tiene un valor específico o ver un intervalo de valores permitidos.</span><span class="sxs-lookup"><span data-stu-id="ed947-116">You can optionally check toosee if hello header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="ed947-117">Si se produce un error en la comprobación de hello, directiva de hello finaliza el procesamiento de la solicitud y devuelve Hola código y error de mensaje de estado HTTP especificado por la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed947-117">If hello check fails, hello policy terminates request processing and returns hello HTTP status code and error message specified by hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ed947-118">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="ed947-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="ed947-119">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ed947-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="ed947-120">Elementos</span><span class="sxs-lookup"><span data-stu-id="ed947-120">Elements</span></span>  
  
|<span data-ttu-id="ed947-121">Nombre</span><span class="sxs-lookup"><span data-stu-id="ed947-121">Name</span></span>|<span data-ttu-id="ed947-122">Descripción</span><span class="sxs-lookup"><span data-stu-id="ed947-122">Description</span></span>|<span data-ttu-id="ed947-123">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ed947-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ed947-124">check-header</span><span class="sxs-lookup"><span data-stu-id="ed947-124">check-header</span></span>|<span data-ttu-id="ed947-125">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="ed947-125">Root element.</span></span>|<span data-ttu-id="ed947-126">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-126">Yes</span></span>|  
|<span data-ttu-id="ed947-127">value</span><span class="sxs-lookup"><span data-stu-id="ed947-127">value</span></span>|<span data-ttu-id="ed947-128">Valor del encabezado HTTP permitido.</span><span class="sxs-lookup"><span data-stu-id="ed947-128">Allowed HTTP header value.</span></span> <span data-ttu-id="ed947-129">Cuando se especifican varios elementos de valor, verificación de Hola se considera correcta si cualquiera de los valores de hello es una coincidencia.</span><span class="sxs-lookup"><span data-stu-id="ed947-129">When multiple value elements are specified, hello check is considered a success if any one of hello values is a match.</span></span>|<span data-ttu-id="ed947-130">No</span><span class="sxs-lookup"><span data-stu-id="ed947-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ed947-131">Attributes</span><span class="sxs-lookup"><span data-stu-id="ed947-131">Attributes</span></span>  
  
|<span data-ttu-id="ed947-132">Nombre</span><span class="sxs-lookup"><span data-stu-id="ed947-132">Name</span></span>|<span data-ttu-id="ed947-133">Descripción</span><span class="sxs-lookup"><span data-stu-id="ed947-133">Description</span></span>|<span data-ttu-id="ed947-134">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ed947-134">Required</span></span>|<span data-ttu-id="ed947-135">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="ed947-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ed947-136">failed-check-error-message</span><span class="sxs-lookup"><span data-stu-id="ed947-136">failed-check-error-message</span></span>|<span data-ttu-id="ed947-137">Tooreturn de mensaje de error en el cuerpo de la respuesta de hello HTTP si el encabezado de hello no existe o tiene un valor no válido.</span><span class="sxs-lookup"><span data-stu-id="ed947-137">Error message tooreturn in hello HTTP response body if hello header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="ed947-138">Los caracteres especiales de este mensaje deben incluir los caracteres de escape correctos.</span><span class="sxs-lookup"><span data-stu-id="ed947-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="ed947-139">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-139">Yes</span></span>|<span data-ttu-id="ed947-140">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-140">N/A</span></span>|  
|<span data-ttu-id="ed947-141">failed-check-httpcode</span><span class="sxs-lookup"><span data-stu-id="ed947-141">failed-check-httpcode</span></span>|<span data-ttu-id="ed947-142">Tooreturn de código de estado HTTP, si el encabezado de hello no existe o tiene un valor no válido.</span><span class="sxs-lookup"><span data-stu-id="ed947-142">HTTP Status code tooreturn if hello header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="ed947-143">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-143">Yes</span></span>|<span data-ttu-id="ed947-144">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-144">N/A</span></span>|  
|<span data-ttu-id="ed947-145">header-name</span><span class="sxs-lookup"><span data-stu-id="ed947-145">header-name</span></span>|<span data-ttu-id="ed947-146">nombre de Hola de hello toocheck de encabezado HTTP.</span><span class="sxs-lookup"><span data-stu-id="ed947-146">hello name of hello HTTP Header toocheck.</span></span>|<span data-ttu-id="ed947-147">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-147">Yes</span></span>|<span data-ttu-id="ed947-148">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-148">N/A</span></span>|  
|<span data-ttu-id="ed947-149">ignore-case</span><span class="sxs-lookup"><span data-stu-id="ed947-149">ignore-case</span></span>|<span data-ttu-id="ed947-150">Se puede establecer tooTrue o False.</span><span class="sxs-lookup"><span data-stu-id="ed947-150">Can be set tooTrue or False.</span></span> <span data-ttu-id="ed947-151">Si set tooTrue caso se omite cuando el valor del encabezado de Hola se compara con el conjunto de Hola de valores aceptables.</span><span class="sxs-lookup"><span data-stu-id="ed947-151">If set tooTrue case is ignored when hello header value is compared against hello set of acceptable values.</span></span>|<span data-ttu-id="ed947-152">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-152">Yes</span></span>|<span data-ttu-id="ed947-153">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ed947-154">Uso</span><span class="sxs-lookup"><span data-stu-id="ed947-154">Usage</span></span>  
 <span data-ttu-id="ed947-155">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ed947-155">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ed947-156">**Secciones de la directiva:** entrante y saliente</span><span class="sxs-lookup"><span data-stu-id="ed947-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="ed947-157">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="ed947-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="ed947-158"><a name="LimitCallRate"></a> Limitar la tasa de llamadas por suscripción</span><span class="sxs-lookup"><span data-stu-id="ed947-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="ed947-159">Hola `rate-limit` directiva impide el uso de la API picos según una suscripción por limitando Hola llamar tooa velocidad especificado número por un período de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="ed947-159">hello `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="ed947-160">Cuando se activa esta directiva llamador Hola recibe un `429 Too Many Requests` código de estado de respuesta.</span><span class="sxs-lookup"><span data-stu-id="ed947-160">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="ed947-161">Esta directiva se puede usar una sola vez por documento de directiva.</span><span class="sxs-lookup"><span data-stu-id="ed947-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="ed947-162">[Las expresiones de directiva](api-management-policy-expressions.md) no se puede usar en cualquiera de los atributos de directiva de Hola para esta directiva.</span><span class="sxs-lookup"><span data-stu-id="ed947-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ed947-163">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="ed947-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="ed947-164">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ed947-164">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="ed947-165">Elementos</span><span class="sxs-lookup"><span data-stu-id="ed947-165">Elements</span></span>  
  
|<span data-ttu-id="ed947-166">Nombre</span><span class="sxs-lookup"><span data-stu-id="ed947-166">Name</span></span>|<span data-ttu-id="ed947-167">Descripción</span><span class="sxs-lookup"><span data-stu-id="ed947-167">Description</span></span>|<span data-ttu-id="ed947-168">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ed947-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ed947-169">set-limit</span><span class="sxs-lookup"><span data-stu-id="ed947-169">set-limit</span></span>|<span data-ttu-id="ed947-170">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="ed947-170">Root element.</span></span>|<span data-ttu-id="ed947-171">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-171">Yes</span></span>|  
|<span data-ttu-id="ed947-172">api</span><span class="sxs-lookup"><span data-stu-id="ed947-172">api</span></span>|<span data-ttu-id="ed947-173">Agregar uno o varios de estos tooimpose elementos un límite de tasa de llamadas en API dentro del producto de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed947-173">Add one  or more of these elements tooimpose a call rate limit on APIs within hello product.</span></span> <span data-ttu-id="ed947-174">Los límites de tasa de llamadas a la API y al producto se aplican de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="ed947-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="ed947-175">No</span><span class="sxs-lookup"><span data-stu-id="ed947-175">No</span></span>|  
|<span data-ttu-id="ed947-176">operación</span><span class="sxs-lookup"><span data-stu-id="ed947-176">operation</span></span>|<span data-ttu-id="ed947-177">Agregue uno o varios de estos tooimpose elementos un límite de tasa de llamadas en operaciones dentro una API.</span><span class="sxs-lookup"><span data-stu-id="ed947-177">Add one  or more of these elements tooimpose a call rate limit on operations within an API.</span></span> <span data-ttu-id="ed947-178">Los límites de tasa de llamadas se aplican de forma independiente a la API, a la operación y al producto.</span><span class="sxs-lookup"><span data-stu-id="ed947-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="ed947-179">No</span><span class="sxs-lookup"><span data-stu-id="ed947-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ed947-180">Attributes</span><span class="sxs-lookup"><span data-stu-id="ed947-180">Attributes</span></span>  
  
|<span data-ttu-id="ed947-181">Nombre</span><span class="sxs-lookup"><span data-stu-id="ed947-181">Name</span></span>|<span data-ttu-id="ed947-182">Descripción</span><span class="sxs-lookup"><span data-stu-id="ed947-182">Description</span></span>|<span data-ttu-id="ed947-183">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ed947-183">Required</span></span>|<span data-ttu-id="ed947-184">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="ed947-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ed947-185">name</span><span class="sxs-lookup"><span data-stu-id="ed947-185">name</span></span>|<span data-ttu-id="ed947-186">nombre de Hola de hello API para cuyo límite de velocidad de tooapply Hola.</span><span class="sxs-lookup"><span data-stu-id="ed947-186">hello name of hello API for which tooapply hello rate limit.</span></span>|<span data-ttu-id="ed947-187">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-187">Yes</span></span>|<span data-ttu-id="ed947-188">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-188">N/A</span></span>|  
|<span data-ttu-id="ed947-189">calls</span><span class="sxs-lookup"><span data-stu-id="ed947-189">calls</span></span>|<span data-ttu-id="ed947-190">Hola número total máximo de llamadas permitidas durante el intervalo de tiempo de hello especificado en hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="ed947-190">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="ed947-191">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-191">Yes</span></span>|<span data-ttu-id="ed947-192">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-192">N/A</span></span>|  
|<span data-ttu-id="ed947-193">renewal-period</span><span class="sxs-lookup"><span data-stu-id="ed947-193">renewal-period</span></span>|<span data-ttu-id="ed947-194">Hola período de tiempo en segundos tras el cual hello cuota se restablece.</span><span class="sxs-lookup"><span data-stu-id="ed947-194">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="ed947-195">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-195">Yes</span></span>|<span data-ttu-id="ed947-196">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ed947-197">Uso</span><span class="sxs-lookup"><span data-stu-id="ed947-197">Usage</span></span>  
 <span data-ttu-id="ed947-198">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ed947-198">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ed947-199">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="ed947-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="ed947-200">**Ámbitos de la directiva:** producto</span><span class="sxs-lookup"><span data-stu-id="ed947-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="ed947-201"><a name="LimitCallRateByKey"></a> Limitar la tasa de llamadas por clave</span><span class="sxs-lookup"><span data-stu-id="ed947-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="ed947-202">Hola `rate-limit-by-key` directiva impide el uso de la API picos según una clave por limitando Hola llamar tooa velocidad especificado número por un período de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="ed947-202">hello `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="ed947-203">clave de Hello puede tener un valor de cadena arbitraria y se proporciona normalmente mediante una expresión de directiva.</span><span class="sxs-lookup"><span data-stu-id="ed947-203">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="ed947-204">Se pueden agregar condición de incremento opcional toospecify qué solicitudes se deben contar hacia el límite de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed947-204">Optional increment condition can be added toospecify which requests should be counted towards hello limit.</span></span> <span data-ttu-id="ed947-205">Cuando se activa esta directiva llamador Hola recibe un `429 Too Many Requests` código de estado de respuesta.</span><span class="sxs-lookup"><span data-stu-id="ed947-205">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="ed947-206">Para obtener más información y ver ejemplos de esta directiva, consulte [Limitación avanzada de solicitudes con Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="ed947-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="ed947-207">Esta directiva se puede usar una sola vez por documento de directiva.</span><span class="sxs-lookup"><span data-stu-id="ed947-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ed947-208">Declaración de la directiva</span><span class="sxs-lookup"><span data-stu-id="ed947-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="ed947-209">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ed947-209">Example</span></span>  
 <span data-ttu-id="ed947-210">En el siguiente ejemplo de Hola, el límite de velocidad de hello es ordenado por dirección IP de hello llamador.</span><span class="sxs-lookup"><span data-stu-id="ed947-210">In hello following example, hello rate limit is keyed by hello caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="ed947-211">Elementos</span><span class="sxs-lookup"><span data-stu-id="ed947-211">Elements</span></span>  
  
|<span data-ttu-id="ed947-212">Nombre</span><span class="sxs-lookup"><span data-stu-id="ed947-212">Name</span></span>|<span data-ttu-id="ed947-213">Descripción</span><span class="sxs-lookup"><span data-stu-id="ed947-213">Description</span></span>|<span data-ttu-id="ed947-214">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ed947-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ed947-215">set-limit</span><span class="sxs-lookup"><span data-stu-id="ed947-215">set-limit</span></span>|<span data-ttu-id="ed947-216">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="ed947-216">Root element.</span></span>|<span data-ttu-id="ed947-217">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ed947-218">Atributos</span><span class="sxs-lookup"><span data-stu-id="ed947-218">Attributes</span></span>  
  
|<span data-ttu-id="ed947-219">Nombre</span><span class="sxs-lookup"><span data-stu-id="ed947-219">Name</span></span>|<span data-ttu-id="ed947-220">Descripción</span><span class="sxs-lookup"><span data-stu-id="ed947-220">Description</span></span>|<span data-ttu-id="ed947-221">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ed947-221">Required</span></span>|<span data-ttu-id="ed947-222">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="ed947-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ed947-223">calls</span><span class="sxs-lookup"><span data-stu-id="ed947-223">calls</span></span>|<span data-ttu-id="ed947-224">Hola número total máximo de llamadas permitidas durante el intervalo de tiempo de hello especificado en hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="ed947-224">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="ed947-225">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-225">Yes</span></span>|<span data-ttu-id="ed947-226">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-226">N/A</span></span>|  
|<span data-ttu-id="ed947-227">counter-key</span><span class="sxs-lookup"><span data-stu-id="ed947-227">counter-key</span></span>|<span data-ttu-id="ed947-228">Hola toouse clave de directiva de límite de velocidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed947-228">hello key toouse for hello rate limit policy.</span></span>|<span data-ttu-id="ed947-229">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-229">Yes</span></span>|<span data-ttu-id="ed947-230">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-230">N/A</span></span>|  
|<span data-ttu-id="ed947-231">increment-condition</span><span class="sxs-lookup"><span data-stu-id="ed947-231">increment-condition</span></span>|<span data-ttu-id="ed947-232">expresión booleana que Hola especifica si se debe contar solicitud Hola hacia la cuota de hello (`true`).</span><span class="sxs-lookup"><span data-stu-id="ed947-232">hello boolean expression specifying if hello request should be counted towards hello quota (`true`).</span></span>|<span data-ttu-id="ed947-233">No</span><span class="sxs-lookup"><span data-stu-id="ed947-233">No</span></span>|<span data-ttu-id="ed947-234">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-234">N/A</span></span>|  
|<span data-ttu-id="ed947-235">renewal-period</span><span class="sxs-lookup"><span data-stu-id="ed947-235">renewal-period</span></span>|<span data-ttu-id="ed947-236">Hola período de tiempo en segundos tras el cual hello cuota se restablece.</span><span class="sxs-lookup"><span data-stu-id="ed947-236">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="ed947-237">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-237">Yes</span></span>|<span data-ttu-id="ed947-238">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ed947-239">Uso</span><span class="sxs-lookup"><span data-stu-id="ed947-239">Usage</span></span>  
 <span data-ttu-id="ed947-240">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ed947-240">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ed947-241">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="ed947-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="ed947-242">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="ed947-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="ed947-243"><a name="RestrictCallerIPs"></a> Restringir IP de autor de llamada</span><span class="sxs-lookup"><span data-stu-id="ed947-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="ed947-244">Hola `ip-filter` directiva filtra (permite o deniega) llamadas de determinadas direcciones IP y/o intervalos de direcciones.</span><span class="sxs-lookup"><span data-stu-id="ed947-244">hello `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ed947-245">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="ed947-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="ed947-246">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ed947-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="ed947-247">Elementos</span><span class="sxs-lookup"><span data-stu-id="ed947-247">Elements</span></span>  
  
|<span data-ttu-id="ed947-248">Nombre</span><span class="sxs-lookup"><span data-stu-id="ed947-248">Name</span></span>|<span data-ttu-id="ed947-249">Descripción</span><span class="sxs-lookup"><span data-stu-id="ed947-249">Description</span></span>|<span data-ttu-id="ed947-250">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ed947-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ed947-251">ip-filter</span><span class="sxs-lookup"><span data-stu-id="ed947-251">ip-filter</span></span>|<span data-ttu-id="ed947-252">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="ed947-252">Root element.</span></span>|<span data-ttu-id="ed947-253">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-253">Yes</span></span>|  
|<span data-ttu-id="ed947-254">address</span><span class="sxs-lookup"><span data-stu-id="ed947-254">address</span></span>|<span data-ttu-id="ed947-255">Especifica una única dirección IP en qué toofilter.</span><span class="sxs-lookup"><span data-stu-id="ed947-255">Specifies a single IP address on which toofilter.</span></span>|<span data-ttu-id="ed947-256">Es necesario al menos un elemento `address` o `address-range`.</span><span class="sxs-lookup"><span data-stu-id="ed947-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="ed947-257">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="ed947-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="ed947-258">Especifica un intervalo de direcciones IP en qué toofilter.</span><span class="sxs-lookup"><span data-stu-id="ed947-258">Specifies a range of IP address on which toofilter.</span></span>|<span data-ttu-id="ed947-259">Es necesario al menos un elemento `address` o `address-range`.</span><span class="sxs-lookup"><span data-stu-id="ed947-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ed947-260">Attributes</span><span class="sxs-lookup"><span data-stu-id="ed947-260">Attributes</span></span>  
  
|<span data-ttu-id="ed947-261">Nombre</span><span class="sxs-lookup"><span data-stu-id="ed947-261">Name</span></span>|<span data-ttu-id="ed947-262">Descripción</span><span class="sxs-lookup"><span data-stu-id="ed947-262">Description</span></span>|<span data-ttu-id="ed947-263">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ed947-263">Required</span></span>|<span data-ttu-id="ed947-264">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="ed947-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ed947-265">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="ed947-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="ed947-266">Un intervalo de IP direcciones tooallow o denegar el acceso.</span><span class="sxs-lookup"><span data-stu-id="ed947-266">A range of IP addresses tooallow or deny access for.</span></span>|<span data-ttu-id="ed947-267">Se requiere si hello `address-range` elemento se utiliza.</span><span class="sxs-lookup"><span data-stu-id="ed947-267">Required when hello `address-range` element is used.</span></span>|<span data-ttu-id="ed947-268">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-268">N/A</span></span>|  
|<span data-ttu-id="ed947-269">ip-filter action="allow &#124; forbid"</span><span class="sxs-lookup"><span data-stu-id="ed947-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="ed947-270">Especifica si las llamadas deben permitirse o no para hello especifica intervalos y direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="ed947-270">Specifies whether calls should be allowed or not for hello specified IP addresses and ranges.</span></span>|<span data-ttu-id="ed947-271">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-271">Yes</span></span>|<span data-ttu-id="ed947-272">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ed947-273">Uso</span><span class="sxs-lookup"><span data-stu-id="ed947-273">Usage</span></span>  
 <span data-ttu-id="ed947-274">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ed947-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ed947-275">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="ed947-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="ed947-276">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="ed947-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="ed947-277"><a name="SetUsageQuota"></a> Establecer cuota de uso por suscripción</span><span class="sxs-lookup"><span data-stu-id="ed947-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="ed947-278">Hola `quota` la directiva exige un llamadas renovable o duración volumen o ancho de banda de cuota, por suscripción.</span><span class="sxs-lookup"><span data-stu-id="ed947-278">hello `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="ed947-279">Esta directiva se puede usar una sola vez por documento de directiva.</span><span class="sxs-lookup"><span data-stu-id="ed947-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="ed947-280">[Las expresiones de directiva](api-management-policy-expressions.md) no se puede usar en cualquiera de los atributos de directiva de Hola para esta directiva.</span><span class="sxs-lookup"><span data-stu-id="ed947-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ed947-281">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="ed947-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="ed947-282">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ed947-282">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="ed947-283">Elementos</span><span class="sxs-lookup"><span data-stu-id="ed947-283">Elements</span></span>  
  
|<span data-ttu-id="ed947-284">Nombre</span><span class="sxs-lookup"><span data-stu-id="ed947-284">Name</span></span>|<span data-ttu-id="ed947-285">Descripción</span><span class="sxs-lookup"><span data-stu-id="ed947-285">Description</span></span>|<span data-ttu-id="ed947-286">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ed947-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ed947-287">quota</span><span class="sxs-lookup"><span data-stu-id="ed947-287">quota</span></span>|<span data-ttu-id="ed947-288">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="ed947-288">Root element.</span></span>|<span data-ttu-id="ed947-289">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-289">Yes</span></span>|  
|<span data-ttu-id="ed947-290">api</span><span class="sxs-lookup"><span data-stu-id="ed947-290">api</span></span>|<span data-ttu-id="ed947-291">Agregar uno o varios de estos tooimpose elementos una cuota en API dentro del producto de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed947-291">Add one  or more of these elements tooimpose a quota on APIs within hello product.</span></span> <span data-ttu-id="ed947-292">Las cuotas de API y de producto se aplican de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="ed947-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="ed947-293">No</span><span class="sxs-lookup"><span data-stu-id="ed947-293">No</span></span>|  
|<span data-ttu-id="ed947-294">operación</span><span class="sxs-lookup"><span data-stu-id="ed947-294">operation</span></span>|<span data-ttu-id="ed947-295">Agregue uno o varios de estos tooimpose elementos una cuota en operaciones dentro una API.</span><span class="sxs-lookup"><span data-stu-id="ed947-295">Add one  or more of these elements tooimpose a quota on operations within an API.</span></span> <span data-ttu-id="ed947-296">Las cuotas de API, operación y producto se aplican de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="ed947-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="ed947-297">No</span><span class="sxs-lookup"><span data-stu-id="ed947-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ed947-298">Attributes</span><span class="sxs-lookup"><span data-stu-id="ed947-298">Attributes</span></span>  
  
|<span data-ttu-id="ed947-299">Nombre</span><span class="sxs-lookup"><span data-stu-id="ed947-299">Name</span></span>|<span data-ttu-id="ed947-300">Descripción</span><span class="sxs-lookup"><span data-stu-id="ed947-300">Description</span></span>|<span data-ttu-id="ed947-301">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ed947-301">Required</span></span>|<span data-ttu-id="ed947-302">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="ed947-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ed947-303">name</span><span class="sxs-lookup"><span data-stu-id="ed947-303">name</span></span>|<span data-ttu-id="ed947-304">nombre de Hola de API de Hola o la operación para qué hello cuota se aplica.</span><span class="sxs-lookup"><span data-stu-id="ed947-304">hello name of hello API or operation for which hello quota applies.</span></span>|<span data-ttu-id="ed947-305">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-305">Yes</span></span>|<span data-ttu-id="ed947-306">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-306">N/A</span></span>|  
|<span data-ttu-id="ed947-307">bandwidth</span><span class="sxs-lookup"><span data-stu-id="ed947-307">bandwidth</span></span>|<span data-ttu-id="ed947-308">Hola número total máximo de kilobytes permitidos durante el intervalo de tiempo de hello especificado en hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="ed947-308">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="ed947-309">Debe especificarse `calls`, `bandwidth` o ambos.</span><span class="sxs-lookup"><span data-stu-id="ed947-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="ed947-310">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-310">N/A</span></span>|  
|<span data-ttu-id="ed947-311">calls</span><span class="sxs-lookup"><span data-stu-id="ed947-311">calls</span></span>|<span data-ttu-id="ed947-312">Hola número total máximo de llamadas permitidas durante el intervalo de tiempo de hello especificado en hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="ed947-312">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="ed947-313">Debe especificarse `calls`, `bandwidth` o ambos.</span><span class="sxs-lookup"><span data-stu-id="ed947-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="ed947-314">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-314">N/A</span></span>|  
|<span data-ttu-id="ed947-315">renewal-period</span><span class="sxs-lookup"><span data-stu-id="ed947-315">renewal-period</span></span>|<span data-ttu-id="ed947-316">Hola período de tiempo en segundos tras el cual hello cuota se restablece.</span><span class="sxs-lookup"><span data-stu-id="ed947-316">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="ed947-317">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-317">Yes</span></span>|<span data-ttu-id="ed947-318">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ed947-319">Uso</span><span class="sxs-lookup"><span data-stu-id="ed947-319">Usage</span></span>  
 <span data-ttu-id="ed947-320">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ed947-320">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ed947-321">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="ed947-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="ed947-322">**Ámbitos de la directiva:** producto</span><span class="sxs-lookup"><span data-stu-id="ed947-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="ed947-323"><a name="SetUsageQuotaByKey"></a>Establecer cuota de uso por clave</span><span class="sxs-lookup"><span data-stu-id="ed947-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="ed947-324">Hola `quota-by-key` la directiva exige un llamadas renovable o duración volumen o ancho de banda de cuota, según una por cada clave.</span><span class="sxs-lookup"><span data-stu-id="ed947-324">hello `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="ed947-325">clave de Hello puede tener un valor de cadena arbitraria y se proporciona normalmente mediante una expresión de directiva.</span><span class="sxs-lookup"><span data-stu-id="ed947-325">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="ed947-326">Se pueden agregar condición de incremento opcional toospecify qué solicitudes se deben contar hacia la cuota de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed947-326">Optional increment condition can be added toospecify which requests should be counted towards hello quota.</span></span>  
  
 <span data-ttu-id="ed947-327">Para obtener más información y ver ejemplos de esta directiva, consulte [Limitación avanzada de solicitudes con Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="ed947-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="ed947-328">Esta directiva se puede usar una sola vez por documento de directiva.</span><span class="sxs-lookup"><span data-stu-id="ed947-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="ed947-329">[Las expresiones de directiva](api-management-policy-expressions.md) no se puede usar en cualquiera de los atributos de directiva de Hola para esta directiva.</span><span class="sxs-lookup"><span data-stu-id="ed947-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ed947-330">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="ed947-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="ed947-331">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ed947-331">Example</span></span>  
 <span data-ttu-id="ed947-332">En el siguiente ejemplo de Hola, cuota de hello es ordenado por dirección IP de hello llamador.</span><span class="sxs-lookup"><span data-stu-id="ed947-332">In hello following example, hello quota is keyed by hello caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="ed947-333">Elementos</span><span class="sxs-lookup"><span data-stu-id="ed947-333">Elements</span></span>  
  
|<span data-ttu-id="ed947-334">Nombre</span><span class="sxs-lookup"><span data-stu-id="ed947-334">Name</span></span>|<span data-ttu-id="ed947-335">Descripción</span><span class="sxs-lookup"><span data-stu-id="ed947-335">Description</span></span>|<span data-ttu-id="ed947-336">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ed947-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ed947-337">quota</span><span class="sxs-lookup"><span data-stu-id="ed947-337">quota</span></span>|<span data-ttu-id="ed947-338">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="ed947-338">Root element.</span></span>|<span data-ttu-id="ed947-339">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ed947-340">Atributos</span><span class="sxs-lookup"><span data-stu-id="ed947-340">Attributes</span></span>  
  
|<span data-ttu-id="ed947-341">Nombre</span><span class="sxs-lookup"><span data-stu-id="ed947-341">Name</span></span>|<span data-ttu-id="ed947-342">Descripción</span><span class="sxs-lookup"><span data-stu-id="ed947-342">Description</span></span>|<span data-ttu-id="ed947-343">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ed947-343">Required</span></span>|<span data-ttu-id="ed947-344">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="ed947-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ed947-345">bandwidth</span><span class="sxs-lookup"><span data-stu-id="ed947-345">bandwidth</span></span>|<span data-ttu-id="ed947-346">Hola número total máximo de kilobytes permitidos durante el intervalo de tiempo de hello especificado en hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="ed947-346">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="ed947-347">Debe especificarse `calls`, `bandwidth` o ambos.</span><span class="sxs-lookup"><span data-stu-id="ed947-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="ed947-348">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-348">N/A</span></span>|  
|<span data-ttu-id="ed947-349">calls</span><span class="sxs-lookup"><span data-stu-id="ed947-349">calls</span></span>|<span data-ttu-id="ed947-350">Hola número total máximo de llamadas permitidas durante el intervalo de tiempo de hello especificado en hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="ed947-350">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="ed947-351">Debe especificarse `calls`, `bandwidth` o ambos.</span><span class="sxs-lookup"><span data-stu-id="ed947-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="ed947-352">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-352">N/A</span></span>|  
|<span data-ttu-id="ed947-353">counter-key</span><span class="sxs-lookup"><span data-stu-id="ed947-353">counter-key</span></span>|<span data-ttu-id="ed947-354">Hola toouse clave para la directiva de cuota de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed947-354">hello key toouse for hello quota policy.</span></span>|<span data-ttu-id="ed947-355">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-355">Yes</span></span>|<span data-ttu-id="ed947-356">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-356">N/A</span></span>|  
|<span data-ttu-id="ed947-357">increment-condition</span><span class="sxs-lookup"><span data-stu-id="ed947-357">increment-condition</span></span>|<span data-ttu-id="ed947-358">expresión booleana que Hola especifica si se debe contar solicitud Hola hacia la cuota de hello (`true`)</span><span class="sxs-lookup"><span data-stu-id="ed947-358">hello boolean expression specifying if hello request should be counted towards hello quota (`true`)</span></span>|<span data-ttu-id="ed947-359">No</span><span class="sxs-lookup"><span data-stu-id="ed947-359">No</span></span>|<span data-ttu-id="ed947-360">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-360">N/A</span></span>|  
|<span data-ttu-id="ed947-361">renewal-period</span><span class="sxs-lookup"><span data-stu-id="ed947-361">renewal-period</span></span>|<span data-ttu-id="ed947-362">Hola período de tiempo en segundos tras el cual hello cuota se restablece.</span><span class="sxs-lookup"><span data-stu-id="ed947-362">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="ed947-363">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-363">Yes</span></span>|<span data-ttu-id="ed947-364">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ed947-365">Uso</span><span class="sxs-lookup"><span data-stu-id="ed947-365">Usage</span></span>  
 <span data-ttu-id="ed947-366">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ed947-366">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ed947-367">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="ed947-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="ed947-368">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="ed947-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="ed947-369"><a name="ValidateJWT"></a> Validación de JWT</span><span class="sxs-lookup"><span data-stu-id="ed947-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="ed947-370">Hola `validate-jwt` directiva aplica la existencia y validez de un JWT extraído de un determinado encabezado HTTP o un parámetro de consulta especificado.</span><span class="sxs-lookup"><span data-stu-id="ed947-370">hello `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="ed947-371">Hola `validate-jwt` directiva requiere que hello `exp` notificación registrado es incluidos en el token de JWT de hello, a menos que `require-expiration-time` atributo se especifica y se establece demasiado`false`.</span><span class="sxs-lookup"><span data-stu-id="ed947-371">hello `validate-jwt` policy requires that hello `exp` registered claim is inlcuded in hello JWT token, unless `require-expiration-time` attribute is specified and set too`false`.</span></span>  
> <span data-ttu-id="ed947-372">Hola `validate-jwt` directiva es compatible con HS256 y RS256 los algoritmos de firma.</span><span class="sxs-lookup"><span data-stu-id="ed947-372">hello `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="ed947-373">Para HS256 clave Hola debe proporcionarse en línea dentro de la directiva de hello en formato codificado en base64 de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed947-373">For HS256 hello key must be provided inline within hello policy in hello base64 encoded form.</span></span> <span data-ttu-id="ed947-374">Para RS256 clave hello tiene toobe proporcionan a través de un punto de conexión de configuración Openid.</span><span class="sxs-lookup"><span data-stu-id="ed947-374">For RS256 hello key has toobe provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ed947-375">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="ed947-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
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
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="ed947-376">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="ed947-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="ed947-377">Validación de tokens de Azure Mobile Services</span><span class="sxs-lookup"><span data-stu-id="ed947-377">Azure Mobile Services token validation</span></span>  
  
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
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="ed947-378">Validación de tokens de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed947-378">Azure Active Directory token validation</span></span>  
  
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

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="ed947-379">Validación de tokens de Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="ed947-379">Azure Active Directory B2C token validation</span></span>  
  
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
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a><span data-ttu-id="ed947-380">Autorizar toooperations de acceso basado en notificaciones de tokens</span><span class="sxs-lookup"><span data-stu-id="ed947-380">Authorize access toooperations based on token claims</span></span>  
 <span data-ttu-id="ed947-381">Este ejemplo se muestra cómo hello toouse [validar JWT](api-management-access-restriction-policies.md#ValidateJWT) toopre directiva-autorizar toooperations de acceso basado en notificaciones de token.</span><span class="sxs-lookup"><span data-stu-id="ed947-381">This example shows how toouse hello [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy toopre-authorize access toooperations based on token claims.</span></span> <span data-ttu-id="ed947-382">Para ver una demostración de cómo configurar y usar esta directiva, consulte [177 episodio abarcan de nube: más características de administración de API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avancemos too13:50.</span><span class="sxs-lookup"><span data-stu-id="ed947-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="ed947-383">Avance rápido too15:00 las directivas de hello toosee configuradas en el editor de directiva de hello y, a continuación, too18:50 para ver una demostración de la llamada a una operación de portal para desarrolladores de hello con y sin Hola necesario token de autorización.</span><span class="sxs-lookup"><span data-stu-id="ed947-383">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
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
  
### <a name="elements"></a><span data-ttu-id="ed947-384">Elementos</span><span class="sxs-lookup"><span data-stu-id="ed947-384">Elements</span></span>  
  
|<span data-ttu-id="ed947-385">Elemento</span><span class="sxs-lookup"><span data-stu-id="ed947-385">Element</span></span>|<span data-ttu-id="ed947-386">Descripción</span><span class="sxs-lookup"><span data-stu-id="ed947-386">Description</span></span>|<span data-ttu-id="ed947-387">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ed947-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ed947-388">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="ed947-388">validate-jwt</span></span>|<span data-ttu-id="ed947-389">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="ed947-389">Root element.</span></span>|<span data-ttu-id="ed947-390">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-390">Yes</span></span>|  
|<span data-ttu-id="ed947-391">audiences</span><span class="sxs-lookup"><span data-stu-id="ed947-391">audiences</span></span>|<span data-ttu-id="ed947-392">Contiene una lista de notificaciones de audiencia aceptables que pueden estar presentes en el símbolo (token) de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed947-392">Contains a list of acceptable audience claims that can be present on hello token.</span></span> <span data-ttu-id="ed947-393">Si existen varios valores de audiencia, se prueban los valores uno a uno hasta que se agoten todos (en cuyo caso no se superará la validación) o hasta que se obtenga un resultado positivo con alguno.</span><span class="sxs-lookup"><span data-stu-id="ed947-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="ed947-394">Debe especificarse al menos una audiencia.</span><span class="sxs-lookup"><span data-stu-id="ed947-394">At least one audience must be specified.</span></span>|<span data-ttu-id="ed947-395">No</span><span class="sxs-lookup"><span data-stu-id="ed947-395">No</span></span>|  
|<span data-ttu-id="ed947-396">issuer-signing-keys</span><span class="sxs-lookup"><span data-stu-id="ed947-396">issuer-signing-keys</span></span>|<span data-ttu-id="ed947-397">Una lista de toovalidate de claves que se utilizan con codificación Base64 de seguridad firmado símbolos (tokens).</span><span class="sxs-lookup"><span data-stu-id="ed947-397">A list of Base64-encoded security keys used toovalidate signed tokens.</span></span> <span data-ttu-id="ed947-398">Si existen varias claves de seguridad, se prueban las claves una a una hasta que se agoten todas (en cuyo caso no se superará la validación) o hasta que una sea correcta (lo que es útil para la sustitución de tokens).</span><span class="sxs-lookup"><span data-stu-id="ed947-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="ed947-399">Elementos claves tienen una función opcional `id` toomatch de atributo que se utiliza con `kid` de notificación.</span><span class="sxs-lookup"><span data-stu-id="ed947-399">Key elements have an optional `id` attribute used toomatch against `kid` claim.</span></span>|<span data-ttu-id="ed947-400">No</span><span class="sxs-lookup"><span data-stu-id="ed947-400">No</span></span>|  
|<span data-ttu-id="ed947-401">issuers</span><span class="sxs-lookup"><span data-stu-id="ed947-401">issuers</span></span>|<span data-ttu-id="ed947-402">Una lista de entidades de seguridad aceptables que emitió el token de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed947-402">A list of acceptable principals that issued hello token.</span></span> <span data-ttu-id="ed947-403">Si existen varios valores de emisor, se prueban los valores uno a uno hasta que se agoten todos (en cuyo caso no se superará la validación) o hasta que se obtenga un resultado positivo con alguno.</span><span class="sxs-lookup"><span data-stu-id="ed947-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="ed947-404">No</span><span class="sxs-lookup"><span data-stu-id="ed947-404">No</span></span>|  
|<span data-ttu-id="ed947-405">openid-config</span><span class="sxs-lookup"><span data-stu-id="ed947-405">openid-config</span></span>|<span data-ttu-id="ed947-406">elemento de Hello utilizado para especificar un extremo de configuración Openid compatible desde el que se puede obtener las claves y el emisor de la firma.</span><span class="sxs-lookup"><span data-stu-id="ed947-406">hello element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="ed947-407">No</span><span class="sxs-lookup"><span data-stu-id="ed947-407">No</span></span>|  
|<span data-ttu-id="ed947-408">required-claims</span><span class="sxs-lookup"><span data-stu-id="ed947-408">required-claims</span></span>|<span data-ttu-id="ed947-409">Contiene una lista de notificaciones que se espera toobe presente en el token de Hola para que lo toobe considere válido.</span><span class="sxs-lookup"><span data-stu-id="ed947-409">Contains a list of claims expected toobe present on hello token for it toobe considered valid.</span></span> <span data-ttu-id="ed947-410">Cuando Hola `match` atributo está establecido demasiado`all` cada valor de notificación en la directiva de hello debe estar presente en el token de Hola para toosucceed de validación.</span><span class="sxs-lookup"><span data-stu-id="ed947-410">When hello `match` attribute is set too`all` every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="ed947-411">Cuando Hola `match` atributo está establecido demasiado`any` al menos una notificación debe estar presente en el token de Hola para toosucceed de validación.</span><span class="sxs-lookup"><span data-stu-id="ed947-411">When hello `match` attribute is set too`any` at least one claim must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="ed947-412">No</span><span class="sxs-lookup"><span data-stu-id="ed947-412">No</span></span>|  
|<span data-ttu-id="ed947-413">zumo-master-key</span><span class="sxs-lookup"><span data-stu-id="ed947-413">zumo-master-key</span></span>|<span data-ttu-id="ed947-414">Clave maestra para los tokens que emite Azure Mobile Services.</span><span class="sxs-lookup"><span data-stu-id="ed947-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="ed947-415">No</span><span class="sxs-lookup"><span data-stu-id="ed947-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ed947-416">Attributes</span><span class="sxs-lookup"><span data-stu-id="ed947-416">Attributes</span></span>  
  
|<span data-ttu-id="ed947-417">Nombre</span><span class="sxs-lookup"><span data-stu-id="ed947-417">Name</span></span>|<span data-ttu-id="ed947-418">Descripción</span><span class="sxs-lookup"><span data-stu-id="ed947-418">Description</span></span>|<span data-ttu-id="ed947-419">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ed947-419">Required</span></span>|<span data-ttu-id="ed947-420">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="ed947-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ed947-421">clock-skew</span><span class="sxs-lookup"><span data-stu-id="ed947-421">clock-skew</span></span>|<span data-ttu-id="ed947-422">Intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="ed947-422">Timespan.</span></span> <span data-ttu-id="ed947-423">Proporciona cierto margen de tiempo en caso de notificación de expiración del token de hello está presente en el token de Hola y está más allá de hello actual fecha / hora.</span><span class="sxs-lookup"><span data-stu-id="ed947-423">Provides some small leeway in case hello token's expiration claim is present in hello token and is past hello current date / time.</span></span>|<span data-ttu-id="ed947-424">No</span><span class="sxs-lookup"><span data-stu-id="ed947-424">No</span></span>|<span data-ttu-id="ed947-425">0 segundos</span><span class="sxs-lookup"><span data-stu-id="ed947-425">0 seconds</span></span>|  
|<span data-ttu-id="ed947-426">failed-validation-error-message</span><span class="sxs-lookup"><span data-stu-id="ed947-426">failed-validation-error-message</span></span>|<span data-ttu-id="ed947-427">Tooreturn de mensaje de error en el cuerpo de la respuesta HTTP Hola si hello JWT no pasa la validación.</span><span class="sxs-lookup"><span data-stu-id="ed947-427">Error message tooreturn in hello HTTP response body if hello JWT does not pass validation.</span></span> <span data-ttu-id="ed947-428">Los caracteres especiales de este mensaje deben incluir los caracteres de escape correctos.</span><span class="sxs-lookup"><span data-stu-id="ed947-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="ed947-429">No</span><span class="sxs-lookup"><span data-stu-id="ed947-429">No</span></span>|<span data-ttu-id="ed947-430">El mensaje de error predeterminado depende del problema de validación, por ejemplo, la notificación de la ausencia del elemento JWT.</span><span class="sxs-lookup"><span data-stu-id="ed947-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="ed947-431">failed-validation-httpcode</span><span class="sxs-lookup"><span data-stu-id="ed947-431">failed-validation-httpcode</span></span>|<span data-ttu-id="ed947-432">Tooreturn de código de estado HTTP si hello JWT no pasa la validación.</span><span class="sxs-lookup"><span data-stu-id="ed947-432">HTTP Status code tooreturn if hello JWT doesn't pass validation.</span></span>|<span data-ttu-id="ed947-433">No</span><span class="sxs-lookup"><span data-stu-id="ed947-433">No</span></span>|<span data-ttu-id="ed947-434">401</span><span class="sxs-lookup"><span data-stu-id="ed947-434">401</span></span>|  
|<span data-ttu-id="ed947-435">header-name</span><span class="sxs-lookup"><span data-stu-id="ed947-435">header-name</span></span>|<span data-ttu-id="ed947-436">nombre de Hello del encabezado de hello HTTP que contiene el token de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed947-436">hello name of hello HTTP header holding hello token.</span></span>|<span data-ttu-id="ed947-437">Se debe especificar `header-name` o `query-paremeter-name`, pero no ambos.</span><span class="sxs-lookup"><span data-stu-id="ed947-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="ed947-438">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-438">N/A</span></span>|  
|<span data-ttu-id="ed947-439">id</span><span class="sxs-lookup"><span data-stu-id="ed947-439">id</span></span>|<span data-ttu-id="ed947-440">Hola `id` atributo hello `key` elemento le permite la cadena de hello toospecify que se comparará con `kid` toofind token (si existe) de hello out hello toouse de clave adecuado para la validación de firma de notificación.</span><span class="sxs-lookup"><span data-stu-id="ed947-440">hello `id` attribute on hello `key` element allows you toospecify hello string that will be matched against `kid` claim in hello token (if present) toofind out hello appropriate key toouse for signature validation.</span></span>|<span data-ttu-id="ed947-441">No</span><span class="sxs-lookup"><span data-stu-id="ed947-441">No</span></span>|<span data-ttu-id="ed947-442">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-442">N/A</span></span>|  
|<span data-ttu-id="ed947-443">match</span><span class="sxs-lookup"><span data-stu-id="ed947-443">match</span></span>|<span data-ttu-id="ed947-444">Hola `match` atributo hello `claim` elemento especifica si cada valor de notificación en la directiva de hello debe estar presente en el token de Hola para toosucceed de validación.</span><span class="sxs-lookup"><span data-stu-id="ed947-444">hello `match` attribute on hello `claim` element specifies whether every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="ed947-445">Los valores posibles son:</span><span class="sxs-lookup"><span data-stu-id="ed947-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="ed947-446">-                          `all`-cada valor de notificación en la directiva de hello debe estar presente en el token de Hola para toosucceed de validación.</span><span class="sxs-lookup"><span data-stu-id="ed947-446">-                          `all` - every claim value in hello policy must be present in hello token for validation toosucceed.</span></span><br /><br /> <span data-ttu-id="ed947-447">-                          `any`-valor de al menos una notificación debe estar presente en el token de Hola para toosucceed de validación.</span><span class="sxs-lookup"><span data-stu-id="ed947-447">-                          `any` - at least one claim value must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="ed947-448">No</span><span class="sxs-lookup"><span data-stu-id="ed947-448">No</span></span>|<span data-ttu-id="ed947-449">todas</span><span class="sxs-lookup"><span data-stu-id="ed947-449">all</span></span>|  
|<span data-ttu-id="ed947-450">query-paremeter-name</span><span class="sxs-lookup"><span data-stu-id="ed947-450">query-paremeter-name</span></span>|<span data-ttu-id="ed947-451">nombre de Hola Hola Hola del parámetro de consulta que contiene el token de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed947-451">hello name of hello hello query parameter holding hello token.</span></span>|<span data-ttu-id="ed947-452">Se debe especificar `header-name` o `query-paremeter-name`, pero no ambos.</span><span class="sxs-lookup"><span data-stu-id="ed947-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="ed947-453">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-453">N/A</span></span>|  
|<span data-ttu-id="ed947-454">require-expiration-time</span><span class="sxs-lookup"><span data-stu-id="ed947-454">require-expiration-time</span></span>|<span data-ttu-id="ed947-455">Booleano.</span><span class="sxs-lookup"><span data-stu-id="ed947-455">Boolean.</span></span> <span data-ttu-id="ed947-456">Especifica si se requiere una notificación de expiración en el token de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed947-456">Specifies whether an expiration claim is required in hello token.</span></span>|<span data-ttu-id="ed947-457">No</span><span class="sxs-lookup"><span data-stu-id="ed947-457">No</span></span>|<span data-ttu-id="ed947-458">true</span><span class="sxs-lookup"><span data-stu-id="ed947-458">true</span></span>|
|<span data-ttu-id="ed947-459">require-scheme</span><span class="sxs-lookup"><span data-stu-id="ed947-459">require-scheme</span></span>|<span data-ttu-id="ed947-460">Hola nombre del esquema de token de hello, p. ej. "Bearer".</span><span class="sxs-lookup"><span data-stu-id="ed947-460">hello name of hello token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="ed947-461">Cuando se establece este atributo, directiva de Hola se asegurará de que especifica el esquema está presente en el valor del encabezado de autorización de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed947-461">When this attribute is set, hello policy will ensure that specified scheme is present in hello Authorization header value.</span></span>|<span data-ttu-id="ed947-462">No</span><span class="sxs-lookup"><span data-stu-id="ed947-462">No</span></span>|<span data-ttu-id="ed947-463">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-463">N/A</span></span>|
|<span data-ttu-id="ed947-464">require-signed-tokens</span><span class="sxs-lookup"><span data-stu-id="ed947-464">require-signed-tokens</span></span>|<span data-ttu-id="ed947-465">Booleano.</span><span class="sxs-lookup"><span data-stu-id="ed947-465">Boolean.</span></span> <span data-ttu-id="ed947-466">Especifica si un token es necesario toobe firmado.</span><span class="sxs-lookup"><span data-stu-id="ed947-466">Specifies whether a token is required toobe signed.</span></span>|<span data-ttu-id="ed947-467">No</span><span class="sxs-lookup"><span data-stu-id="ed947-467">No</span></span>|<span data-ttu-id="ed947-468">true</span><span class="sxs-lookup"><span data-stu-id="ed947-468">true</span></span>|  
|<span data-ttu-id="ed947-469">url</span><span class="sxs-lookup"><span data-stu-id="ed947-469">url</span></span>|<span data-ttu-id="ed947-470">Dirección URL de punto de conexión de configuración de OpenID desde donde se pueden obtener los metadatos de configuración de OpenID.</span><span class="sxs-lookup"><span data-stu-id="ed947-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="ed947-471">Para Azure Active Directory usar hello después de la dirección URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` sustituyendo el nombre del inquilino de directorio, por ejemplo, `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="ed947-471">For Azure Active Directory use hello following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="ed947-472">Sí</span><span class="sxs-lookup"><span data-stu-id="ed947-472">Yes</span></span>|<span data-ttu-id="ed947-473">N/D</span><span class="sxs-lookup"><span data-stu-id="ed947-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ed947-474">Uso</span><span class="sxs-lookup"><span data-stu-id="ed947-474">Usage</span></span>  
 <span data-ttu-id="ed947-475">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ed947-475">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ed947-476">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="ed947-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="ed947-477">**Ámbitos de la directiva:** global, producto, API y operación</span><span class="sxs-lookup"><span data-stu-id="ed947-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="ed947-478">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ed947-478">Next steps</span></span>
<span data-ttu-id="ed947-479">Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="ed947-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
