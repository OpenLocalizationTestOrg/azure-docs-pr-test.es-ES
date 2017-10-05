---
title: Escalado de Azure Redis Cache | Microsoft Docs
description: "Obtenga información acerca de cómo ampliar las instancias de Azure Redis Cache"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 350db214-3b7c-4877-bd43-fef6df2db96c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: sdanie
ms.openlocfilehash: 91b3580491a1e3504a3891b66606a9bd18c0638f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-azure-redis-cache"></a><span data-ttu-id="15fab-103">Escalado de Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="15fab-103">How to Scale Azure Redis Cache</span></span>
<span data-ttu-id="15fab-104">Azure Redis Cache tiene diferentes ofertas de caché que proporcionan flexibilidad en la elección del tamaño y las características de la caché.</span><span class="sxs-lookup"><span data-stu-id="15fab-104">Azure Redis Cache has different cache offerings, which provide flexibility in the choice of cache size and features.</span></span> <span data-ttu-id="15fab-105">Después de crear una memoria caché, puede ajustar su tamaño y el plan de tarifa si cambian los requisitos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="15fab-105">After a cache is created, you can scale the size and the pricing tier of the cache if the requirements of your application change.</span></span> <span data-ttu-id="15fab-106">En este artículo se muestra cómo escalar la memoria caché en Azure Portal o con herramientas tales como Azure PowerShell y la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="15fab-106">This article shows you how to scale your cache in both the Azure portal and using tools such as Azure PowerShell and Azure CLI.</span></span>

## <a name="when-to-scale"></a><span data-ttu-id="15fab-107">Cuándo se debe escalar</span><span class="sxs-lookup"><span data-stu-id="15fab-107">When to scale</span></span>
<span data-ttu-id="15fab-108">Puede utilizar las características de [supervisión](cache-how-to-monitor.md) de Azure Redis Cache para supervisar el estado y el rendimiento de la memoria caché y para ayudar a determinar si es necesario escalarla.</span><span class="sxs-lookup"><span data-stu-id="15fab-108">You can use the [monitoring](cache-how-to-monitor.md) features of Azure Redis Cache to monitor the health and performance of your cache and help determine when to scale the cache.</span></span> 

<span data-ttu-id="15fab-109">Puede supervisar las métricas siguientes para ayudar a determinar si necesita escalado.</span><span class="sxs-lookup"><span data-stu-id="15fab-109">You can monitor the following metrics to help determine if you need to scale.</span></span>

* <span data-ttu-id="15fab-110">Carga de servidor de Redis</span><span class="sxs-lookup"><span data-stu-id="15fab-110">Redis Server Load</span></span>
* <span data-ttu-id="15fab-111">Uso de la memoria</span><span class="sxs-lookup"><span data-stu-id="15fab-111">Memory Usage</span></span>
* <span data-ttu-id="15fab-112">Ancho de banda de red</span><span class="sxs-lookup"><span data-stu-id="15fab-112">Network Bandwidth</span></span>
* <span data-ttu-id="15fab-113">Uso de CPU</span><span class="sxs-lookup"><span data-stu-id="15fab-113">CPU Usage</span></span>

<span data-ttu-id="15fab-114">Si determina que la memoria caché ya no cumple los requisitos de su aplicación, puede cambiar a un plan de tarifa de caché mayor o menor que sea adecuado para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="15fab-114">If you determine that your cache is no longer meeting your application's requirements, you can scale to a larger or smaller cache pricing tier that is right for your application.</span></span> <span data-ttu-id="15fab-115">Para obtener más información acerca de cómo determinar qué nivel de precios de caché, consulte [¿Qué oferta y tamaño de Caché en Redis debo utilizar?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span><span class="sxs-lookup"><span data-stu-id="15fab-115">For more information on determining which cache pricing tier to use, see [What Redis Cache offering and size should I use](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span></span>

