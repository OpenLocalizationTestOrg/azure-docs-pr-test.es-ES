---
title: "aaaHow tooScale caché en Redis de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooscale su Redis de Azure, instancias de caché"
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
ms.openlocfilehash: 8d7c015a539f872913056392aa080bf3f445bd03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-azure-redis-cache"></a>Cómo tooScale Redis de Azure almacenan en caché
Caché en Redis de Azure tiene diferentes ofertas de caché, lo que proporciona flexibilidad en la elección de Hola de tamaño de caché y las características. Después de crea una memoria caché, puede ajustar tamaño de Hola y Hola tarifa de caché de hello si cambian los requisitos de saludo de la aplicación. Este artículo muestra cómo tooscale la memoria caché en hello portal de Azure y usar herramientas como PowerShell de Azure y la CLI de Azure.

## <a name="when-tooscale"></a>Cuando tooscale
Puede usar hello [supervisión](cache-how-to-monitor.md) características de caché en Redis de Azure toomonitor Hola estado y el rendimiento de la memoria caché y ayudar a determinar cuándo tooscale Hola caché. 

Puede supervisar siguiente Hola métricas toohelp determinar si necesita tooscale.

* Carga de servidor de Redis
* Uso de la memoria
* Ancho de banda de red
* Uso de CPU

Si determina que la memoria caché ya no cumple los requisitos de su aplicación, puede escalar tooa mayor o menor en memoria caché de tarifa que es adecuado para su aplicación. Para obtener más información acerca de cómo determinar que almacenar en caché toouse de nivel de precios, consulte [qué oferta de caché de Redis y tamaño debo usar](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).

