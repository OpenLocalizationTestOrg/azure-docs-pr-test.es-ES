---
title: "aaaError control en las directivas de administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo Hola a toorespond tooerror condiciones que pueden producirse durante el procesamiento de solicitudes de administración de API de Azure."
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
ms.openlocfilehash: 002c65f21e763fd644da61b6a11685ffd97488c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-api-management-policies"></a>Control de errores en las directivas de API Management
Administración de API de Azure permite a los editores toorespond tooerror condiciones que pueden producirse durante el procesamiento de Hola de proxy de solicitudes toohello proporcionando un `ProxyError` objeto. Hola `ProxyError` objeto se accede a través de hello [contexto. ÚltErr](api-management-policy-expressions.md#ContextVariables) propiedad y puede utilizarse en las directivas de hello `on-error` sección sobre la directiva. Este tema proporciona una referencia para el error de hello capacidades de control en la administración de API de Azure.  
  
## <a name="error-handling-in-api-management"></a>Control de errores en API Management  
 Las directivas de administración de API de Azure se dividen en `inbound`, `backend`, `outbound`, y `on-error` secciones tal y como se muestra en el siguiente ejemplo de Hola.  
  
```xml  
<policies>  
  <inbound>  
    <!-- statements toobe applied toohello request go here -->  
  </inbound>  
  <backend>  
    <!-- statements toobe applied before hello request is   
         forwarded toohello backend service go here -->  
    </backend>  
    <outbound>  
      <!-- statements toobe applied toohello response go here -->  
    </outbound>  
    <on-error>  
        <!-- statements toobe applied if there is an error   
             condition go here -->  
  </on-error>  
</policies>  
```  
  
 Durante el procesamiento de Hola de una solicitud, se ejecutan pasos integradas junto con las directivas que pertenecen al ámbito de la solicitud de saludo. Si se produce un error, el procesamiento inmediatamente salta toohello `on-error` sección sobre la directiva. Hola `on-error` sección directiva puede usarse en cualquier ámbito y publicadores de API pueden configurar el comportamiento personalizado como registro de los centros de hello error tooevent o crear una nueva respuesta tooreturn toohello autor de la llamada.  
  
> [!NOTE]
>  Hola `on-error` sección no está presente en las directivas de forma predeterminada. Hola tooadd `on-error` sección Directiva tooa, busque la directiva toohello deseado en el editor de directiva de Hola y agregarlo. Para más información sobre cómo configurar directivas, consulte [Directivas en API Management](https://azure.microsoft.com/documentation/articles/api-management-howto-policies/).  
>   
>  Si no hay ninguna sección `on-error`, los autores de la llamada recibirán mensajes de respuesta HTTP 400 o 500 si se produce una condición de error.  
  
### <a name="policies-allowed-in-on-error"></a>Directivas permitidas en on-error  
 Hello las directivas siguientes pueden usarse en hello `on-error` sección sobre la directiva.  
  
-   [choose](api-management-advanced-policies.md#choose)  
  
-   [set-variable](api-management-advanced-policies.md#set-variable)  
  
-   [find-and-replace](api-management-transformation-policies.md#Findandreplacestringinbody)  
  
-   [return-response](api-management-advanced-policies.md#ReturnResponse)  
  
-   [set-header](api-management-transformation-policies.md#SetHTTPheader)  
  
-   [set-method](api-management-advanced-policies.md#SetRequestMethod)  
  
-   [set-status](api-management-advanced-policies.md#SetStatus)  
  
-   [send-request](api-management-advanced-policies.md#SendRequest)  
  
-   [send-one-way-request](api-management-advanced-policies.md#SendOneWayRequest)  
  
-   [log-to-eventhub](api-management-advanced-policies.md#log-to-eventhub)  
  
-   [json-to-xml](api-management-transformation-policies.md#ConvertJSONtoXML)  
  
-   [xml-to-json](api-management-transformation-policies.md#ConvertXMLtoJSON)  
  
## <a name="lasterror"></a>LastError  
 Cuando se produce un error y el control salta toohello `on-error` sección Directiva, error de Hola se almacena en [contexto. ÚltErr](api-management-policy-expressions.md#ContextVariables) propiedad que puede tener acceso a las directivas de hello `on-error` sección y tiene Hola propiedades siguientes.  
  
|Nombre|Tipo|Descripción|Obligatorio|  
|----------|----------|-----------------|--------------|  
|Origen|cadena|Elemento de Hola de nombres donde se produjo el error de Hola. Puede ser el nombre de una directiva o el nombre de un paso de canalización integrado.|Sí|  
|Motivo|string|Código de error reconocible por la máquina, que se puede utilizar en el control de errores.|No|  
|Message|string|Descripción del error legible para el usuario.|Sí|  
|Scope|cadena|Nombre del ámbito de Hola donde error Hola se produjo y puede ser uno de "global", "producto", "api" o "operación"|No|  
|Sección|string|Nombre de la sección donde se produjo el error; podría ser: "entrada", "back-end", "salida" o "error".|No|  
|Ruta de acceso|string|Especifica directivas anidadas, por ejemplo, "choose[3]/when[2]".|No|  
|PolicyId|cadena|Valor de hello `id` atributo, si se especifica por el cliente de hello, en la directiva de Hola donde se produjo el error|No|  
  
> [!NOTE]
>  Todas las directivas tienen opcional `id` atributo que se pueden agregar elemento de raíz toohello de directiva de Hola. Si este atributo está presente en una directiva cuando se produce una condición de error, valor de hello del atributo de hello puede recuperarse utilizando hello `context.LastError.PolicyId` propiedad.  
  
## <a name="predefined-errors-for-built-in-steps"></a>Errores predefinidos para pasos integrados  
 Hello están predefinidos siguientes errores para condiciones de error que se pueden producir durante la evaluación de Hola de pasos de procesamiento integrados.  
  
|Origen|Condición|Motivo|Message|  
|------------|---------------|------------|-------------|  
|configuración|URI no coincide con tooany Api u operación|OperationNotFound|Operación de tooan de solicitud entrante no se puede toomatch.|  
|authorization|No se ha proporcionado la clave de suscripción.|SubscriptionKeyNotFound|Acceso denegado debido a toomissing clave de la suscripción. Establecer como clave de suscripción tooinclude seguro al realizar solicitudes toothis API.|  
|authorization|El valor de la clave de suscripción no es válido.|SubscriptionKeyInvalid|Acceso denegado debido a tooinvalid clave de la suscripción. Asegúrese de que tooprovide una clave válida para una suscripción activa.|  
  
## <a name="predefined-errors-for-policies"></a>Errores predefinidos en directivas  
 Hello están predefinidos siguientes errores para condiciones de error que pueden producirse durante la evaluación de la directiva.  
  
|Origen|Condición|Motivo|Message|  
|------------|---------------|------------|-------------|  
|rate-limit|Límite de velocidad excedido|RateLimitExceeded|Rate limit is exceeded (Se ha excedido el límite de velocidad).|  
|quota|Cuota superada|QuotaExceeded|Out of call volume quota. (Fuera de la cuota de volumen de la llamada.) La cuota se reabastecerá en xx:xx:xx. O bien, Out of bandwidth quota (Fuera de la cuota de ancho de banda). La cuota se reabastecerá en xx:xx:xx.|  
|jsonp|El valor del parámetro de devolución de llamada no es válido (contiene caracteres incorrectos).|CallbackParameterInvalid|Value of callback parameter {callback-parameter-name} is not a valid JavaScript identifier (El valor del parámetro de devolución de llamada {callback-parameter-name} no es un identificador de JavaScript válido).|  
|ip-filter|IP de autor de llamada de tooparse errores de solicitud|FailedToParseCallerIP|No se pudo tooestablish dirección IP para el llamador de Hola. Acceso denegado.|  
|ip-filter|La IP del autor de la llamada no está en la lista de permitidos.|CallerIpNotAllowed|Caller IP address {ip-address} is not allowed. Access denied (No se permite la IP del autor de la llamada {ip-address}. Acceso denegado).|  
|ip-filter|La IP del autor de la llamada está en la lista de bloqueados.|CallerIpBlocked|Caller IP address is blocked. Access denied (La IP del autor de la llamada está bloqueada. Acceso denegado).|  
|check-header|El encabezado necesario no está presente o falta un valor.|HeaderNotFound|No se encontró el encabezado {encabezado-name} en la solicitud de Hola. Acceso denegado.|  
|check-header|El encabezado necesario no está presente o falta un valor.|HeaderValueNotAllowed|Header {header-name} value of {header-value} is not allowed. Access denied (No se permite el valor {header-name} del encabezado de {header-value}. Acceso denegado).|  
|validate-jwt|Falta el token Jwt en la solicitud.|TokenNotFound|JWT no se encuentra en la solicitud de saludo. Acceso denegado.|  
|validate-jwt|Error de validación de contraseña.|TokenSignatureInvalid|<mensaje de la biblioteca de jwt\>. Acceso denegado.|  
|validate-jwt|Audiencia no válida.|TokenAudienceNotAllowed|<mensaje de la biblioteca de jwt\>. Acceso denegado.|  
|validate-jwt|Emisor no válido|TokenIssuerNotAllowed|<mensaje de la biblioteca de jwt\>. Acceso denegado.|  
|validate-jwt|Token expirado|TokenExpired|<mensaje de la biblioteca de jwt\>. Acceso denegado.|  
|validate-jwt|La clave de firma no se resolvió por el id.|TokenSignatureKeyNotFound|<mensaje de la biblioteca de jwt\>. Acceso denegado.|  
|validate-jwt|Faltan las notificaciones necesarias del token.|TokenClaimNotFound|Token de JWT falta Hola siguientes notificaciones: < c1\>, < c2\>,... Acceso denegado.|  
|validate-jwt|Error de coincidencia de valores de notificación.|TokenClaimValueNotAllowed|Claim {claim-name} value of {claim-value} is not allowed. Acceso denegado.|  
|validate-jwt|Otros errores de validación|JwtInvalid|<mensaje de la biblioteca de jwt\>.|

## <a name="next-steps"></a>Pasos siguientes
Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).  