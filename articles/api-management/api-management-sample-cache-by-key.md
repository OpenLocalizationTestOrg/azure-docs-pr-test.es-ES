---
title: "almacenamiento en caché aaaCustom en administración de API de Azure"
description: "Obtenga información acerca de cómo toocache los elementos clave en la administración de API de Azure"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 772bc8dd-5cda-41c4-95bf-b9f6f052bc85
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 681380743c8c96af5d0a8e25948a8c0663e9fd35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="custom-caching-in-azure-api-management"></a>Almacenamiento en caché personalizado en Administración de API de Azure
Servicio de administración de API de Azure tiene compatibilidad integrada para [el almacenamiento en caché de la respuesta HTTP](api-management-howto-cache.md) utilizando la dirección URL del recurso hello como clave de Hola. Hello clave se puede modificar por encabezados de solicitud utilizando hello `vary-by` propiedades. Esto es útil para almacenar en caché todas las respuestas de HTTP (también conocido como representaciones), pero a veces resulta útil toojust caché una parte de una representación. Hola nueva [valor de búsqueda de caché](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) y [valor de almacén de caché](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) directivas proporcionan capacidad de hello toostore y recuperar fragmentos arbitrarios de datos desde dentro de definiciones de directiva. Esta capacidad también agrega toohello valor introducido anteriormente [solicitud de envío](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) directiva porque ahora puede almacenar en caché las respuestas de servicios externos.

## <a name="architecture"></a>Arquitectura
Servicio de administración de API utiliza una caché de datos compartido por inquilino que, cuando se escala toomultiple unidades aún obtendrá acceso toohello mismo datos almacenados en caché. Sin embargo, cuando se trabaja con una implementación de varias regiones son memorias caché independientes en cada una de las regiones de Hola. Due toothis, es importante toonot tratar caché Hola como un almacén de datos, donde es la única fuente de Hola de cierta información. Si se ha y más adelante decide tootake aprovechar la implementación de varias regiones de hello, los clientes con los usuarios que viajan pueden perder acceso a los datos almacenados en memoria caché de toothat.

## <a name="fragment-caching"></a>Almacenamiento en caché de fragmentos
Hay algunos casos donde las respuestas que se devuelven contienen alguna parte de datos que se toodetermine costoso y aún permanecen actualizada para un intervalo de tiempo razonable. Como ejemplo, piense en un servicio creado por una línea aérea que ofrece información relacionada con las reservas de vuelos, estado del vuelo, etc. Si el usuario de hello es miembro del programa de puntos de compañías aéreas de hello, también tendrían información relacionada con kilometraje acumulado y el estado actual de tootheir. Esta información relacionada con el usuario podría almacenarse en un sistema diferente, pero puede ser deseable tooinclude devuelve en respuestas acerca de las reservas y el estado del vuelo. Esto puede hacerse mediante un proceso denominado almacenamiento en caché de fragmentos. Hello representación principal se puede devolver desde el servidor de origen de hello mediante algún tipo de token tooindicate donde obtener información relacionada con el usuario de hello es toobe insertado. 

Considere la posibilidad de hello después de la respuesta JSON de un API de back-end.

```json
{
  "airline" : "Air Canada",
  "flightno" : "871",
  "status" : "ontime",
  "gate" : "B40",
  "terminal" : "2A",
  "userprofile" : "$userprofile$"
}  
```

Y el recurso secundario en `/userprofile/{userid}` que es como sigue,

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

En orden toodetermine Hola usuario correspondiente información tooinclude, necesitamos tooidentify que sea el usuario final de Hola. Este mecanismo depende de la implementación. Por ejemplo, utilizo hello `Subject` de notificación de un `JWT` símbolo (token). 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

Almacenamos este valor `enduserid` en una variable de contexto para su uso posterior. Hola siguiente paso es toodetermine si una solicitud anterior ya recuperar información de usuario de Hola y almacenado en memoria caché de Hola. Para ello se utilice hello `cache-lookup-value` directiva.

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

