---
title: "Referencia de la directiva de Administración de API de Azure"
description: "Obtenga información acerca de las directivas disponibles para configurar API Management."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 9d4ac609-b221-4032-93ae-e27a1254d43d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: adc0c4415e10ddd0b4994cecef17f026546e91a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-policy-reference"></a><span data-ttu-id="19c08-103">Referencia de la directiva de Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="19c08-103">Azure API Management Policy Reference</span></span>
<span data-ttu-id="19c08-104">Esta sección proporciona un índice de las directivas en la [Referencia de la directiva de API Management de Azure][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="19c08-104">This section provides an index for the policies in the [API Management policy reference][API Management policy reference].</span></span> <span data-ttu-id="19c08-105">Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en API Management][Policies in API Management].</span><span class="sxs-lookup"><span data-stu-id="19c08-105">For information on adding and configuring policies, see [Policies in API Management][Policies in API Management].</span></span>

<span data-ttu-id="19c08-106">Las expresiones de directiva pueden utilizarse como valores de atributos o valores de texto en cualquiera de las directivas de Administración de API, a menos que la directiva especifique lo contrario.</span><span class="sxs-lookup"><span data-stu-id="19c08-106">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="19c08-107">Algunas directivas como [Flujo de control][Control flow] y [Establecer variable][Set variable] se basan en expresiones de directiva.</span><span class="sxs-lookup"><span data-stu-id="19c08-107">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="19c08-108">Para obtener más información, consulte [Directivas avanzadas][Advanced policies] y [Expresiones de directiva][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="19c08-108">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions]</span></span>

