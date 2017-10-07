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
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="2cf01-103">Almacenamiento en caché personalizado en Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="2cf01-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="2cf01-104">Servicio de administración de API de Azure tiene compatibilidad integrada para [el almacenamiento en caché de la respuesta HTTP](api-management-howto-cache.md) utilizando la dirección URL del recurso hello como clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="2cf01-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using hello resource URL as hello key.</span></span> <span data-ttu-id="2cf01-105">Hello clave se puede modificar por encabezados de solicitud utilizando hello `vary-by` propiedades.</span><span class="sxs-lookup"><span data-stu-id="2cf01-105">hello key can be modified by request headers using hello `vary-by` properties.</span></span> <span data-ttu-id="2cf01-106">Esto es útil para almacenar en caché todas las respuestas de HTTP (también conocido como representaciones), pero a veces resulta útil toojust caché una parte de una representación.</span><span class="sxs-lookup"><span data-stu-id="2cf01-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful toojust cache a portion of a representation.</span></span> <span data-ttu-id="2cf01-107">Hola nueva [valor de búsqueda de caché](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) y [valor de almacén de caché](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) directivas proporcionan capacidad de hello toostore y recuperar fragmentos arbitrarios de datos desde dentro de definiciones de directiva.</span><span class="sxs-lookup"><span data-stu-id="2cf01-107">hello new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide hello ability toostore and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="2cf01-108">Esta capacidad también agrega toohello valor introducido anteriormente [solicitud de envío](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) directiva porque ahora puede almacenar en caché las respuestas de servicios externos.</span><span class="sxs-lookup"><span data-stu-id="2cf01-108">This ability also adds value toohello previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="2cf01-109">Arquitectura</span><span class="sxs-lookup"><span data-stu-id="2cf01-109">Architecture</span></span>
<span data-ttu-id="2cf01-110">Servicio de administración de API utiliza una caché de datos compartido por inquilino que, cuando se escala toomultiple unidades aún obtendrá acceso toohello mismo datos almacenados en caché.</span><span class="sxs-lookup"><span data-stu-id="2cf01-110">API Management service uses a shared per-tenant data cache so that, as you scale up toomultiple units you will still get access toohello same cached data.</span></span> <span data-ttu-id="2cf01-111">Sin embargo, cuando se trabaja con una implementación de varias regiones son memorias caché independientes en cada una de las regiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="2cf01-111">However, when working with a multi-region deployment there are independent caches within each of hello regions.</span></span> <span data-ttu-id="2cf01-112">Due toothis, es importante toonot tratar caché Hola como un almacén de datos, donde es la única fuente de Hola de cierta información.</span><span class="sxs-lookup"><span data-stu-id="2cf01-112">Due toothis, it is important toonot treat hello cache as a data store, where it is hello only source of some piece of information.</span></span> <span data-ttu-id="2cf01-113">Si se ha y más adelante decide tootake aprovechar la implementación de varias regiones de hello, los clientes con los usuarios que viajan pueden perder acceso a los datos almacenados en memoria caché de toothat.</span><span class="sxs-lookup"><span data-stu-id="2cf01-113">If you did, and later decided tootake advantage of hello multi-region deployment, then customers with users that travel may lose access toothat cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="2cf01-114">Almacenamiento en caché de fragmentos</span><span class="sxs-lookup"><span data-stu-id="2cf01-114">Fragment caching</span></span>
<span data-ttu-id="2cf01-115">Hay algunos casos donde las respuestas que se devuelven contienen alguna parte de datos que se toodetermine costoso y aún permanecen actualizada para un intervalo de tiempo razonable.</span><span class="sxs-lookup"><span data-stu-id="2cf01-115">There are certain cases where responses being returned contain some portion of data that is expensive toodetermine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="2cf01-116">Como ejemplo, piense en un servicio creado por una línea aérea que ofrece información relacionada con las reservas de vuelos, estado del vuelo, etc. Si el usuario de hello es miembro del programa de puntos de compañías aéreas de hello, también tendrían información relacionada con kilometraje acumulado y el estado actual de tootheir.</span><span class="sxs-lookup"><span data-stu-id="2cf01-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If hello user is a member of hello airlines points program, they would also have information relating tootheir current status and mileage accumulated.</span></span> <span data-ttu-id="2cf01-117">Esta información relacionada con el usuario podría almacenarse en un sistema diferente, pero puede ser deseable tooinclude devuelve en respuestas acerca de las reservas y el estado del vuelo.</span><span class="sxs-lookup"><span data-stu-id="2cf01-117">This user-related information might be stored in a different system, but it may be desirable tooinclude it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="2cf01-118">Esto puede hacerse mediante un proceso denominado almacenamiento en caché de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="2cf01-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="2cf01-119">Hello representación principal se puede devolver desde el servidor de origen de hello mediante algún tipo de token tooindicate donde obtener información relacionada con el usuario de hello es toobe insertado.</span><span class="sxs-lookup"><span data-stu-id="2cf01-119">hello primary representation can be returned from hello origin server using some kind of token tooindicate where hello user-related information is toobe inserted.</span></span> 

