---
title: "Almacenamiento en caché personalizado en Administración de API de Azure"
description: "Aprenda a almacenar en caché elementos por clave en Administración de API de Azure"
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
ms.openlocfilehash: f5d5f44e34fbcd122a10be0ca5b3001760c4c64d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="0b0f1-103">Almacenamiento en caché personalizado en Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="0b0f1-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="0b0f1-104">El servicio Administración de API de Azure integra compatibilidad para [el almacenamiento en caché de respuestas HTTP](api-management-howto-cache.md) mediante el uso de la dirección URL como clave.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using the resource URL as the key.</span></span> <span data-ttu-id="0b0f1-105">La clave se puede modificar por los encabezados de solicitud con las propiedades `vary-by` .</span><span class="sxs-lookup"><span data-stu-id="0b0f1-105">The key can be modified by request headers using the `vary-by` properties.</span></span> <span data-ttu-id="0b0f1-106">Esto es útil para almacenar en caché las respuestas HTTP completas (también conocidas como representaciones), pero a veces resulta útil almacenar en caché solo una parte de una representación.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful to just cache a portion of a representation.</span></span> <span data-ttu-id="0b0f1-107">Las nuevas directivas [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) y [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) permiten almacenar y recuperar fragmentos arbitrarios de datos desde las definiciones de directiva.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-107">The new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide the ability to store and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="0b0f1-108">Esta capacidad también agrega valor a la directiva [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) previamente introducida porque ahora se puede almacenar en caché las respuestas desde servicios externos.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-108">This ability also adds value to the previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="0b0f1-109">Arquitectura</span><span class="sxs-lookup"><span data-stu-id="0b0f1-109">Architecture</span></span>
<span data-ttu-id="0b0f1-110">El servicio Administración de API usa una caché de datos compartida por inquilino que, cuando escale verticalmente a varias unidades, seguirá obteniendo acceso a los mismos datos almacenados en caché.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-110">API Management service uses a shared per-tenant data cache so that, as you scale up to multiple units you will still get access to the same cached data.</span></span> <span data-ttu-id="0b0f1-111">Sin embargo, cuando se trabaja con una implementación de varias regiones son memorias caché independientes dentro de cada una de las regiones.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-111">However, when working with a multi-region deployment there are independent caches within each of the regions.</span></span> <span data-ttu-id="0b0f1-112">Debido a esto, es importante no tratar la memoria caché como un almacén de datos, donde está el único origen de información.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-112">Due to this, it is important to not treat the cache as a data store, where it is the only source of some piece of information.</span></span> <span data-ttu-id="0b0f1-113">Sin embargo, si ya lo hizo y más adelante decide aprovechar las ventajas de la implementación en varias regiones, es posible que los clientes con los usuarios que viajan puedan perder el acceso a los datos almacenados en caché.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-113">If you did, and later decided to take advantage of the multi-region deployment, then customers with users that travel may lose access to that cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="0b0f1-114">Almacenamiento en caché de fragmentos</span><span class="sxs-lookup"><span data-stu-id="0b0f1-114">Fragment caching</span></span>
<span data-ttu-id="0b0f1-115">Hay algunos casos donde las respuestas que se devuelven contienen parte de datos que es costoso determinar y todavía siguen actualizadas durante un tiempo razonable.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-115">There are certain cases where responses being returned contain some portion of data that is expensive to determine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="0b0f1-116">Como ejemplo, piense en un servicio creado por una línea aérea que ofrece información relacionada con las reservas de vuelos, estado del vuelo, etc. Si el usuario es miembro del programa de puntos de la compañía aérea, tendría además información relativa a su estado actual y a las millas acumuladas.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If the user is a member of the airlines points program, they would also have information relating to their current status and mileage accumulated.</span></span> <span data-ttu-id="0b0f1-117">Esta información relacionada con el usuario se puede almacenar en un sistema diferente, pero quizá sea deseable incluirlo en las respuestas devueltas sobre las reservas y el estado de los vuelos.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-117">This user-related information might be stored in a different system, but it may be desirable to include it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="0b0f1-118">Esto puede hacerse mediante un proceso denominado almacenamiento en caché de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="0b0f1-119">La representación principal puede devolverse desde el servidor de origen mediante algún tipo de token para indicar donde se insertará la información relacionada con el usuario.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-119">The primary representation can be returned from the origin server using some kind of token to indicate where the user-related information is to be inserted.</span></span> 