## <a name="scale-a-cache"></a><span data-ttu-id="15fab-116">Escalado de una caché</span><span class="sxs-lookup"><span data-stu-id="15fab-116">Scale a cache</span></span>
<span data-ttu-id="15fab-117">Para escalar la memoria caché, [vaya a la caché](cache-configure.md#configure-redis-cache-settings) en [Azure Portal](https://portal.azure.com) y haga clic en **Escalar** en el menú **Recurso**.</span><span class="sxs-lookup"><span data-stu-id="15fab-117">To scale your cache, [browse to the cache](cache-configure.md#configure-redis-cache-settings) in the [Azure portal](https://portal.azure.com) and click **Scale** from the **Resource menu**.</span></span>

![Escala](./media/cache-how-to-scale/redis-cache-scale-menu.png)

<span data-ttu-id="15fab-119">Seleccione el plan de tarifa deseado en la hoja **Seleccionar plan de tarifa** y haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="15fab-119">Select the desired pricing tier from the **Select pricing tier** blade and click **Select**.</span></span>

![Nivel de precios][redis-cache-pricing-tier-blade]


<span data-ttu-id="15fab-121">Puede escalar a un plan de tarifa diferente con las siguientes restricciones:</span><span class="sxs-lookup"><span data-stu-id="15fab-121">You can scale to a different pricing tier with the following restrictions:</span></span>

* <span data-ttu-id="15fab-122">No se puede escalar desde un plan de tarifa superior a un plan de tarifa inferior.</span><span class="sxs-lookup"><span data-stu-id="15fab-122">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
  * <span data-ttu-id="15fab-123">No puede cambiar de una memoria caché **Premium** a una memoria caché **Estándar** o **Básica**.</span><span class="sxs-lookup"><span data-stu-id="15fab-123">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="15fab-124">No puede cambiar de una memoria caché **Estándar** a una memoria caché **Básica**.</span><span class="sxs-lookup"><span data-stu-id="15fab-124">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
* <span data-ttu-id="15fab-125">Puede cambiar de una memoria caché **Básica** a una memoria caché **Estándar**, pero no puede cambiar el tamaño al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="15fab-125">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="15fab-126">Si necesita un tamaño distinto, puede realizar una operación de escalado posterior hasta el tamaño deseado.</span><span class="sxs-lookup"><span data-stu-id="15fab-126">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
* <span data-ttu-id="15fab-127">No puede escalar de una memoria caché **Básica** directamente a una memoria caché **Premium**.</span><span class="sxs-lookup"><span data-stu-id="15fab-127">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="15fab-128">Debe escalar desde **Básica** a **Estándar** en una operación de escalado y, después, desde **Estándar** a **Premium** en una operación de escalado posterior.</span><span class="sxs-lookup"><span data-stu-id="15fab-128">You must scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="15fab-129">No puede escalar desde un tamaño mayor hasta el tamaño **C0 (250 MB)** .</span><span class="sxs-lookup"><span data-stu-id="15fab-129">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>
 
<span data-ttu-id="15fab-130">Durante la operación de escalado de la memoria caché al nuevo plan de tarifa, se muestra el estado **Escalando** en la hoja **Redis Cache**.</span><span class="sxs-lookup"><span data-stu-id="15fab-130">While the cache is scaling to the new pricing tier, a **Scaling** status is displayed in the **Redis Cache** blade.</span></span>

![Escalado][redis-cache-scaling]

<span data-ttu-id="15fab-132">Cuando se completa el escalado, el estado cambia de **Escalado** a **En ejecución**.</span><span class="sxs-lookup"><span data-stu-id="15fab-132">When scaling is complete, the status changes from **Scaling** to **Running**.</span></span>

## <a name="how-to-automate-a-scaling-operation"></a><span data-ttu-id="15fab-133">Automatización de una operación de escalado</span><span class="sxs-lookup"><span data-stu-id="15fab-133">How to automate a scaling operation</span></span>
<span data-ttu-id="15fab-134">Además de escalar las instancias de caché en Azure Portal, puede escalar mediante los cmdlets de PowerShell, la CLI de Azure y las Bibliotecas de administración de Microsoft Azure (MAML).</span><span class="sxs-lookup"><span data-stu-id="15fab-134">In addition to scaling your cache instances in the Azure portal, you can scale using PowerShell cmdlets, Azure CLI, and by using the Microsoft Azure Management Libraries (MAML).</span></span> 

* [<span data-ttu-id="15fab-135">Escalado mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="15fab-135">Scale using PowerShell</span></span>](#scale-using-powershell)
* [<span data-ttu-id="15fab-136">Escalado con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="15fab-136">Scale using Azure CLI</span></span>](#scale-using-azure-cli)
* [<span data-ttu-id="15fab-137">Escalado mediante MAML</span><span class="sxs-lookup"><span data-stu-id="15fab-137">Scale using MAML</span></span>](#scale-using-maml)

### <a name="scale-using-powershell"></a><span data-ttu-id="15fab-138">Escalado mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="15fab-138">Scale using PowerShell</span></span>
<span data-ttu-id="15fab-139">Las instancias de Azure Redis Cache se pueden escalar con PowerShell con el cmdlet [AzureRmRedisCache Set](https://msdn.microsoft.com/library/azure/mt634518.aspx) cuando se modifican las propiedades `Size`, `Sku` o `ShardCount`.</span><span class="sxs-lookup"><span data-stu-id="15fab-139">You can scale your Azure Redis Cache instances with PowerShell by using the [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet when the `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> <span data-ttu-id="15fab-140">En el ejemplo siguiente se muestra cómo escalar una memoria caché denominada `myCache` a una caché de 2,5 GB.</span><span class="sxs-lookup"><span data-stu-id="15fab-140">The following example shows how to scale a cache named `myCache` to a 2.5 GB cache.</span></span> 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="15fab-141">Para obtener más información sobre cómo escalar con PowerShell, consulte [Escalado de una caché de Redis con Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span><span class="sxs-lookup"><span data-stu-id="15fab-141">For more information on scaling with PowerShell, see [To scale a Redis cache using Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span></span>

### <a name="scale-using-azure-cli"></a><span data-ttu-id="15fab-142">Escalado con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="15fab-142">Scale using Azure CLI</span></span>
<span data-ttu-id="15fab-143">Para escalar las instancias de Azure Redis Cache con la CLI de Azure, llame al comando `azure rediscache set` y pase los cambios de configuración que desee que incluyen un nuevo tamaño, sku o tamaño de clúster, dependiendo de la operación de escalado deseada.</span><span class="sxs-lookup"><span data-stu-id="15fab-143">To scale your Azure Redis Cache instances using Azure CLI, call the `azure rediscache set` command and pass in the desired configuration changes that include a new size, sku, or cluster size, depending on the desired scaling operation.</span></span>

<span data-ttu-id="15fab-144">Para obtener más información sobre el escalado con la CLI de Azure, consulte [Cambio de la configuración de una caché en Redis existente](cache-manage-cli.md#scale).</span><span class="sxs-lookup"><span data-stu-id="15fab-144">For more information on scaling with Azure CLI, see [Change settings of an existing Redis Cache](cache-manage-cli.md#scale).</span></span>

### <a name="scale-using-maml"></a><span data-ttu-id="15fab-145">Escalado mediante MAML</span><span class="sxs-lookup"><span data-stu-id="15fab-145">Scale using MAML</span></span>
<span data-ttu-id="15fab-146">Para escalar las instancias de Azure Redis Cache mediante [Microsoft Azure Management Libraries (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), llame al método `IRedisOperations.CreateOrUpdate` y pase el nuevo tamaño para `RedisProperties.SKU.Capacity`.</span><span class="sxs-lookup"><span data-stu-id="15fab-146">To scale your Azure Redis Cache instances using the [Microsoft Azure Management Libraries (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), call the `IRedisOperations.CreateOrUpdate` method and pass in the new size for the `RedisProperties.SKU.Capacity`.</span></span>

    static void Main(string[] args)
    {
        // For instructions on getting the access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // To scale, set a new size for the redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

<span data-ttu-id="15fab-147">Para obtener más información, consulte el ejemplo [Administrar Caché en Redis mediante MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) .</span><span class="sxs-lookup"><span data-stu-id="15fab-147">For more information, see the [Manage Redis Cache using MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample.</span></span>

## <a name="scaling-faq"></a><span data-ttu-id="15fab-148">Preguntas frecuentes de escalado</span><span class="sxs-lookup"><span data-stu-id="15fab-148">Scaling FAQ</span></span>
<span data-ttu-id="15fab-149">La lista siguiente contiene las respuestas a las preguntas más frecuentes sobre el escalado de Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="15fab-149">The following list contains answers to commonly asked questions about Azure Redis Cache scaling.</span></span>

* [<span data-ttu-id="15fab-150">¿Puedo realizar operaciones de escalado en una memoria caché Premium?</span><span class="sxs-lookup"><span data-stu-id="15fab-150">Can I scale to, from, or within a Premium cache?</span></span>](#can-i-scale-to-from-or-within-a-premium-cache)
* [<span data-ttu-id="15fab-151">Después de escalar, ¿tengo que cambiar el nombre de la memoria caché o las teclas de acceso?</span><span class="sxs-lookup"><span data-stu-id="15fab-151">After scaling, do I have to change my cache name or access keys?</span></span>](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [<span data-ttu-id="15fab-152">¿Cómo funciona el escalado?</span><span class="sxs-lookup"><span data-stu-id="15fab-152">How does scaling work?</span></span>](#how-does-scaling-work)
* [<span data-ttu-id="15fab-153">¿Se pierden los datos de mi memoria caché durante el escalado?</span><span class="sxs-lookup"><span data-stu-id="15fab-153">Will I lose data from my cache during scaling?</span></span>](#will-i-lose-data-from-my-cache-during-scaling)
* [<span data-ttu-id="15fab-154">¿Mi configuración de bases de datos personalizada se ve afectada durante el escalado?</span><span class="sxs-lookup"><span data-stu-id="15fab-154">Is my custom databases setting affected during scaling?</span></span>](#is-my-custom-databases-setting-affected-during-scaling)
* [<span data-ttu-id="15fab-155">¿La caché estará disponible durante el escalado?</span><span class="sxs-lookup"><span data-stu-id="15fab-155">Will my cache be available during scaling?</span></span>](#will-my-cache-be-available-during-scaling)
* [<span data-ttu-id="15fab-156">Operaciones que no son compatibles</span><span class="sxs-lookup"><span data-stu-id="15fab-156">Operations that are not supported</span></span>](#operations-that-are-not-supported)
* [<span data-ttu-id="15fab-157">¿Cuánto tarda el escalado?</span><span class="sxs-lookup"><span data-stu-id="15fab-157">How long does scaling take?</span></span>](#how-long-does-scaling-take)
* [<span data-ttu-id="15fab-158">¿Cómo puedo saber si el escalado ha terminado?</span><span class="sxs-lookup"><span data-stu-id="15fab-158">How can I tell when scaling is complete?</span></span>](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a><span data-ttu-id="15fab-159">¿Puedo realizar operaciones de escalado en una memoria caché Premium?</span><span class="sxs-lookup"><span data-stu-id="15fab-159">Can I scale to, from, or within a Premium cache?</span></span>
* <span data-ttu-id="15fab-160">No puede escalar desde una caché **Premium** a un plan de tarifa **Básico** o **Estándar**.</span><span class="sxs-lookup"><span data-stu-id="15fab-160">You can't scale from a **Premium** cache down to a **Basic** or **Standard** pricing tier.</span></span>
* <span data-ttu-id="15fab-161">Puede escalar desde un plan de tarifa de caché **Premium** a otro.</span><span class="sxs-lookup"><span data-stu-id="15fab-161">You can scale from one **Premium** cache pricing tier to another.</span></span>
* <span data-ttu-id="15fab-162">No puede escalar de una memoria caché **Básica** directamente a una memoria caché **Premium**.</span><span class="sxs-lookup"><span data-stu-id="15fab-162">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="15fab-163">La primera operación debe ser escalar primero desde **Básica** a **Estándar** y, después, desde **Estándar** a **Premium** en una operación de escalado posterior.</span><span class="sxs-lookup"><span data-stu-id="15fab-163">You must first scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="15fab-164">Si ha habilitado la agrupación en clústeres cuando creó su caché **Premium**, puede [cambiar el tamaño de clúster](cache-how-to-premium-clustering.md#cluster-size).</span><span class="sxs-lookup"><span data-stu-id="15fab-164">If you enabled clustering when you created your **Premium** cache, you can [change the cluster size](cache-how-to-premium-clustering.md#cluster-size).</span></span> <span data-ttu-id="15fab-165">Si su caché se creó sin habilitar la agrupación en clústeres, no puede configurar la agrupación en clústeres después.</span><span class="sxs-lookup"><span data-stu-id="15fab-165">If your cache was created without clustering enabled, you can't configure clustering at a later time.</span></span>
  
  <span data-ttu-id="15fab-166">Para obtener más información, consulte [Cómo configurar la agrupación en clústeres para una instancia Premium de Azure Redis Cache](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="15fab-166">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>

### <a name="after-scaling-do-i-have-to-change-my-cache-name-or-access-keys"></a><span data-ttu-id="15fab-167">Después de escalar, ¿tengo que cambiar el nombre de la memoria caché o las teclas de acceso?</span><span class="sxs-lookup"><span data-stu-id="15fab-167">After scaling, do I have to change my cache name or access keys?</span></span>
<span data-ttu-id="15fab-168">No, el nombre de la memoria caché y las claves no se cambian durante una operación de escalado.</span><span class="sxs-lookup"><span data-stu-id="15fab-168">No, your cache name and keys are unchanged during a scaling operation.</span></span>

### <a name="how-does-scaling-work"></a><span data-ttu-id="15fab-169">¿Cómo funciona el escalado?</span><span class="sxs-lookup"><span data-stu-id="15fab-169">How does scaling work?</span></span>
* <span data-ttu-id="15fab-170">Cuando se escala una memoria caché **Basic** a un tamaño diferente, se cierra y se aprovisiona una nueva caché con el nuevo tamaño.</span><span class="sxs-lookup"><span data-stu-id="15fab-170">When a **Basic** cache is scaled to a different size, it is shut down and a new cache is provisioned using the new size.</span></span> <span data-ttu-id="15fab-171">Durante este tiempo, la caché no está disponible y se pierden todos los datos en la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="15fab-171">During this time, the cache is unavailable and all data in the cache is lost.</span></span>
* <span data-ttu-id="15fab-172">Cuando se escala una memoria caché del plan **Básico** al plan **Estándar**, se aprovisiona una caché de réplica y los datos se copian desde la caché principal a la de réplica.</span><span class="sxs-lookup"><span data-stu-id="15fab-172">When a **Basic** cache is scaled to a **Standard** cache, a replica cache is provisioned and the data is copied from the primary cache to the replica cache.</span></span> <span data-ttu-id="15fab-173">La memoria caché permanece disponible durante el proceso de escalado.</span><span class="sxs-lookup"><span data-stu-id="15fab-173">The cache remains available during the scaling process.</span></span>
* <span data-ttu-id="15fab-174">Cuando se escala una memoria caché del plan **Estándar** a un tamaño diferente o a una del plan **Premium**, se cierra una de las réplicas y se vuelve a aprovisionar para el nuevo tamaño y los datos se transfieren a través de ella y, después, la otra realiza una conmutación por error antes de volverse a aprovisionar, un proceso que es similar al que se produce durante un error en uno de los nodos de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="15fab-174">When a **Standard** cache is scaled to a different size or to a **Premium** cache, one of the replicas is shut down and re-provisioned to the new size and the data transferred over, and then the other replica performs a failover before it is re-provisioned, similar to the process that occurs during a failure of one of the cache nodes.</span></span>

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a><span data-ttu-id="15fab-175">¿Se pierden los datos de mi memoria caché durante el escalado?</span><span class="sxs-lookup"><span data-stu-id="15fab-175">Will I lose data from my cache during scaling?</span></span>
* <span data-ttu-id="15fab-176">Cuando se escala una memoria caché **Básica** a un nuevo tamaño, se pierden todos los datos y la memoria caché no está disponible durante la operación de escalado.</span><span class="sxs-lookup"><span data-stu-id="15fab-176">When a **Basic** cache is scaled to a new size, all data is lost and the cache is unavailable during the scaling operation.</span></span>
* <span data-ttu-id="15fab-177">Cuando se escala una memoria caché del plan **Básico** al plan **Estándar**, normalmente se conservan los datos de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="15fab-177">When a **Basic** cache is scaled to a **Standard** cache, the data in the cache is typically preserved.</span></span>
* <span data-ttu-id="15fab-178">Cuando se escala una memoria caché del plan **Estándar** a un tamaño o plan superior, o cuando una del plan **Premium** se escala a un tamaño superior, normalmente se conservan todos los datos.</span><span class="sxs-lookup"><span data-stu-id="15fab-178">When a **Standard** cache is scaled to a larger size or tier, or a **Premium** cache is scaled to a larger size, all data is typically preserved.</span></span> <span data-ttu-id="15fab-179">Si una memoria caché del plan **Estándar** o **Premium** se reduce verticalmente, la posibilidad de que se pierdan los datos depende de la cantidad que haya en la caché, en relación con el nuevo tamaño cuando se realice el escalado.</span><span class="sxs-lookup"><span data-stu-id="15fab-179">When scaling a **Standard** or **Premium** cache down to a smaller size, data may be lost depending on how much data is in the cache related to the new size when it is scaled.</span></span> <span data-ttu-id="15fab-180">Si se pierden datos al reducir, las claves se expulsan mediante el directiva de expulsión [allkeys-lru](http://redis.io/topics/lru-cache) .</span><span class="sxs-lookup"><span data-stu-id="15fab-180">If data is lost when scaling down, keys are evicted using the [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span> 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a><span data-ttu-id="15fab-181">¿Mi configuración de bases de datos personalizada se ve afectada durante el escalado?</span><span class="sxs-lookup"><span data-stu-id="15fab-181">Is my custom databases setting affected during scaling?</span></span>
<span data-ttu-id="15fab-182">Algunos planes de tarifa tienen diferentes [límites de bases de datos](cache-configure.md#databases), por lo que es preciso tener en cuenta varios factores al reducir verticalmente si se ha configurado un valor personalizado para el parámetro `databases` al crear la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="15fab-182">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when scaling down if you configured a custom value for the `databases` setting during cache creation.</span></span>

* <span data-ttu-id="15fab-183">Cuando se escala a un plan de tarifa con un límite de `databases` menor que el nivel actual:</span><span class="sxs-lookup"><span data-stu-id="15fab-183">When scaling to a pricing tier with a lower `databases` limit than the current tier:</span></span>
  * <span data-ttu-id="15fab-184">Si utiliza el número predeterminado de `databases`, que es 16 para todos los planes de tarifa, no se pierden datos.</span><span class="sxs-lookup"><span data-stu-id="15fab-184">If you are using the default number of `databases` which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="15fab-185">Si utiliza un número personalizado de `databases` que está dentro de los límites del plan al que va a escalar, se mantiene la configuración de `databases` y no se pierden datos.</span><span class="sxs-lookup"><span data-stu-id="15fab-185">If you are using a custom number of `databases` that falls within the limits for the tier to which you are scaling, this `databases` setting is retained and no data is lost.</span></span>
  * <span data-ttu-id="15fab-186">Si utiliza un número personalizado de `databases` que supera los límites del nuevo plan, el parámetro `databases` se reduce a los límites del nuevo plan y se pierden todos los datos de las bases de datos quitadas.</span><span class="sxs-lookup"><span data-stu-id="15fab-186">If you are using a custom number of `databases` that exceeds the limits of the new tier, the `databases` setting is lowered to the limits of the new tier and all data in the removed databases is lost.</span></span>
* <span data-ttu-id="15fab-187">Cuando se escala a un plan de tarifa con el mismo límite de `databases` o mayor que el plan actual, la configuración de `databases` se mantiene y no se pierden datos.</span><span class="sxs-lookup"><span data-stu-id="15fab-187">When scaling to a pricing tier with the same or higher `databases` limit than the current tier your `databases` setting is retained and no data is lost.</span></span>

<span data-ttu-id="15fab-188">Tenga en cuenta que mientras las memorias caché Standard y Premium tienen un contrato de nivel de servicio del 99,9% de disponibilidad, no hay ningún contrato de nivel de servicio para la pérdida de datos.</span><span class="sxs-lookup"><span data-stu-id="15fab-188">Note that while Standard and Premium caches have a 99.9% SLA for availability, there is no SLA for data loss.</span></span>

### <a name="will-my-cache-be-available-during-scaling"></a><span data-ttu-id="15fab-189">¿La caché estará disponible durante el escalado?</span><span class="sxs-lookup"><span data-stu-id="15fab-189">Will my cache be available during scaling?</span></span>
* <span data-ttu-id="15fab-190">Las memorias caché de los planes **Estándar** y **Premium** permanecen disponibles durante la operación de escalado.</span><span class="sxs-lookup"><span data-stu-id="15fab-190">**Standard** and **Premium** caches remain available during the scaling operation.</span></span>
* <span data-ttu-id="15fab-191">Las memorias caché del plan **Básico** están sin conexión durante las operaciones de escalado a un otro tamaño, pero siguen estando disponibles cuando se escala desde el plan **Básico** al **Estándar**.</span><span class="sxs-lookup"><span data-stu-id="15fab-191">**Basic** caches are offline during scaling operations to a different size, but remain available when scaling from **Basic** to **Standard**.</span></span>

### <a name="operations-that-are-not-supported"></a><span data-ttu-id="15fab-192">Operaciones que no son compatibles</span><span class="sxs-lookup"><span data-stu-id="15fab-192">Operations that are not supported</span></span>
* <span data-ttu-id="15fab-193">No se puede escalar desde un plan de tarifa superior a un plan de tarifa inferior.</span><span class="sxs-lookup"><span data-stu-id="15fab-193">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
  * <span data-ttu-id="15fab-194">No puede cambiar de una memoria caché **Premium** a una memoria caché **Estándar** o **Básica**.</span><span class="sxs-lookup"><span data-stu-id="15fab-194">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="15fab-195">No puede cambiar de una memoria caché **Estándar** a una memoria caché **Básica**.</span><span class="sxs-lookup"><span data-stu-id="15fab-195">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
* <span data-ttu-id="15fab-196">Puede cambiar de una memoria caché **Básica** a una memoria caché **Estándar**, pero no puede cambiar el tamaño al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="15fab-196">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="15fab-197">Si necesita un tamaño distinto, puede realizar una operación de escalado posterior hasta el tamaño deseado.</span><span class="sxs-lookup"><span data-stu-id="15fab-197">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
* <span data-ttu-id="15fab-198">No puede escalar de una memoria caché **Básica** directamente a una memoria caché **Premium**.</span><span class="sxs-lookup"><span data-stu-id="15fab-198">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="15fab-199">La primera operación debe ser escalar primero desde **Básica** a **Estándar** y, después, desde **Estándar** a **Premium** en una operación de escalado posterior.</span><span class="sxs-lookup"><span data-stu-id="15fab-199">You must first scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="15fab-200">No puede escalar desde un tamaño mayor hasta el tamaño **C0 (250 MB)** .</span><span class="sxs-lookup"><span data-stu-id="15fab-200">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>

<span data-ttu-id="15fab-201">Si se produce un error en una operación de escalado, el servicio intentará revertir la operación y la memoria caché se restablecerá al tamaño original.</span><span class="sxs-lookup"><span data-stu-id="15fab-201">If a scaling operation fails, the service will try to revert the operation and the cache will revert to the original size.</span></span>

### <a name="how-long-does-scaling-take"></a><span data-ttu-id="15fab-202">¿Cuánto tarda el escalado?</span><span class="sxs-lookup"><span data-stu-id="15fab-202">How long does scaling take?</span></span>
<span data-ttu-id="15fab-203">El escalado tarda aproximadamente 20 minutos, según la cantidad de datos que haya en la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="15fab-203">Scaling takes approximately 20 minutes, depending on how much data is in the cache.</span></span>

### <a name="how-can-i-tell-when-scaling-is-complete"></a><span data-ttu-id="15fab-204">¿Cómo puedo saber si el escalado ha terminado?</span><span class="sxs-lookup"><span data-stu-id="15fab-204">How can I tell when scaling is complete?</span></span>
<span data-ttu-id="15fab-205">En Azure Portal puede ver la operación de escalado en curso.</span><span class="sxs-lookup"><span data-stu-id="15fab-205">In the Azure portal you can see the scaling operation in progress.</span></span> <span data-ttu-id="15fab-206">Cuando se completa el escalado, el estado de la memoria caché cambia de **En ejecución**.</span><span class="sxs-lookup"><span data-stu-id="15fab-206">When scaling is complete, the status of the cache changes to **Running**.</span></span>

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