<span data-ttu-id="2cf01-120">Considere la posibilidad de hello después de la respuesta JSON de un API de back-end.</span><span class="sxs-lookup"><span data-stu-id="2cf01-120">Consider hello following JSON response from a backend API.</span></span>

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

<span data-ttu-id="2cf01-121">Y el recurso secundario en `/userprofile/{userid}` que es como sigue,</span><span class="sxs-lookup"><span data-stu-id="2cf01-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="2cf01-122">En orden toodetermine Hola usuario correspondiente información tooinclude, necesitamos tooidentify que sea el usuario final de Hola.</span><span class="sxs-lookup"><span data-stu-id="2cf01-122">In order toodetermine hello appropriate user information tooinclude, we need tooidentify who hello end user is.</span></span> <span data-ttu-id="2cf01-123">Este mecanismo depende de la implementación.</span><span class="sxs-lookup"><span data-stu-id="2cf01-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="2cf01-124">Por ejemplo, utilizo hello `Subject` de notificación de un `JWT` símbolo (token).</span><span class="sxs-lookup"><span data-stu-id="2cf01-124">As an example, I am using hello `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="2cf01-125">Almacenamos este valor `enduserid` en una variable de contexto para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="2cf01-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="2cf01-126">Hola siguiente paso es toodetermine si una solicitud anterior ya recuperar información de usuario de Hola y almacenado en memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="2cf01-126">hello next step is toodetermine if a previous request has already retrieved hello user information and stored it in hello cache.</span></span> <span data-ttu-id="2cf01-127">Para ello se utilice hello `cache-lookup-value` directiva.</span><span class="sxs-lookup"><span data-stu-id="2cf01-127">For this we use hello `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="2cf01-128">Si no hay ninguna entrada en memoria caché de Hola que corresponde el valor de clave de toohello y, a continuación, no `userprofile` se creará la variable de contexto.</span><span class="sxs-lookup"><span data-stu-id="2cf01-128">If there is no entry in hello cache that corresponds toohello key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="2cf01-129">Comprobamos el éxito de Hola de búsqueda de hello mediante hello `choose` directiva de flujo de control.</span><span class="sxs-lookup"><span data-stu-id="2cf01-129">We check hello success of hello lookup using hello `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="2cf01-130">Si hello `userprofile` no existe la variable de contexto, a continuación, se va toohave toomake HTTP solicitud tooretrieve lo.</span><span class="sxs-lookup"><span data-stu-id="2cf01-130">If hello `userprofile` context variable doesn’t exist, then we are going toohave toomake an HTTP request tooretrieve it.</span></span>

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

<span data-ttu-id="2cf01-131">Usamos hello `enduserid` recurso de perfil de usuario de tooconstruct Hola URL toohello.</span><span class="sxs-lookup"><span data-stu-id="2cf01-131">We use hello `enduserid` tooconstruct hello URL toohello user profile resource.</span></span> <span data-ttu-id="2cf01-132">Una vez que tenemos respuesta hello, podemos extraer texto del cuerpo Hola fuera de respuesta de Hola y almacenarlo en una variable de contexto.</span><span class="sxs-lookup"><span data-stu-id="2cf01-132">Once we have hello response, we can pull hello body text out of hello response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="2cf01-133">tooavoid nos tener esta solicitud HTTP de toomake nuevo, al mismo usuario hello realiza otra solicitud, podemos almacenar perfil de usuario de hello en memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="2cf01-133">tooavoid us having toomake this HTTP request again, when hello same user makes another request, we can store hello user profile in hello cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="2cf01-134">Almacenamos valor hello en memoria caché de hello con hello exacta misma clave que intentamos originalmente tooretrieve con.</span><span class="sxs-lookup"><span data-stu-id="2cf01-134">We store hello value in hello cache using hello exact same key that we originally attempted tooretrieve it with.</span></span> <span data-ttu-id="2cf01-135">Hello duración que se elija el valor de hello toostore debe basarse en la frecuencia con hello cambios en la información y cómo tolerante a los usuarios son tooout de información de fecha.</span><span class="sxs-lookup"><span data-stu-id="2cf01-135">hello duration that we choose toostore hello value should be based on how often hello information changes and how tolerant users are tooout of date information.</span></span> 

<span data-ttu-id="2cf01-136">Es importante toorealize que recuperar de la caché de hello sigue siendo un fuera de proceso, la solicitud de la red y potencialmente, puedes agregar decenas de milisegundos toohello solicitud.</span><span class="sxs-lookup"><span data-stu-id="2cf01-136">It is important toorealize that retrieving from hello cache is still an out-of-process, network request and potentially can still add tens of milliseconds toohello request.</span></span> <span data-ttu-id="2cf01-137">ventajas de Hello proceden al determinar información de perfil de usuario de hello tarda significativamente más debido a las consultas de base de datos de toodo tooneeding o agregar información de varios back-end.</span><span class="sxs-lookup"><span data-stu-id="2cf01-137">hello benefits come when determining hello user profile information takes significantly longer than that due tooneeding toodo database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="2cf01-138">Hello último paso en el proceso de hello es hello tooupdate devolvió una respuesta con la información de perfil de usuario.</span><span class="sxs-lookup"><span data-stu-id="2cf01-138">hello final step in hello process is tooupdate hello returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="2cf01-139">Eligió tooinclude Hola comillas como parte del token de Hola para que incluso cuando no se produce el reemplazo de hello, respuesta de hello era JSON siguen siendo válido.</span><span class="sxs-lookup"><span data-stu-id="2cf01-139">I chose tooinclude hello quotation marks as part of hello token so that even when hello replace doesn’t occur, hello response was still valid JSON.</span></span> <span data-ttu-id="2cf01-140">Esto resultaba principalmente toomake depuración.</span><span class="sxs-lookup"><span data-stu-id="2cf01-140">This was primarily toomake debugging easier.</span></span>

<span data-ttu-id="2cf01-141">Una vez que se combinan todos estos pasos juntos, obteniéndose hello es una directiva que es similar a Hola sigue uno.</span><span class="sxs-lookup"><span data-stu-id="2cf01-141">Once you combine all these steps together, hello end result is a policy that looks like hello following one.</span></span>

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

<span data-ttu-id="2cf01-142">Este enfoque de almacenamiento en caché se utiliza principalmente en los sitios web donde se compone HTML en el lado del servidor de Hola para que se puede representar como una sola página.</span><span class="sxs-lookup"><span data-stu-id="2cf01-142">This caching approach is primarily used in web sites where HTML is composed on hello server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="2cf01-143">Sin embargo, también puede ser útil en donde los clientes no cliente de las API del lado del almacenamiento en caché de HTTP o es deseable no tooput esa responsabilidad en cliente Hola.</span><span class="sxs-lookup"><span data-stu-id="2cf01-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not tooput that responsibility on hello client.</span></span>

<span data-ttu-id="2cf01-144">Este mismo tipo de almacenamiento en caché de fragmento permite llevar a cabo en servidores web Hola back-end a través de un servidor el almacenamiento en caché de Redis, sin embargo, con tooperform de servicio de administración de API de hello este trabajo es útil si fragmentos de hello en caché provienen de diferentes back-end que Hola respuestas principales.</span><span class="sxs-lookup"><span data-stu-id="2cf01-144">This same kind of fragment caching can also be done on hello backend web servers using a Redis caching server, however, using hello API Management service tooperform this work is useful when hello cached fragments are coming from different back-ends than hello primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="2cf01-145">Control de versiones transparente</span><span class="sxs-lookup"><span data-stu-id="2cf01-145">Transparent versioning</span></span>
<span data-ttu-id="2cf01-146">Es una práctica común para varias versiones de implementación diferente de una toobe de API compatibles en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="2cf01-146">It is common practice for multiple different implementation versions of an API toobe supported at any one time.</span></span> <span data-ttu-id="2cf01-147">Se trata quizás toosupport distintos entornos, como desarrollo, prueba, producción, etcetera, o puede ser toosupport versiones anteriores de tiempo de toogive Hola API para las versiones de API a los consumidores toomigrate toonewer.</span><span class="sxs-lookup"><span data-stu-id="2cf01-147">This is perhaps toosupport different environments, like dev, test, production, etc, or it may be toosupport older versions of hello API toogive time for API consumers toomigrate toonewer versions.</span></span> 

<span data-ttu-id="2cf01-148">Un enfoque toohandling de este en su lugar, que requiere direcciones URL de toochange Hola a los desarrolladores de cliente de `/v1/customers` demasiado`/v2/customers` es toostore en los datos de perfil del consumidor de hello qué versión de API de Hola actualmente va toouse y llamar Hola adecuado dirección URL de back-end.</span><span class="sxs-lookup"><span data-stu-id="2cf01-148">One approach toohandling this instead of requiring client developers toochange hello URLs from `/v1/customers` too`/v2/customers` is toostore in hello consumer’s profile data which version of hello API they currently wish toouse and call hello appropriate backend URL.</span></span> <span data-ttu-id="2cf01-149">En orden toodetermine Hola correcto back-end URL toocall para un cliente determinado, es necesario tooquery algunos datos de configuración.</span><span class="sxs-lookup"><span data-stu-id="2cf01-149">In order toodetermine hello correct backend URL toocall for a particular client, it is necessary tooquery some configuration data.</span></span> <span data-ttu-id="2cf01-150">Al almacenar en caché estos datos de configuración, que podemos minimizar la reducción del rendimiento Hola de realizar esta búsqueda.</span><span class="sxs-lookup"><span data-stu-id="2cf01-150">By caching this configuration data, we can minimize hello performance penalty of doing this lookup.</span></span>

<span data-ttu-id="2cf01-151">Hola primer paso es identificador de Hola de toodetermine usa la versión deseada de tooconfigure Hola.</span><span class="sxs-lookup"><span data-stu-id="2cf01-151">hello first step is toodetermine hello identifier used tooconfigure hello desired version.</span></span> <span data-ttu-id="2cf01-152">En este ejemplo, eligió clave de suscripción de producto de tooassociate Hola versión toohello.</span><span class="sxs-lookup"><span data-stu-id="2cf01-152">In this example, I chose tooassociate hello version toohello product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="2cf01-153">A continuación, hacemos una toosee de búsqueda de la memoria caché si ya hemos recuperado versión de cliente deseado Hola.</span><span class="sxs-lookup"><span data-stu-id="2cf01-153">We then do a cache lookup toosee if we already have retrieved hello desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="2cf01-154">A continuación, comprobamos toosee si no se ha encontrado en la caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="2cf01-154">Then we check toosee if we did not find it in hello cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="2cf01-155">Si no la encontramos, en este caso procedemos a su recuperación.</span><span class="sxs-lookup"><span data-stu-id="2cf01-155">If we didn’t then we go and retrieve it.</span></span>

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

<span data-ttu-id="2cf01-156">Extraer el texto del cuerpo de respuesta de Hola de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="2cf01-156">Extract hello response body text from hello response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="2cf01-157">Almacene en memoria caché de Hola para un uso futuro.</span><span class="sxs-lookup"><span data-stu-id="2cf01-157">Store it back in hello cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="2cf01-158">Y finalmente Hola back-end dirección URL tooselect Hola versión actualización del servicio de hello deseado por cliente hello.</span><span class="sxs-lookup"><span data-stu-id="2cf01-158">And finally update hello back-end URL tooselect hello version of hello service desired by hello client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="2cf01-159">Hello completamente directiva es como sigue.</span><span class="sxs-lookup"><span data-stu-id="2cf01-159">hello completely policy is as follows.</span></span>

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

<span data-ttu-id="2cf01-160">Habilitar control de API a los consumidores tootransparently qué versión de back-end está teniendo acceso a los clientes sin necesidad de tooupdate y volver a implementar los clientes es una solución elegante que dirige a muchos problemas de control de versiones de API.</span><span class="sxs-lookup"><span data-stu-id="2cf01-160">Enabling API consumers tootransparently control which backend version is being accessed by clients without having tooupdate and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="2cf01-161">Aislamiento de inquilinos</span><span class="sxs-lookup"><span data-stu-id="2cf01-161">Tenant Isolation</span></span>
<span data-ttu-id="2cf01-162">En implementaciones grandes multiinquilino algunas compañías crean grupos independientes de inquilinos en distintas implementaciones del hardware de back-end.</span><span class="sxs-lookup"><span data-stu-id="2cf01-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="2cf01-163">Esto reduce el número de Hola de clientes que se ven afectados por un problema de hardware en hello back-end.</span><span class="sxs-lookup"><span data-stu-id="2cf01-163">This minimizes hello number of customers who are impacted by a hardware issue on hello backend.</span></span> <span data-ttu-id="2cf01-164">También permite toobe de versiones de software nuevo implantado en fases.</span><span class="sxs-lookup"><span data-stu-id="2cf01-164">It also enables new software versions toobe rolled out in stages.</span></span> <span data-ttu-id="2cf01-165">Lo ideal es que esta arquitectura de back-end debe ser transparente tooAPI consumidores.</span><span class="sxs-lookup"><span data-stu-id="2cf01-165">Ideally this backend architecture should be transparent tooAPI consumers.</span></span> <span data-ttu-id="2cf01-166">Esto se puede lograr de un control de versiones de tootransparent de manera similar porque se basa en hello misma técnica de manipulación de URL de back-end de hello usando el estado de configuración por clave de API.</span><span class="sxs-lookup"><span data-stu-id="2cf01-166">This can be achieved in a similar way tootransparent versioning because it is based on hello same technique of manipulating hello backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="2cf01-167">En lugar de devolver una versión preferida de hello API para cada clave de la suscripción, debe devolver un identificador que está relacionada con un grupo de hardware de inquilino toohello asignado.</span><span class="sxs-lookup"><span data-stu-id="2cf01-167">Instead of returning a preferred version of hello API for each subscription key, you would return an identifier that relates a tenant toohello assigned hardware group.</span></span> <span data-ttu-id="2cf01-168">Ese identificador puede ser la dirección URL de back-end adecuados de Hola de tooconstruct usado.</span><span class="sxs-lookup"><span data-stu-id="2cf01-168">That identifier can be used tooconstruct hello appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="2cf01-169">Resumen</span><span class="sxs-lookup"><span data-stu-id="2cf01-169">Summary</span></span>
<span data-ttu-id="2cf01-170">Hola toouse de libertad Hola caché de administración de API de Azure para almacenar cualquier tipo de datos permite un acceso eficiente tooconfiguration que los datos pueden afectar al modo de saludo que se procesa una solicitud entrante.</span><span class="sxs-lookup"><span data-stu-id="2cf01-170">hello freedom toouse hello Azure API management cache for storing any kind of data enables efficient access tooconfiguration data that can affect hello way an inbound request is processed.</span></span> <span data-ttu-id="2cf01-171">También puede ser usado toostore los fragmentos de datos que pueden aumentar las respuestas, devueltas desde una API de back-end.</span><span class="sxs-lookup"><span data-stu-id="2cf01-171">It can also be used toostore data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2cf01-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2cf01-172">Next steps</span></span>
<span data-ttu-id="2cf01-173">Por favor, envíenos sus comentarios en hello Disqus subproceso de este tema si hay otros escenarios que estas directivas se han habilitado para usted, o si existen escenarios desearía tooachieve pero no se sienta son actualmente posibles.</span><span class="sxs-lookup"><span data-stu-id="2cf01-173">Please give us your feedback in hello Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like tooachieve but do not feel are currently possible.</span></span>

