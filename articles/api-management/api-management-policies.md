---
title: Directivas de Azure API Management | Microsoft Docs
description: "Aprenda sobre las directivas de transformación disponibles para su uso en Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 1cc460cb-8e67-41aa-bc76-bbafc1892798
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 485dc3a87a81dc67f5144596a30d498293d6b76a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-policies"></a><span data-ttu-id="a413b-103">Directivas de administración de API</span><span class="sxs-lookup"><span data-stu-id="a413b-103">API Management policies</span></span>
<span data-ttu-id="a413b-104">En esta sección se proporciona una referencia para las siguientes directivas de API Management.</span><span class="sxs-lookup"><span data-stu-id="a413b-104">This section provides a reference for the following API Management policies.</span></span> <span data-ttu-id="a413b-105">Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="a413b-105">For information on adding and configuring policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
  
 <span data-ttu-id="a413b-106">Las directivas constituyen una eficaz funcionalidad del sistema que permite al publicador cambiar el comportamiento de la API a través de la configuración.</span><span class="sxs-lookup"><span data-stu-id="a413b-106">Policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="a413b-107">Las directivas son una colección de declaraciones que se ejecutan secuencialmente en la solicitud o respuesta de una API.</span><span class="sxs-lookup"><span data-stu-id="a413b-107">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="a413b-108">Entre las declaraciones más usadas se encuentran la conversión de formato de XML a JSON y la limitación de tasa de llamadas para restringir la cantidad de llamadas entrantes de un desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a413b-108">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="a413b-109">Hay muchas más directivas disponibles y listas para usar.</span><span class="sxs-lookup"><span data-stu-id="a413b-109">Many more policies are available out of the box.</span></span>  
  
 <span data-ttu-id="a413b-110">Las expresiones de directiva pueden utilizarse como valores de atributos o valores de texto en cualquiera de las directivas de Administración de API, a menos que la directiva especifique lo contrario.</span><span class="sxs-lookup"><span data-stu-id="a413b-110">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="a413b-111">Algunas directivas como [Flujo de control](api-management-advanced-policies.md#choose) y [Establecer variable](api-management-advanced-policies.md#set-variable) se basan en expresiones de directiva.</span><span class="sxs-lookup"><span data-stu-id="a413b-111">Some policies such as the [Control flow](api-management-advanced-policies.md#choose) and [Set variable](api-management-advanced-policies.md#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="a413b-112">Para más información, consulte [Directivas avanzadas](api-management-advanced-policies.md#AdvancedPolicies) y [Expresiones de directiva](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="a413b-112">For more information, see [Advanced policies](api-management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](api-management-policy-expressions.md).</span></span>  
  
##  <span data-ttu-id="a413b-113"><a name="ProxyPolicies"></a> Directivas</span><span class="sxs-lookup"><span data-stu-id="a413b-113"><a name="ProxyPolicies"></a> Policies</span></span>  
  
-   [<span data-ttu-id="a413b-114">Directivas de restricción de acceso</span><span class="sxs-lookup"><span data-stu-id="a413b-114">Access restriction policies</span></span>](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   <span data-ttu-id="a413b-115">[Activar encabezado HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) : aplica la existencia o el valor de un encabezado HTTP.</span><span class="sxs-lookup"><span data-stu-id="a413b-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
    -   <span data-ttu-id="a413b-116">[Limitar la frecuencia de llamadas por suscripción](api-management-access-restriction-policies.md#LimitCallRate) : evita los picos de uso de la API limitando la frecuencia de llamadas, por suscripción.</span><span class="sxs-lookup"><span data-stu-id="a413b-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="a413b-117">[Limitar la frecuencia de llamadas por clave](api-management-access-restriction-policies.md#LimitCallRateByKey) : evita los picos de uso de la API limitando la frecuencia de llamadas, por clave.</span><span class="sxs-lookup"><span data-stu-id="a413b-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="a413b-118">[Restringir IP de autor de llamada](api-management-access-restriction-policies.md#RestrictCallerIPs) : filtra (permite/deniega) las llamadas de direcciones IP específicas o de intervalos de direcciones.</span><span class="sxs-lookup"><span data-stu-id="a413b-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
    -   <span data-ttu-id="a413b-119">[Establecer cuota de uso por suscripción](api-management-access-restriction-policies.md#SetUsageQuota) : le permite aplicar un volumen de llamadas renovables o permanentes o una cuota de ancho de banda por suscripción.</span><span class="sxs-lookup"><span data-stu-id="a413b-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="a413b-120">[Establecer cuota de uso por clave](api-management-access-restriction-policies.md#SetUsageQuotaByKey) : le permite aplicar un volumen de llamadas renovables o permanentes o una cuota de ancho de banda por clave.</span><span class="sxs-lookup"><span data-stu-id="a413b-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="a413b-121">[Validar JWT](api-management-access-restriction-policies.md#ValidateJWT) : aplica la existencia y la validez de un JWT extraído de un encabezado HTTP especificado o un parámetro de consulta especificado.</span><span class="sxs-lookup"><span data-stu-id="a413b-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
-   [<span data-ttu-id="a413b-122">Directivas avanzadas</span><span class="sxs-lookup"><span data-stu-id="a413b-122">Advanced policies</span></span>](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   <span data-ttu-id="a413b-123">[Flujo de control](api-management-advanced-policies.md#choose): aplica condicionalmente instrucciones de directiva basadas en la evaluación de expresiones booleanas.</span><span class="sxs-lookup"><span data-stu-id="a413b-123">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the evaluation of Boolean expressions.</span></span>  
  
    -   <span data-ttu-id="a413b-124">[Reenviar solicitud](api-management-advanced-policies.md#ForwardRequest) : reenvía la solicitud al servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="a413b-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) - Forwards the request to the backend service.</span></span>  
  
    -   <span data-ttu-id="a413b-125">[Log to Event Hub](api-management-advanced-policies.md#log-to-eventhub) (Registrar en el centro de eventos): envía mensajes en el formato especificado a un destino de mensaje definido por una entidad del registrador.</span><span class="sxs-lookup"><span data-stu-id="a413b-125">[Log to Event Hub](api-management-advanced-policies.md#log-to-eventhub) - Sends messages in the specified format to a message target defined by a Logger entity.</span></span>  
  
    -   <span data-ttu-id="a413b-126">[Reintentar](api-management-advanced-policies.md#Retry): reintenta ejecutar las instrucciones de directiva adjuntas, si y hasta que se cumple la condición.</span><span class="sxs-lookup"><span data-stu-id="a413b-126">[Retry](api-management-advanced-policies.md#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="a413b-127">La ejecución se repite en los intervalos de tiempo especificados y hasta el número de reintentos indicado.</span><span class="sxs-lookup"><span data-stu-id="a413b-127">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
    -   <span data-ttu-id="a413b-128">[Devolver respuesta](api-management-advanced-policies.md#ReturnResponse) : anula la ejecución de la canalización y devuelve la respuesta especificada directamente al llamador.</span><span class="sxs-lookup"><span data-stu-id="a413b-128">[Return response](api-management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span>  
  
    -   <span data-ttu-id="a413b-129">[Enviar solicitud unidireccional](api-management-advanced-policies.md#SendOneWayRequest) : envía una solicitud a la dirección URL especificada sin esperar una respuesta.</span><span class="sxs-lookup"><span data-stu-id="a413b-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
    -   <span data-ttu-id="a413b-130">[Enviar solicitud](api-management-advanced-policies.md#SendRequest) : envía una solicitud a la dirección URL especificada.</span><span class="sxs-lookup"><span data-stu-id="a413b-130">[Send request](api-management-advanced-policies.md#SendRequest) - Sends a request to the specified URL.</span></span>  
  
    -   <span data-ttu-id="a413b-131">[Set variable](api-management-advanced-policies.md#set-variable) (Establecer variable): conserva un valor en una variable de contexto con nombre para el acceso posterior.</span><span class="sxs-lookup"><span data-stu-id="a413b-131">[Set variable](api-management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.</span></span>  
  
    -   <span data-ttu-id="a413b-132">[Establecer método de solicitud](api-management-advanced-policies.md#SetRequestMethod) : le permite cambiar el método HTTP de una solicitud.</span><span class="sxs-lookup"><span data-stu-id="a413b-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
    -   <span data-ttu-id="a413b-133">[Establecimiento de código de estado](api-management-advanced-policies.md#SetStatus): cambia el código de estado HTTP al valor especificado.</span><span class="sxs-lookup"><span data-stu-id="a413b-133">[Set status code](api-management-advanced-policies.md#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
    -   <span data-ttu-id="a413b-134">[Seguimiento](api-management-advanced-policies.md#Trace): agrega una cadena a la salida de [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/).</span><span class="sxs-lookup"><span data-stu-id="a413b-134">[Trace](api-management-advanced-policies.md#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
    -   <span data-ttu-id="a413b-135">[Wait](api-management-advanced-policies.md#Wait) (Esperar): espera a que se completen las directivas adjuntas [Send request](api-management-advanced-policies.md#SendRequest) (Enviar solicitud), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) (Obtener el valor de caché) o [Control flow](api-management-advanced-policies.md#choose) (Flujo de control) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="a413b-135">[Wait](api-management-advanced-policies.md#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
-   [<span data-ttu-id="a413b-136">Directivas de autenticación</span><span class="sxs-lookup"><span data-stu-id="a413b-136">Authentication policies</span></span>](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   <span data-ttu-id="a413b-137">[Autenticar con opción básica](api-management-authentication-policies.md#Basic) : autenticar con un servicio de back-end mediante la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="a413b-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
    -   <span data-ttu-id="a413b-138">[Autenticar con certificado de cliente](api-management-authentication-policies.md#ClientCertificate) : autenticar con un servicio de back-end mediante certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="a413b-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
-   [<span data-ttu-id="a413b-139">Directivas de almacenamiento en caché</span><span class="sxs-lookup"><span data-stu-id="a413b-139">Caching policies</span></span>](api-management-caching-policies.md#CachingPolicies)  
  
    -   <span data-ttu-id="a413b-140">[Obtener de caché](api-management-caching-policies.md#GetFromCache) : realiza una búsqueda en caché y devuelve una respuesta en caché válida cuando esté disponible.</span><span class="sxs-lookup"><span data-stu-id="a413b-140">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.</span></span>  
  
    -   <span data-ttu-id="a413b-141">[Almacenar en caché](api-management-caching-policies.md#StoreToCache) : almacena en caché la respuesta de acuerdo con la configuración de control de caché especificada.</span><span class="sxs-lookup"><span data-stu-id="a413b-141">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches response according to the specified cache control configuration.</span></span>  
  
    -   <span data-ttu-id="a413b-142">[Obtener valor de caché](api-management-caching-policies.md#GetFromCacheByKey) : recupere un elemento almacenado en caché por clave.</span><span class="sxs-lookup"><span data-stu-id="a413b-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="a413b-143">[Almacenar valor en caché](api-management-caching-policies.md#StoreToCacheByKey) : almacene un elemento en la memoria caché por clave.</span><span class="sxs-lookup"><span data-stu-id="a413b-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="a413b-144">[Quitar valor de caché](api-management-caching-policies.md#RemoveCacheByKey); quita un elemento de la memoria caché por clave.</span><span class="sxs-lookup"><span data-stu-id="a413b-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
-   [<span data-ttu-id="a413b-145">Directivas entre dominios</span><span class="sxs-lookup"><span data-stu-id="a413b-145">Cross domain policies</span></span>](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   <span data-ttu-id="a413b-146">[Permitir llamadas entre dominios](api-management-cross-domain-policies.md#AllowCrossDomainCalls) : permite que la API sea accesible desde los clientes basados en explorador de Adobe Flash y Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="a413b-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
    -   <span data-ttu-id="a413b-147">[CORS](api-management-cross-domain-policies.md#CORS) : agrega soporte de uso compartido de recursos entre orígenes (CORS) a una operación o a una API para permitir llamadas entre dominios desde clientes basados en explorador.</span><span class="sxs-lookup"><span data-stu-id="a413b-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
    -   <span data-ttu-id="a413b-148">[JSONP](api-management-cross-domain-policies.md#JSONP) : agrega JSON con soporte de relleno (JSONP) a una operación o a una API para permitir llamadas entre dominios desde clientes basados en explorador de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a413b-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
-   [<span data-ttu-id="a413b-149">Directivas de transformación</span><span class="sxs-lookup"><span data-stu-id="a413b-149">Transformation policies</span></span>](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   <span data-ttu-id="a413b-150">[Convertir JSON a XML](api-management-transformation-policies.md#ConvertJSONtoXML) : convierte el cuerpo de solicitud o respuesta de JSON a XML.</span><span class="sxs-lookup"><span data-stu-id="a413b-150">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
    -   <span data-ttu-id="a413b-151">[Convertir XML a JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) : convierte el cuerpo de solicitud o respuesta de XML a JSON.</span><span class="sxs-lookup"><span data-stu-id="a413b-151">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
    -   <span data-ttu-id="a413b-152">[Buscar y reemplazar la cadena en el cuerpo](api-management-transformation-policies.md#Findandreplacestringinbody) : encuentra una subcadena de solicitud o de respuesta y la reemplaza por una subcadena diferente.</span><span class="sxs-lookup"><span data-stu-id="a413b-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
    -   <span data-ttu-id="a413b-153">[Enmascarar URL en el contenido](api-management-transformation-policies.md#MaskURLSContent) : reescribe (enmascara) vínculos en el cuerpo de respuesta para que apunten al vínculo equivalente a través de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="a413b-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
    -   <span data-ttu-id="a413b-154">[Establecer el servicio back-end](api-management-transformation-policies.md#SetBackendService) : cambia el servicio back-end para una solicitud entrante.</span><span class="sxs-lookup"><span data-stu-id="a413b-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
    -   <span data-ttu-id="a413b-155">[Establecer cuerpo](api-management-transformation-policies.md#SetBody) -establece el cuerpo del mensaje para las solicitudes entrantes y salientes.</span><span class="sxs-lookup"><span data-stu-id="a413b-155">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
    -   <span data-ttu-id="a413b-156">[Establecer encabezado HTTP](api-management-transformation-policies.md#SetHTTPheader) : asigna un valor a un encabezado de respuesta o de solicitud existente o agrega un nuevo encabezado de este tipo.</span><span class="sxs-lookup"><span data-stu-id="a413b-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
    -   <span data-ttu-id="a413b-157">[Establecer el parámetro de cadena de consulta](api-management-transformation-policies.md#SetQueryStringParameter) : agrega, reemplaza el valor o elimina el parámetro de la cadena de consulta de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="a413b-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
    -   <span data-ttu-id="a413b-158">[URL de reescritura](api-management-transformation-policies.md#RewriteURL) : convierte una URL de solicitud de su forma pública a la forma esperada por el servicio web.</span><span class="sxs-lookup"><span data-stu-id="a413b-158">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
    -   <span data-ttu-id="a413b-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) (Transformar XML mediante una XSLT): aplica una transformación de XSL al XML del cuerpo de la solicitud o respuesta.</span><span class="sxs-lookup"><span data-stu-id="a413b-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="a413b-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a413b-160">Next steps</span></span>
<span data-ttu-id="a413b-161">Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="a413b-161">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
