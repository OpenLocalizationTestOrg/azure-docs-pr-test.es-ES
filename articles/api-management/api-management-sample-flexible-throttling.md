---
title: "Limitación avanzada de solicitudes con Administración de API de Azure"
description: "Aprenda a crear y aplicar directivas de limitación de velocidad y de cuota flexibles con Administración de API de Azure."
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 35375e599891a9443a91c4c3a8657e8c9c48c7b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a><span data-ttu-id="bb0b0-103">Limitación avanzada de solicitudes con Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="bb0b0-103">Advanced request throttling with Azure API Management</span></span>
<span data-ttu-id="bb0b0-104">La posibilidad de limitar las solicitudes entrantes es un rol clave de Administración de API de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-104">Being able to throttle incoming requests is a key role of Azure API Management.</span></span> <span data-ttu-id="bb0b0-105">Ya sea mediante el control de la velocidad de solicitudes o de las solicitudes y los datos totales transferidos, Administración de API permite a los proveedores de API proteger sus API de uso indebido y crear valor para los diferentes niveles de productos de API.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-105">Either by controlling the rate of requests or the total requests/data transferred, API Management allows API providers to protect their APIs from abuse and create value for different API product tiers.</span></span>

## <a name="product-based-throttling"></a><span data-ttu-id="bb0b0-106">Limitación por producto</span><span class="sxs-lookup"><span data-stu-id="bb0b0-106">Product based throttling</span></span>
<span data-ttu-id="bb0b0-107">Hasta la fecha, las capacidades de limitación de velocidad se han circunscrito al ámbito de una suscripción de producto concreta (esencialmente una clave), que se define en el portal para editores de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-107">To date, the rate throttling capabilities have been limited to being scoped to a particular Product subscription (essentially a key), defined in the API Management publisher portal.</span></span> <span data-ttu-id="bb0b0-108">Resulta útil para que el proveedor de la API aplique límites a los desarrolladores que inicien sesión para usar su API, pero no ayuda, por ejemplo, a imponer limitaciones a los usuarios finales individuales de la API.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-108">This is useful for the API provider to apply limits on the developers who have signed up to use their API, however, it does not help, for example, in throttling individual end-users of the API.</span></span> <span data-ttu-id="bb0b0-109">Es posible que un solo usuario de la aplicación del desarrollador consuma toda la cuota e impida que otros clientes del desarrollador puedan usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-109">It is possible that for single user of the developer's application to consume the entire quota and then prevent other customers of the developer from being able to use the application.</span></span> <span data-ttu-id="bb0b0-110">Además, es posible que varios clientes que generen un gran volumen de solicitudes limiten el acceso a los usuarios ocasionales.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-110">Also, several customers who might generate a high volume of requests may limit access to occasional users.</span></span>

## <a name="custom-key-based-throttling"></a><span data-ttu-id="bb0b0-111">Limitación por clave personalizada</span><span class="sxs-lookup"><span data-stu-id="bb0b0-111">Custom key based throttling</span></span>
<span data-ttu-id="bb0b0-112">Las nuevas directivas [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) y [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) ofrecen una solución considerablemente más flexible para el control del tráfico.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-112">The new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a significantly more flexible solution to traffic control.</span></span> <span data-ttu-id="bb0b0-113">Estas nuevas directivas permiten definir expresiones para identificar las claves que se usarán para realizar un seguimiento del uso del tráfico.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-113">These new policies allow you to define expressions to identify the keys that will be used to track traffic usage.</span></span> <span data-ttu-id="bb0b0-114">El funcionamiento de esto se ilustra más claramente con un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-114">The way this works is easiest illustrated with an example.</span></span> 

## <a name="ip-address-throttling"></a><span data-ttu-id="bb0b0-115">Limitación por dirección IP</span><span class="sxs-lookup"><span data-stu-id="bb0b0-115">IP Address throttling</span></span>
<span data-ttu-id="bb0b0-116">Las siguientes directivas restringen una única dirección IP de cliente a solo 10 llamadas por minuto, con un total de 1 000 000 llamadas y 10 000 kilobytes de ancho de banda al mes.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-116">The following policies restrict a single client IP address to only 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span></span> 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

<span data-ttu-id="bb0b0-117">Si todos los clientes en Internet utilizasen una única dirección IP, esta podría ser una forma eficaz de limitar el uso por usuario.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-117">If all clients on the Internet used a unique IP address, this might be an effective way of limiting usage by user.</span></span> <span data-ttu-id="bb0b0-118">Pero es bastante probable que varios usuarios compartan una única dirección IP pública debido a su acceso a Internet a través de un dispositivo NAT.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-118">However, it is quite likely that multiple users will sharing a single public IP address due to them accessing the Internet via a NAT device.</span></span> <span data-ttu-id="bb0b0-119">A pesar de esto, es posible que para las API que permiten el acceso no autenticado, `IpAddress` sea la mejor opción.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-119">Despite this, for APIs that allow unauthenticated access the `IpAddress` might be the best option.</span></span>

## <a name="user-identity-throttling"></a><span data-ttu-id="bb0b0-120">Limitación por identidad de usuario</span><span class="sxs-lookup"><span data-stu-id="bb0b0-120">User identity throttling</span></span>
<span data-ttu-id="bb0b0-121">Si se autentica un usuario final, puede generarse una clave de limitación basada en información que identifica de forma única a ese usuario.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-121">If an end user is authenticated then a throttling key can be generated based on information that uniquely identifies an that user.</span></span>

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

