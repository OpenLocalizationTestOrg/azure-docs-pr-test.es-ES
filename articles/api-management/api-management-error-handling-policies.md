---
title: Control de errores en las directivas de Azure API Management | Microsoft Docs
description: Aprenda a responder a las condiciones de error que se pueden producir durante el procesamiento de solicitudes en Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 3c777964-02b2-4f55-8731-8c3bd3c0ae27
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2fb403cc7454227083dc34d41a6f5f3a5876b1e7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="error-handling-in-api-management-policies"></a><span data-ttu-id="4d040-103">Control de errores en las directivas de API Management</span><span class="sxs-lookup"><span data-stu-id="4d040-103">Error handling in API Management policies</span></span>
<span data-ttu-id="4d040-104">Azure API Management proporciona un objeto `ProxyError` que permite a los publicadores responder a las condiciones de error que se pueden producir durante el procesamiento de solicitudes en el proxy.</span><span class="sxs-lookup"><span data-stu-id="4d040-104">Azure API Management allows publishers to respond to error conditions that may occur during the processing of requests to the proxy by providing a `ProxyError` object.</span></span> <span data-ttu-id="4d040-105">Para acceder al objeto `ProxyError` se usa la propiedad [context.LastError](api-management-policy-expressions.md#ContextVariables). Este objeto se puede usar en las directivas de la sección de directivas `on-error`.</span><span class="sxs-lookup"><span data-stu-id="4d040-105">The `ProxyError` object is accessed through the [context.LastError](api-management-policy-expressions.md#ContextVariables) property and can be used by policies in the `on-error` policy section.</span></span> <span data-ttu-id="4d040-106">En este tema se proporciona una referencia a las funcionalidades de control de errores de Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="4d040-106">This topic provides a reference for the error handling capabilities in Azure API Management.</span></span>  
  
## <a name="error-handling-in-api-management"></a><span data-ttu-id="4d040-107">Control de errores en API Management</span><span class="sxs-lookup"><span data-stu-id="4d040-107">Error handling in API Management</span></span>  
 <span data-ttu-id="4d040-108">Las directivas de Azure API Management están divididas en las secciones `inbound`, `backend`, `outbound` y `on-error`, como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="4d040-108">Policies in Azure API Management are divided into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in the following example.</span></span>  
  
```xml  
<policies>  
  <inbound>  
    <!-- statements to be applied to the request go here -->  
  </inbound>  
  <backend>  
    <!-- statements to be applied before the request is   
         forwarded to the backend service go here -->  
    </backend>  
    <outbound>  
      <!-- statements to be applied to the response go here -->  
    </outbound>  
    <on-error>  
        <!-- statements to be applied if there is an error   
             condition go here -->  
  </on-error>  
</policies>  
```  
  
 <span data-ttu-id="4d040-109">Durante el procesamiento de una solicitud, se ejecutan pasos integrados junto con las directivas que están en el ámbito de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="4d040-109">During the processing of a request, built-in steps are executed along with any policies that are in scope for the request.</span></span> <span data-ttu-id="4d040-110">Si se produce un error, el procesamiento salta inmediatamente a la sección de directivas `on-error`.</span><span class="sxs-lookup"><span data-stu-id="4d040-110">If an error occurs, processing immediately jumps to the `on-error` policy section.</span></span> <span data-ttu-id="4d040-111">La sección de directivas `on-error` se puede usar en cualquier ámbito, y los publicadores de API pueden configurar comportamientos predeterminados, como registrar el error en los centros de eventos o crear una nueva respuesta para devolver al autor de la llamada.</span><span class="sxs-lookup"><span data-stu-id="4d040-111">The `on-error` policy section can be used at any scope, and API publishers can configure custom behavior such as logging the error to event hubs or creating a new response to return to the caller.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="4d040-112">La sección `on-error` no está presente en las directivas de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4d040-112">The `on-error` section is not present in policies by default.</span></span> <span data-ttu-id="4d040-113">Para agregar la sección `on-error` a una directiva, vaya a la directiva deseada en el editor de directivas y agréguela.</span><span class="sxs-lookup"><span data-stu-id="4d040-113">To add the `on-error` section to a policy, browse to the desired policy in the policy editor and add it.</span></span> <span data-ttu-id="4d040-114">Para más información sobre cómo configurar directivas, consulte [Directivas en API Management](https://azure.microsoft.com/documentation/articles/api-management-howto-policies/).</span><span class="sxs-lookup"><span data-stu-id="4d040-114">For more information about configuring policies, see [Policies in API Management](https://azure.microsoft.com/documentation/articles/api-management-howto-policies/).</span></span>  
>   
>  <span data-ttu-id="4d040-115">Si no hay ninguna sección `on-error`, los autores de la llamada recibirán mensajes de respuesta HTTP 400 o 500 si se produce una condición de error.</span><span class="sxs-lookup"><span data-stu-id="4d040-115">If there is no `on-error` section, callers will receive 400 or 500 HTTP response messages if an error condition occurs.</span></span>  
  
### <a name="policies-allowed-in-on-error"></a><span data-ttu-id="4d040-116">Directivas permitidas en on-error</span><span class="sxs-lookup"><span data-stu-id="4d040-116">Policies allowed in on-error</span></span>  
 <span data-ttu-id="4d040-117">Las siguientes directivas se pueden usar en la sección de directivas `on-error`.</span><span class="sxs-lookup"><span data-stu-id="4d040-117">The following policies can be used in the `on-error` policy section.</span></span>  
  
-   [<span data-ttu-id="4d040-118">choose</span><span class="sxs-lookup"><span data-stu-id="4d040-118">choose</span></span>](api-management-advanced-policies.md#choose)  
  
-   [<span data-ttu-id="4d040-119">set-variable</span><span class="sxs-lookup"><span data-stu-id="4d040-119">set-variable</span></span>](api-management-advanced-policies.md#set-variable)  
  
-   [<span data-ttu-id="4d040-120">find-and-replace</span><span class="sxs-lookup"><span data-stu-id="4d040-120">find-and-replace</span></span>](api-management-transformation-policies.md#Findandreplacestringinbody)  
  
-   [<span data-ttu-id="4d040-121">return-response</span><span class="sxs-lookup"><span data-stu-id="4d040-121">return-response</span></span>](api-management-advanced-policies.md#ReturnResponse)  
  
-   [<span data-ttu-id="4d040-122">set-header</span><span class="sxs-lookup"><span data-stu-id="4d040-122">set-header</span></span>](api-management-transformation-policies.md#SetHTTPheader)  
  
-   [<span data-ttu-id="4d040-123">set-method</span><span class="sxs-lookup"><span data-stu-id="4d040-123">set-method</span></span>](api-management-advanced-policies.md#SetRequestMethod)  
  
-   [<span data-ttu-id="4d040-124">set-status</span><span class="sxs-lookup"><span data-stu-id="4d040-124">set-status</span></span>](api-management-advanced-policies.md#SetStatus)  
  
-   [<span data-ttu-id="4d040-125">send-request</span><span class="sxs-lookup"><span data-stu-id="4d040-125">send-request</span></span>](api-management-advanced-policies.md#SendRequest)  
  
-   [<span data-ttu-id="4d040-126">send-one-way-request</span><span class="sxs-lookup"><span data-stu-id="4d040-126">send-one-way-request</span></span>](api-management-advanced-policies.md#SendOneWayRequest)  
  
-   [<span data-ttu-id="4d040-127">log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="4d040-127">log-to-eventhub</span></span>](api-management-advanced-policies.md#log-to-eventhub)  
  
-   [<span data-ttu-id="4d040-128">json-to-xml</span><span class="sxs-lookup"><span data-stu-id="4d040-128">json-to-xml</span></span>](api-management-transformation-policies.md#ConvertJSONtoXML)  
  
-   [<span data-ttu-id="4d040-129">xml-to-json</span><span class="sxs-lookup"><span data-stu-id="4d040-129">xml-to-json</span></span>](api-management-transformation-policies.md#ConvertXMLtoJSON)  
  
## <a name="lasterror"></a><span data-ttu-id="4d040-130">LastError</span><span class="sxs-lookup"><span data-stu-id="4d040-130">LastError</span></span>  
 <span data-ttu-id="4d040-131">Cuando se produce un error y el control salta a la sección de directivas `on-error`, el error se almacena en la propiedad [context.LastError](api-management-policy-expressions.md#ContextVariables) a la que pueden acceder las directivas de la sección `on-error` y tiene las siguientes propiedades.</span><span class="sxs-lookup"><span data-stu-id="4d040-131">When an error occurs and control jumps to the `on-error` policy section, the error is stored in  [context.LastError](api-management-policy-expressions.md#ContextVariables) property which can be accessed by policies in the `on-error` section and has the following properties.</span></span>  
  
|<span data-ttu-id="4d040-132">Nombre</span><span class="sxs-lookup"><span data-stu-id="4d040-132">Name</span></span>|<span data-ttu-id="4d040-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="4d040-133">Type</span></span>|<span data-ttu-id="4d040-134">Descripción</span><span class="sxs-lookup"><span data-stu-id="4d040-134">Description</span></span>|<span data-ttu-id="4d040-135">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="4d040-135">Required</span></span>|  
|----------|----------|-----------------|--------------|  
|<span data-ttu-id="4d040-136">Origen</span><span class="sxs-lookup"><span data-stu-id="4d040-136">Source</span></span>|<span data-ttu-id="4d040-137">string</span><span class="sxs-lookup"><span data-stu-id="4d040-137">string</span></span>|<span data-ttu-id="4d040-138">Nombre del elemento donde se produjo el error.</span><span class="sxs-lookup"><span data-stu-id="4d040-138">Names the element where the error occurred.</span></span> <span data-ttu-id="4d040-139">Puede ser el nombre de una directiva o el nombre de un paso de canalización integrado.</span><span class="sxs-lookup"><span data-stu-id="4d040-139">Could be either policy or a  built-in pipeline step name.</span></span>|<span data-ttu-id="4d040-140">Sí</span><span class="sxs-lookup"><span data-stu-id="4d040-140">Yes</span></span>|  
|<span data-ttu-id="4d040-141">Motivo</span><span class="sxs-lookup"><span data-stu-id="4d040-141">Reason</span></span>|<span data-ttu-id="4d040-142">string</span><span class="sxs-lookup"><span data-stu-id="4d040-142">string</span></span>|<span data-ttu-id="4d040-143">Código de error reconocible por la máquina, que se puede utilizar en el control de errores.</span><span class="sxs-lookup"><span data-stu-id="4d040-143">Machine-friendly error code, which could be used in error handling.</span></span>|<span data-ttu-id="4d040-144">No</span><span class="sxs-lookup"><span data-stu-id="4d040-144">No</span></span>|  
|<span data-ttu-id="4d040-145">Message</span><span class="sxs-lookup"><span data-stu-id="4d040-145">Message</span></span>|<span data-ttu-id="4d040-146">string</span><span class="sxs-lookup"><span data-stu-id="4d040-146">string</span></span>|<span data-ttu-id="4d040-147">Descripción del error legible para el usuario.</span><span class="sxs-lookup"><span data-stu-id="4d040-147">Human-readable error description.</span></span>|<span data-ttu-id="4d040-148">Sí</span><span class="sxs-lookup"><span data-stu-id="4d040-148">Yes</span></span>|  
|<span data-ttu-id="4d040-149">Scope</span><span class="sxs-lookup"><span data-stu-id="4d040-149">Scope</span></span>|<span data-ttu-id="4d040-150">string</span><span class="sxs-lookup"><span data-stu-id="4d040-150">string</span></span>|<span data-ttu-id="4d040-151">Nombre del ámbito donde se produjo el error; podría ser "global", "producto", "api" u "operación"</span><span class="sxs-lookup"><span data-stu-id="4d040-151">Name of the scope where the error occurred and could be one of "global", "product", "api", or "operation"</span></span>|<span data-ttu-id="4d040-152">No</span><span class="sxs-lookup"><span data-stu-id="4d040-152">No</span></span>|  
|<span data-ttu-id="4d040-153">Sección</span><span class="sxs-lookup"><span data-stu-id="4d040-153">Section</span></span>|<span data-ttu-id="4d040-154">string</span><span class="sxs-lookup"><span data-stu-id="4d040-154">string</span></span>|<span data-ttu-id="4d040-155">Nombre de la sección donde se produjo el error; podría ser: "entrada", "back-end", "salida" o "error".</span><span class="sxs-lookup"><span data-stu-id="4d040-155">Section name where error occurred and could one of "inbound", "backend", "outbound", or "on-error".</span></span>|<span data-ttu-id="4d040-156">No</span><span class="sxs-lookup"><span data-stu-id="4d040-156">No</span></span>|  
|<span data-ttu-id="4d040-157">Ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="4d040-157">Path</span></span>|<span data-ttu-id="4d040-158">string</span><span class="sxs-lookup"><span data-stu-id="4d040-158">string</span></span>|<span data-ttu-id="4d040-159">Especifica directivas anidadas, por ejemplo, "choose[3]/when[2]".</span><span class="sxs-lookup"><span data-stu-id="4d040-159">Specifies nested policy, e.g. "choose[3]/when[2]".</span></span>|<span data-ttu-id="4d040-160">No</span><span class="sxs-lookup"><span data-stu-id="4d040-160">No</span></span>|  
|<span data-ttu-id="4d040-161">PolicyId</span><span class="sxs-lookup"><span data-stu-id="4d040-161">PolicyId</span></span>|<span data-ttu-id="4d040-162">string</span><span class="sxs-lookup"><span data-stu-id="4d040-162">string</span></span>|<span data-ttu-id="4d040-163">Valor del atributo `id`, si lo especifica el cliente, en la directiva donde se produjo el error.</span><span class="sxs-lookup"><span data-stu-id="4d040-163">Value of the `id` attribute, if specified by the customer, on the policy where error occurred</span></span>|<span data-ttu-id="4d040-164">No</span><span class="sxs-lookup"><span data-stu-id="4d040-164">No</span></span>|  
  
> [!NOTE]
>  <span data-ttu-id="4d040-165">Todas las directivas tienen un atributo `id` opcional que se pude agregar al elemento raíz de la directiva.</span><span class="sxs-lookup"><span data-stu-id="4d040-165">All policies have an optional `id` attribute that can be added to the root element of the policy.</span></span> <span data-ttu-id="4d040-166">Si este atributo está presente en una directiva cuando se produce una condición de error, el valor del atributo se puede recuperar mediante la propiedad `context.LastError.PolicyId`.</span><span class="sxs-lookup"><span data-stu-id="4d040-166">If this attribute is present in a policy when an error condition occurs, the value of the attribute can be retrieved using the `context.LastError.PolicyId` property.</span></span>  
  
## <a name="predefined-errors-for-built-in-steps"></a><span data-ttu-id="4d040-167">Errores predefinidos para pasos integrados</span><span class="sxs-lookup"><span data-stu-id="4d040-167">Predefined errors for built-in steps</span></span>  
 <span data-ttu-id="4d040-168">Los errores siguientes están predefinidos para condiciones de error que se pueden producir durante la evaluación de pasos de procesamiento integrados.</span><span class="sxs-lookup"><span data-stu-id="4d040-168">The following errors are predefined for error conditions that can occur during the evaluation of built-in processing steps.</span></span>  
  
|<span data-ttu-id="4d040-169">Origen</span><span class="sxs-lookup"><span data-stu-id="4d040-169">Source</span></span>|<span data-ttu-id="4d040-170">Condición</span><span class="sxs-lookup"><span data-stu-id="4d040-170">Condition</span></span>|<span data-ttu-id="4d040-171">Motivo</span><span class="sxs-lookup"><span data-stu-id="4d040-171">Reason</span></span>|<span data-ttu-id="4d040-172">Message</span><span class="sxs-lookup"><span data-stu-id="4d040-172">Message</span></span>|  
|------------|---------------|------------|-------------|  
|<span data-ttu-id="4d040-173">configuración</span><span class="sxs-lookup"><span data-stu-id="4d040-173">configuration</span></span>|<span data-ttu-id="4d040-174">El URI no coincide con ninguna API u operación.</span><span class="sxs-lookup"><span data-stu-id="4d040-174">Uri doesn't match to any Api or Operation</span></span>|<span data-ttu-id="4d040-175">OperationNotFound</span><span class="sxs-lookup"><span data-stu-id="4d040-175">OperationNotFound</span></span>|<span data-ttu-id="4d040-176">No se puede hacer coincidir la solicitud entrante con una operación.</span><span class="sxs-lookup"><span data-stu-id="4d040-176">Unable to match incoming request to an operation.</span></span>|  
|<span data-ttu-id="4d040-177">authorization</span><span class="sxs-lookup"><span data-stu-id="4d040-177">authorization</span></span>|<span data-ttu-id="4d040-178">No se ha proporcionado la clave de suscripción.</span><span class="sxs-lookup"><span data-stu-id="4d040-178">Subscription key not supplied</span></span>|<span data-ttu-id="4d040-179">SubscriptionKeyNotFound</span><span class="sxs-lookup"><span data-stu-id="4d040-179">SubscriptionKeyNotFound</span></span>|<span data-ttu-id="4d040-180">Acceso denegado debido a que falta la clave de suscripción.</span><span class="sxs-lookup"><span data-stu-id="4d040-180">Access denied due to missing subscription key.</span></span> <span data-ttu-id="4d040-181">Asegúrese de incluir la clave de la suscripción al realizar solicitudes a esta API.</span><span class="sxs-lookup"><span data-stu-id="4d040-181">Make sure to include subscription key when making requests to this API.</span></span>|  
|<span data-ttu-id="4d040-182">authorization</span><span class="sxs-lookup"><span data-stu-id="4d040-182">authorization</span></span>|<span data-ttu-id="4d040-183">El valor de la clave de suscripción no es válido.</span><span class="sxs-lookup"><span data-stu-id="4d040-183">Subscription key value is invalid</span></span>|<span data-ttu-id="4d040-184">SubscriptionKeyInvalid</span><span class="sxs-lookup"><span data-stu-id="4d040-184">SubscriptionKeyInvalid</span></span>|<span data-ttu-id="4d040-185">Acceso denegado debido a una clave de suscripción no válida.</span><span class="sxs-lookup"><span data-stu-id="4d040-185">Access denied due to invalid subscription key.</span></span> <span data-ttu-id="4d040-186">Asegúrese de proporcionar una clave válida para una suscripción activa.</span><span class="sxs-lookup"><span data-stu-id="4d040-186">Make sure to provide a valid key for an active subscription.</span></span>|  
  
## <a name="predefined-errors-for-policies"></a><span data-ttu-id="4d040-187">Errores predefinidos en directivas</span><span class="sxs-lookup"><span data-stu-id="4d040-187">Predefined errors for policies</span></span>  
 <span data-ttu-id="4d040-188">Los errores siguientes están predefinidos para condiciones de error que se pueden producir durante la evaluación de directivas.</span><span class="sxs-lookup"><span data-stu-id="4d040-188">The following errors are predefined for error conditions that can occur during policy evaluation.</span></span>  
  
|<span data-ttu-id="4d040-189">Origen</span><span class="sxs-lookup"><span data-stu-id="4d040-189">Source</span></span>|<span data-ttu-id="4d040-190">Condición</span><span class="sxs-lookup"><span data-stu-id="4d040-190">Condition</span></span>|<span data-ttu-id="4d040-191">Motivo</span><span class="sxs-lookup"><span data-stu-id="4d040-191">Reason</span></span>|<span data-ttu-id="4d040-192">Message</span><span class="sxs-lookup"><span data-stu-id="4d040-192">Message</span></span>|  
|------------|---------------|------------|-------------|  
|<span data-ttu-id="4d040-193">rate-limit</span><span class="sxs-lookup"><span data-stu-id="4d040-193">rate-limit</span></span>|<span data-ttu-id="4d040-194">Límite de velocidad excedido</span><span class="sxs-lookup"><span data-stu-id="4d040-194">Rate limit exceeded</span></span>|<span data-ttu-id="4d040-195">RateLimitExceeded</span><span class="sxs-lookup"><span data-stu-id="4d040-195">RateLimitExceeded</span></span>|<span data-ttu-id="4d040-196">Rate limit is exceeded (Se ha excedido el límite de velocidad).</span><span class="sxs-lookup"><span data-stu-id="4d040-196">Rate limit is exceeded</span></span>|  
|<span data-ttu-id="4d040-197">quota</span><span class="sxs-lookup"><span data-stu-id="4d040-197">quota</span></span>|<span data-ttu-id="4d040-198">Cuota superada</span><span class="sxs-lookup"><span data-stu-id="4d040-198">Quota exceeded</span></span>|<span data-ttu-id="4d040-199">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="4d040-199">QuotaExceeded</span></span>|<span data-ttu-id="4d040-200">Out of call volume quota. (Fuera de la cuota de volumen de la llamada.)</span><span class="sxs-lookup"><span data-stu-id="4d040-200">Out of call volume quota.</span></span> <span data-ttu-id="4d040-201">La cuota se reabastecerá en xx:xx:xx.</span><span class="sxs-lookup"><span data-stu-id="4d040-201">Quota will be replenished in xx:xx:xx.</span></span> <span data-ttu-id="4d040-202">O bien, Out of bandwidth quota (Fuera de la cuota de ancho de banda).</span><span class="sxs-lookup"><span data-stu-id="4d040-202">-or- Out of bandwidth quota.</span></span> <span data-ttu-id="4d040-203">La cuota se reabastecerá en xx:xx:xx.</span><span class="sxs-lookup"><span data-stu-id="4d040-203">Quota will be replenished in xx:xx:xx.</span></span>|  
|<span data-ttu-id="4d040-204">jsonp</span><span class="sxs-lookup"><span data-stu-id="4d040-204">jsonp</span></span>|<span data-ttu-id="4d040-205">El valor del parámetro de devolución de llamada no es válido (contiene caracteres incorrectos).</span><span class="sxs-lookup"><span data-stu-id="4d040-205">Callback parameter value is invalid (contains wrong characters)</span></span>|<span data-ttu-id="4d040-206">CallbackParameterInvalid</span><span class="sxs-lookup"><span data-stu-id="4d040-206">CallbackParameterInvalid</span></span>|<span data-ttu-id="4d040-207">Value of callback parameter {callback-parameter-name} is not a valid JavaScript identifier (El valor del parámetro de devolución de llamada {callback-parameter-name} no es un identificador de JavaScript válido).</span><span class="sxs-lookup"><span data-stu-id="4d040-207">Value of callback parameter {callback-parameter-name} is not a valid JavaScript identifier.</span></span>|  
|<span data-ttu-id="4d040-208">ip-filter</span><span class="sxs-lookup"><span data-stu-id="4d040-208">ip-filter</span></span>|<span data-ttu-id="4d040-209">No se pudo analizar la IP de autor de llamada de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="4d040-209">Failed to parse caller IP from request</span></span>|<span data-ttu-id="4d040-210">FailedToParseCallerIP</span><span class="sxs-lookup"><span data-stu-id="4d040-210">FailedToParseCallerIP</span></span>|<span data-ttu-id="4d040-211">Failed to establish IP address for the caller.</span><span class="sxs-lookup"><span data-stu-id="4d040-211">Failed to establish IP address for the caller.</span></span> <span data-ttu-id="4d040-212">Access denied (No se pudo establecer la dirección IP del autor de la llamada. Acceso denegado).</span><span class="sxs-lookup"><span data-stu-id="4d040-212">Access denied.</span></span>|  
|<span data-ttu-id="4d040-213">ip-filter</span><span class="sxs-lookup"><span data-stu-id="4d040-213">ip-filter</span></span>|<span data-ttu-id="4d040-214">La IP del autor de la llamada no está en la lista de permitidos.</span><span class="sxs-lookup"><span data-stu-id="4d040-214">Caller IP is not in allowed list</span></span>|<span data-ttu-id="4d040-215">CallerIpNotAllowed</span><span class="sxs-lookup"><span data-stu-id="4d040-215">CallerIpNotAllowed</span></span>|<span data-ttu-id="4d040-216">Caller IP address {ip-address} is not allowed.</span><span class="sxs-lookup"><span data-stu-id="4d040-216">Caller IP address {ip-address} is not allowed.</span></span> <span data-ttu-id="4d040-217">Access denied (No se permite la IP del autor de la llamada {ip-address}. Acceso denegado).</span><span class="sxs-lookup"><span data-stu-id="4d040-217">Access denied.</span></span>|  
|<span data-ttu-id="4d040-218">ip-filter</span><span class="sxs-lookup"><span data-stu-id="4d040-218">ip-filter</span></span>|<span data-ttu-id="4d040-219">La IP del autor de la llamada está en la lista de bloqueados.</span><span class="sxs-lookup"><span data-stu-id="4d040-219">Caller IP is in blocked list</span></span>|<span data-ttu-id="4d040-220">CallerIpBlocked</span><span class="sxs-lookup"><span data-stu-id="4d040-220">CallerIpBlocked</span></span>|<span data-ttu-id="4d040-221">Caller IP address is blocked.</span><span class="sxs-lookup"><span data-stu-id="4d040-221">Caller IP address is blocked.</span></span> <span data-ttu-id="4d040-222">Access denied (La IP del autor de la llamada está bloqueada. Acceso denegado).</span><span class="sxs-lookup"><span data-stu-id="4d040-222">Access denied.</span></span>|  
|<span data-ttu-id="4d040-223">check-header</span><span class="sxs-lookup"><span data-stu-id="4d040-223">check-header</span></span>|<span data-ttu-id="4d040-224">El encabezado necesario no está presente o falta un valor.</span><span class="sxs-lookup"><span data-stu-id="4d040-224">Required header not presented or value is missing</span></span>|<span data-ttu-id="4d040-225">HeaderNotFound</span><span class="sxs-lookup"><span data-stu-id="4d040-225">HeaderNotFound</span></span>|<span data-ttu-id="4d040-226">Header {header-name} was not found in the request.</span><span class="sxs-lookup"><span data-stu-id="4d040-226">Header {header-name} was not found in the request.</span></span> <span data-ttu-id="4d040-227">Access denied (No se encontró el encabezado {header-name} en la solicitud. Acceso denegado).</span><span class="sxs-lookup"><span data-stu-id="4d040-227">Access denied.</span></span>|  
|<span data-ttu-id="4d040-228">check-header</span><span class="sxs-lookup"><span data-stu-id="4d040-228">check-header</span></span>|<span data-ttu-id="4d040-229">El encabezado necesario no está presente o falta un valor.</span><span class="sxs-lookup"><span data-stu-id="4d040-229">Required header not presented or value is missing</span></span>|<span data-ttu-id="4d040-230">HeaderValueNotAllowed</span><span class="sxs-lookup"><span data-stu-id="4d040-230">HeaderValueNotAllowed</span></span>|<span data-ttu-id="4d040-231">Header {header-name} value of {header-value} is not allowed.</span><span class="sxs-lookup"><span data-stu-id="4d040-231">Header {header-name} value of {header-value} is not allowed.</span></span> <span data-ttu-id="4d040-232">Access denied (No se permite el valor {header-name} del encabezado de {header-value}. Acceso denegado).</span><span class="sxs-lookup"><span data-stu-id="4d040-232">Access denied.</span></span>|  
|<span data-ttu-id="4d040-233">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="4d040-233">validate-jwt</span></span>|<span data-ttu-id="4d040-234">Falta el token Jwt en la solicitud.</span><span class="sxs-lookup"><span data-stu-id="4d040-234">Jwt token is missing in request</span></span>|<span data-ttu-id="4d040-235">TokenNotFound</span><span class="sxs-lookup"><span data-stu-id="4d040-235">TokenNotFound</span></span>|<span data-ttu-id="4d040-236">JWT not found in the request.</span><span class="sxs-lookup"><span data-stu-id="4d040-236">JWT not found in the request.</span></span> <span data-ttu-id="4d040-237">Access denied (No se encuentra JWT en la solicitud. Acceso denegado).</span><span class="sxs-lookup"><span data-stu-id="4d040-237">Access denied.</span></span>|  
|<span data-ttu-id="4d040-238">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="4d040-238">validate-jwt</span></span>|<span data-ttu-id="4d040-239">Error de validación de contraseña.</span><span class="sxs-lookup"><span data-stu-id="4d040-239">Signature validation failed</span></span>|<span data-ttu-id="4d040-240">TokenSignatureInvalid</span><span class="sxs-lookup"><span data-stu-id="4d040-240">TokenSignatureInvalid</span></span>|<span data-ttu-id="4d040-241"><mensaje de la biblioteca de jwt\>.</span><span class="sxs-lookup"><span data-stu-id="4d040-241"><message from jwt library\>.</span></span> <span data-ttu-id="4d040-242">Acceso denegado.</span><span class="sxs-lookup"><span data-stu-id="4d040-242">Access denied.</span></span>|  
|<span data-ttu-id="4d040-243">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="4d040-243">validate-jwt</span></span>|<span data-ttu-id="4d040-244">Audiencia no válida.</span><span class="sxs-lookup"><span data-stu-id="4d040-244">Invalid audience</span></span>|<span data-ttu-id="4d040-245">TokenAudienceNotAllowed</span><span class="sxs-lookup"><span data-stu-id="4d040-245">TokenAudienceNotAllowed</span></span>|<span data-ttu-id="4d040-246"><mensaje de la biblioteca de jwt\>.</span><span class="sxs-lookup"><span data-stu-id="4d040-246"><message from jwt library\>.</span></span> <span data-ttu-id="4d040-247">Acceso denegado.</span><span class="sxs-lookup"><span data-stu-id="4d040-247">Access denied.</span></span>|  
|<span data-ttu-id="4d040-248">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="4d040-248">validate-jwt</span></span>|<span data-ttu-id="4d040-249">Emisor no válido</span><span class="sxs-lookup"><span data-stu-id="4d040-249">Invalid issuer</span></span>|<span data-ttu-id="4d040-250">TokenIssuerNotAllowed</span><span class="sxs-lookup"><span data-stu-id="4d040-250">TokenIssuerNotAllowed</span></span>|<span data-ttu-id="4d040-251"><mensaje de la biblioteca de jwt\>.</span><span class="sxs-lookup"><span data-stu-id="4d040-251"><message from jwt library\>.</span></span> <span data-ttu-id="4d040-252">Acceso denegado.</span><span class="sxs-lookup"><span data-stu-id="4d040-252">Access denied.</span></span>|  
|<span data-ttu-id="4d040-253">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="4d040-253">validate-jwt</span></span>|<span data-ttu-id="4d040-254">Token expirado</span><span class="sxs-lookup"><span data-stu-id="4d040-254">Token expired</span></span>|<span data-ttu-id="4d040-255">TokenExpired</span><span class="sxs-lookup"><span data-stu-id="4d040-255">TokenExpired</span></span>|<span data-ttu-id="4d040-256"><mensaje de la biblioteca de jwt\>.</span><span class="sxs-lookup"><span data-stu-id="4d040-256"><message from jwt library\>.</span></span> <span data-ttu-id="4d040-257">Acceso denegado.</span><span class="sxs-lookup"><span data-stu-id="4d040-257">Access denied.</span></span>|  
|<span data-ttu-id="4d040-258">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="4d040-258">validate-jwt</span></span>|<span data-ttu-id="4d040-259">La clave de firma no se resolvió por el id.</span><span class="sxs-lookup"><span data-stu-id="4d040-259">Signature key was not resolved by id</span></span>|<span data-ttu-id="4d040-260">TokenSignatureKeyNotFound</span><span class="sxs-lookup"><span data-stu-id="4d040-260">TokenSignatureKeyNotFound</span></span>|<span data-ttu-id="4d040-261"><mensaje de la biblioteca de jwt\>.</span><span class="sxs-lookup"><span data-stu-id="4d040-261"><message from jwt library\>.</span></span> <span data-ttu-id="4d040-262">Acceso denegado.</span><span class="sxs-lookup"><span data-stu-id="4d040-262">Access denied.</span></span>|  
|<span data-ttu-id="4d040-263">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="4d040-263">validate-jwt</span></span>|<span data-ttu-id="4d040-264">Faltan las notificaciones necesarias del token.</span><span class="sxs-lookup"><span data-stu-id="4d040-264">Required claims are missing from token</span></span>|<span data-ttu-id="4d040-265">TokenClaimNotFound</span><span class="sxs-lookup"><span data-stu-id="4d040-265">TokenClaimNotFound</span></span>|<span data-ttu-id="4d040-266">JWT token is missing the following claims (Falta el token de JWT en las siguientes notificaciones): <c1\>, <c2\>, …</span><span class="sxs-lookup"><span data-stu-id="4d040-266">JWT token is missing the following claims: <c1\>, <c2\>, …</span></span> <span data-ttu-id="4d040-267">Acceso denegado.</span><span class="sxs-lookup"><span data-stu-id="4d040-267">Access denied.</span></span>|  
|<span data-ttu-id="4d040-268">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="4d040-268">validate-jwt</span></span>|<span data-ttu-id="4d040-269">Error de coincidencia de valores de notificación.</span><span class="sxs-lookup"><span data-stu-id="4d040-269">Claim values mismatch</span></span>|<span data-ttu-id="4d040-270">TokenClaimValueNotAllowed</span><span class="sxs-lookup"><span data-stu-id="4d040-270">TokenClaimValueNotAllowed</span></span>|<span data-ttu-id="4d040-271">Claim {claim-name} value of {claim-value} is not allowed.</span><span class="sxs-lookup"><span data-stu-id="4d040-271">Claim {claim-name} value of {claim-value} is not allowed.</span></span> <span data-ttu-id="4d040-272">Acceso denegado.</span><span class="sxs-lookup"><span data-stu-id="4d040-272">Access denied.</span></span>|  
|<span data-ttu-id="4d040-273">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="4d040-273">validate-jwt</span></span>|<span data-ttu-id="4d040-274">Otros errores de validación</span><span class="sxs-lookup"><span data-stu-id="4d040-274">Other validation failures</span></span>|<span data-ttu-id="4d040-275">JwtInvalid</span><span class="sxs-lookup"><span data-stu-id="4d040-275">JwtInvalid</span></span>|<span data-ttu-id="4d040-276"><mensaje de la biblioteca de jwt\>.</span><span class="sxs-lookup"><span data-stu-id="4d040-276"><message from jwt library\></span></span>|

## <a name="next-steps"></a><span data-ttu-id="4d040-277">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4d040-277">Next steps</span></span>
<span data-ttu-id="4d040-278">Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4d040-278">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  