## <a name="scale-a-cache"></a>Escalado de una caché
tooscale la memoria caché, [examinar la caché de toohello](cache-configure.md#configure-redis-cache-settings) en hello [portal de Azure](https://portal.azure.com) y haga clic en **escala** de hello **menú recursos**.

![Escala](./media/cache-how-to-scale/redis-cache-scale-menu.png)

Seleccione Hola deseado de tarifa de hello **seleccione tarifa** hoja y haga clic en **seleccione**.

![Plan de tarifa ][redis-cache-pricing-tier-blade]


Puede escalar tooa diferente de nivel de precios con hello después de restricciones:

* No se puede escalar de un plan de tarifa mayor nivel tooa menor nivel de precios.
  * No se puede escalar de un **Premium** caché hacia abajo tooa **estándar** o un **básica** memoria caché.
  * No se puede escalar de un **estándar** caché hacia abajo tooa **básica** memoria caché.
* Puede escalar de un **básica** almacenar en caché tooa **estándar** caché pero no se puede cambiar el tamaño de hello en hello mismo tiempo. Si tiene un tamaño diferente, puede hacer un tamaño de toohello deseado de operación de escalado posteriores.
* No se puede escalar de un **básica** almacenar en caché directamente tooa **Premium** memoria caché. Debe escalar **básica** demasiado**estándar** en una sola operación de escala y, a continuación, desde **estándar** demasiado**Premium** en una escala posteriores operación.
* No se puede escalar de un tamaño mayor profundidad toohello **C0 (250 MB)** tamaño.
 
Mientras caché Hola está reduciendo toohello nuevos tarifa, un **ajuste de escala en** estado se muestra en hello **caché en Redis** hoja.

![Escalado][redis-cache-scaling]

Cuando finalice el ajuste de escala, estado de hello cambia de **ajuste de escala en** demasiado**ejecutando**.

## <a name="how-tooautomate-a-scaling-operation"></a>¿Cómo tooautomate una operación de ajuste de escala
En suma tooscaling sus instancias de caché de Hola portal de Azure, puede escalar con los cmdlets de PowerShell, CLI de Azure y mediante el uso de hello las bibliotecas de administración de Microsoft Azure (MAML). 

* [Escalado mediante PowerShell](#scale-using-powershell)
* [Escalado con la CLI de Azure](#scale-using-azure-cli)
* [Escalado mediante MAML](#scale-using-maml)

### <a name="scale-using-powershell"></a>Escalado mediante PowerShell
Puede escalar las instancias de caché en Redis de Azure con PowerShell mediante el uso de hello [conjunto AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet cuando hello `Size`, `Sku`, o `ShardCount` propiedades se modifican. Hello en el ejemplo siguiente se muestra cómo tooscale una memoria caché denominado `myCache` 2,5 GB de memoria caché de tooa. 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

Para obtener más información sobre cómo ampliar con PowerShell, vea [tooscale un Redis almacenar en caché mediante Powershell](cache-howto-manage-redis-cache-powershell.md#scale).

### <a name="scale-using-azure-cli"></a>Escalado con la CLI de Azure
invocada por las instancias de caché en Redis de Azure mediante Azure CLI, tooscale hello `azure rediscache set` comando y pase los cambios de configuración de hello deseado que incluyen un nuevo tamaño, la sku o el tamaño de clúster, dependiendo de hello deseado de operación de escalado.

Para obtener más información sobre el escalado con la CLI de Azure, consulte [Cambio de la configuración de una caché en Redis existente](cache-manage-cli.md#scale).

### <a name="scale-using-maml"></a>Escalado mediante MAML
tooscale las instancias de caché en Redis de Azure con hello [bibliotecas de administración de Microsoft Azure (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), llamada hello `IRedisOperations.CreateOrUpdate` método y pase Hola nuevo tamaño hello `RedisProperties.SKU.Capacity`.

    static void Main(string[] args)
    {
        // For instructions on getting hello access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // tooscale, set a new size for hello redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

Para obtener más información, vea hello [administrar caché en Redis mediante MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) ejemplo.

## <a name="scaling-faq"></a>Preguntas frecuentes de escalado
Hello lista siguiente contiene toocommonly respuestas preguntas más frecuentes sobre escalar la memoria caché de Redis de Azure.

* [¿Puedo realizar operaciones de escalado en una memoria caché Premium?](#can-i-scale-to-from-or-within-a-premium-cache)
* [Después de escalar, ¿tengo toochange Mis claves de acceso o nombre de la memoria caché?](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [¿Cómo funciona el escalado?](#how-does-scaling-work)
* [¿Se pierden los datos de mi memoria caché durante el escalado?](#will-i-lose-data-from-my-cache-during-scaling)
* [¿Mi configuración de bases de datos personalizada se ve afectada durante el escalado?](#is-my-custom-databases-setting-affected-during-scaling)
* [¿La caché estará disponible durante el escalado?](#will-my-cache-be-available-during-scaling)
* [Operaciones que no son compatibles](#operations-that-are-not-supported)
* [¿Cuánto tarda el escalado?](#how-long-does-scaling-take)
* [¿Cómo puedo saber si el escalado ha terminado?](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a>¿Puedo realizar operaciones de escalado en una memoria caché Premium?
* No se puede escalar de un **Premium** caché hacia abajo tooa **básica** o **estándar** nivel de precios.
* Puede escalar de una **Premium** tooanother de nivel de precios de caché.
* No se puede escalar de un **básica** almacenar en caché directamente tooa **Premium** memoria caché. En primer lugar debe ajustar la escala de **básica** demasiado**estándar** en una sola operación de escala y, a continuación, desde **estándar** demasiado**Premium** en una posterior la operación de escalado.
* Si habilita la agrupación en clústeres cuando creó su **Premium** de memoria caché, también puede [cambiar el tamaño de clúster de hello](cache-how-to-premium-clustering.md#cluster-size). Si su caché se creó sin habilitar la agrupación en clústeres, no puede configurar la agrupación en clústeres después.
  
  Para obtener más información, consulte [cómo tooconfigure agrupación en clústeres para una caché en Redis de Azure Premium](cache-how-to-premium-clustering.md).

### <a name="after-scaling-do-i-have-toochange-my-cache-name-or-access-keys"></a>Después de escalar, ¿tengo toochange Mis claves de acceso o nombre de la memoria caché?
No, el nombre de la memoria caché y las claves no se cambian durante una operación de escalado.

### <a name="how-does-scaling-work"></a>¿Cómo funciona el escalado?
* Cuando un **básica** caché se escala tooa tamaño distinto, se cierra y se aprovisiona una nueva memoria caché con el nuevo tamaño de Hola. Durante este tiempo, Hola caché no está disponible y se pierden todos los datos en memoria caché de Hola.
* Cuando un **básica** caché es escalado tooa **estándar** de memoria caché, se aprovisiona una caché de réplica y Hola datos se copian de caché de réplica de hello caché principal toohello. caché de Hello sigue estando disponible durante Hola ajuste de escala en proceso.
* Cuando un **estándar** caché es tooa escala de tamaño distinto o tooa **Premium** memoria caché, una de las réplicas de Hola se apaga y se vuelven a aprovisionar toohello nueva hello y tamaño de datos transferidos a través y, a continuación, Hola otro réplica realiza una conmutación por error antes de se vuelven a aprovisionar, el proceso toohello similar que se produce durante un error de uno de los nodos de la memoria caché de Hola.

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a>¿Se pierden los datos de mi memoria caché durante el escalado?
* Cuando un **básica** caché se escalado tooa nuevo tamaño, todos los datos se pierde y Hola caché no está disponible durante la operación de escalado de Hola.
* Cuando un **básica** caché es escalado tooa **estándar** caché, hello en memoria caché de Hola se suelen conservar los datos.
* Cuando un **estándar** caché es tooa escala mayor tamaño o nivel, o un **Premium** se escala caché normalmente se conserva el tamaño de tooa, todos los datos. Al escalar un **estándar** o **Premium** caché hacia abajo de menor tamaño tooa, datos podrían perderse según la cantidad de datos está en memoria caché de hello relacionadas con toohello nuevo tamaño al que se escala. Si se pierden datos al escalar hacia abajo, las claves se desalojan con hello [allkeys lru](http://redis.io/topics/lru-cache) directiva de expulsión. 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a>¿Mi configuración de bases de datos personalizada se ve afectada durante el escalado?
Algunos niveles de precios tienen diferentes [límites de las bases de datos](cache-configure.md#databases), por lo que hay algunas consideraciones cuando reduzca if configura un valor personalizado para hello `databases` establecer durante la creación de la memoria caché.

* Cuando ajuste de escala tooa tarifa con un menor `databases` límite que el nivel actual de hello:
  * Si usas el número predeterminado de Hola de `databases` que es 16 para todos los niveles de precios, se perderá ningún dato.
  * Si usas un número personalizado de `databases` que entra dentro de los límites de Hola para toowhich de nivel de hello escalará, esto `databases` configuración se mantiene y se perderá ningún dato.
  * Si usas un número personalizado de `databases` que supera los límites de Hola de nuevo nivel hello, hello `databases` configuración está toohello menor de los límites del nuevo nivel de Hola y se pierden todos los datos en bases de datos de hello quita.
* Cuando ajuste de escala tooa tarifa con hello, igual o mayor `databases` límite que el nivel actual de hello su `databases` configuración se mantiene y se perderá ningún dato.

Tenga en cuenta que mientras las memorias caché Standard y Premium tienen un contrato de nivel de servicio del 99,9% de disponibilidad, no hay ningún contrato de nivel de servicio para la pérdida de datos.

### <a name="will-my-cache-be-available-during-scaling"></a>¿La caché estará disponible durante el escalado?
* **Estándar** y **Premium** memorias caché permanecen disponibles durante la operación de escalado de Hola.
* **Básico** memorias caché están sin conexión durante el ajuste de tamaño de las operaciones tooa distinto, pero siguen estando disponibles si la escala de **básica** demasiado**estándar**.

### <a name="operations-that-are-not-supported"></a>Operaciones que no son compatibles
* No se puede escalar de un plan de tarifa mayor nivel tooa menor nivel de precios.
  * No se puede escalar de un **Premium** caché hacia abajo tooa **estándar** o un **básica** memoria caché.
  * No se puede escalar de un **estándar** caché hacia abajo tooa **básica** memoria caché.
* Puede escalar de un **básica** almacenar en caché tooa **estándar** caché pero no se puede cambiar el tamaño de hello en hello mismo tiempo. Si tiene un tamaño diferente, puede hacer un tamaño de toohello deseado de operación de escalado posteriores.
* No se puede escalar de un **básica** almacenar en caché directamente tooa **Premium** memoria caché. En primer lugar debe ajustar la escala de **básica** demasiado**estándar** en una sola operación de escala y, a continuación, desde **estándar** demasiado**Premium** en una posterior la operación de escalado.
* No se puede escalar de un tamaño mayor profundidad toohello **C0 (250 MB)** tamaño.

Si se produce un error en una operación de escalado, servicio de Hola se e intente la operación de hello toorevert y caché de hello volverá toohello de tamaño original.

### <a name="how-long-does-scaling-take"></a>¿Cuánto tarda el escalado?
Ajuste de escala tarda aproximadamente 20 minutos, según la cantidad de datos está en memoria caché de Hola.

### <a name="how-can-i-tell-when-scaling-is-complete"></a>¿Cómo puedo saber si el escalado ha terminado?
Hola portal de Azure puede ver Hola la operación de escalado en curso. Cuando finalice el ajuste de escala, Hola estado de los cambios de la memoria caché de hello demasiado**ejecutando**.

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