<span data-ttu-id="0b0f1-120">Considere la siguiente respuesta JSON de una API de back-end.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-120">Consider the following JSON response from a backend API.</span></span>

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

<span data-ttu-id="0b0f1-121">Y el recurso secundario en `/userprofile/{userid}` que es como sigue,</span><span class="sxs-lookup"><span data-stu-id="0b0f1-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="0b0f1-122">Para determinar la información de usuario adecuada que se va a incluir, es necesario identificar quién es el usuario final.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-122">In order to determine the appropriate user information to include, we need to identify who the end user is.</span></span> <span data-ttu-id="0b0f1-123">Este mecanismo depende de la implementación.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="0b0f1-124">Por ejemplo, estamos usando la notificación `Subject` de un token `JWT`.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-124">As an example, I am using the `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="0b0f1-125">Almacenamos este valor `enduserid` en una variable de contexto para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="0b0f1-126">El siguiente paso es determinar si una solicitud anterior ya ha recuperado la información de usuario y la ha almacenado en la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-126">The next step is to determine if a previous request has already retrieved the user information and stored it in the cache.</span></span> <span data-ttu-id="0b0f1-127">Para ello, usamos la directiva `cache-lookup-value` .</span><span class="sxs-lookup"><span data-stu-id="0b0f1-127">For this we use the `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="0b0f1-128">Si no hay ninguna entrada en la memoria caché que se corresponda con el valor de clave, no se creará la variable de contexto `userprofile` .</span><span class="sxs-lookup"><span data-stu-id="0b0f1-128">If there is no entry in the cache that corresponds to the key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="0b0f1-129">Comprobamos el éxito de la búsqueda mediante la directiva de flujo de control `choose` .</span><span class="sxs-lookup"><span data-stu-id="0b0f1-129">We check the success of the lookup using the `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If the userprofile context variable doesn’t exist, make an HTTP request to retrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="0b0f1-130">Si la variable de contexto `userprofile` no existe, tenemos que realizar una solicitud HTTP para recuperarla.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-130">If the `userprofile` context variable doesn’t exist, then we are going to have to make an HTTP request to retrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points to the profile for the current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="0b0f1-131">Usamos `enduserid` para construir la dirección URL en el recurso del perfil de usuario.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-131">We use the `enduserid` to construct the URL to the user profile resource.</span></span> <span data-ttu-id="0b0f1-132">Una vez que tengamos la respuesta, podemos extraer el texto del cuerpo de la respuesta y almacenarlo en una variable de contexto.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-132">Once we have the response, we can pull the body text out of the response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="0b0f1-133">Para evitar que tengamos que realizar esta solicitud HTTP de nuevo, cuando el mismo usuario realiza otra solicitud, podemos almacenar el perfil de usuario en la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-133">To avoid us having to make this HTTP request again, when the same user makes another request, we can store the user profile in the cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="0b0f1-134">El valor se almacena en la memoria caché con la misma clave que hemos intentado recuperar originalmente.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-134">We store the value in the cache using the exact same key that we originally attempted to retrieve it with.</span></span> <span data-ttu-id="0b0f1-135">La duración que elegimos para almacenar el valor debe basarse en la frecuencia de los cambios de información y en lo tolerantes que son los usuarios con la información sin actualizar.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-135">The duration that we choose to store the value should be based on how often the information changes and how tolerant users are to out of date information.</span></span> 

<span data-ttu-id="0b0f1-136">Es importante tener en cuenta que la recuperación desde la caché sigue siendo una solicitud de red fuera del proceso y posiblemente pueda agregar decenas de milisegundos a la solicitud.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-136">It is important to realize that retrieving from the cache is still an out-of-process, network request and potentially can still add tens of milliseconds to the request.</span></span> <span data-ttu-id="0b0f1-137">Las ventajas se derivan de determinar que la información de perfil de usuario dura bastante más que eso, debido a que se necesitan realizar consultas en la base de datos o agregar información de varios back-end.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-137">The benefits come when determining the user profile information takes significantly longer than that due to needing to do database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="0b0f1-138">El último paso del proceso consiste en actualizar la respuesta devuelta con nuestra información de perfil de usuario.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-138">The final step in the process is to update the returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="0b0f1-139">Elegí incluir las comillas como parte del token para que incluso cuando no se produzca el reemplazo, la respuesta siga siendo un JSON válido.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-139">I chose to include the quotation marks as part of the token so that even when the replace doesn’t occur, the response was still valid JSON.</span></span> <span data-ttu-id="0b0f1-140">El motivo principalmente fue facilitar la depuración.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-140">This was primarily to make debugging easier.</span></span>