## <a name="policy-reference-index"></a><span data-ttu-id="19c08-109">Índice de referencia de directiva</span><span class="sxs-lookup"><span data-stu-id="19c08-109">Policy reference index</span></span>
* <span data-ttu-id="19c08-110">[Directivas de restricción de acceso][Access restriction policies]</span><span class="sxs-lookup"><span data-stu-id="19c08-110">[Access restriction policies][Access restriction policies]</span></span>
  * <span data-ttu-id="19c08-111">[Activar encabezado HTTP][Check HTTP header]: aplica la existencia o el valor de un encabezado HTTP.</span><span class="sxs-lookup"><span data-stu-id="19c08-111">[Check HTTP header][Check HTTP header] - Enforces existence and/or value of a HTTP Header.</span></span>
  * <span data-ttu-id="19c08-112">[Limitar la frecuencia de llamadas por suscripción][Limit call rate by subscription]: evita los picos de uso de la API limitando la frecuencia de llamadas, por suscripción.</span><span class="sxs-lookup"><span data-stu-id="19c08-112">[Limit call rate by subscription][Limit call rate by subscription] - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>
  * <span data-ttu-id="19c08-113">[Limitar la frecuencia de llamadas por clave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) : evita los picos de uso de la API limitando la frecuencia de llamadas, por clave.</span><span class="sxs-lookup"><span data-stu-id="19c08-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>
  * <span data-ttu-id="19c08-114">[Restringir IP de autor de llamada][Restrict caller IPs]: filtra (permite/deniega) las llamadas de direcciones IP específicas o de intervalos de direcciones.</span><span class="sxs-lookup"><span data-stu-id="19c08-114">[Restrict caller IPs][Restrict caller IPs] - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>
  * <span data-ttu-id="19c08-115">[Establecer cuota de uso por suscripción][Set usage quota by subscription]: le permite aplicar un volumen de llamadas renovables o permanentes o una cuota de ancho de banda por suscripción.</span><span class="sxs-lookup"><span data-stu-id="19c08-115">[Set usage quota by subscription][Set usage quota by subscription] - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>
  * <span data-ttu-id="19c08-116">[Establecer cuota de uso por clave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) : le permite aplicar un volumen de llamadas renovables o permanentes o una cuota de ancho de banda por clave.</span><span class="sxs-lookup"><span data-stu-id="19c08-116">[Set usage quota by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>
  * <span data-ttu-id="19c08-117">[Validar JWT][Validate JWT]: aplica la existencia y la validez de un JWT extraído de un encabezado HTTP especificado o un parámetro de consulta especificado.</span><span class="sxs-lookup"><span data-stu-id="19c08-117">[Validate JWT][Validate JWT] - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>
* <span data-ttu-id="19c08-118">[Directivas avanzadas][Advanced policies]</span><span class="sxs-lookup"><span data-stu-id="19c08-118">[Advanced policies][Advanced policies]</span></span>
  * <span data-ttu-id="19c08-119">[Flujo de control][Control flow]: aplica condicionalmente instrucciones de directiva basadas en los resultados de la evaluación de [expresiones booleanas][expressions].</span><span class="sxs-lookup"><span data-stu-id="19c08-119">[Control flow][Control flow] - Conditionally applies policy statements based on the results of the evaluation of Boolean [expressions][expressions].</span></span>
  * <span data-ttu-id="19c08-120">[Reenviar solicitud][Forward request]: reenvía la solicitud al servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="19c08-120">[Forward request][Forward request] - Forwards the request to the backend service.</span></span>
  * <span data-ttu-id="19c08-121">[Registro en el centro de eventos][Log to Event Hub]: envía mensajes en el formato especificado a un destino de mensaje definido por una entidad del [registrador](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger).</span><span class="sxs-lookup"><span data-stu-id="19c08-121">[Log to Event Hub][Log to Event Hub] - Sends messages in the specified format to a message target defined by a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entity.</span></span>
  * <span data-ttu-id="19c08-122">[Reintentar](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry): reintenta ejecutar las instrucciones de directiva adjuntas, si y hasta que se cumple la condición.</span><span class="sxs-lookup"><span data-stu-id="19c08-122">[Retry](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="19c08-123">La ejecución se repite en los intervalos de tiempo especificados y hasta el número de reintentos indicado.</span><span class="sxs-lookup"><span data-stu-id="19c08-123">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>
  * <span data-ttu-id="19c08-124">[Devolver respuesta](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) : anula la ejecución de la canalización y devuelve la respuesta especificada directamente al llamador.</span><span class="sxs-lookup"><span data-stu-id="19c08-124">[Return response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span>
  * <span data-ttu-id="19c08-125">[Enviar solicitud unidireccional](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) : envía una solicitud a la dirección URL especificada sin esperar una respuesta.</span><span class="sxs-lookup"><span data-stu-id="19c08-125">[Send one way request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>
  * <span data-ttu-id="19c08-126">[Enviar solicitud](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) : envía una solicitud a la dirección URL especificada.</span><span class="sxs-lookup"><span data-stu-id="19c08-126">[Send request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) - Sends a request to the specified URL.</span></span>
  * <span data-ttu-id="19c08-127">[Establecer método de solicitud](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) : le permite cambiar el método HTTP de una solicitud.</span><span class="sxs-lookup"><span data-stu-id="19c08-127">[Set request method](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>
  * <span data-ttu-id="19c08-128">[Establecer estado](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) : cambia el código de estado HTTP al valor especificado.</span><span class="sxs-lookup"><span data-stu-id="19c08-128">[Set status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) - Changes the HTTP status code to the specified value.</span></span>
  * <span data-ttu-id="19c08-129">[Establecer variable][Set variable]: conserva un valor en una variable de [contexto][context] con nombre para el acceso posterior.</span><span class="sxs-lookup"><span data-stu-id="19c08-129">[Set variable][Set variable] - Persist a value in a named [context][context] variable for later access.</span></span>
  * <span data-ttu-id="19c08-130">[Seguimiento](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace): agrega una cadena a la salida de [API Inspector](api-management-howto-api-inspector.md).</span><span class="sxs-lookup"><span data-stu-id="19c08-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) - Adds a string into the [API Inspector](api-management-howto-api-inspector.md) output.</span></span>
  * <span data-ttu-id="19c08-131">[Esperar](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) : espera a que se completen las directivas adjuntas Enviar solicitud, Obtener el valor de caché o Flujo de control antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="19c08-131">[Wait](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - Waits for enclosed Send request, Get value from cache, or Control flow policies to complete before proceeding.</span></span>
* <span data-ttu-id="19c08-132">[Directivas de autenticación][Authentication policies]</span><span class="sxs-lookup"><span data-stu-id="19c08-132">[Authentication policies][Authentication policies]</span></span>
  * <span data-ttu-id="19c08-133">[Autenticar con opción básica][Authenticate with Basic]: autenticar con un servicio de back-end mediante la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="19c08-133">[Authenticate with Basic][Authenticate with Basic] - Authenticate with a backend service using Basic authentication.</span></span>
  * <span data-ttu-id="19c08-134">[Autenticar con certificado de cliente][Authenticate with client certificate]: autenticar con un servicio de back-end mediante certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="19c08-134">[Authenticate with client certificate][Authenticate with client certificate] - Authenticate with a backend service using client certificates.</span></span>
* <span data-ttu-id="19c08-135">[Directivas de almacenamiento en caché][Caching policies]</span><span class="sxs-lookup"><span data-stu-id="19c08-135">[Caching policies][Caching policies]</span></span> 
  * <span data-ttu-id="19c08-136">[Obtener de caché][Get from cache]: realiza una búsqueda en caché y devuelve una respuesta en caché válida cuando esté disponible.</span><span class="sxs-lookup"><span data-stu-id="19c08-136">[Get from cache][Get from cache] - Perform cache look up and return a valid cached response when available.</span></span>
  * <span data-ttu-id="19c08-137">[Almacenar en caché][Store to cache]: almacena en caché la respuesta de acuerdo con la configuración de control de caché especificada.</span><span class="sxs-lookup"><span data-stu-id="19c08-137">[Store to cache][Store to cache] - Caches response according to the specified cache control configuration.</span></span>
  * <span data-ttu-id="19c08-138">[Obtener valor de caché](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) : recupere un elemento almacenado en caché por clave.</span><span class="sxs-lookup"><span data-stu-id="19c08-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>
  * <span data-ttu-id="19c08-139">[Almacenar valor en caché](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) : almacene un elemento en la memoria caché por clave.</span><span class="sxs-lookup"><span data-stu-id="19c08-139">[Store value in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) - Store an item in the cache by key.</span></span>
  * <span data-ttu-id="19c08-140">[Quitar valor de caché](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey); quita un elemento de la memoria caché por clave.</span><span class="sxs-lookup"><span data-stu-id="19c08-140">[Remove value from cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>
* <span data-ttu-id="19c08-141">[Directivas entre dominios][Cross domain policies]</span><span class="sxs-lookup"><span data-stu-id="19c08-141">[Cross domain policies][Cross domain policies]</span></span> 
  * <span data-ttu-id="19c08-142">[Permitir llamadas entre dominios][Allow cross-domain calls]: permite que la API sea accesible desde los clientes basados en explorador de Adobe Flash y Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="19c08-142">[Allow cross-domain calls][Allow cross-domain calls] - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>
  * <span data-ttu-id="19c08-143">[CORS][CORS]: agrega soporte de uso compartido de recursos entre orígenes (CORS) a una operación o a una API para permitir llamadas entre dominios desde clientes basados en explorador.</span><span class="sxs-lookup"><span data-stu-id="19c08-143">[CORS][CORS] - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>
  * <span data-ttu-id="19c08-144">[JSONP][JSONP]: agrega JSON con soporte de relleno (JSONP) a una operación o a una API para permitir llamadas entre dominios desde clientes basados en explorador de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="19c08-144">[JSONP][JSONP] - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>
* <span data-ttu-id="19c08-145">[Directivas de transformación][Transformation policies]</span><span class="sxs-lookup"><span data-stu-id="19c08-145">[Transformation policies][Transformation policies]</span></span> 
  * <span data-ttu-id="19c08-146">[Convertir JSON a XML][Convert JSON to XML]: convierte el cuerpo de solicitud o respuesta de JSON a XML.</span><span class="sxs-lookup"><span data-stu-id="19c08-146">[Convert JSON to XML][Convert JSON to XML] - Converts request or response body from JSON to XML.</span></span>
  * <span data-ttu-id="19c08-147">[Convertir XML a JSON][Convert XML to JSON]: convierte el cuerpo de solicitud o respuesta de XML a JSON.</span><span class="sxs-lookup"><span data-stu-id="19c08-147">[Convert XML to JSON][Convert XML to JSON] - Converts request or response body from XML to JSON.</span></span>
  * <span data-ttu-id="19c08-148">[Buscar y reemplazar la cadena en el cuerpo][Find and replace string in body]: encuentra una subcadena de solicitud o de respuesta y la reemplaza por una subcadena diferente.</span><span class="sxs-lookup"><span data-stu-id="19c08-148">[Find and replace string in body][Find and replace string in body] - Finds a request or response substring and replaces it with a different substring.</span></span>
  * <span data-ttu-id="19c08-149">[Enmascarar URL en el contenido][Mask URLs in content]: reescribe (enmascara) vínculos en el cuerpo de respuesta para que apunten al vínculo equivalente a través de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="19c08-149">[Mask URLs in content][Mask URLs in content] - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>
  * <span data-ttu-id="19c08-150">[Establecer el servicio back-end][Set backend service]: cambia el servicio back-end para una solicitud entrante.</span><span class="sxs-lookup"><span data-stu-id="19c08-150">[Set backend service][Set backend service] - Changes the backend service for an incoming request.</span></span>
  * <span data-ttu-id="19c08-151">[Establecer cuerpo][Set body]: establece el cuerpo del mensaje para las solicitudes entrantes y salientes.</span><span class="sxs-lookup"><span data-stu-id="19c08-151">[Set body][Set body] - Sets the message body for incoming and outgoing requests.</span></span>
  * <span data-ttu-id="19c08-152">[Establecer encabezado HTTP][Set HTTP header]: asigna un valor a un encabezado de respuesta o de solicitud existente o agrega un nuevo encabezado de este tipo.</span><span class="sxs-lookup"><span data-stu-id="19c08-152">[Set HTTP header][Set HTTP header] - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>
  * <span data-ttu-id="19c08-153">[Establecer el parámetro de cadena de consulta][Set query string parameter]: agrega, reemplaza el valor o elimina el parámetro de la cadena de consulta de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="19c08-153">[Set query string parameter][Set query string parameter] - Adds, replaces value of, or deletes request query string parameter.</span></span>
  * <span data-ttu-id="19c08-154">[URL de reescritura][Rewrite URL]: convierte una URL de solicitud de su forma pública a la forma esperada por el servicio web.</span><span class="sxs-lookup"><span data-stu-id="19c08-154">[Rewrite URL][Rewrite URL] - Converts a request URL from its public form to the form expected by the web service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19c08-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="19c08-155">Next steps</span></span>
<span data-ttu-id="19c08-156">Para obtener más información acerca de las expresiones de directivas, vea el siguiente vídeo.</span><span class="sxs-lookup"><span data-stu-id="19c08-156">For more information on policy expressions, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Access restriction policies]: https://msdn.microsoft.com/library/azure/dn894078.aspx
[Check HTTP header]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#CheckHTTPHeader
[Limit call rate by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#LimitCallRate
[Restrict caller IPs]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#RestrictCallerIPs
[Set usage quota by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#SetUsageQuota
[Validate JWT]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx
[context]: https://msdn.microsoft.com/library/azure/ea160028-fc04-4782-aa26-4b8329df3448#ContextVariables
[Forward request]: https://msdn.microsoft.com/library/azure/dn894085.aspx#ForwardRequest
[Log to Event Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store to cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON to XML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML to JSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
[Find and replace string in body]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#Findandreplacestringinbody
[Mask URLs in content]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#MaskURLSContent
[Set backend service]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetBackendService
[Set body]: https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBody
[Set HTTP header]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetHTTPheader
[Set query string parameter]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetQueryStringParameter
[Rewrite URL]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#RewriteURL



[Policies in API Management]: api-management-howto-policies.md
[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx

[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx


