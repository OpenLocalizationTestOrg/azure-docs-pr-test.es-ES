---
title: "aaaAzure referencia de directiva de administración de API"
description: "Obtenga información acerca de hello directivas disponibles tooconfigure administración de API."
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
ms.openlocfilehash: 7ee194f4d6f172bf836c789cbe8ab732e18a7e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-policy-reference"></a><span data-ttu-id="a22ea-103">Referencia de la directiva de Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="a22ea-103">Azure API Management Policy Reference</span></span>
<span data-ttu-id="a22ea-104">Esta sección proporciona un índice para las directivas de Hola Hola [referencia de directiva de administración de API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="a22ea-104">This section provides an index for hello policies in hello [API Management policy reference][API Management policy reference].</span></span> <span data-ttu-id="a22ea-105">Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en API Management][Policies in API Management].</span><span class="sxs-lookup"><span data-stu-id="a22ea-105">For information on adding and configuring policies, see [Policies in API Management][Policies in API Management].</span></span>

<span data-ttu-id="a22ea-106">Las expresiones de directiva se pueden usar como valores de atributo o valores de texto en cualquiera de las directivas de administración de API de hello, a menos que la directiva de Hola se especifique lo contrario.</span><span class="sxs-lookup"><span data-stu-id="a22ea-106">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="a22ea-107">Algunas directivas como hello [flujo de Control] [ Control flow] y [Set variable] [ Set variable] directivas basadas en expresiones de directiva.</span><span class="sxs-lookup"><span data-stu-id="a22ea-107">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="a22ea-108">Para obtener más información, consulte [Directivas avanzadas][Advanced policies] y [Expresiones de directiva][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="a22ea-108">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions]</span></span>

