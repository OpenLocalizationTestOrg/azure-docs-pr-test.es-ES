---
title: "Administración de API de aaaAzure directivas entre dominios | Documentos de Microsoft"
description: "Obtenga información acerca de hello directivas entre dominios disponibles para su uso en la administración de API de Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7689d277-8abe-472a-a78c-e6d4bd43455d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: dd5ebfd65b92ebd0c1f589a2bac669a3928d40b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-cross-domain-policies"></a>Directivas entre dominios de Administración de API
En este tema se proporciona una referencia para hello las siguientes directivas de administración de API. Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="CrossDomainPolicies"></a> Directivas entre dominios  
  
-   [Permitir llamadas entre dominios](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -hace Hola API sea accesible desde clientes basados en exploradores de Adobe Flash y Microsoft Silverlight.  
  
-   [CORS](api-management-cross-domain-policies.md#CORS) -agrega recursos entre orígenes (CORS) de uso compartido admite la operación de tooan o llama a una API tooallow dominios desde clientes basados en explorador.  
  
-   [JSONP](api-management-cross-domain-policies.md#JSONP) : agrega JSON con relleno (JSONP) soporte tooan operación o llama a una API tooallow dominios desde clientes basados en exploradores de JavaScript.  
  
##  <a name="AllowCrossDomainCalls"></a> Allow cross-domain calls (Permitir llamadas entre dominios)  
 Hola de uso `cross-domain` Hola de toomake directiva API que sea accesible desde clientes basados en exploradores de Adobe Flash y Microsoft Silverlight.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a>Ejemplo  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|entre dominios|Elemento raíz. Elementos secundarios deben ajustarse toohello [especificación de archivo de directivas entre dominios de Adobe](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).|Sí|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante  
  
-   **Ámbitos de la directiva:** global  
  
##  <a name="CORS"></a> CORS  
 Hola `cors` directiva agrega recursos entre orígenes (CORS) de uso compartido admite la operación de tooan o llama a una API tooallow dominios desde clientes basados en explorador.  
  
 CORS permite que un explorador y un servidor toointeract y determinar si se permite o no tooallow específicas entre orígenes las solicitudes (es decir, llamadas XMLHttpRequests realizadas desde JavaScript en una página web tooother los dominios). Esto permite más flexibilidad que si solo se permiten solicitudes del mismo origen, pero es más seguro que permitir todas las solicitudes entre orígenes.  
  
### <a name="policy-statement"></a>Declaración de directiva  
  
```xml  
<cors allow-credentials="false|true">  
    <allowed-origins>  
        <origin>origin uri</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="number of seconds">  
        <method>http verb</method>  
    </allowed-methods>  
    <allowed-headers>  
        <header>header name</header>  
    </allowed-headers>  
    <expose-headers>  
        <header>header name</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="example"></a>Ejemplo  
 En este ejemplo se muestra cómo las solicitudes preparatorias toosupport, como aquellos con encabezados personalizados o métodos distintos de GET y POST. encabezados personalizados toosupport y verbos HTTP adicionales, use hello `allowed-methods` y `allowed-headers` secciones tal y como se muestra en el siguiente ejemplo de Hola.  
  
```xml  
<cors allow-credentials="true">  
    <allowed-origins>  
        <!-- Localhost useful for development -->  
        <origin>http://localhost:8080/</origin>  
        <origin>http://example.com/</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="300">  
        <method>GET</method>  
        <method>POST</method>  
        <method>PATCH</method>  
        <method>DELETE</method>  
    </allowed-methods>  
    <allowed-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
        <header>x-zumo-version</header>  
        <header>x-zumo-auth</header>  
        <header>content-type</header>  
        <header>accept</header>  
    </allowed-headers>  
    <expose-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|cors|Elemento raíz.|Sí|N/D|  
|allowed-origins|Contiene `origin` elementos que describen la Hola permitida orígenes para las solicitudes entre dominios. `allowed-origins`puede contener un único `origin` elemento que especifica `*` tooallow cualquier origen, o uno o varios `origin` elementos que contienen un identificador URI.|Sí|N/D|  
|origin|Hello valor puede ser `*` tooallow todos los orígenes o un URI que especifica un único origen. Hola URI debe incluir un esquema, host y puerto.|Sí|Si se omite el puerto de hello en un URI, usa el puerto 80 para HTTP y se utiliza el puerto 443 para HTTPS.|  
|allowed-methods|Este elemento es necesario si se permiten métodos distintos de GET o POST. Contiene `method` elementos que especifican Hola admite verbos HTTP.|No|Si esta sección no está presente, se admiten GET y POST.|  
|estático|Especifica un verbo HTTP.|Al menos un `method` elemento es necesario si hello `allowed-methods` sección está presente.|N/D|  
|allowed-headers|Este elemento contiene `header` elementos especifican nombres de encabezados de Hola que pueden incluirse en la solicitud de saludo.|No|N/D|  
|expose-headers|Este elemento contiene `header` elementos especifican nombres de encabezados de Hola que estarán accesibles por cliente Hola.|No|N/D|  
|encabezado|Especifica un nombre de encabezado.|Al menos un `header` elemento es necesario en `allowed-headers` o `expose-headers` si Hola sección está presente.|N/D|  
  
### <a name="attributes"></a>Attributes  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|allow-credentials|Hola `Access-Control-Allow-Credentials` encabezado de respuesta preparatoria Hola se establezca el valor de este atributo toohello y afecta a credenciales de toosubmit de capacidad del cliente de hello en solicitudes entre dominios.|No|false|  
|preflight-result-max-age|Hola `Access-Control-Max-Age` encabezado de respuesta preparatoria Hola se establezca el valor de este atributo toohello y afectan a la respuesta preparatoria del agente de usuario de hello capacidad toocache.|No|0|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** entrante  
  
-   **Ámbitos de la directiva:** API, operación  
  
##  <a name="JSONP"></a> JSONP  
 Hola `jsonp` directiva agrega JSON con relleno de la operación de tooan de soporte (JSONP) o un llamadas a API tooallow entre dominios desde clientes basados en exploradores de JavaScript. JSONP es un método utilizado en los datos de toorequest de programas de JavaScript de un servidor en un dominio diferente. JSONP omite la limitación de hello aplicada por la mayoría de los exploradores web que las páginas de tooweb de acceso deben tener Hola mismo dominio.  
  
### <a name="policy-statement"></a>Instrucción de la directiva  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a>Ejemplo  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 Si llama al método hello sin el parámetro de devolución de llamada de hello? cb = XXX, devolverá JSON sin formato (sin un contenedor de llamadas de función).  
  
 Si agrega el parámetro de devolución de llamada de hello `?cb=XXX` devolverá un resultado JSONP, ajuste resultados JSON originales de hello alrededor de la función de devolución de llamada de hello como`XYZ('<json result goes here>');`  
  
### <a name="elements"></a>Elementos  
  
|Nombre|Descripción|Obligatorio|  
|----------|-----------------|--------------|  
|jsonp|Elemento raíz.|Sí|  
  
### <a name="attributes"></a>Atributos  
  
|Nombre|Descripción|Obligatorio|Valor predeterminado|  
|----------|-----------------|--------------|-------------|  
|callback-parameter-name|Hello llamada de función de JavaScript entre dominios como prefijo con el nombre de dominio completo de Hola donde hello función reside.|Sí|N/D|  
  
### <a name="usage"></a>Uso  
 Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Secciones de la directiva:** outbound  
  
-   **Ámbitos de la directiva:** global, producto, API, operación  
  
## <a name="next-steps"></a>Pasos siguientes
Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).  