Si no hay ninguna entrada en memoria caché de Hola que corresponde el valor de clave de toohello y, a continuación, no `userprofile` se creará la variable de contexto. Comprobamos el éxito de Hola de búsqueda de hello mediante hello `choose` directiva de flujo de control.

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

Si hello `userprofile` no existe la variable de contexto, a continuación, se va toohave toomake HTTP solicitud tooretrieve lo.

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points toohello profile for hello current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

Usamos hello `enduserid` recurso de perfil de usuario de tooconstruct Hola URL toohello. Una vez que tenemos respuesta hello, podemos extraer texto del cuerpo Hola fuera de respuesta de Hola y almacenarlo en una variable de contexto.

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

tooavoid nos tener esta solicitud HTTP de toomake nuevo, al mismo usuario hello realiza otra solicitud, podemos almacenar perfil de usuario de hello en memoria caché de Hola.

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

Almacenamos valor hello en memoria caché de hello con hello exacta misma clave que intentamos originalmente tooretrieve con. Hello duración que se elija el valor de hello toostore debe basarse en la frecuencia con hello cambios en la información y cómo tolerante a los usuarios son tooout de información de fecha. 

Es importante toorealize que recuperar de la caché de hello sigue siendo un fuera de proceso, la solicitud de la red y potencialmente, puedes agregar decenas de milisegundos toohello solicitud. ventajas de Hello proceden al determinar información de perfil de usuario de hello tarda significativamente más debido a las consultas de base de datos de toodo tooneeding o agregar información de varios back-end.

Hello último paso en el proceso de hello es hello tooupdate devolvió una respuesta con la información de perfil de usuario.

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

Eligió tooinclude Hola comillas como parte del token de Hola para que incluso cuando no se produce el reemplazo de hello, respuesta de hello era JSON siguen siendo válido. Esto resultaba principalmente toomake depuración.

Una vez que se combinan todos estos pasos juntos, obteniéndose hello es una directiva que es similar a Hola sigue uno.

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in hello cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in hello cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request tooget user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points toohello profile for hello current end-user -->
                    <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),(string)context.Variables["enduserid"]).AbsoluteUri)</set-url>
                    <set-method>GET</set-method>
                </send-request>

                <!-- Store response body in context variable -->
                <set-variable
                  name="userprofile"
                  value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />

                <!-- Store result in cache -->
                <cache-store-value
                  key="@("userprofile-" + context.Variables["enduserid"])"
                  value="@((string)context.Variables["userprofile"])"
                  duration="100000" />
            </when>
        </choose>
        <base />
    </inbound>
    <outbound>
        <!-- Update response body with user profile-->
        <find-and-replace
              from='"$userprofile$"'
              to="@((string)context.Variables["userprofile"])" />
        <base />
    </outbound>
