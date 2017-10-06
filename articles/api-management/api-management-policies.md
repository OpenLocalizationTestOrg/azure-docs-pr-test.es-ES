---
title: "directivas de administración de API aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de las directivas de hello disponibles para su uso en la administración de API de Azure."
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
ms.openlocfilehash: 1c468ff37d73359f1dd694b91e20c2ca04f8934e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-policies"></a>Directivas de administración de API
En esta sección se proporciona una referencia para hello las siguientes directivas de administración de API. Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](api-management-howto-policies.md).  
  
 Las directivas son una capacidad eficaz del sistema de Hola que permiten a publicador hello toochange comportamiento de Hola de hello API a través de la configuración. Las directivas son una colección de instrucciones que se ejecutan secuencialmente en la solicitud de Hola o respuesta de una API. Las instrucciones más usadas incluyen la conversión de formato de XML tooJSON y llamar a la cantidad de hello toorestrict de llamadas entrantes de un desarrollador de limitación de velocidad. Existen muchas más directivas desde el principio de Hola.  
  
 Las expresiones de directiva se pueden usar como valores de atributo o valores de texto en cualquiera de las directivas de administración de API de hello, a menos que la directiva de Hola se especifique lo contrario. Algunas directivas como hello [flujo de Control](api-management-advanced-policies.md#choose) y [Set variable](api-management-advanced-policies.md#set-variable) directivas basadas en expresiones de directiva. Para más información, consulte [Directivas avanzadas](api-management-advanced-policies.md#AdvancedPolicies) y [Expresiones de directiva](api-management-policy-expressions.md).  
  
##  <a name="ProxyPolicies"></a> Directivas  
  
-   [Directivas de restricción de acceso](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   [Activar encabezado HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) : aplica la existencia o el valor de un encabezado HTTP.  
  
    -   [Limitar la frecuencia de llamadas por suscripción](api-management-access-restriction-policies.md#LimitCallRate) : evita los picos de uso de la API limitando la frecuencia de llamadas, por suscripción.  
  
    -   [Limitar la frecuencia de llamadas por clave](api-management-access-restriction-policies.md#LimitCallRateByKey) : evita los picos de uso de la API limitando la frecuencia de llamadas, por clave.  
  
    -   [Restringir IP de autor de llamada](api-management-access-restriction-policies.md#RestrictCallerIPs) : filtra (permite/deniega) las llamadas de direcciones IP específicas o de intervalos de direcciones.  
  
    -   [Establecer la cuota de uso por suscripción](api-management-access-restriction-policies.md#SetUsageQuota) -permite tooenforce un llamadas renovable o duración volumen o ancho de banda de cuota, por suscripción.  
  
    -   [Establecer la cuota de uso clave](api-management-access-restriction-policies.md#SetUsageQuotaByKey) -permite tooenforce un llamadas renovable o duración volumen o ancho de banda de cuota, de forma por clave.  
  
    -   [Validar JWT](api-management-access-restriction-policies.md#ValidateJWT) : aplica la existencia y la validez de un JWT extraído de un encabezado HTTP especificado o un parámetro de consulta especificado.  
  
-   [Directivas avanzadas](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   [Flujo de control](api-management-advanced-policies.md#choose) : condicionalmente aplica las instrucciones de directiva en función de hello evaluación de expresiones booleanas.  
  
    -   [Reenviar la solicitud](api-management-advanced-policies.md#ForwardRequest) -reenvía el servicio back-end de hello solicitud toohello.  
  
    -   [Inicie sesión tooEvent concentrador](api-management-advanced-policies.md#log-to-eventhub) -envía mensajes de destino de mensaje Hola formato especificado tooa definido por una entidad de registrador.  
  
    -   [Vuelva a intentar](api-management-advanced-policies.md#Retry) -ejecución de reintentos de hello entre las instrucciones de directiva, si y hasta que se cumpla la condición de Hola. Ejecución se repetirá en intervalos de tiempo especificados de Hola y seguridad toohello especificada el número de reintentos.  
  
    -   [Devolver la respuesta](api-management-advanced-policies.md#ReturnResponse) -Hola de ejecución y devuelve de la canalización de anulaciones especificado respuesta directamente toohello autor de la llamada.  
  
    -   [Enviar solicitud unidireccionales](api-management-advanced-policies.md#SendOneWayRequest) -envía una solicitud toohello especificó la dirección URL sin tener que esperar una respuesta.  
  
    -   [Enviar solicitud](api-management-advanced-policies.md#SendRequest) -envía una solicitud toohello URL especificada.  
  
    -   [Set variable](api-management-advanced-policies.md#set-variable) (Establecer variable): conserva un valor en una variable de contexto con nombre para el acceso posterior.  
  
    -   [Establecer el método de solicitud](api-management-advanced-policies.md#SetRequestMethod) -permite toochange método de hello HTTP para una solicitud.  
  
    -   [Código de estado del conjunto de](api-management-advanced-policies.md#SetStatus) -toohello de código de estado HTTP de Hola de cambios de valor especificado.  
  
    -   [Seguimiento](api-management-advanced-policies.md#Trace) -agrega una cadena en hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) salida.  
  
    -   [Espere](api-management-advanced-policies.md#Wait) -espera entre [solicitud de envío](api-management-advanced-policies.md#SendRequest), [obtener el valor de caché](api-management-caching-policies.md#GetFromCacheByKey), o [flujo de Control](api-management-advanced-policies.md#choose) toocomplete directivas antes de continuar.  
  
-   [Directivas de autenticación](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   [Autenticar con opción básica](api-management-authentication-policies.md#Basic) : autenticar con un servicio de back-end mediante la autenticación básica.  
  
    -   [Autenticar con certificado de cliente](api-management-authentication-policies.md#ClientCertificate) : autenticar con un servicio de back-end mediante certificados de cliente.  
  
-   [Directivas de almacenamiento en caché](api-management-caching-policies.md#CachingPolicies)  
  
    -   [Obtener de caché](api-management-caching-policies.md#GetFromCache) : realiza una búsqueda en caché y devuelve una respuesta en caché válida cuando esté disponible.  
  
    -   [Almacenar toocache](api-management-caching-policies.md#StoreToCache) -respuesta de las memorias caché según toohello especifica la configuración de control de caché.  
  
    -   [Obtener valor de caché](api-management-caching-policies.md#GetFromCacheByKey) : recupere un elemento almacenado en caché por clave.  
  
    -   [Valor de almacenar en caché](api-management-caching-policies.md#StoreToCacheByKey) -almacenar un elemento en caché de Hola por clave.  
  
    -   [Quitar el valor de la caché](api-management-caching-policies.md#RemoveCacheByKey) -quitar un elemento en caché de Hola por clave.  
  
-   [Directivas entre dominios](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   [Permitir llamadas entre dominios](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -hace Hola API sea accesible desde clientes basados en exploradores de Adobe Flash y Microsoft Silverlight.  
  
    -   [CORS](api-management-cross-domain-policies.md#CORS) -agrega recursos entre orígenes (CORS) de uso compartido admite la operación de tooan o llama a una API tooallow dominios desde clientes basados en explorador.  
  
    -   [JSONP](api-management-cross-domain-policies.md#JSONP) : agrega JSON con relleno (JSONP) soporte tooan operación o llama a una API tooallow dominios desde clientes basados en exploradores de JavaScript.  
  
-   [Directivas de transformación](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   [Convertir JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) : convierte solicitar o cuerpo de la respuesta de JSON tooXML.  
  
    -   [Convertir XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) : convierte solicitar o cuerpo de la respuesta de XML tooJSON.  
  
    -   [Buscar y reemplazar la cadena en el cuerpo](api-management-transformation-policies.md#Findandreplacestringinbody) : encuentra una subcadena de solicitud o de respuesta y la reemplaza por una subcadena diferente.  
  
    -   [Enmascarar direcciones URL en contenido](api-management-transformation-policies.md#MaskURLSContent) -reescribe (enmascara) vínculos en la respuesta de hello cuerpo para que apunten toohello vínculo equivalente a través de puerta de enlace de Hola.  
  
    -   [Establecer el servicio back-end](api-management-transformation-policies.md#SetBackendService) -cambia el servicio back-end de Hola para una solicitud entrante.  
  
    -   [Establecer cuerpo](api-management-transformation-policies.md#SetBody) -establece el cuerpo del mensaje de Hola para las solicitudes entrantes y salientes.  
  
    -   [Definir el encabezado HTTP](api-management-transformation-policies.md#SetHTTPheader) : asigna una respuesta de valor tooan existente o un encabezado de solicitud o agrega un nuevo encabezado de respuesta y/o de solicitud.  
  
    -   [Establecer el parámetro de cadena de consulta](api-management-transformation-policies.md#SetQueryStringParameter) : agrega, reemplaza el valor o elimina el parámetro de la cadena de consulta de la solicitud.  
  
    -   [Reescribir dirección URL](api-management-transformation-policies.md#RewriteURL) -convierte una dirección URL de solicitud desde su formato de toohello de formato público esperado por el servicio web de Hola.  
  
    -   [Transformar XML mediante una transformación XSLT](api-management-transformation-policies.md#XSLTransform) -se aplica un tooXML de transformación XSL en el cuerpo de solicitud o respuesta Hola.  
  
## <a name="next-steps"></a>Pasos siguientes
Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).  