<span data-ttu-id="0b0f1-141">Una vez que se combinan todos estos pasos, el resultado final es una directiva similar a la siguiente.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-141">Once you combine all these steps together, the end result is a policy that looks like the following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in the cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in the cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request to get user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points to the profile for the current end-user -->
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

<span data-ttu-id="0b0f1-142">Este enfoque de almacenamiento en caché se utiliza principalmente en los sitios web donde se compone HTML en el servidor para que se pueda representar como una sola página.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-142">This caching approach is primarily used in web sites where HTML is composed on the server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="0b0f1-143">Sin embargo, también puede ser útil en las API donde los clientes no pueden realizar almacenamiento en caché de HTTP en el cliente o sea deseable que la responsabilidad no recaiga en el cliente.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not to put that responsibility on the client.</span></span>

<span data-ttu-id="0b0f1-144">Este mismo tipo de almacenamiento en caché también puede realizarse en los servidores web de back-end con un servidor de Caché en Redis; sin embargo, el uso del servicio Administración de API para realizar este trabajo resulta útil cuando los fragmentos en caché proceden de servidores back-end distintos a los de las respuestas principales.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-144">This same kind of fragment caching can also be done on the backend web servers using a Redis caching server, however, using the API Management service to perform this work is useful when the cached fragments are coming from different back-ends than the primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="0b0f1-145">Control de versiones transparente</span><span class="sxs-lookup"><span data-stu-id="0b0f1-145">Transparent versioning</span></span>
<span data-ttu-id="0b0f1-146">Es una práctica común que se admitan al mismo tiempo varias versiones de implementación distintas de una API.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-146">It is common practice for multiple different implementation versions of an API to be supported at any one time.</span></span> <span data-ttu-id="0b0f1-147">Quizá sea para admitir diferentes entornos, como desarrollo, prueba o producción, o quizá sea por compatibilidad con versiones anteriores de la API para dar tiempo a los usuarios de la API a migrar a versiones más recientes.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-147">This is perhaps to support different environments, like dev, test, production, etc, or it may be to support older versions of the API to give time for API consumers to migrate to newer versions.</span></span> 

<span data-ttu-id="0b0f1-148">Un método para tratar eso en lugar de requerir a los desarrolladores de cliente que cambien las direcciones URL de `/v1/customers` a `/v2/customers` es almacenar en los datos de perfil del cliente, qué versión de la API desean usar y llamar a la dirección URL del back-end adecuada.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-148">One approach to handling this instead of requiring client developers to change the URLs from `/v1/customers` to `/v2/customers` is to store in the consumer’s profile data which version of the API they currently wish to use and call the appropriate backend URL.</span></span> <span data-ttu-id="0b0f1-149">Para determinar la dirección URL correcta de back-end para llamar a un cliente determinado, es necesario consultar algunos datos de configuración.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-149">In order to determine the correct backend URL to call for a particular client, it is necessary to query some configuration data.</span></span> <span data-ttu-id="0b0f1-150">Al almacenar en caché estos datos de configuración, podemos minimizar la reducción del rendimiento al realizar esta búsqueda.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-150">By caching this configuration data, we can minimize the performance penalty of doing this lookup.</span></span>

<span data-ttu-id="0b0f1-151">El primer paso consiste en determinar el identificador usado para configurar la versión deseada.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-151">The first step is to determine the identifier used to configure the desired version.</span></span> <span data-ttu-id="0b0f1-152">En este ejemplo, decidí asociar la versión con la clave de suscripción del producto.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-152">In this example, I chose to associate the version to the product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="0b0f1-153">Después hacemos una búsqueda en la caché para ver si ya hemos recuperado la versión de cliente deseada.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-153">We then do a cache lookup to see if we already have retrieved the desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="0b0f1-154">A continuación, comprobamos si la encontramos o no en la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-154">Then we check to see if we did not find it in the cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="0b0f1-155">Si no la encontramos, en este caso procedemos a su recuperación.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-155">If we didn’t then we go and retrieve it.</span></span>

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

