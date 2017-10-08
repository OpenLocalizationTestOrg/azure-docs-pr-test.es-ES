---
title: "expresiones de directiva de administración de API aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de las expresiones de las directivas de Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: ea160028-fc04-4782-aa26-4b8329df3448
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 79da0d6ca3963307ec811a33aaac3d63a7abd97d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-policy-expressions"></a>Expresiones de las directivas de API Management
La sintaxis de las expresiones de las directivas es C# 6.0. Cada expresión tiene toohello de acceso proporciona de forma implícita [contexto](api-management-policy-expressions.md#ContextVariables) variable y permitido [subconjunto](api-management-policy-expressions.md#CLRTypes) de tipos de .NET Framework.  
  
> [!NOTE]
>  Para obtener más información acerca de las expresiones de directiva, vea hello [expresiones de directiva](https://azure.microsoft.com/documentation/videos/policy-expressions-in-azure-api-management/) vídeo.  
>   
>  Para ver una demostración de la configuración de directivas que usan expresiones, consulte [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Episodio 177 de Cloud Cover: más características API Management con Vlad Vinogradsky). Este vídeo contiene Hola después demostraciones de expresión de directiva.  
>   
>  -   10:30 - vea cómo Directiva tooapply en API Hola nivel servicio toosupply contexto información toohello back-end mediante hello [establecer el parámetro de cadena de consulta](api-management-transformation-policies.md#SetQueryStringParameter) y [encabezado HTTP establecer](api-management-transformation-policies.md#SetHTTPheader) directivas. No hay una demostración de llamar a una operación de portal para desarrolladores de Hola donde puede ver estas directivas en el trabajo a las 12:10.  
> -   13:50 - vea cómo hello toouse [validar JWT](api-management-access-restriction-policies.md#ValidateJWT) toopre directiva-autorizar toooperations de acceso basado en notificaciones de token. Avance rápido too15:00 las directivas de hello toosee configuradas en el editor de directiva de hello y, a continuación, too18:50 para ver una demostración de la llamada a una operación de portal para desarrolladores de hello con y sin Hola necesario token de autorización.  
> -   21:00 - vea cómo toouse una [API Inspector](https://azure.microsoft.com/documentation/articles/api-management-howto-api-inspector/) toosee cómo las directivas se evalúan y Hola resultados de las evaluaciones de Hola de seguimiento.  
> -   25:25 - vea cómo Hola toouse las expresiones de directiva con [obtener de caché](api-management-caching-policies.md#GetFromCache) y [toocache almacén](api-management-caching-policies.md#StoreToCache) respuesta de administración de API de directivas tooconfigure almacenamiento en caché de duración que coincidencias hello las respuestas en caché de hello servicio de back-end tal y como especifica Hola realizó la copia del servicio `Cache-Control` directiva.  
> -   34:30 - vea cómo contenido tooperform filtrado mediante la eliminación de elementos de datos de respuesta de hello recibido del servicio de back-end de hello mediante hello [flujo de Control](api-management-advanced-policies.md#choose) y [establecer cuerpo](api-management-transformation-policies.md#SetBody) directivas. Iniciar en 31:50 toosee una visión general de [Hola API de previsión de Sky oscuro](https://developer.forecast.io/) utilizada para esta demostración.  
> -   las instrucciones de directiva de hello toodownload utilizadas en este vídeo, consulte hello [api--ejemplos/directivas de administración de](https://github.com/Azure/api-management-samples/tree/master/policies) repositorio de github.  
  
  
##  <a name="Syntax"></a> Sintaxis  
 Las expresiones de declaración única se incluyen en `@(expression)`, donde `expression` es una instrucción de expresión bien formada de C#.  
  
 Las expresiones de múltiples declaraciones se incluyen en `@{expression}`. Todas las rutas de código de las expresiones de múltiples declaraciones deben terminar con una declaración `return`.  
  
##  <a name="PolicyExpressionsExamples"></a> Ejemplos  
  
```  
@(true)  
  
@((1+1).ToString())  
  
@("Hi There".Length)  
  
@(Regex.Match(context.Response.Headers.GetValueOrDefault("Cache-Control",""), @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value)  
  
@(context.Variables.ContainsKey("maxAge") ? int.Parse((string)context.Variables["maxAge"]) : 3600)  
  
@{   
  string value;   
  if (context.Request.Headers.TryGetValue("Authorization", out value))   
  {   
    return Encoding.UTF8.GetString(Convert.FromBase64String(value));  
  }   
  else   
  {   
    return null;  
  }  
}  
```  
  
##  <a name="PolicyExpressionsUsage"></a> Uso  
 Pueden utilizarse expresiones como valores de atributo o valores de texto en cualquiera de administración de API de hello [directivas](api-management-policies.md), a menos que la referencia de la directiva de Hola se especifique lo contrario.  
  
> [!IMPORTANT]
>  Tenga en cuenta que cuando utilice expresiones de directiva, hay solo una comprobación limitada de expresiones de directiva de Hola Hola directiva definida. Dado que las expresiones de Hola se ejecutan en tiempo de ejecución de canalización de entrada o salida de hello puerta de enlace de hello, las excepciones de tiempo de ejecución generadas por las expresiones de directiva Hola producirá un error en tiempo de ejecución en la llamada de hello API.  
  
##  <a name="CLRTypes"></a>Tipos de .NET framework que se permiten en expresiones de directiva  
 Hello tabla siguiente enumeran los tipos de .NET Framework de Hola y los miembros que se permiten en expresiones de directiva.  
  
|Tipos CLR|Métodos admitidos|  
|--------------|-----------------------|  
|Newtonsoft.Json.Linq.Extensions|Se admiten todos los métodos.|  
|Newtonsoft.Json.Linq.JArray|Se admiten todos los métodos.|  
|Newtonsoft.Json.Linq.JConstructor|Se admiten todos los métodos.|  
|Newtonsoft.Json.Linq.JContainer|Se admiten todos los métodos.|  
|Newtonsoft.Json.Linq.JObject|Se admiten todos los métodos.|  
|Newtonsoft.Json.Linq.JProperty|Se admiten todos los métodos.|  
|Newtonsoft.Json.Linq.JRaw|Se admiten todos los métodos.|  
|Newtonsoft.Json.Linq.JToken|Se admiten todos los métodos.|  
|Newtonsoft.Json.Linq.JTokenType|Se admiten todos los métodos.|  
|Newtonsoft.Json.Linq.JValue|Se admiten todos los métodos.|  
|System.Collections.Generic.IReadOnlyCollection<T\>|Todo|  
|System.Collections.Generic.IReadOnlyDictionary<TKey,  TValue>|Todo|  
|System.Collections.Generic.ISet<TKey, TValue>|Todo|  
|System.Collections.Generic.KeyValuePair<TKey,  TValue>|Key, Value.|  
|System.Collections.Generic.List<TKey, TValue>|Todo|  
|System.Collections.Generic.Queue<TKey, TValue>|Todo|  
|System.Collections.Generic.Stack<TKey, TValue>|Todo|  
|System.Convert|Todo|  
|System.DateTime|Todo|  
|System.DateTimeKind|UTC|  
|System.DateTimeOffset|Todo|  
|System.Decimal|Todo|  
|System.Double|Todo|  
|System.Guid|Todo|  
|System.IEnumerable<T\>|Todo|  
|System.IEnumerator<T\>|Todo|  
|System.Int16|Todo|  
|System.Int32|Todo|  
|System.Int64|Todo|  
|System.Linq.Enumerable<T\>|Se admiten todos los métodos.|  
|System.Math|Todo|  
|System.MidpointRounding|Todo|  
|System.Nullable<T\>|Todo|  
|System.Random|Todo|  
|System.SByte|Todo|  
|System.Security.Cryptography. HMACSHA384|Todo|  
|System.Security.Cryptography. HMACSHA512|Todo|  
|System.Security.Cryptography.HashAlgorithm|Todo|  
|System.Security.Cryptography.HMAC|Todo|  
|System.Security.Cryptography.HMACMD5|Todo|  
|System.Security.Cryptography.HMACSHA1|Todo|  
|System.Security.Cryptography.HMACSHA256|Todo|  
|System.Security.Cryptography.KeyedHashAlgorithm|Todo|  
|System.Security.Cryptography.MD5|Todo|  
|System.Security.Cryptography.RNGCryptoServiceProvider|Todo|  
|System.Security.Cryptography.SHA1|Todo|  
|System.Security.Cryptography.SHA1Managed|Todo|  
|System.Security.Cryptography.SHA256|Todo|  
|System.Security.Cryptography.SHA256Managed|Todo|  
|System.Security.Cryptography.SHA384|Todo|  
|System.Security.Cryptography.SHA384Managed|Todo|  
|System.Security.Cryptography.SHA512|Todo|  
|System.Security.Cryptography.SHA512Managed|Todo|  
|System.Single|Todo|  
|System.String|Todo|  
|System.StringSplitOptions|Todo|  
|System.Text.Encoding|Todo|  
|System.Text.RegularExpressions.Capture|Index, Length, Value.|  
|System.Text.RegularExpressions.CaptureCollection|Count, Item.|  
|System.Text.RegularExpressions.Group|Captures, Success.|  
|System.Text.RegularExpressions.GroupCollection|Count, Item.|  
|System.Text.RegularExpressions.Match|Empty, Groups, Result.|  
|System.Text.RegularExpressions.Regex|.ctor, IsMatch, Match, Matches, Replace.|  
|System.Text.RegularExpressions.RegexOptions|Compiled, IgnoreCase, IgnorePatternWhitespace, Multiline, None, RightToLeft, Singleline.|  
|System.TimeSpan|Todo|  
|System.Tuple|Todo|  
|System.UInt16|Todo|  
|System.UInt32|Todo|  
|System.UInt64|Todo|  
|System.Uri|Todo|  
|System.Xml.Linq.Extensions|Se admiten todos los métodos.|  
|System.Xml.Linq.XAttribute|Se admiten todos los métodos.|  
|System.Xml.Linq.XCData|Se admiten todos los métodos.|  
|System.Xml.Linq.XComment|Se admiten todos los métodos.|  
|System.Xml.Linq.XContainer|Se admiten todos los métodos.|  
|System.Xml.Linq.XDeclaration|Se admiten todos los métodos.|  
|System.Xml.Linq.XDocument|Se admiten todos los métodos.|  
|System.Xml.Linq.XDocumentType|Se admiten todos los métodos.|  
|System.Xml.Linq.XElement|Se admiten todos los métodos.|  
|System.Xml.Linq.XName|Se admiten todos los métodos.|  
|System.Xml.Linq.XNamespace|Se admiten todos los métodos.|  
|System.Xml.Linq.XNode|Se admiten todos los métodos.|  
|System.Xml.Linq.XNodeDocumentOrderComparer|Se admiten todos los métodos.|  
|System.Xml.Linq.XNodeEqualityComparer|Se admiten todos los métodos.|  
|System.Xml.Linq.XObject|Se admiten todos los métodos.|  
|System.Xml.Linq.XProcessingInstruction|Se admiten todos los métodos.|  
|System.Xml.Linq.XText|Se admiten todos los métodos.|  
|System.Xml.XmlNodeType|Todo|  
  
##  <a name="ContextVariables"></a> Variable de contexto  
 Una variable denominada `context` está disponible implícitamente en todas las [expresiones](api-management-policy-expressions.md#Syntax) de directiva. Sus miembros proporcionan información pertinente toohello `\request`. Todos los de hello `context` miembros son de solo lectura.  
  
|Variable de contexto|Métodos, propiedades y valores de parámetro admitidos|  
|----------------------|-------------------------------------------------------|  
|contexto|Api: IApi<br /><br /> Implementación<br /><br /> LastError<br /><br /> Operación<br /><br /> Producto<br /><br /> Solicitud<br /><br /> RequestId: cadena<br /><br /> Response<br /><br /> La suscripción<br /><br /> Tracing: bool<br /><br /> Usuario<br /><br /> Variables:IReadOnlyDictionary<cadena, objeto><br /><br /> void Trace(message: cadena)|  
|context.Api|Id: cadena<br /><br /> Name: cadena<br /><br /> Path: cadena<br /><br /> ServiceUrl: IUrl|  
|context.Deployment|Region: cadena<br /><br /> ServiceName: cadena|  
|context.LastError|Source: cadena<br /><br /> Reason: cadena<br /><br /> Message: cadena<br /><br /> Scope: cadena<br /><br /> Section: cadena<br /><br /> Path: cadena<br /><br /> PolicyId: cadena<br /><br /> Para obtener más información sobre context.LastError, consulte [Error handling in API Management policies](api-management-error-handling-policies.md) (Control de errores en directivas de API Management).|  
|context.Operation|Id: cadena<br /><br /> Method: cadena<br /><br /> Name: cadena<br /><br /> UrlTemplate: cadena|  
|context.Product|Apis: IEnumerable<IApi\><br /><br /> ApprovalRequired: bool<br /><br /> Groups: IEnumerable<IGroup\><br /><br /> Id: cadena<br /><br /> Name: cadena<br /><br /> State: enum ProductState {NotPublished, Published}<br /><br /> SubscriptionLimit: int?<br /><br /> SubscriptionRequired: bool|  
|context.Request|Body: IMessageBody<br /><br /> Certificate: System.Security.Cryptography.X509Certificates.X509Certificate2<br /><br /> Headers: IReadOnlyDictionary<cadena, cadena[]><br /><br /> IpAddress: cadena<br /><br /> MatchedParameters: IReadOnlyDictionary<cadena, cadena><br /><br /> Method: cadena<br /><br /> OriginalUrl:IUrl<br /><br /> Url: IUrl|  
|string context.Request.Headers.GetValueOrDefault(headerName: cadena, defaultValue: cadena)|headerName: cadena<br /><br /> defaultValue: cadena<br /><br /> Valores de encabezado de solicitud separados por comas de Devuelve o `defaultValue` si no se encuentra el encabezado de Hola.|  
|context.Response|Body: IMessageBody<br /><br /> Headers: IReadOnlyDictionary<cadena, cadena[]><br /><br /> StatusCode: int<br /><br /> StatusReason: cadena|  
|string context.Response.Headers.GetValueOrDefault(headerName: cadena, defaultValue: cadena)|headerName: cadena<br /><br /> defaultValue: cadena<br /><br /> Devuelve valores de encabezado de respuesta separados por coma o `defaultValue` si no se encuentra el encabezado de Hola.|  
|context.Subscription|CreatedTime: DateTime<br /><br /> EndDate: DateTime?<br /><br /> Id: cadena<br /><br /> Key: cadena<br /><br /> Name: cadena<br /><br /> PrimaryKey: cadena<br /><br /> SecondaryKey: cadena<br /><br /> StartDate: DateTime?|  
|context.User|Email: cadena<br /><br /> FirstName: cadena<br /><br /> Groups: IEnumerable<IGroup\><br /><br /> Id: cadena<br /><br /> Identities: IEnumerable<IUserIdentity\><br /><br /> LastName: cadena<br /><br /> Note: cadena<br /><br /> RegistrationDate: DateTime|  
|IApi|Id: cadena<br /><br /> Name: cadena<br /><br /> Path: cadena<br /><br /> Protocols: IEnumerable<cadena\><br /><br /> ServiceUrl: IUrl<br /><br /> SubscriptionKeyParameterNames: ISubscriptionKeyParameterNames|  
|IGroup|Id: cadena<br /><br /> Name: cadena|  
|IMessageBody|As<T\>(preserveContent: bool = false): donde T: cadena, JObject, JToken, JArray, XNode, XElement, XDocument<br /><br /> Hola `context.Request.Body.As<T>` y `context.Response.Body.As<T>` métodos son utilizado tooread organismos de un mensaje de solicitud y respuesta en un tipo especificado `T`. De forma predeterminada hello secuencia de cuerpo de método usa Hola original mensajes y reneders no está disponible después de devuelve. tooavoid que manteniendo método hello operan en una copia de la secuencia del cuerpo hello, conjunto hello `preserveContent` parámetro demasiado`true`. Vaya [aquí](api-management-transformation-policies.md#SetBody) toosee muestra un ejemplo.|  
|IUrl|Host: cadena<br /><br /> Path: cadena<br /><br /> Port: int<br /><br /> Query: IReadOnlyDictionary<cadena, cadena[]><br /><br /> QueryString: cadena<br /><br /> Scheme: cadena|  
|IUserIdentity|Id: cadena<br /><br /> Provider: cadena|  
|ISubscriptionKeyParameterNames|Header: cadena<br /><br /> Query: cadena|  
|string IUrl.Query.GetValueOrDefault(queryParameterName: cadena, defaultValue: cadena)|queryParameterName: cadena<br /><br /> defaultValue: cadena<br /><br /> Valores de parámetro de consulta separados por comas de Devuelve o `defaultValue` si no se encuentra el parámetro hello.|  
|T context.Variables.GetValueOrDefault<T\>(variableName: cadena, defaultValue: T)|variableName: cadena<br /><br /> defaultValue: T<br /><br /> Devuelve el valor de la variable conversión tootype `T` o `defaultValue` si no se encuentra la variable de saludo.<br /><br /> Este método produce una excepción si hello tipo especificado no coincide con tipo real de Hola de hello devuelve la variable.|  
|BasicAuthCredentials AsBasic(input: esta cadena)|input: cadena<br /><br /> Si el parámetro de entrada de hello contiene un valor válido del encabezado de solicitud de autorización de la autenticación básica HTTP, método hello devuelve un objeto de tipo `BasicAuthCredentials`; en caso contrario, el método hello devuelve null.|  
|bool TryParseBasic(input: esta cadena, result: BasicAuthCredentials de salida)|input: cadena<br /><br /> resultado: out BasicAuthCredentials<br /><br /> Si el parámetro de entrada de hello contiene un valor válido del encabezado de solicitud de autorización de la autenticación básica HTTP, método hello devuelve `true` y parámetro de resultado de hello contiene un valor de tipo `BasicAuthCredentials`; en caso contrario, devuelve el método hello `false`.|  
|BasicAuthCredentials|Password: cadena<br /><br /> UserId: cadena|  
|Jwt AsJwt(input: esta cadena)|input: cadena<br /><br /> Si el parámetro de entrada de hello contiene un valor de token JWT válido, el método hello devuelve un objeto de tipo `Jwt`; en caso contrario, devuelve el método hello `null`.|  
|bool TryParseJwt(input: esta cadena, result: Jwt de salida)|input: cadena<br /><br /> resultado: JWT de salida<br /><br /> Si el parámetro de entrada de hello contiene un valor de token JWT válido, método hello devuelve `true` y parámetro de resultado de hello contiene un valor de tipo `Jwt`; en caso contrario, devuelve el método hello `false`.|  
|Jwt|Algorithm: cadena<br /><br /> Audience: IEnumerable<cadena\><br /><br /> Claims: IReadOnlyDictionary<cadena, cadena[]><br /><br /> ExpirationTime: DateTime?<br /><br /> Id: cadena<br /><br /> Issuer: cadena<br /><br /> NotBefore: DateTime?<br /><br /> Subject: cadena<br /><br /> Type: cadena|  
|cadena Jwt.Claims.GetValueOrDefault(claimName: cadena, defaultValue: cadena)|claimName: cadena<br /><br /> defaultValue: cadena<br /><br /> Devuelve los valores de notificación separados por comas o `defaultValue` si no se encuentra el encabezado de Hola.|

## <a name="next-steps"></a>Pasos siguientes
Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).  