<span data-ttu-id="bb0b0-122">En este ejemplo se extrae el encabezado de autorización, se convierte en objeto `JWT` y se usa el firmante del token para identificar al usuario y usarlo como clave de limitación de velocidad.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-122">In this example we extract the Authorization header, convert it to `JWT` object and use the subject of the token to identify the user and use that as the rate limiting key.</span></span> <span data-ttu-id="bb0b0-123">Si la identidad del usuario se almacena en el `JWT` como una de las otras notificaciones, ese valor podría usarse en su lugar.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-123">If the user identity is stored in the `JWT` as one of the other claims then that value could be used in its place.</span></span>

## <a name="combined-policies"></a><span data-ttu-id="bb0b0-124">Directivas de combinación</span><span class="sxs-lookup"><span data-stu-id="bb0b0-124">Combined policies</span></span>
<span data-ttu-id="bb0b0-125">Aunque las nuevas directivas de limitación proporcionan más control que las directivas existentes de limitación, sigue siendo útil combinar ambas capacidades.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-125">Although the new throttling policies provide more control than the existing throttling policies, there is still value combining both capabilities.</span></span> <span data-ttu-id="bb0b0-126">La limitación por clave de suscripción de producto ([Limitar tarifa de llamadas por suscripción](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) y [Establecer cuota de uso por suscripción](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) es una excelente manera de habilitar la monetización de una API mediante el cobro por niveles de uso.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way to enable monetizing of an API by charging based on usage levels.</span></span> <span data-ttu-id="bb0b0-127">El control más preciso de poder limitar por usuario es complementario e impide que el comportamiento de un usuario degrade la experiencia de otro.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-127">The finer grained control of being able to throttle by user is complementary and prevents one user's behavior from degrading the experience of another.</span></span> 

## <a name="client-driven-throttling"></a><span data-ttu-id="bb0b0-128">Limitación controlada por cliente</span><span class="sxs-lookup"><span data-stu-id="bb0b0-128">Client driven throttling</span></span>
<span data-ttu-id="bb0b0-129">Cuando la clave de limitación se define con una [expresión de directiva](https://msdn.microsoft.com/library/azure/dn910913.aspx), es el proveedor de la API el que elige el ámbito de la limitación.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-129">When the throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is the API provider that is choosing how the throttling is scoped.</span></span> <span data-ttu-id="bb0b0-130">Pero puede que un desarrollador desee controlar cómo limita la frecuencia de sus propios clientes.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-130">However, a developer might want to control how they rate limit their own customers.</span></span> <span data-ttu-id="bb0b0-131">Esto lo podría habilitar el proveedor de la API introduciendo un encabezado personalizado que permita a la aplicación cliente del desarrollador comunicar la clave a la API.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-131">This could be enabled by the API provider by introducing a custom header to allow the developer's client application to communicate the key to the API.</span></span>

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

<span data-ttu-id="bb0b0-132">Así se permite a la aplicación cliente del desarrollador elegir cómo se quiere crear la clave de limitación de velocidad.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-132">This enables the developer's client application to choose how they want to create the rate limiting key.</span></span> <span data-ttu-id="bb0b0-133">Con un poco de ingenio un desarrollador del cliente puede crear sus propios niveles de velocidad asignando conjuntos de claves a los usuarios y rotando el uso de claves.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-133">With a little bit of ingenuity a client developer could create their own rate tiers by allocating sets of keys to users and rotating the key usage.</span></span>

## <a name="summary"></a><span data-ttu-id="bb0b0-134">Resumen</span><span class="sxs-lookup"><span data-stu-id="bb0b0-134">Summary</span></span>
<span data-ttu-id="bb0b0-135">Administración de API de Azure ofrece limitación de velocidad y de cuota para proteger y agregar valor al servicio de API.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-135">Azure API Management provides rate and quote throttling to both protect and add value to your API service.</span></span> <span data-ttu-id="bb0b0-136">Las nuevas directivas de limitación con reglas de ámbito personalizadas permiten un control más preciso sobre las directivas para permitir a los clientes crear aplicaciones aún mejores.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-136">The new throttling policies with custom scoping rules allow you finer grained control over those policies to enable your customers to build even better applications.</span></span> <span data-ttu-id="bb0b0-137">Los ejemplos de este artículo muestran el uso de estas nuevas directivas fabricando claves de limitación de velocidad con direcciones IP de cliente, identidad de usuario y valores generados por el cliente.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-137">The examples in this article demonstrate the use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span></span> <span data-ttu-id="bb0b0-138">Pero hay muchas más partes del mensaje que podrían usarse como, por ejemplo, agente de usuario, fragmentos de ruta de dirección URL, tamaño del mensaje.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-138">However, there are many other parts of the message that could be used such as user agent, URL path fragments, message size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb0b0-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bb0b0-139">Next steps</span></span>
<span data-ttu-id="bb0b0-140">Háganos sus comentarios en la conversación Disqus sobre este tema.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-140">Please give us your feedback in the Disqus thread for this topic.</span></span> <span data-ttu-id="bb0b0-141">Sería estupendo conocer otros posibles valores de clave que hayan sido una elección lógica en sus escenarios.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-141">It would be great to hear about other potential key values that have been a logical choice in your scenarios.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="bb0b0-142">Ver un vídeo de información general de estas directivas</span><span class="sxs-lookup"><span data-stu-id="bb0b0-142">Watch a video overview of these policies</span></span>
<span data-ttu-id="bb0b0-143">Para más información sobre las directivas [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) y [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) que se describen en este artículo, vea el siguiente vídeo.</span><span class="sxs-lookup"><span data-stu-id="bb0b0-143">For more information on the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