<span data-ttu-id="0b0f1-156">Extraemos el texto del cuerpo de respuesta de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-156">Extract the response body text from the response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="0b0f1-157">Lo almacenamos en la caché para un uso futuro.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-157">Store it back in the cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="0b0f1-158">Y finalmente actualizamos la dirección URL de back-end para seleccionar la versión del servicio requerido por el cliente.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-158">And finally update the back-end URL to select the version of the service desired by the client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="0b0f1-159">La directiva completa es como sigue.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-159">The completely policy is as follows.</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in the cache, make a request for it and store it -->
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

<span data-ttu-id="0b0f1-160">Permitir a los usuarios de la API controlar de forma transparente la versión de back-end a la que acceden los clientes sin tener que actualizar y volver a implementar los clientes es una solución elegante que soluciona muchos problemas de control de versiones de la API.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-160">Enabling API consumers to transparently control which backend version is being accessed by clients without having to update and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="0b0f1-161">Aislamiento de inquilinos</span><span class="sxs-lookup"><span data-stu-id="0b0f1-161">Tenant Isolation</span></span>
<span data-ttu-id="0b0f1-162">En implementaciones grandes multiinquilino algunas compañías crean grupos independientes de inquilinos en distintas implementaciones del hardware de back-end.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="0b0f1-163">Esto minimiza el número de clientes que se ven afectados por un problema de hardware en el back-end.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-163">This minimizes the number of customers who are impacted by a hardware issue on the backend.</span></span> <span data-ttu-id="0b0f1-164">También permite que nuevas versiones de software se implementen en etapas.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-164">It also enables new software versions to be rolled out in stages.</span></span> <span data-ttu-id="0b0f1-165">Lo ideal es que esta arquitectura de back-end sea transparente para los usuarios de las API.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-165">Ideally this backend architecture should be transparent to API consumers.</span></span> <span data-ttu-id="0b0f1-166">Esto puede lograrse de manera similar con el control de versiones transparente porque se basa en la misma técnica de manipular la dirección URL de back-end mediante el estado de configuración por clave de API.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-166">This can be achieved in a similar way to transparent versioning because it is based on the same technique of manipulating the backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="0b0f1-167">En lugar de devolver una versión preferida de la API para cada clave de la suscripción, debe devolver un identificador que relacione un inquilino con el grupo de hardware asignado.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-167">Instead of returning a preferred version of the API for each subscription key, you would return an identifier that relates a tenant to the assigned hardware group.</span></span> <span data-ttu-id="0b0f1-168">Este identificador se puede usar para construir la dirección URL apropiada de back-end.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-168">That identifier can be used to construct the appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="0b0f1-169">Resumen</span><span class="sxs-lookup"><span data-stu-id="0b0f1-169">Summary</span></span>
<span data-ttu-id="0b0f1-170">La libertad de utilizar la caché de Administración de API de Azure para almacenar cualquier tipo de datos permite un acceso eficaz a los datos de configuración, lo que puede afectar a la manera de procesar una solicitud entrante.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-170">The freedom to use the Azure API management cache for storing any kind of data enables efficient access to configuration data that can affect the way an inbound request is processed.</span></span> <span data-ttu-id="0b0f1-171">También puede usarse para almacenar fragmentos de datos que pueden aumentar las respuestas devueltas desde una API de back-end.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-171">It can also be used to store data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b0f1-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0b0f1-172">Next steps</span></span>
<span data-ttu-id="0b0f1-173">Envíenos sus comentarios sobre este tema en la conversación Disqus si hay otros escenarios en los que estas directivas se hayan habilitado para usted, o si existen escenarios que le gustaría conseguir pero que actualmente no cree posibles.</span><span class="sxs-lookup"><span data-stu-id="0b0f1-173">Please give us your feedback in the Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like to achieve but do not feel are currently possible.</span></span>

