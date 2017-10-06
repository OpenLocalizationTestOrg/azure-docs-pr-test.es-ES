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
# <a name="azure-api-management-policy-reference"></a>Referencia de la directiva de Administración de API de Azure
Esta sección proporciona un índice para las directivas de Hola Hola [referencia de directiva de administración de API][API Management policy reference]. Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en API Management][Policies in API Management].

Las expresiones de directiva se pueden usar como valores de atributo o valores de texto en cualquiera de las directivas de administración de API de hello, a menos que la directiva de Hola se especifique lo contrario. Algunas directivas como hello [flujo de Control] [ Control flow] y [Set variable] [ Set variable] directivas basadas en expresiones de directiva. Para obtener más información, consulte [Directivas avanzadas][Advanced policies] y [Expresiones de directiva][Policy expressions].

## <a name="policy-reference-index"></a>Índice de referencia de directiva
* [Directivas de restricción de acceso][Access restriction policies]
  * [Activar encabezado HTTP][Check HTTP header]: aplica la existencia o el valor de un encabezado HTTP.
  * [Limitar la frecuencia de llamadas por suscripción][Limit call rate by subscription]: evita los picos de uso de la API limitando la frecuencia de llamadas, por suscripción.
  * [Limitar la frecuencia de llamadas por clave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) : evita los picos de uso de la API limitando la frecuencia de llamadas, por clave.
  * [Restringir IP de autor de llamada][Restrict caller IPs]: filtra (permite/deniega) las llamadas de direcciones IP específicas o de intervalos de direcciones.
  * [Establecer la cuota de uso por suscripción] [ Set usage quota by subscription] -permite tooenforce un llamadas renovable o duración volumen o ancho de banda de cuota, por suscripción.
  * [Establecer la cuota de uso clave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -permite tooenforce un llamadas renovable o duración volumen o ancho de banda de cuota, de forma por clave.
  * [Validar JWT][Validate JWT]: aplica la existencia y la validez de un JWT extraído de un encabezado HTTP especificado o un parámetro de consulta especificado.
* [Directivas avanzadas][Advanced policies]
  * [Flujo de control] [ Control flow] - condicionalmente aplica las instrucciones de directiva en función de los resultados de Hola de evaluación de Hola de tipo Boolean [expresiones][expressions].
  * [Reenviar la solicitud] [ Forward request] -reenvía el servicio back-end de hello solicitud toohello.
  * [Inicie sesión tooEvent concentrador] [ Log tooEvent Hub] -envía los mensajes en el destino de mensaje Hola formato especificado tooa definido por un [registrador](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entidad.
  * [Vuelva a intentar](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -ejecución de reintentos de hello entre las instrucciones de directiva, si y hasta que se cumpla la condición de Hola. Ejecución se repetirá en intervalos de tiempo especificados de Hola y seguridad toohello especificada el número de reintentos.
  * [Devolver la respuesta](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -Hola de ejecución y devuelve de la canalización de anulaciones especificado respuesta directamente toohello autor de la llamada.
  * [Enviar solicitud unidireccionales](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) -envía una solicitud toohello especificó la dirección URL sin tener que esperar una respuesta.
  * [Enviar solicitud](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) -envía una solicitud toohello URL especificada.
  * [Establecer el método de solicitud](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) -permite toochange método de hello HTTP para una solicitud.
  * [Establecer el estado](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -toohello de código de estado HTTP de Hola de cambios de valor especificado.
  * [Establecer variable][Set variable]: conserva un valor en una variable de [contexto][context] con nombre para el acceso posterior.
  * [Seguimiento](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -agrega una cadena en hello [API Inspector](api-management-howto-api-inspector.md) salida.
  * [Espere](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) : solicita espera envío entre comillas, obtener el valor de la memoria caché, o controlar el flujo directivas toocomplete antes de continuar.
* [Directivas de autenticación][Authentication policies]
  * [Autenticar con opción básica][Authenticate with Basic]: autenticar con un servicio de back-end mediante la autenticación básica.
  * [Autenticar con certificado de cliente][Authenticate with client certificate]: autenticar con un servicio de back-end mediante certificados de cliente.
* [Directivas de almacenamiento en caché][Caching policies] 
  * [Obtener de caché][Get from cache]: realiza una búsqueda en caché y devuelve una respuesta en caché válida cuando esté disponible.
  * [Almacenar toocache] [ Store toocache] -respuesta de las memorias caché según toohello especifica la configuración de control de caché.
  * [Obtener valor de caché](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) : recupere un elemento almacenado en caché por clave.
  * [Valor de almacenar en caché](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -almacenar un elemento en caché de Hola por clave.
  * [Quitar el valor de la caché](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -quitar un elemento en caché de Hola por clave.
* [Directivas entre dominios][Cross domain policies] 
  * [Permitir llamadas entre dominios] [ Allow cross-domain calls] -hace Hola API sea accesible desde clientes basados en exploradores de Adobe Flash y Microsoft Silverlight.
  * [CORS] [ CORS] -agrega recursos entre orígenes (CORS) de uso compartido admite la operación de tooan o llama a una API tooallow dominios desde clientes basados en explorador.
  * [JSONP] [ JSONP] : agrega JSON con relleno (JSONP) soporte tooan operación o llama a una API tooallow dominios desde clientes basados en exploradores de JavaScript.
* [Directivas de transformación][Transformation policies] 
  * [Convertir JSON tooXML] [ Convert JSON tooXML] : convierte solicitar o cuerpo de la respuesta de JSON tooXML.
  * [Convertir XML tooJSON] [ Convert XML tooJSON] : convierte solicitar o cuerpo de la respuesta de XML tooJSON.
  * [Buscar y reemplazar la cadena en el cuerpo][Find and replace string in body]: encuentra una subcadena de solicitud o de respuesta y la reemplaza por una subcadena diferente.
  * [Enmascarar direcciones URL en contenido] [ Mask URLs in content] -reescribe (enmascara) vínculos en la respuesta de hello cuerpo para que apunten toohello vínculo equivalente a través de puerta de enlace de Hola.
  * [Establecer el servicio back-end] [ Set backend service] -cambia el servicio back-end de Hola para una solicitud entrante.
  * [Establecer cuerpo] [ Set body] -establece el cuerpo del mensaje de Hola para las solicitudes entrantes y salientes.
  * [Definir el encabezado HTTP] [ Set HTTP header] : asigna una respuesta de valor tooan existente o un encabezado de solicitud o agrega un nuevo encabezado de respuesta y/o de solicitud.
  * [Establecer el parámetro de cadena de consulta][Set query string parameter]: agrega, reemplaza el valor o elimina el parámetro de la cadena de consulta de la solicitud.
  * [Reescribir dirección URL] [ Rewrite URL] -convierte una dirección URL de solicitud desde su formato de toohello de formato público esperado por el servicio web de Hola.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre las expresiones de directiva, vea Hola después de vídeo.

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


