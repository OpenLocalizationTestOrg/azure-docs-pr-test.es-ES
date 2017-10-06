---
title: "directivas de almacenamiento en caché de administración de API aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de hello almacenamiento en caché de directivas disponibles para su uso en la administración de API de Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: bd6b0721945609b28dbf6e7ef0631979c08c8c65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-caching-policies"></a>Directivas de almacenamiento en caché de API Management
En este tema se proporciona una referencia para hello las siguientes directivas de administración de API. Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="CachingPolicies"></a> Directivas de almacenamiento en caché  
  
-   Directivas de almacenamiento en caché de respuesta  
  
    -   [Get from cache](api-management-caching-policies.md#GetFromCache): realiza una búsqueda en caché y devuelve una respuesta en caché válida cuando está disponible.  
  
    -   [Almacenar toocache](api-management-caching-policies.md#StoreToCache) : las respuestas de las memorias caché según la configuración de control de caché especificado toohello.  
  
-   Directivas de almacenamiento en caché de valores  
  
    -   [Obtener valor de caché](#GetFromCacheByKey) : recupere un elemento almacenado en caché por clave.  
  
    -   [Valor de almacenar en caché](#StoreToCacheByKey) -almacenar un elemento en caché de Hola por clave.  
  
    -   [Quitar el valor de la caché](#RemoveCacheByKey) -quitar un elemento en caché de Hola por clave.  
  
##  <a name="GetFromCache"></a> Get from cache  
 Hola de uso `cache-lookup` caché de directiva tooperform buscar y devolver una respuesta almacenada en caché válida si está disponible. Esta directiva se puede aplicar en aquellos casos en los que el contenido de respuesta permanezca estático durante un período de tiempo. Las respuestas en caché reducen el ancho de banda y los requisitos de procesamiento impuesta en hello back-end web server y reduce la latencia percibida por los consumidores de API.  
  
> [!NOTE]
>  Esta directiva debe tener su correspondiente [toocache almacén](api-management-caching-policies.md#StoreToCache) directiva.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression tooevaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-authorized-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a>Ejemplos  
  
#### <a name="example"></a>Ejemplo  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="none" must-revalidate="true">  
            <vary-by-query-parameter>version</vary-by-query-parameter>  
        </cache-lookup>           
    </inbound>  
    <outbound>  
        <cache-store duration="seconds" />  
        <base />          
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>Ejemplo de uso de expresiones de directiva  
 Este ejemplo muestra cómo hacer las respuesta de administración de API tootooconfigure almacenamiento en caché de duración que coincidencias hello las respuestas en caché del servicio de back-end de hello según lo especificado por Hola de seguridad del servicio `Cache-Control` directiva. Para ver una demostración de cómo configurar y usar esta directiva, consulte [177 episodio abarcan de nube: más características de administración de API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avancemos too25:25.  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 Para obtener más información, consulte [Policy expressions](api-management-policy-expressions.md) (Expresiones de política) y [Context variable](api-management-policy-expressions.md#ContextVariables) (Variable de contexto).  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|cache-lookup|Elemento raíz.|Sí|  
|vary-by-header|Inicia el almacenamiento en caché de respuestas por valor del encabezado especificado, por ejemplo, Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.|No|  
|vary-by-query-parameter|Inicia el almacenamiento en caché de las respuestas por valor de los parámetros de consulta especificados. Permite introducir uno o varios parámetros. Utilice el punto y coma como separador. Si no se especifica ninguno, se usan todos los parámetros de consulta.|No|  
  
### <a name="attributes"></a>Attributes  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|allow-private-response-caching|Cuando se establece demasiado`true`, permite el almacenamiento en caché de las solicitudes que contienen un encabezado de autorización.|No|false|  
|downstream-caching-type|Este atributo debe establecerse tooone de hello después de valores.<br /><br /> -   none: no se permite el almacenamiento en caché de bajada.<br />-   private: se permite el almacenamiento en caché de bajada privado.<br />-   public: se permite el almacenamiento en caché de bajada privado y compartido.|No|Ninguna|  
|must-revalidate|Cuando se habilita el almacenamiento en caché descendente este atributo activa o desactiva hello `must-revalidate` directiva de control de caché en las respuestas de la puerta de enlace.|No|true|  
|vary-by-developer|Establecer demasiado`true` toocache respuestas por clave de desarrollador.|No|false|  
|vary-by-developer-groups|Establecer demasiado`true` toocache respuestas por función de usuario.|No|false|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante  
  
-   **Ámbitos de directiva:** API, operation, product  
  
##  <a name="StoreToCache"></a>Toocache almacén  
 Hola `cache-store` según toohello las respuestas de las memorias caché de directiva especifica la configuración de la caché. Esta directiva se puede aplicar en aquellos casos en los que el contenido de respuesta permanezca estático durante un período de tiempo. Las respuestas en caché reducen el ancho de banda y los requisitos de procesamiento impuesta en hello back-end web server y reduce la latencia percibida por los consumidores de API.  
  
> [!NOTE]
>  Esta directiva debe tener una directiva [Get from cache](api-management-caching-policies.md#GetFromCache) correspondiente.  
  
### <a name="policy-statement"></a>Declaración de directiva  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a>Ejemplos  
  
#### <a name="example"></a>Ejemplo  
  
```xml  
<policies>  
    <inbound>  
        <base />  
          <cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false">  
                <vary-by-query-parameter>parameter name</vary-by-query-parameter> <!-- optional, can repeated several times -->  
        </cache-lookup>  
    </inbound>  
    <outbound>  
        <base />  
            <cache-store duration="3600" />  
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>Ejemplo de uso de expresiones de directiva  
 Este ejemplo muestra cómo hacer las respuesta de administración de API tootooconfigure almacenamiento en caché de duración que coincidencias hello las respuestas en caché del servicio de back-end de hello según lo especificado por Hola de seguridad del servicio `Cache-Control` directiva. Para ver una demostración de cómo configurar y usar esta directiva, consulte [177 episodio abarcan de nube: más características de administración de API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avancemos too25:25.  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 Para obtener más información, consulte [Policy expressions](api-management-policy-expressions.md) (Expresiones de política) y [Context variable](api-management-policy-expressions.md#ContextVariables) (Variable de contexto).  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|cache-store|Elemento raíz.|Sí|  
  
### <a name="attributes"></a>Atributos  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|duration|Tiempo de vida del programa Hola a almacenar en caché las entradas, especificadas en segundos.|Sí|N/D|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** outbound  
  
-   **Ámbitos de directiva:** API, operation, product  
  
##  <a name="GetFromCacheByKey"></a> Get value from cache (Obtener valor de la caché)  
 Hola de uso `cache-lookup-value` tooperform directiva caché búsqueda por clave y devolver un valor almacenado en caché. clave de Hello puede tener un valor de cadena arbitraria y se proporciona normalmente mediante una expresión de directiva.  
  
> [!NOTE]
>  Esta directiva debe tener una directiva [Store value in cache](#StoreToCacheByKey) (Almacenar valor en la caché) correspondiente.  
  
### <a name="policy-statement"></a>Declaración de directiva  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a>Ejemplo  
 Para más información y ver ejemplos de esta directiva, consulte [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/) (Almacenamiento en caché personalizado en Azure API Management).  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|cache-lookup-value|Elemento raíz.|Sí|  
  
### <a name="attributes"></a>Atributos  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|default-value|Un valor que se va a asignar toohello variable si generó un error de búsqueda de claves de caché de Hola. Si no se especifica este atributo, se asigna `null`.|No|`null`|  
|key|Almacenar en caché toouse de valor de clave en la búsqueda de Hola.|Sí|N/D|  
|variable-name|Nombre del programa Hola a [variable de contexto](api-management-policy-expressions.md#ContextVariables) Hola buscado valor se asignará a, si la búsqueda es correcta. Si se produce un error de búsqueda, se asignará variable Hola valor Hola de hello `default-value` atributo o `null`, si hello `default-value` se omite el atributo.|Sí|N/D|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante, saliente, back-end y en caso de error  
  
-   **Ámbitos de la directiva:** global, API, operación, producto  
  
##  <a name="StoreToCacheByKey"></a> Store value in cache (Almacenar valor en la caché)  
 Hola `cache-store-value` realiza el almacenamiento en caché por clave. clave de Hello puede tener un valor de cadena arbitraria y se proporciona normalmente mediante una expresión de directiva.  
  
> [!NOTE]
>  Esta directiva debe tener una directiva [Get from cache](#GetFromCacheByKey) (Obtener de la caché) correspondiente.  
  
### <a name="policy-statement"></a>Declaración de directiva  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a>Ejemplo  
 Para más información y ver ejemplos de esta directiva, consulte [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/) (Almacenamiento en caché personalizado en Azure API Management).  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|cache-store-value|Elemento raíz.|Sí|  
  
### <a name="attributes"></a>Atributos  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|duration|Valor se almacenarán en caché para hello proporcionada el valor de duración, especificado en segundos.|Sí|N/D|  
|key|Valor de clave Hola de caché se almacenarán en.|Sí|N/D|  
|value|Hola toobe de valor almacenado en memoria caché.|Sí|N/D|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante, saliente, back-end y en caso de error  
  
-   **Ámbitos de la directiva:** global, API, operación, producto  
  
###  <a name="RemoveCacheByKey"></a> Remove value from cache (Quitar valor de la caché)  
 Hola `cache-remove-value` elimina un elemento almacenado en caché identificado por su clave. clave de Hello puede tener un valor de cadena arbitraria y se proporciona normalmente mediante una expresión de directiva.  
  
#### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a>Ejemplo  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|cache-remove-value|Elemento raíz.|Sí|  
  
#### <a name="attributes"></a>Atributos  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|key|clave de Hola de hello previamente en caché toobe valor quitado de la memoria caché de Hola.|Sí|N/D|  
  
#### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .  
  
-   **Secciones de la directiva:** entrante, saliente, back-end y en caso de error  
  
-   **Ámbitos de la directiva:** global, API, operación, producto  
  

## <a name="next-steps"></a>Pasos siguientes
Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).  