## <a name="policy-reference-index"></a><span data-ttu-id="a22ea-109">Índice de referencia de directiva</span><span class="sxs-lookup"><span data-stu-id="a22ea-109">Policy reference index</span></span>
* <span data-ttu-id="a22ea-110">[Directivas de restricción de acceso][Access restriction policies]</span><span class="sxs-lookup"><span data-stu-id="a22ea-110">[Access restriction policies][Access restriction policies]</span></span>
  * <span data-ttu-id="a22ea-111">[Activar encabezado HTTP][Check HTTP header]: aplica la existencia o el valor de un encabezado HTTP.</span><span class="sxs-lookup"><span data-stu-id="a22ea-111">[Check HTTP header][Check HTTP header] - Enforces existence and/or value of a HTTP Header.</span></span>
  * <span data-ttu-id="a22ea-112">[Limitar la frecuencia de llamadas por suscripción][Limit call rate by subscription]: evita los picos de uso de la API limitando la frecuencia de llamadas, por suscripción.</span><span class="sxs-lookup"><span data-stu-id="a22ea-112">[Limit call rate by subscription][Limit call rate by subscription] - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>
  * <span data-ttu-id="a22ea-113">[Limitar la frecuencia de llamadas por clave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) : evita los picos de uso de la API limitando la frecuencia de llamadas, por clave.</span><span class="sxs-lookup"><span data-stu-id="a22ea-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>
  * <span data-ttu-id="a22ea-114">[Restringir IP de autor de llamada][Restrict caller IPs]: filtra (permite/deniega) las llamadas de direcciones IP específicas o de intervalos de direcciones.</span><span class="sxs-lookup"><span data-stu-id="a22ea-114">[Restrict caller IPs][Restrict caller IPs] - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>
  * <span data-ttu-id="a22ea-115">[Establecer la cuota de uso por suscripción] [ Set usage quota by subscription] -permite tooenforce un llamadas renovable o duración volumen o ancho de banda de cuota, por suscripción.</span><span class="sxs-lookup"><span data-stu-id="a22ea-115">[Set usage quota by subscription][Set usage quota by subscription] - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>
  * <span data-ttu-id="a22ea-116">[Establecer la cuota de uso clave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -permite tooenforce un llamadas renovable o duración volumen o ancho de banda de cuota, de forma por clave.</span><span class="sxs-lookup"><span data-stu-id="a22ea-116">[Set usage quota by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>
  * <span data-ttu-id="a22ea-117">[Validar JWT][Validate JWT]: aplica la existencia y la validez de un JWT extraído de un encabezado HTTP especificado o un parámetro de consulta especificado.</span><span class="sxs-lookup"><span data-stu-id="a22ea-117">[Validate JWT][Validate JWT] - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>
* <span data-ttu-id="a22ea-118">[Directivas avanzadas][Advanced policies]</span><span class="sxs-lookup"><span data-stu-id="a22ea-118">[Advanced policies][Advanced policies]</span></span>
  * <span data-ttu-id="a22ea-119">[Flujo de control] [ Control flow] - condicionalmente aplica las instrucciones de directiva en función de los resultados de Hola de evaluación de Hola de tipo Boolean [expresiones][expressions].</span><span class="sxs-lookup"><span data-stu-id="a22ea-119">[Control flow][Control flow] - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions][expressions].</span></span>
  * <span data-ttu-id="a22ea-120">[Reenviar la solicitud] [ Forward request] -reenvía el servicio back-end de hello solicitud toohello.</span><span class="sxs-lookup"><span data-stu-id="a22ea-120">[Forward request][Forward request] - Forwards hello request toohello backend service.</span></span>
  * <span data-ttu-id="a22ea-121">[Inicie sesión tooEvent concentrador] [ Log tooEvent Hub] -envía los mensajes en el destino de mensaje Hola formato especificado tooa definido por un [registrador](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entidad.</span><span class="sxs-lookup"><span data-stu-id="a22ea-121">[Log tooEvent Hub][Log tooEvent Hub] - Sends messages in hello specified format tooa message target defined by a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entity.</span></span>
  * <span data-ttu-id="a22ea-122">[Vuelva a intentar](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -ejecución de reintentos de hello entre las instrucciones de directiva, si y hasta que se cumpla la condición de Hola.</span><span class="sxs-lookup"><span data-stu-id="a22ea-122">[Retry](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="a22ea-123">Ejecución se repetirá en intervalos de tiempo especificados de Hola y seguridad toohello especificada el número de reintentos.</span><span class="sxs-lookup"><span data-stu-id="a22ea-123">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>
  * <span data-ttu-id="a22ea-124">[Devolver la respuesta](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -Hola de ejecución y devuelve de la canalización de anulaciones especificado respuesta directamente toohello autor de la llamada.</span><span class="sxs-lookup"><span data-stu-id="a22ea-124">[Return response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span>
  * <span data-ttu-id="a22ea-125">[Enviar solicitud unidireccionales](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) -envía una solicitud toohello especificó la dirección URL sin tener que esperar una respuesta.</span><span class="sxs-lookup"><span data-stu-id="a22ea-125">[Send one way request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>
  * <span data-ttu-id="a22ea-126">[Enviar solicitud](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) -envía una solicitud toohello URL especificada.</span><span class="sxs-lookup"><span data-stu-id="a22ea-126">[Send request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) - Sends a request toohello specified URL.</span></span>
  * <span data-ttu-id="a22ea-127">[Establecer el método de solicitud](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) -permite toochange método de hello HTTP para una solicitud.</span><span class="sxs-lookup"><span data-stu-id="a22ea-127">[Set request method](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>
  * <span data-ttu-id="a22ea-128">[Establecer el estado](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -toohello de código de estado HTTP de Hola de cambios de valor especificado.</span><span class="sxs-lookup"><span data-stu-id="a22ea-128">[Set status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>
  * <span data-ttu-id="a22ea-129">[Establecer variable][Set variable]: conserva un valor en una variable de [contexto][context] con nombre para el acceso posterior.</span><span class="sxs-lookup"><span data-stu-id="a22ea-129">[Set variable][Set variable] - Persist a value in a named [context][context] variable for later access.</span></span>
  * <span data-ttu-id="a22ea-130">[Seguimiento](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -agrega una cadena en hello [API Inspector](api-management-howto-api-inspector.md) salida.</span><span class="sxs-lookup"><span data-stu-id="a22ea-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) - Adds a string into hello [API Inspector](api-management-howto-api-inspector.md) output.</span></span>
  * <span data-ttu-id="a22ea-131">[Espere](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) : solicita espera envío entre comillas, obtener el valor de la memoria caché, o controlar el flujo directivas toocomplete antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="a22ea-131">[Wait](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - Waits for enclosed Send request, Get value from cache, or Control flow policies toocomplete before proceeding.</span></span>
* <span data-ttu-id="a22ea-132">[Directivas de autenticación][Authentication policies]</span><span class="sxs-lookup"><span data-stu-id="a22ea-132">[Authentication policies][Authentication policies]</span></span>
  * <span data-ttu-id="a22ea-133">[Autenticar con opción básica][Authenticate with Basic]: autenticar con un servicio de back-end mediante la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="a22ea-133">[Authenticate with Basic][Authenticate with Basic] - Authenticate with a backend service using Basic authentication.</span></span>
  * <span data-ttu-id="a22ea-134">[Autenticar con certificado de cliente][Authenticate with client certificate]: autenticar con un servicio de back-end mediante certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="a22ea-134">[Authenticate with client certificate][Authenticate with client certificate] - Authenticate with a backend service using client certificates.</span></span>
* <span data-ttu-id="a22ea-135">[Directivas de almacenamiento en caché][Caching policies]</span><span class="sxs-lookup"><span data-stu-id="a22ea-135">[Caching policies][Caching policies]</span></span> 
  * <span data-ttu-id="a22ea-136">[Obtener de caché][Get from cache]: realiza una búsqueda en caché y devuelve una respuesta en caché válida cuando esté disponible.</span><span class="sxs-lookup"><span data-stu-id="a22ea-136">[Get from cache][Get from cache] - Perform cache look up and return a valid cached response when available.</span></span>
  * <span data-ttu-id="a22ea-137">[Almacenar toocache] [ Store toocache] -respuesta de las memorias caché según toohello especifica la configuración de control de caché.</span><span class="sxs-lookup"><span data-stu-id="a22ea-137">[Store toocache][Store toocache] - Caches response according toohello specified cache control configuration.</span></span>
  * <span data-ttu-id="a22ea-138">[Obtener valor de caché](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) : recupere un elemento almacenado en caché por clave.</span><span class="sxs-lookup"><span data-stu-id="a22ea-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>
  * <span data-ttu-id="a22ea-139">[Valor de almacenar en caché](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -almacenar un elemento en caché de Hola por clave.</span><span class="sxs-lookup"><span data-stu-id="a22ea-139">[Store value in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>
  * <span data-ttu-id="a22ea-140">[Quitar el valor de la caché](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -quitar un elemento en caché de Hola por clave.</span><span class="sxs-lookup"><span data-stu-id="a22ea-140">[Remove value from cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>
* <span data-ttu-id="a22ea-141">[Directivas entre dominios][Cross domain policies]</span><span class="sxs-lookup"><span data-stu-id="a22ea-141">[Cross domain policies][Cross domain policies]</span></span> 
  * <span data-ttu-id="a22ea-142">[Permitir llamadas entre dominios] [ Allow cross-domain calls] -hace Hola API sea accesible desde clientes basados en exploradores de Adobe Flash y Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="a22ea-142">[Allow cross-domain calls][Allow cross-domain calls] - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>
  * <span data-ttu-id="a22ea-143">[CORS] [ CORS] -agrega recursos entre orígenes (CORS) de uso compartido admite la operación de tooan o llama a una API tooallow dominios desde clientes basados en explorador.</span><span class="sxs-lookup"><span data-stu-id="a22ea-143">[CORS][CORS] - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>
  * <span data-ttu-id="a22ea-144">[JSONP] [ JSONP] : agrega JSON con relleno (JSONP) soporte tooan operación o llama a una API tooallow dominios desde clientes basados en exploradores de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a22ea-144">[JSONP][JSONP] - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>
* <span data-ttu-id="a22ea-145">[Directivas de transformación][Transformation policies]</span><span class="sxs-lookup"><span data-stu-id="a22ea-145">[Transformation policies][Transformation policies]</span></span> 
  * <span data-ttu-id="a22ea-146">[Convertir JSON tooXML] [ Convert JSON tooXML] : convierte solicitar o cuerpo de la respuesta de JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="a22ea-146">[Convert JSON tooXML][Convert JSON tooXML] - Converts request or response body from JSON tooXML.</span></span>
  * <span data-ttu-id="a22ea-147">[Convertir XML tooJSON] [ Convert XML tooJSON] : convierte solicitar o cuerpo de la respuesta de XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="a22ea-147">[Convert XML tooJSON][Convert XML tooJSON] - Converts request or response body from XML tooJSON.</span></span>
  * <span data-ttu-id="a22ea-148">[Buscar y reemplazar la cadena en el cuerpo][Find and replace string in body]: encuentra una subcadena de solicitud o de respuesta y la reemplaza por una subcadena diferente.</span><span class="sxs-lookup"><span data-stu-id="a22ea-148">[Find and replace string in body][Find and replace string in body] - Finds a request or response substring and replaces it with a different substring.</span></span>
  * <span data-ttu-id="a22ea-149">[Enmascarar direcciones URL en contenido] [ Mask URLs in content] -reescribe (enmascara) vínculos en la respuesta de hello cuerpo para que apunten toohello vínculo equivalente a través de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="a22ea-149">[Mask URLs in content][Mask URLs in content] - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>
  * <span data-ttu-id="a22ea-150">[Establecer el servicio back-end] [ Set backend service] -cambia el servicio back-end de Hola para una solicitud entrante.</span><span class="sxs-lookup"><span data-stu-id="a22ea-150">[Set backend service][Set backend service] - Changes hello backend service for an incoming request.</span></span>
  * <span data-ttu-id="a22ea-151">[Establecer cuerpo] [ Set body] -establece el cuerpo del mensaje de Hola para las solicitudes entrantes y salientes.</span><span class="sxs-lookup"><span data-stu-id="a22ea-151">[Set body][Set body] - Sets hello message body for incoming and outgoing requests.</span></span>
  * <span data-ttu-id="a22ea-152">[Definir el encabezado HTTP] [ Set HTTP header] : asigna una respuesta de valor tooan existente o un encabezado de solicitud o agrega un nuevo encabezado de respuesta y/o de solicitud.</span><span class="sxs-lookup"><span data-stu-id="a22ea-152">[Set HTTP header][Set HTTP header] - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>
  * <span data-ttu-id="a22ea-153">[Establecer el parámetro de cadena de consulta][Set query string parameter]: agrega, reemplaza el valor o elimina el parámetro de la cadena de consulta de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="a22ea-153">[Set query string parameter][Set query string parameter] - Adds, replaces value of, or deletes request query string parameter.</span></span>
  * <span data-ttu-id="a22ea-154">[Reescribir dirección URL] [ Rewrite URL] -convierte una dirección URL de solicitud desde su formato de toohello de formato público esperado por el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="a22ea-154">[Rewrite URL][Rewrite URL] - Converts a request URL from its public form toohello form expected by hello web service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a22ea-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a22ea-155">Next steps</span></span>
<span data-ttu-id="a22ea-156">Para obtener más información sobre las expresiones de directiva, vea Hola después de vídeo.</span><span class="sxs-lookup"><span data-stu-id="a22ea-156">For more information on policy expressions, see hello following video.</span></span>

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
[Log tooEvent Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store toocache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON tooXML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML tooJSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
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