</policies>
```

Este enfoque de almacenamiento en caché se utiliza principalmente en los sitios web donde se compone HTML en el lado del servidor de Hola para que se puede representar como una sola página. Sin embargo, también puede ser útil en donde los clientes no cliente de las API del lado del almacenamiento en caché de HTTP o es deseable no tooput esa responsabilidad en cliente Hola.

Este mismo tipo de almacenamiento en caché de fragmento permite llevar a cabo en servidores web Hola back-end a través de un servidor el almacenamiento en caché de Redis, sin embargo, con tooperform de servicio de administración de API de hello este trabajo es útil si fragmentos de hello en caché provienen de diferentes back-end que Hola respuestas principales.

## <a name="transparent-versioning"></a>Control de versiones transparente
Es una práctica común para varias versiones de implementación diferente de una toobe de API compatibles en cualquier momento. Se trata quizás toosupport distintos entornos, como desarrollo, prueba, producción, etcetera, o puede ser toosupport versiones anteriores de tiempo de toogive Hola API para las versiones de API a los consumidores toomigrate toonewer. 

Un enfoque toohandling de este en su lugar, que requiere direcciones URL de toochange Hola a los desarrolladores de cliente de `/v1/customers` demasiado`/v2/customers` es toostore en los datos de perfil del consumidor de hello qué versión de API de Hola actualmente va toouse y llamar Hola adecuado dirección URL de back-end. En orden toodetermine Hola correcto back-end URL toocall para un cliente determinado, es necesario tooquery algunos datos de configuración. Al almacenar en caché estos datos de configuración, que podemos minimizar la reducción del rendimiento Hola de realizar esta búsqueda.

Hola primer paso es identificador de Hola de toodetermine usa la versión deseada de tooconfigure Hola. En este ejemplo, eligió clave de suscripción de producto de tooassociate Hola versión toohello. 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

A continuación, hacemos una toosee de búsqueda de la memoria caché si ya hemos recuperado versión de cliente deseado Hola.

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

A continuación, comprobamos toosee si no se ha encontrado en la caché de Hola.

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

Si no la encontramos, en este caso procedemos a su recuperación.

```xml
<send-request
    mode="new"
    response-variable-name="clientconfiguresponse"
    timeout="10"
    ignore-error="true">
            <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
            <set-method>GET</set-method>
</send-request>
```

Extraer el texto del cuerpo de respuesta de Hola de respuesta de Hola.

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

Almacene en memoria caché de Hola para un uso futuro.

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

Y finalmente Hola back-end dirección URL tooselect Hola versión actualización del servicio de hello deseado por cliente hello.

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

Hello completamente directiva es como sigue.

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in hello cache, make a request for it and store it -->
    <choose>
        <when condition="@(!context.Variables.ContainsKey("clientversion"))">
            <send-request mode="new" response-variable-name="clientconfiguresponse" timeout="10" ignore-error="true">
                <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
                <set-method>GET</set-method>
            </send-request>
            <!-- Store response body in context variable -->
            <set-variable name="clientversion" value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
            <!-- Store result in cache -->
            <cache-store-value key="@("clientversion-" + context.Variables["clientid"])" value="@((string)context.Variables["clientversion"])" duration="100000" />
        </when>
    </choose>
    <set-backend-service base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
</inbound>
```

Habilitar control de API a los consumidores tootransparently qué versión de back-end está teniendo acceso a los clientes sin necesidad de tooupdate y volver a implementar los clientes es una solución elegante que dirige a muchos problemas de control de versiones de API.

## <a name="tenant-isolation"></a>Aislamiento de inquilinos
En implementaciones grandes multiinquilino algunas compañías crean grupos independientes de inquilinos en distintas implementaciones del hardware de back-end. Esto reduce el número de Hola de clientes que se ven afectados por un problema de hardware en hello back-end. También permite toobe de versiones de software nuevo implantado en fases. Lo ideal es que esta arquitectura de back-end debe ser transparente tooAPI consumidores. Esto se puede lograr de un control de versiones de tootransparent de manera similar porque se basa en hello misma técnica de manipulación de URL de back-end de hello usando el estado de configuración por clave de API.  

En lugar de devolver una versión preferida de hello API para cada clave de la suscripción, debe devolver un identificador que está relacionada con un grupo de hardware de inquilino toohello asignado. Ese identificador puede ser la dirección URL de back-end adecuados de Hola de tooconstruct usado.

## <a name="summary"></a>Resumen
Hola toouse de libertad Hola caché de administración de API de Azure para almacenar cualquier tipo de datos permite un acceso eficiente tooconfiguration que los datos pueden afectar al modo de saludo que se procesa una solicitud entrante. También puede ser usado toostore los fragmentos de datos que pueden aumentar las respuestas, devueltas desde una API de back-end.

## <a name="next-steps"></a>Pasos siguientes
Por favor, envíenos sus comentarios en hello Disqus subproceso de este tema si hay otros escenarios que estas directivas se han habilitado para usted, o si existen escenarios desearía tooachieve pero no se sienta son actualmente posibles.

