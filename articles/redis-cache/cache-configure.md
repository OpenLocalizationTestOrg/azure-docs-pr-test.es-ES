---
title: "aaaHow tooconfigure caché en Redis de Azure | Documentos de Microsoft"
description: "Comprender la configuración de Redis Hola predeterminada para caché en Redis de Azure y obtenga información acerca de cómo tooconfigure su Redis de Azure, instancias de caché"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a><span data-ttu-id="44e1c-103">Cómo tooconfigure Redis de Azure almacenan en caché</span><span class="sxs-lookup"><span data-stu-id="44e1c-103">How tooconfigure Azure Redis Cache</span></span>
<span data-ttu-id="44e1c-104">Este tema describe cómo Hola tooreview y actualización de configuración para las instancias de caché en Redis de Azure y la configuración del servidor de Redis portadas Hola predeterminado para instancias de caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="44e1c-104">This topic describes how tooreview and update hello configuration for your Azure Redis Cache instances, and covers hello default Redis server configuration for Azure Redis Cache instances.</span></span>

> [!NOTE]
> <span data-ttu-id="44e1c-105">Para obtener más información sobre cómo configurar y usar las características de caché premium, consulte [cómo persistencia tooconfigure](cache-how-to-premium-persistence.md), [cómo tooconfigure clústeres](cache-how-to-premium-clustering.md), y [cómo son compatibles con tooconfigure red Virtual ](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-105">For more information on configuring and using premium cache features, see [How tooconfigure persistence](cache-how-to-premium-persistence.md), [How tooconfigure clustering](cache-how-to-premium-clustering.md), and [How tooconfigure Virtual Network support](cache-how-to-premium-vnet.md).</span></span>
> 
> 

## <a name="configure-redis-cache-settings"></a><span data-ttu-id="44e1c-106">Configuración de opciones de la memoria caché en Redis</span><span class="sxs-lookup"><span data-stu-id="44e1c-106">Configure Redis cache settings</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="44e1c-107">Configuración de caché en Redis de Azure se ven y se configuran en hello **caché en Redis** hoja con la opción hello **menú recursos**.</span><span class="sxs-lookup"><span data-stu-id="44e1c-107">Azure Redis Cache settings are viewed and configured on hello **Redis Cache** blade using hello **Resource Menu**.</span></span>

![Caché en Redis - Configuración](./media/cache-configure/redis-cache-settings.png)

<span data-ttu-id="44e1c-109">Puede ver y configurar Hola después de la configuración mediante hello **menú recursos**.</span><span class="sxs-lookup"><span data-stu-id="44e1c-109">You can view and configure hello following settings using hello **Resource Menu**.</span></span>

* [<span data-ttu-id="44e1c-110">Información general</span><span class="sxs-lookup"><span data-stu-id="44e1c-110">Overview</span></span>](#overview)
* [<span data-ttu-id="44e1c-111">Registro de actividad</span><span class="sxs-lookup"><span data-stu-id="44e1c-111">Activity log</span></span>](#activity-log)
* [<span data-ttu-id="44e1c-112">Control de acceso (IAM)</span><span class="sxs-lookup"><span data-stu-id="44e1c-112">Access control (IAM)</span></span>](#access-control-iam)
* [<span data-ttu-id="44e1c-113">Etiquetas</span><span class="sxs-lookup"><span data-stu-id="44e1c-113">Tags</span></span>](#tags)
* [<span data-ttu-id="44e1c-114">Diagnóstico y solución de problemas</span><span class="sxs-lookup"><span data-stu-id="44e1c-114">Diagnose and solve problems</span></span>](#diagnose-and-solve-problems)
* [<span data-ttu-id="44e1c-115">Configuración</span><span class="sxs-lookup"><span data-stu-id="44e1c-115">Settings</span></span>](#settings)
    * [<span data-ttu-id="44e1c-116">Claves de acceso</span><span class="sxs-lookup"><span data-stu-id="44e1c-116">Access keys</span></span>](#access-keys)
    * [<span data-ttu-id="44e1c-117">Configuración avanzada</span><span class="sxs-lookup"><span data-stu-id="44e1c-117">Advanced settings</span></span>](#advanced-settings)
    * [<span data-ttu-id="44e1c-118">Asesor de caché en Redis</span><span class="sxs-lookup"><span data-stu-id="44e1c-118">Redis Cache Advisor</span></span>](#redis-cache-advisor)
    * [<span data-ttu-id="44e1c-119">Escala</span><span class="sxs-lookup"><span data-stu-id="44e1c-119">Scale</span></span>](#scale)
    * [<span data-ttu-id="44e1c-120">Tamaño del Clúster en Redis</span><span class="sxs-lookup"><span data-stu-id="44e1c-120">Redis cluster size</span></span>](#cluster-size)
    * [<span data-ttu-id="44e1c-121">Persistencia de datos de Redis</span><span class="sxs-lookup"><span data-stu-id="44e1c-121">Redis data persistence</span></span>](#redis-data-persistence)
    * [<span data-ttu-id="44e1c-122">Programación de actualizaciones</span><span class="sxs-lookup"><span data-stu-id="44e1c-122">Schedule updates</span></span>](#schedule-updates)
    * [<span data-ttu-id="44e1c-123">Replicación geográfica</span><span class="sxs-lookup"><span data-stu-id="44e1c-123">Geo-replication</span></span>](#geo-replication)
    * [<span data-ttu-id="44e1c-124">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="44e1c-124">Virtual Network</span></span>](#virtual-network)
    * [<span data-ttu-id="44e1c-125">Firewall</span><span class="sxs-lookup"><span data-stu-id="44e1c-125">Firewall</span></span>](#firewall)
    * [<span data-ttu-id="44e1c-126">Propiedades</span><span class="sxs-lookup"><span data-stu-id="44e1c-126">Properties</span></span>](#properties)
    * [<span data-ttu-id="44e1c-127">Bloqueos</span><span class="sxs-lookup"><span data-stu-id="44e1c-127">Locks</span></span>](#locks)
    * [<span data-ttu-id="44e1c-128">Script de automatización</span><span class="sxs-lookup"><span data-stu-id="44e1c-128">Automation script</span></span>](#automation-script)
* [<span data-ttu-id="44e1c-129">Administración</span><span class="sxs-lookup"><span data-stu-id="44e1c-129">Administration</span></span>](#administration)
    * [<span data-ttu-id="44e1c-130">Importación de datos</span><span class="sxs-lookup"><span data-stu-id="44e1c-130">Import data</span></span>](#importexport)
    * [<span data-ttu-id="44e1c-131">Exportación de datos</span><span class="sxs-lookup"><span data-stu-id="44e1c-131">Export data</span></span>](#importexport)
    * [<span data-ttu-id="44e1c-132">Reboot</span><span class="sxs-lookup"><span data-stu-id="44e1c-132">Reboot</span></span>](#reboot)
* [<span data-ttu-id="44e1c-133">Supervisión</span><span class="sxs-lookup"><span data-stu-id="44e1c-133">Monitoring</span></span>](#monitoring)
    * [<span data-ttu-id="44e1c-134">Métricas de Redis</span><span class="sxs-lookup"><span data-stu-id="44e1c-134">Redis metrics</span></span>](#redis-metrics)
    * [<span data-ttu-id="44e1c-135">Reglas de alertas</span><span class="sxs-lookup"><span data-stu-id="44e1c-135">Alert rules</span></span>](#alert-rules)
    * [<span data-ttu-id="44e1c-136">Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="44e1c-136">Diagnostics</span></span>](#diagnostics)
* [<span data-ttu-id="44e1c-137">Configuración de soporte técnico y solución de problemas</span><span class="sxs-lookup"><span data-stu-id="44e1c-137">Support & troubleshooting settings</span></span>](#support-amp-troubleshooting-settings)
    * [<span data-ttu-id="44e1c-138">Estado de los recursos</span><span class="sxs-lookup"><span data-stu-id="44e1c-138">Resource health</span></span>](#resource-health)
    * [<span data-ttu-id="44e1c-139">Nueva solicitud de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="44e1c-139">New support request</span></span>](#new-support-request)


## <a name="overview"></a><span data-ttu-id="44e1c-140">Información general</span><span class="sxs-lookup"><span data-stu-id="44e1c-140">Overview</span></span>

<span data-ttu-id="44e1c-141">**Información general** proporciona también con información básica sobre la memoria caché, como el nombre, puertos, plan de tarifa y las métricas de la caché seleccionada.</span><span class="sxs-lookup"><span data-stu-id="44e1c-141">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span></span>

### <a name="activity-log"></a><span data-ttu-id="44e1c-142">Registro de actividades</span><span class="sxs-lookup"><span data-stu-id="44e1c-142">Activity log</span></span>

<span data-ttu-id="44e1c-143">Haga clic en **registro de actividad** tooview acciones realizan en la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-143">Click **Activity log** tooview actions performed on your cache.</span></span> <span data-ttu-id="44e1c-144">También puede usar filtrado tooexpand esta tooinclude ver otros recursos.</span><span class="sxs-lookup"><span data-stu-id="44e1c-144">You can also use filtering tooexpand this view tooinclude other resources.</span></span> <span data-ttu-id="44e1c-145">Para obtener más información sobre cómo trabajar con los registros de auditoría, consulte [Operaciones de auditoría con Resource Manager](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-145">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span></span> <span data-ttu-id="44e1c-146">Para obtener más información sobre la supervisión de eventos de Caché en Redis de Azure, consulte [Operaciones y alertas](cache-how-to-monitor.md#operations-and-alerts).</span><span class="sxs-lookup"><span data-stu-id="44e1c-146">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="access-control-iam"></a><span data-ttu-id="44e1c-147">Control de acceso (IAM)</span><span class="sxs-lookup"><span data-stu-id="44e1c-147">Access control (IAM)</span></span>

<span data-ttu-id="44e1c-148">Hola **(de índices IAM) de control de acceso** sección proporciona compatibilidad para control de acceso basado en roles (RBAC) en hello Azure toohelp portal las organizaciones a cumplir sus requisitos de administración de acceso sencilla y precisa.</span><span class="sxs-lookup"><span data-stu-id="44e1c-148">hello **Access control (IAM)** section provides support for role-based access control (RBAC) in hello Azure portal toohelp organizations meet their access management requirements simply and precisely.</span></span> <span data-ttu-id="44e1c-149">Para obtener más información, consulte [el control de acceso basada en roles en el portal de Azure hello](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-149">For more information, see [Role-based access control in hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>

### <a name="tags"></a><span data-ttu-id="44e1c-150">Etiquetas</span><span class="sxs-lookup"><span data-stu-id="44e1c-150">Tags</span></span>

<span data-ttu-id="44e1c-151">Hola **etiquetas** sección le ayudará a organizar los recursos.</span><span class="sxs-lookup"><span data-stu-id="44e1c-151">hello **Tags** section helps you organize your resources.</span></span> <span data-ttu-id="44e1c-152">Para obtener más información, consulte [mediante etiquetas tooorganize los recursos de Azure](../azure-resource-manager/resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-152">For more information, see [Using tags tooorganize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>


### <a name="diagnose-and-solve-problems"></a><span data-ttu-id="44e1c-153">Diagnosticar y solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="44e1c-153">Diagnose and solve problems</span></span>

<span data-ttu-id="44e1c-154">Haga clic en **diagnosticar y resolver problemas** toobe proporcionada con problemas comunes y estrategias para resolverlos.</span><span class="sxs-lookup"><span data-stu-id="44e1c-154">Click **Diagnose and solve problems** toobe provided with common issues and strategies for resolving them.</span></span>



## <a name="settings"></a><span data-ttu-id="44e1c-155">Settings</span><span class="sxs-lookup"><span data-stu-id="44e1c-155">Settings</span></span>
<span data-ttu-id="44e1c-156">Hola **configuración** sección permite tooaccess y configurar Hola después de la configuración de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-156">hello **Settings** section allows you tooaccess and configure hello following settings for your cache.</span></span>

* [<span data-ttu-id="44e1c-157">Claves de acceso</span><span class="sxs-lookup"><span data-stu-id="44e1c-157">Access keys</span></span>](#access-keys)
* [<span data-ttu-id="44e1c-158">Configuración avanzada</span><span class="sxs-lookup"><span data-stu-id="44e1c-158">Advanced settings</span></span>](#advanced-settings)
* [<span data-ttu-id="44e1c-159">Asesor de caché en Redis</span><span class="sxs-lookup"><span data-stu-id="44e1c-159">Redis Cache Advisor</span></span>](#redis-cache-advisor)
* [<span data-ttu-id="44e1c-160">Escala</span><span class="sxs-lookup"><span data-stu-id="44e1c-160">Scale</span></span>](#scale)
* [<span data-ttu-id="44e1c-161">Tamaño del Clúster en Redis</span><span class="sxs-lookup"><span data-stu-id="44e1c-161">Redis cluster size</span></span>](#cluster-size)
* [<span data-ttu-id="44e1c-162">Persistencia de datos de Redis</span><span class="sxs-lookup"><span data-stu-id="44e1c-162">Redis data persistence</span></span>](#redis-data-persistence)
* [<span data-ttu-id="44e1c-163">Programación de actualizaciones</span><span class="sxs-lookup"><span data-stu-id="44e1c-163">Schedule updates</span></span>](#schedule-updates)
* [<span data-ttu-id="44e1c-164">Replicación geográfica</span><span class="sxs-lookup"><span data-stu-id="44e1c-164">Geo-replication</span></span>](#geo-replication)
* [<span data-ttu-id="44e1c-165">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="44e1c-165">Virtual Network</span></span>](#virtual-network)
* [<span data-ttu-id="44e1c-166">Firewall</span><span class="sxs-lookup"><span data-stu-id="44e1c-166">Firewall</span></span>](#firewall)
* [<span data-ttu-id="44e1c-167">Propiedades</span><span class="sxs-lookup"><span data-stu-id="44e1c-167">Properties</span></span>](#properties)
* [<span data-ttu-id="44e1c-168">Bloqueos</span><span class="sxs-lookup"><span data-stu-id="44e1c-168">Locks</span></span>](#locks)
* [<span data-ttu-id="44e1c-169">Script de automatización</span><span class="sxs-lookup"><span data-stu-id="44e1c-169">Automation script</span></span>](#automation-script)



### <a name="access-keys"></a><span data-ttu-id="44e1c-170">Claves de acceso</span><span class="sxs-lookup"><span data-stu-id="44e1c-170">Access keys</span></span>
<span data-ttu-id="44e1c-171">Haga clic en **las claves de acceso** acceso hello tooview o volver a generar las claves de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-171">Click **Access keys** tooview or regenerate hello access keys for your cache.</span></span> <span data-ttu-id="44e1c-172">Estas teclas se utilizan los clientes de hello tooyour caché de conexión.</span><span class="sxs-lookup"><span data-stu-id="44e1c-172">These keys are used by hello clients connecting tooyour cache.</span></span>

![Caché en Redis - Claves de acceso](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a><span data-ttu-id="44e1c-174">Configuración avanzada</span><span class="sxs-lookup"><span data-stu-id="44e1c-174">Advanced settings</span></span>
<span data-ttu-id="44e1c-175">Hello siguiente se configura en hello **configuración avanzada** hoja.</span><span class="sxs-lookup"><span data-stu-id="44e1c-175">hello following settings are configured on hello **Advanced settings** blade.</span></span>

* [<span data-ttu-id="44e1c-176">Puertos de acceso</span><span class="sxs-lookup"><span data-stu-id="44e1c-176">Access Ports</span></span>](#access-ports)
* [<span data-ttu-id="44e1c-177">Directivas de memoria</span><span class="sxs-lookup"><span data-stu-id="44e1c-177">Memory policies</span></span>](#memory-policies)
* [<span data-ttu-id="44e1c-178">Notificaciones de espacio de claves (configuración avanzada)</span><span class="sxs-lookup"><span data-stu-id="44e1c-178">Keyspace notifications (advanced settings)</span></span>](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a><span data-ttu-id="44e1c-179">Puertos de acceso</span><span class="sxs-lookup"><span data-stu-id="44e1c-179">Access Ports</span></span>
<span data-ttu-id="44e1c-180">El acceso no SSL está deshabilitado de forma predeterminada para las nuevas cachés.</span><span class="sxs-lookup"><span data-stu-id="44e1c-180">By default, non-SSL access is disabled for new caches.</span></span> <span data-ttu-id="44e1c-181">tooenable Hola sin SSL de puerto, haga clic en **No** para **permitir el acceso sólo a través de SSL** en hello **configuración avanzada** hoja y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="44e1c-181">tooenable hello non-SSL port, click **No** for **Allow access only via SSL** on hello **Advanced settings** blade and then click **Save**.</span></span>

![Caché en Redis - Puertos de acceso](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a><span data-ttu-id="44e1c-183">Directivas de memoria</span><span class="sxs-lookup"><span data-stu-id="44e1c-183">Memory policies</span></span>
<span data-ttu-id="44e1c-184">Hola **directiva Maxmemory**, **reservado maxmemory**, y **reservado maxfragmentationmemory** configuración en hello **Configuraciónavanzada**hoja configurar directivas de memoria de Hola para caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="44e1c-184">hello **Maxmemory policy**, **maxmemory-reserved**, and **maxfragmentationmemory-reserved** settings on hello **Advanced settings** blade configure hello memory policies for hello cache.</span></span>

![Caché en Redis - Directiva Maxmemory](./media/cache-configure/redis-cache-maxmemory-policy.png)

<span data-ttu-id="44e1c-186">**Directiva MaxMemory** configura la directiva de expulsión de Hola para caché de Hola y le permite toochoose de hello las siguientes directivas de expulsión:</span><span class="sxs-lookup"><span data-stu-id="44e1c-186">**Maxmemory policy** configures hello eviction policy for hello cache and allows you toochoose from hello following eviction policies:</span></span>

* <span data-ttu-id="44e1c-187">`volatile-lru`-Éste es el predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="44e1c-187">`volatile-lru` - this is hello default.</span></span>
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

<span data-ttu-id="44e1c-188">Para más información sobre las directivas `maxmemory`, consulte [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies) (Directivas de expulsión).</span><span class="sxs-lookup"><span data-stu-id="44e1c-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span></span>

<span data-ttu-id="44e1c-189">Hola **reservado maxmemory** configura cantidad Hola de memoria en MB que se reserva para las operaciones de caché no es como la replicación durante la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="44e1c-189">hello **maxmemory-reserved** setting configures hello amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span></span> <span data-ttu-id="44e1c-190">Este valor permite toohave una experiencia más coherente de servidor de Redis cuando varía la carga.</span><span class="sxs-lookup"><span data-stu-id="44e1c-190">Setting this value allows you toohave a more consistent Redis server experience when your load varies.</span></span> <span data-ttu-id="44e1c-191">Este valor debe establecerse más alto para cargas de trabajo con muchas operaciones de escritura.</span><span class="sxs-lookup"><span data-stu-id="44e1c-191">This value should be set higher for workloads that are write heavy.</span></span> <span data-ttu-id="44e1c-192">Cuando se reserva memoria para dichas operaciones, no está disponible para el almacenamiento de datos en caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-192">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="44e1c-193">Hola **maxfragmentationmemory reservadas** configura cantidad Hola de memoria en MB que está reservada tooaccommodate fragmentación de memoria.</span><span class="sxs-lookup"><span data-stu-id="44e1c-193">hello **maxfragmentationmemory-reserved** setting configures hello amount of memory in MB that is reserved tooaccommodate for memory fragmentation.</span></span> <span data-ttu-id="44e1c-194">Este valor permite toohave una experiencia más coherente de servidor de Redis cuando Hola caché está llena o la proporción de fragmentación de hello y toofull cierre también es alta.</span><span class="sxs-lookup"><span data-stu-id="44e1c-194">Setting this value allows you toohave a more consistent Redis server experience when hello cache is full or close toofull and hello fragmentation ratio is also high.</span></span> <span data-ttu-id="44e1c-195">Cuando se reserva memoria para dichas operaciones, no está disponible para el almacenamiento de datos en caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-195">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="44e1c-196">Una cuestión que hay tooconsider al elegir un nuevo valor de reserva de memoria (**reservado maxmemory** o **reservado maxfragmentationmemory**) es cómo este cambio puede afectar a una caché que ya se está ejecutando con grandes cantidades de datos en ella.</span><span class="sxs-lookup"><span data-stu-id="44e1c-196">One thing tooconsider when choosing a new memory reservation value (**maxmemory-reserved** or **maxfragmentationmemory-reserved**) is how this change might affect a cache that is already running with large amounts of data in it.</span></span> <span data-ttu-id="44e1c-197">Por ejemplo, si tienen una memoria caché de 53 GB con 49 GB de datos, cambiar Hola reserva valor too8 GB, Esto quitará la memoria disponible max Hola para sistema Hola hacia abajo too45 GB.</span><span class="sxs-lookup"><span data-stu-id="44e1c-197">For instance, if you have a 53 GB cache with 49 GB of data, then change hello reservation value too8 GB, this will drop hello max available memory for hello system down too45 GB.</span></span> <span data-ttu-id="44e1c-198">Si el valor actual `used_memory` o su `used_memory_rss` valores son mayores que el nuevo límite de Hola de 45 GB, a continuación, sistema de hello tendrá datos tooevict hasta que `used_memory` y `used_memory_rss` están por debajo de 45 GB.</span><span class="sxs-lookup"><span data-stu-id="44e1c-198">If either your current `used_memory` or your `used_memory_rss` values are higher than hello new limit of 45 GB, then hello system will have tooevict data until both `used_memory` and `used_memory_rss` are below 45 GB.</span></span> <span data-ttu-id="44e1c-199">La expulsión puede aumentar la carga del servidor y la fragmentación de memoria.</span><span class="sxs-lookup"><span data-stu-id="44e1c-199">Eviction can increase server load and memory fragmentation.</span></span> <span data-ttu-id="44e1c-200">Para más información sobre las métricas de caché como `used_memory` y `used_memory_rss`, vea [Métricas disponibles e intervalos de informes](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span><span class="sxs-lookup"><span data-stu-id="44e1c-200">For more information on cache metrics such as `used_memory` and `used_memory_rss`, see [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44e1c-201">Hola **reservado maxmemory** y **reservado maxfragmentationmemory** configuraciones solo están disponibles para el nivel Standard y Premium almacena en caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-201">hello **maxmemory-reserved** and **maxfragmentationmemory-reserved** settings are only available for Standard and Premium caches.</span></span>
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a><span data-ttu-id="44e1c-202">Notificaciones de espacio de claves (configuración avanzada)</span><span class="sxs-lookup"><span data-stu-id="44e1c-202">Keyspace notifications (advanced settings)</span></span>
<span data-ttu-id="44e1c-203">Redis keyspace las notificaciones están configuradas en hello **configuración avanzada** hoja.</span><span class="sxs-lookup"><span data-stu-id="44e1c-203">Redis keyspace notifications are configured on hello **Advanced settings** blade.</span></span> <span data-ttu-id="44e1c-204">Notificaciones de Keyspace permiten a los clientes tooreceive notificaciones cuando se producen determinados eventos.</span><span class="sxs-lookup"><span data-stu-id="44e1c-204">Keyspace notifications allow clients tooreceive notifications when certain events occur.</span></span>

![Caché en Redis - Configuración avanzada](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> <span data-ttu-id="44e1c-206">Keyspace hello y notificaciones **eventos keyspace notificar** configuración solo están disponibles para las memorias caché Standard y Premium.</span><span class="sxs-lookup"><span data-stu-id="44e1c-206">Keyspace notifications and hello **notify-keyspace-events** setting are only available for Standard and Premium caches.</span></span>
> 
> 

<span data-ttu-id="44e1c-207">Para obtener más información, vea [Notificaciones de espacio de claves de Redis](http://redis.io/topics/notifications).</span><span class="sxs-lookup"><span data-stu-id="44e1c-207">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span></span> <span data-ttu-id="44e1c-208">Ejemplo de código, vea hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) archivo Hola [Hola a todos](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) ejemplo.</span><span class="sxs-lookup"><span data-stu-id="44e1c-208">For sample code, see hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a><span data-ttu-id="44e1c-209">Asesor de caché en Redis</span><span class="sxs-lookup"><span data-stu-id="44e1c-209">Redis Cache Advisor</span></span>
<span data-ttu-id="44e1c-210">Hola **Asesor de caché de Redis** hoja muestra recomendaciones para la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-210">hello **Redis Cache Advisor** blade displays recommendations for your cache.</span></span> <span data-ttu-id="44e1c-211">Durante las operaciones normales, no se muestra ninguna recomendación.</span><span class="sxs-lookup"><span data-stu-id="44e1c-211">During normal operations, no recommendations are displayed.</span></span> 

![Recomendaciones](./media/cache-configure/redis-cache-no-recommendations.png)

<span data-ttu-id="44e1c-213">Si las condiciones se producen durante las operaciones de saludo de la memoria caché como mayor uso de memoria, ancho de banda de red o de carga del servidor, se muestra una alerta en hello **caché en Redis** hoja.</span><span class="sxs-lookup"><span data-stu-id="44e1c-213">If any conditions occur during hello operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on hello **Redis Cache** blade.</span></span>

![Recomendaciones](./media/cache-configure/redis-cache-recommendations-alert.png)

<span data-ttu-id="44e1c-215">Puede encontrar información adicional en hello **recomendaciones** hoja.</span><span class="sxs-lookup"><span data-stu-id="44e1c-215">Further information can be found on hello **Recommendations** blade.</span></span>

![Recomendaciones](./media/cache-configure/redis-cache-recommendations.png)

<span data-ttu-id="44e1c-217">Puede supervisar estas métricas en hello [gráficos de supervisión](cache-how-to-monitor.md#monitoring-charts) y [gráficos de uso](cache-how-to-monitor.md#usage-charts) secciones de hello **caché en Redis** hoja.</span><span class="sxs-lookup"><span data-stu-id="44e1c-217">You can monitor these metrics on hello [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of hello **Redis Cache** blade.</span></span>

<span data-ttu-id="44e1c-218">Cada plan de tarifa tiene distintos límites para las conexiones de cliente, memoria y ancho de banda.</span><span class="sxs-lookup"><span data-stu-id="44e1c-218">Each pricing tier has different limits for client connections, memory, and bandwidth.</span></span> <span data-ttu-id="44e1c-219">Si la caché se aproxima a la capacidad máxima para estas métricas durante un período prolongado, se crea una recomendación.</span><span class="sxs-lookup"><span data-stu-id="44e1c-219">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span></span> <span data-ttu-id="44e1c-220">Para obtener más información acerca de las métricas de Hola y límites revisados hello **recomendaciones** herramienta, vea hello en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="44e1c-220">For more information about hello metrics and limits reviewed by hello **Recommendations** tool, see hello following table:</span></span>

| <span data-ttu-id="44e1c-221">Métrica de Caché en Redis</span><span class="sxs-lookup"><span data-stu-id="44e1c-221">Redis Cache metric</span></span> | <span data-ttu-id="44e1c-222">Más información</span><span class="sxs-lookup"><span data-stu-id="44e1c-222">More information</span></span> |
| --- | --- |
| <span data-ttu-id="44e1c-223">Uso de ancho de banda de red</span><span class="sxs-lookup"><span data-stu-id="44e1c-223">Network bandwidth usage</span></span> |[<span data-ttu-id="44e1c-224">Rendimiento de la caché: ancho de banda disponible</span><span class="sxs-lookup"><span data-stu-id="44e1c-224">Cache performance - available bandwidth</span></span>](cache-faq.md#cache-performance) |
| <span data-ttu-id="44e1c-225">Clientes conectados</span><span class="sxs-lookup"><span data-stu-id="44e1c-225">Connected clients</span></span> |[<span data-ttu-id="44e1c-226">Configuración predeterminada del servidor Redis: maxclients</span><span class="sxs-lookup"><span data-stu-id="44e1c-226">Default Redis server configuration - maxclients</span></span>](#maxclients) |
| <span data-ttu-id="44e1c-227">Carga de servidor</span><span class="sxs-lookup"><span data-stu-id="44e1c-227">Server load</span></span> |[<span data-ttu-id="44e1c-228">Gráficos de uso: carga del servidor Redis</span><span class="sxs-lookup"><span data-stu-id="44e1c-228">Usage charts - Redis Server Load</span></span>](cache-how-to-monitor.md#usage-charts) |
| <span data-ttu-id="44e1c-229">Uso de la memoria</span><span class="sxs-lookup"><span data-stu-id="44e1c-229">Memory usage</span></span> |[<span data-ttu-id="44e1c-230">Rendimiento y tamaño de la memoria caché</span><span class="sxs-lookup"><span data-stu-id="44e1c-230">Cache performance - size</span></span>](cache-faq.md#cache-performance) |

<span data-ttu-id="44e1c-231">tooupgrade la memoria caché, haga clic en **actualizar ahora** hello toochange nivel de precios y [escala](#scale) la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-231">tooupgrade your cache, click **Upgrade now** toochange hello pricing tier and [scale](#scale) your cache.</span></span> <span data-ttu-id="44e1c-232">Para más información sobre cómo elegir un plan de tarifa, consulte [¿Qué oferta y tamaño de Redis Caché debo utilizar?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="44e1c-232">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>


### <a name="scale"></a><span data-ttu-id="44e1c-233">Escala</span><span class="sxs-lookup"><span data-stu-id="44e1c-233">Scale</span></span>
<span data-ttu-id="44e1c-234">Haga clic en **escala** tooview o cambiar Hola tarifa de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-234">Click **Scale** tooview or change hello pricing tier for your cache.</span></span> <span data-ttu-id="44e1c-235">Para obtener más información sobre cómo ampliar, consulte [cómo tooScale Redis de Azure almacenan en caché](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-235">For more information on scaling, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>

![Nivel de precios de Caché en Redis](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a><span data-ttu-id="44e1c-237">Tamaño del Clúster en Redis</span><span class="sxs-lookup"><span data-stu-id="44e1c-237">Redis Cluster Size</span></span>
<span data-ttu-id="44e1c-238">Haga clic en **tamaño de clúster de Redis (vista previa)** toochange el tamaño del clúster de Hola para una ejecución premium de caché con clúster habilitado.</span><span class="sxs-lookup"><span data-stu-id="44e1c-238">Click **(PREVIEW) Redis Cluster Size** toochange hello cluster size for a running premium cache with clustering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="44e1c-239">Tenga en cuenta que mientras hello Azure Redis caché Premium nivel ha sido liberado tooGeneral disponibilidad, la característica de tamaño de clúster Redis Hola está actualmente en vista previa.</span><span class="sxs-lookup"><span data-stu-id="44e1c-239">Note that while hello Azure Redis Cache Premium tier has been released tooGeneral Availability, hello Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Tamaño del Clúster en Redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

<span data-ttu-id="44e1c-241">tamaño de clúster de toochange hello, utilice el control deslizante de Hola o escriba un número entre 1 y 10 en hello **número de particiones** cuadro de texto y haga clic en **Aceptar** toosave.</span><span class="sxs-lookup"><span data-stu-id="44e1c-241">toochange hello cluster size, use hello slider or type a number between 1 and 10 in hello **Shard count** text box and click **OK** toosave.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44e1c-242">La agrupación en clústeres de Redis solo está disponible para las memorias cachés premium.</span><span class="sxs-lookup"><span data-stu-id="44e1c-242">Redis clustering is only available for Premium caches.</span></span> <span data-ttu-id="44e1c-243">Para obtener más información, consulte [cómo tooconfigure agrupación en clústeres para una caché en Redis de Azure Premium](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-243">For more information, see [How tooconfigure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>
> 
> 


### <a name="redis-data-persistence"></a><span data-ttu-id="44e1c-244">Persistencia de datos de Redis</span><span class="sxs-lookup"><span data-stu-id="44e1c-244">Redis data persistence</span></span>
<span data-ttu-id="44e1c-245">Haga clic en **Redis persistencia de los datos** tooenable, deshabilitar o configurar la persistencia de datos de la memoria caché premium.</span><span class="sxs-lookup"><span data-stu-id="44e1c-245">Click **Redis data persistence** tooenable, disable, or configure data persistence for your premium cache.</span></span> <span data-ttu-id="44e1c-246">Azure Redis Cache ofrece persistencia de Redis mediante [persistencia de RDB](cache-how-to-premium-persistence.md#configure-rdb-persistence) o [persistencia de AOF](cache-how-to-premium-persistence.md#configure-aof-persistence).</span><span class="sxs-lookup"><span data-stu-id="44e1c-246">Azure Redis Cache offers Redis persistence using either [RDB persistence](cache-how-to-premium-persistence.md#configure-rdb-persistence) or [AOF persistence](cache-how-to-premium-persistence.md#configure-aof-persistence).</span></span>

<span data-ttu-id="44e1c-247">Para obtener más información, consulte [cómo persistencia tooconfigure para una caché de Redis de Azure Premium](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-247">For more information, see [How tooconfigure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="44e1c-248">La persistencia de los datos en Redis solo está disponible para las memorias cachés premium.</span><span class="sxs-lookup"><span data-stu-id="44e1c-248">Redis data persistence is only available for Premium caches.</span></span> 
> 
> 

### <a name="schedule-updates"></a><span data-ttu-id="44e1c-249">Programar actualizaciones</span><span class="sxs-lookup"><span data-stu-id="44e1c-249">Schedule updates</span></span>
<span data-ttu-id="44e1c-250">Hola **programar actualizaciones** hoja permite toodesignate una ventana de mantenimiento para las actualizaciones de servidor de Redis para la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-250">hello **Schedule updates** blade allows you toodesignate a maintenance window for Redis server updates for your cache.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="44e1c-251">ventana de mantenimiento de Hola aplica solo las actualizaciones de servidor de tooRedis y tooany Azure actualiza o actualiza el sistema de operativo toohello de máquinas virtuales de Hola que hospedan la memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="44e1c-251">hello maintenance window applies only tooRedis server updates, and not tooany Azure updates or updates toohello operating system of hello VMs that host hello cache.</span></span>
> 
> 

![Programar actualizaciones](./media/cache-configure/redis-schedule-updates.png)

<span data-ttu-id="44e1c-253">toospecify una ventana de mantenimiento, los días de hello deseado y especifique la hora de inicio de ventana de mantenimiento de Hola para cada día y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="44e1c-253">toospecify a maintenance window, check hello desired days and specify hello maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="44e1c-254">Tenga en cuenta que es hora de ventana de mantenimiento de hello en UTC.</span><span class="sxs-lookup"><span data-stu-id="44e1c-254">Note that hello maintenance window time is in UTC.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="44e1c-255">Hola **programar actualizaciones** funcionalidad solo está disponible para las cachés de nivel Premium.</span><span class="sxs-lookup"><span data-stu-id="44e1c-255">hello **Schedule updates** functionality is only available for Premium tier caches.</span></span> <span data-ttu-id="44e1c-256">Para más información e instrucciones, consulte [Administración de la Caché en Redis de Azure - Programación de actualizaciones](cache-administration.md#schedule-updates).</span><span class="sxs-lookup"><span data-stu-id="44e1c-256">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span></span>
> 
> 

### <a name="geo-replication"></a><span data-ttu-id="44e1c-257">Replicación geográfica</span><span class="sxs-lookup"><span data-stu-id="44e1c-257">Geo-replication</span></span>

<span data-ttu-id="44e1c-258">Hola **georreplicación** hoja proporciona un mecanismo para vincular dos instancias de caché en Redis de Azure de nivel Premium.</span><span class="sxs-lookup"><span data-stu-id="44e1c-258">hello **Geo-replication** blade provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="44e1c-259">Una memoria caché se designa como caché primaria vinculada de Hola y Hola otro como caché secundaria vinculado de Hola.</span><span class="sxs-lookup"><span data-stu-id="44e1c-259">One cache is designated as hello primary linked cache, and hello other as hello secondary linked cache.</span></span> <span data-ttu-id="44e1c-260">caché secundaria vinculado de Hello pasa a ser de solo lectura, y datos de caché principal toohello escrito es replican toohello secundario vinculado caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-260">hello secondary linked cache becomes read-only, and data written toohello primary cache is replicated toohello secondary linked cache.</span></span> <span data-ttu-id="44e1c-261">Esta funcionalidad puede ser tooreplicate usa una memoria caché en regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="44e1c-261">This functionality can be used tooreplicate a cache across Azure regions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44e1c-262">La **replicación geográfica** solo está disponible para las cachés de nivel Premium.</span><span class="sxs-lookup"><span data-stu-id="44e1c-262">**Geo-replication** is only available for Premium tier caches.</span></span> <span data-ttu-id="44e1c-263">Para obtener más información e instrucciones, consulte [cómo tooconfigure replicación geográfica para caché en Redis de Azure](cache-how-to-geo-replication.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-263">For more information and instructions, see [How tooconfigure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md).</span></span>
> 
> 

### <a name="virtual-network"></a><span data-ttu-id="44e1c-264">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="44e1c-264">Virtual Network</span></span>
<span data-ttu-id="44e1c-265">Hola **red Virtual** sección le permite la configuración de red virtual de hello tooconfigure de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-265">hello **Virtual Network** section allows you tooconfigure hello virtual network settings for your cache.</span></span> <span data-ttu-id="44e1c-266">Para obtener información sobre cómo crear una caché premium con red virtual admiten y actualizar su configuración, consulte [cómo tooconfigure admite la red Virtual para una caché de Redis de Azure Premium](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-266">For information on creating a premium cache with VNET support and updating its settings, see [How tooconfigure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44e1c-267">La configuración de red virtual solo está disponible para las memorias cachés premium que se configuraron con la compatibilidad de la red virtual durante la creación de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span></span> 
> 
> 

### <a name="firewall"></a><span data-ttu-id="44e1c-268">Firewall</span><span class="sxs-lookup"><span data-stu-id="44e1c-268">Firewall</span></span>

<span data-ttu-id="44e1c-269">Haga clic en **Firewall** tooview y configurar las reglas de firewall para la caché en Redis de Azure Premium.</span><span class="sxs-lookup"><span data-stu-id="44e1c-269">Click **Firewall** tooview and configure firewall rules for your Premium Azure Redis Cache.</span></span>

![Firewall](./media/cache-configure/redis-firewall-rules.png)

<span data-ttu-id="44e1c-271">Puede especificar las reglas de firewall con un intervalo de direcciones IP de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="44e1c-271">You can specify firewall rules with a start and end IP address range.</span></span> <span data-ttu-id="44e1c-272">Cuando se configuran las reglas de firewall, solo las conexiones de cliente de hello especifican intervalos de direcciones IP pueden conectar toohello caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-272">When firewall rules are configured, only client connections from hello specified IP address ranges can connect toohello cache.</span></span> <span data-ttu-id="44e1c-273">Cuando se guarda una regla de firewall no hay un breve retraso antes de regla de hello es efectivo.</span><span class="sxs-lookup"><span data-stu-id="44e1c-273">When a firewall rule is saved there is a short delay before hello rule is effective.</span></span> <span data-ttu-id="44e1c-274">Normalmente, este retraso es inferior a un minuto.</span><span class="sxs-lookup"><span data-stu-id="44e1c-274">This delay is typically less than one minute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44e1c-275">Siempre se permiten las conexiones de los sistemas de supervisión de Azure Redis Cache, incluso si se configuran reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="44e1c-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span></span>
> 
> <span data-ttu-id="44e1c-276">El reinicio solo está disponible para las memorias caché de nivel Premium.</span><span class="sxs-lookup"><span data-stu-id="44e1c-276">Firewall rules are only available for Premium tier caches.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="44e1c-277">Propiedades</span><span class="sxs-lookup"><span data-stu-id="44e1c-277">Properties</span></span>
<span data-ttu-id="44e1c-278">Haga clic en **propiedades** tooview información acerca de la memoria caché, incluidos los puertos y el extremo de la memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="44e1c-278">Click **Properties** tooview information about your cache, including hello cache endpoint and ports.</span></span>

![Caché en Redis - Propiedades](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a><span data-ttu-id="44e1c-280">Bloqueos</span><span class="sxs-lookup"><span data-stu-id="44e1c-280">Locks</span></span>
<span data-ttu-id="44e1c-281">Hola **bloquea** sección le permite toolock una suscripción, el grupo de recursos o recursos tooprevent otros usuarios de su organización accidentalmente eliminen o modifiquen los recursos críticos.</span><span class="sxs-lookup"><span data-stu-id="44e1c-281">hello **Locks** section allows you toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="44e1c-282">Para obtener más información, consulte [Bloqueo de recursos con el Administrador de recursos de Azure](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

### <a name="automation-script"></a><span data-ttu-id="44e1c-283">Script de automatización</span><span class="sxs-lookup"><span data-stu-id="44e1c-283">Automation script</span></span>

<span data-ttu-id="44e1c-284">Haga clic en **script de automatización** toobuild y exportar una plantilla de los recursos implementados para futuras implementaciones.</span><span class="sxs-lookup"><span data-stu-id="44e1c-284">Click **Automation script** toobuild and export a template of your deployed resources for future deployments.</span></span> <span data-ttu-id="44e1c-285">Para más información sobre cómo trabajar con plantillas, consulte [Implementación de recursos con las plantillas de Resource Manager y Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="administration-settings"></a><span data-ttu-id="44e1c-286">Configuración de administración</span><span class="sxs-lookup"><span data-stu-id="44e1c-286">Administration settings</span></span>
<span data-ttu-id="44e1c-287">Hola configuración Hola **administración** sección le permiten hello tooperform después de las tareas administrativas de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-287">hello settings in hello **Administration** section allow you tooperform hello following administrative tasks for your cache.</span></span> 

![Administración](./media/cache-configure/redis-cache-administration.png)

* [<span data-ttu-id="44e1c-289">Importación de datos</span><span class="sxs-lookup"><span data-stu-id="44e1c-289">Import data</span></span>](#importexport)
* [<span data-ttu-id="44e1c-290">Exportación de datos</span><span class="sxs-lookup"><span data-stu-id="44e1c-290">Export data</span></span>](#importexport)
* [<span data-ttu-id="44e1c-291">Reboot</span><span class="sxs-lookup"><span data-stu-id="44e1c-291">Reboot</span></span>](#reboot)


### <a name="importexport"></a><span data-ttu-id="44e1c-292">Importación/Exportación</span><span class="sxs-lookup"><span data-stu-id="44e1c-292">Import/Export</span></span>
<span data-ttu-id="44e1c-293">Importación y exportación es una operación de administración de datos de caché en Redis de Azure, que le permite tooimport y exportar datos en memoria caché de hello al importar y exportar una instantánea de base de datos de caché de Redis (RDB) de un blob en páginas tooa caché premium en una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="44e1c-293">Import/Export is an Azure Redis Cache data management operation, which allows you tooimport and export data in hello cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache tooa page blob in an Azure Storage Account.</span></span> <span data-ttu-id="44e1c-294">Importación y exportación permite toomigrate entre distintas instancias de caché en Redis de Azure o rellenar Hola caché con los datos antes de su uso.</span><span class="sxs-lookup"><span data-stu-id="44e1c-294">Import/Export enables you toomigrate between different Azure Redis Cache instances or populate hello cache with data before use.</span></span>

<span data-ttu-id="44e1c-295">Importación puede ser toobring usado Redis compatible RDB archivos desde cualquier servidor de Redis que se ejecute en cualquier nube o el entorno, incluidos Redis que se ejecutan en Linux, Windows o cualquier proveedor de nube, como Amazon Web Services y otros.</span><span class="sxs-lookup"><span data-stu-id="44e1c-295">Import can be used toobring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="44e1c-296">Importación de datos es un toocreate fácilmente una memoria caché con datos rellenadas previamente.</span><span class="sxs-lookup"><span data-stu-id="44e1c-296">Importing data is an easy way toocreate a cache with pre-populated data.</span></span> <span data-ttu-id="44e1c-297">Durante el proceso de importación de hello, caché en Redis de Azure carga archivos RDB Hola del almacenamiento de Azure en la memoria y, a continuación, inserta las claves de hello en memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="44e1c-297">During hello import process, Azure Redis Cache loads hello RDB files from Azure storage into memory, and then inserts hello keys into hello cache.</span></span>

<span data-ttu-id="44e1c-298">Exportación permite datos de hello tooexport almacenados en caché en Redis de Azure tooRedis compatible RDB archivos.</span><span class="sxs-lookup"><span data-stu-id="44e1c-298">Export allows you tooexport hello data stored in Azure Redis Cache tooRedis compatible RDB files.</span></span> <span data-ttu-id="44e1c-299">Puede usar estos datos de toomove característica de una caché en Redis de Azure instancia tooanother o un servidor de Redis tooanother.</span><span class="sxs-lookup"><span data-stu-id="44e1c-299">You can use this feature toomove data from one Azure Redis Cache instance tooanother or tooanother Redis server.</span></span> <span data-ttu-id="44e1c-300">Durante el proceso de exportación de hello, se crea un archivo temporal en hello VM que hosts Hola instancia del servidor de caché en Redis de Azure y archivo hello toohello cargado designado de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="44e1c-300">During hello export process, a temporary file is created on hello VM that hosts hello Azure Redis Cache server instance, and hello file is uploaded toohello designated storage account.</span></span> <span data-ttu-id="44e1c-301">Cuando se completa la operación de exportación de hello con estado de éxito o error, se elimina el archivo temporal de Hola.</span><span class="sxs-lookup"><span data-stu-id="44e1c-301">When hello export operation completes with either a status of success or failure, hello temporary file is deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44e1c-302">Importación/Exportación solo está disponible para las memorias caché de nivel premium.</span><span class="sxs-lookup"><span data-stu-id="44e1c-302">Import/Export is only available for Premium tier caches.</span></span> <span data-ttu-id="44e1c-303">Para más información e instrucciones, consulte [Importación y exportación de datos en la Caché en Redis de Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-303">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

### <a name="reboot"></a><span data-ttu-id="44e1c-304">Reboot</span><span class="sxs-lookup"><span data-stu-id="44e1c-304">Reboot</span></span>
<span data-ttu-id="44e1c-305">Hola **reiniciar** hoja permite nodos de hello tooreboot de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-305">hello **Reboot** blade allows you tooreboot hello nodes of your cache.</span></span> <span data-ttu-id="44e1c-306">Esta capacidad de reinicio permite que se tootest la aplicación para proporcionar resistencia si se produce un error de un nodo de caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-306">This reboot capability enables you tootest your application for resiliency if there is a failure of a cache node.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot.png)

<span data-ttu-id="44e1c-308">Si tiene una caché premium con clúster habilitado, puede seleccionar qué particiones de hello caché tooreboot.</span><span class="sxs-lookup"><span data-stu-id="44e1c-308">If you have a premium cache with clustering enabled, you can select which shards of hello cache tooreboot.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot-cluster.png)

<span data-ttu-id="44e1c-310">tooreboot uno o varios nodos de la memoria caché, seleccione los nodos de hello deseado y haga clic en **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="44e1c-310">tooreboot one or more nodes of your cache, select hello desired nodes and click **Reboot**.</span></span> <span data-ttu-id="44e1c-311">Si tiene una caché premium con clúster habilitado, seleccione tooreboot de las particiones de hello y, a continuación, haga clic en **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="44e1c-311">If you have a premium cache with clustering enabled, select hello shard(s) tooreboot and then click **Reboot**.</span></span> <span data-ttu-id="44e1c-312">Después de unos minutos, Hola reinicio de los nodos seleccionados y son volver a conectarse más tarde unos minutos.</span><span class="sxs-lookup"><span data-stu-id="44e1c-312">After a few minutes, hello selected node(s) reboot, and are back online a few minutes later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44e1c-313">El reinicio ahora está disponible para todos los planes de tarifas.</span><span class="sxs-lookup"><span data-stu-id="44e1c-313">Reboot is now available for all pricing tiers.</span></span> <span data-ttu-id="44e1c-314">Para más información e instrucciones, consulte [Administración de Caché en Redis de Azure - Reboot](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="44e1c-314">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span></span>
> 
> 


## <a name="monitoring"></a><span data-ttu-id="44e1c-315">Supervisión</span><span class="sxs-lookup"><span data-stu-id="44e1c-315">Monitoring</span></span>

<span data-ttu-id="44e1c-316">Hola **supervisión** sección le permite tooconfigure diagnósticos y supervisión de la memoria caché de Redis.</span><span class="sxs-lookup"><span data-stu-id="44e1c-316">hello **Monitoring** section allows you tooconfigure diagnostics and monitoring for your Redis Cache.</span></span> <span data-ttu-id="44e1c-317">Para obtener más información sobre la supervisión de la caché de Redis de Azure y diagnósticos, vea [cómo toomonitor Redis de Azure almacenan en caché](cache-how-to-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-317">For more information on Azure Redis Cache monitoring and diagnostics, see [How toomonitor Azure Redis Cache](cache-how-to-monitor.md).</span></span>

![Diagnóstico](./media/cache-configure/redis-cache-diagnostics.png)

* [<span data-ttu-id="44e1c-319">Métricas de Redis</span><span class="sxs-lookup"><span data-stu-id="44e1c-319">Redis metrics</span></span>](#redis-metrics)
* [<span data-ttu-id="44e1c-320">Reglas de alertas</span><span class="sxs-lookup"><span data-stu-id="44e1c-320">Alert rules</span></span>](#alert-rules)
* [<span data-ttu-id="44e1c-321">Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="44e1c-321">Diagnostics</span></span>](#diagnostics)

### <a name="redis-metrics"></a><span data-ttu-id="44e1c-322">Caché en Redis</span><span class="sxs-lookup"><span data-stu-id="44e1c-322">Redis metrics</span></span>
<span data-ttu-id="44e1c-323">Haga clic en **Redis métricas** demasiado[ver las métricas](cache-how-to-monitor.md#view-cache-metrics) de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-323">Click **Redis metrics** too[view metrics](cache-how-to-monitor.md#view-cache-metrics) for your cache.</span></span>

### <a name="alert-rules"></a><span data-ttu-id="44e1c-324">Las reglas de alertas</span><span class="sxs-lookup"><span data-stu-id="44e1c-324">Alert rules</span></span>

<span data-ttu-id="44e1c-325">Haga clic en **reglas de alerta** alertas tooconfigure según las métricas de caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="44e1c-325">Click **Alert rules** tooconfigure alerts based on Redis Cache metrics.</span></span> <span data-ttu-id="44e1c-326">Para obtener más información, consulte [Alerts](cache-how-to-monitor.md#alerts) (Alertas).</span><span class="sxs-lookup"><span data-stu-id="44e1c-326">For more information, see [Alerts](cache-how-to-monitor.md#alerts).</span></span>

### <a name="diagnostics"></a><span data-ttu-id="44e1c-327">Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="44e1c-327">Diagnostics</span></span>

<span data-ttu-id="44e1c-328">De manera predeterminada, en Azure Monitor las métricas de caché se [almacenan durante 30 días](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) y después se eliminan.</span><span class="sxs-lookup"><span data-stu-id="44e1c-328">By default, cache metrics in Azure Monitor are [stored for 30 days](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) and then deleted.</span></span> <span data-ttu-id="44e1c-329">toopersist las métricas de memoria caché durante más de 30 días, haga clic en ejecutar **diagnósticos** demasiado[Configurar cuenta de almacenamiento de hello](cache-how-to-monitor.md#export-cache-metrics) usar diagnósticos de caché toostore.</span><span class="sxs-lookup"><span data-stu-id="44e1c-329">toopersist your cache metrics for longer than 30 days, click **Diagnostics** too[configure hello storage account](cache-how-to-monitor.md#export-cache-metrics) used toostore cache diagnostics.</span></span>

>[!NOTE]
><span data-ttu-id="44e1c-330">En suma tooarchiving su toostorage de métricas de caché, también puede [transmitirlos tooan concentrador de eventos o enviarlos tooLog análisis](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span><span class="sxs-lookup"><span data-stu-id="44e1c-330">In addition tooarchiving your cache metrics toostorage, you can also [stream them tooan Event hub or send them tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span></span>
>
>

## <a name="support--troubleshooting-settings"></a><span data-ttu-id="44e1c-331">Configuración de soporte técnico y solución de problemas</span><span class="sxs-lookup"><span data-stu-id="44e1c-331">Support & troubleshooting settings</span></span>
<span data-ttu-id="44e1c-332">Hola configuración Hola **soporte técnico y solución de problemas** sección proporcionan opciones para resolver problemas con la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-332">hello settings in hello **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span></span>

![Soporte y solución de problemas](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [<span data-ttu-id="44e1c-334">Estado de los recursos</span><span class="sxs-lookup"><span data-stu-id="44e1c-334">Resource health</span></span>](#resource-health)
* [<span data-ttu-id="44e1c-335">Nueva solicitud de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="44e1c-335">New support request</span></span>](#new-support-request)

### <a name="resource-health"></a><span data-ttu-id="44e1c-336">Estado de los recursos</span><span class="sxs-lookup"><span data-stu-id="44e1c-336">Resource health</span></span>
<span data-ttu-id="44e1c-337">**estado de los recursos** supervisa el recurso e indica si se ejecuta del modo previsto.</span><span class="sxs-lookup"><span data-stu-id="44e1c-337">**Resource health** watches your resource and tells you if it's running as expected.</span></span> <span data-ttu-id="44e1c-338">Para obtener más información acerca de hello servicio de mantenimiento de recursos de Azure, consulte [información general de mantenimiento de recursos de Azure](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-338">For more information about hello Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="44e1c-339">Estado del recurso es tooreport actualmente, no en estado de Hola de instancias de caché en Redis de Azure hospedados en una red virtual.</span><span class="sxs-lookup"><span data-stu-id="44e1c-339">Resource health is currently unable tooreport on hello health of Azure Redis Cache instances hosted in a virtual network.</span></span> <span data-ttu-id="44e1c-340">Para más información, consulte [¿Funcionarán todas las características al alojar una caché en una red virtual?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span><span class="sxs-lookup"><span data-stu-id="44e1c-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span></span>
> 
> 

### <a name="new-support-request"></a><span data-ttu-id="44e1c-341">Nueva solicitud de soporte</span><span class="sxs-lookup"><span data-stu-id="44e1c-341">New support request</span></span>
<span data-ttu-id="44e1c-342">Haga clic en **nueva solicitud de soporte técnico** tooopen una solicitud de soporte técnico de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-342">Click **New support request** tooopen a support request for your cache.</span></span>





## <a name="default-redis-server-configuration"></a><span data-ttu-id="44e1c-343">Configuración predeterminada del servidor Redis</span><span class="sxs-lookup"><span data-stu-id="44e1c-343">Default Redis server configuration</span></span>
<span data-ttu-id="44e1c-344">Nuevas instancias de caché en Redis de Azure se configuran con hello después de valores de configuración de Redis predeterminados.</span><span class="sxs-lookup"><span data-stu-id="44e1c-344">New Azure Redis Cache instances are configured with hello following default Redis configuration values.</span></span>

> [!NOTE]
> <span data-ttu-id="44e1c-345">no se puede cambiar la configuración de Hello en esta sección con hello `StackExchange.Redis.IServer.ConfigSet` método.</span><span class="sxs-lookup"><span data-stu-id="44e1c-345">hello settings in this section cannot be changed using hello `StackExchange.Redis.IServer.ConfigSet` method.</span></span> <span data-ttu-id="44e1c-346">Si se llama a este método con uno de los comandos de hello en esta sección, se produce un siguiente toohello similar de excepción:</span><span class="sxs-lookup"><span data-stu-id="44e1c-346">If this method is called with one of hello commands in this section, an exception similar toohello following is thrown:</span></span>  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> <span data-ttu-id="44e1c-347">Los valores que se pueden configurables como **directiva de memoria máximo**, son configurables a través del portal de Azure de Hola o herramientas de administración de línea de comandos como PowerShell o CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="44e1c-347">Any values that are configurable, such as **max-memory-policy**, are configurable through hello Azure portal or command-line management tools such as Azure CLI or PowerShell.</span></span>
> 
> 

| <span data-ttu-id="44e1c-348">Configuración</span><span class="sxs-lookup"><span data-stu-id="44e1c-348">Setting</span></span> | <span data-ttu-id="44e1c-349">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="44e1c-349">Default value</span></span> | <span data-ttu-id="44e1c-350">Descripción</span><span class="sxs-lookup"><span data-stu-id="44e1c-350">Description</span></span> |
| --- | --- | --- |
| `databases` |<span data-ttu-id="44e1c-351">16</span><span class="sxs-lookup"><span data-stu-id="44e1c-351">16</span></span> |<span data-ttu-id="44e1c-352">número predeterminado de Hola de bases de datos es 16, pero se puede configurar un diferentes hello en función de número de tarifa. <sup>1</sup> base de datos de hello predeterminada es DB 0, puede seleccionar uno diferente según la por conexión mediante `connection.GetDatabase(dbid)` donde `dbid` es un número entre `0` y `databases - 1`.</span><span class="sxs-lookup"><span data-stu-id="44e1c-352">hello default number of databases is 16 but you can configure a different number based on hello pricing tier.<sup>1</sup> hello default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span></span> |
| `maxclients` |<span data-ttu-id="44e1c-353">Depende de nivel de precios de hello<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="44e1c-353">Depends on hello pricing tier<sup>2</sup></span></span> |<span data-ttu-id="44e1c-354">Es Hola número máximo de clientes conectados permitido en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="44e1c-354">This is hello maximum number of connected clients allowed at hello same time.</span></span> <span data-ttu-id="44e1c-355">Cuando se alcanza el límite de hello Redis cierra todas las conexiones nuevas de hello, devolver un error de 'número máximo de clientes alcanzada'.</span><span class="sxs-lookup"><span data-stu-id="44e1c-355">Once hello limit is reached Redis closes all hello new connections, returning a 'max number of clients reached' error.</span></span> |
| `maxmemory-policy` |`volatile-lru` |<span data-ttu-id="44e1c-356">Directiva MaxMemory es la configuración de hello para el modo en que Redis selecciona qué tooremove cuando `maxmemory` (tamaño de Hola de oferta seleccionado cuando creó la caché de hello de la caché de Hola) se alcanza.</span><span class="sxs-lookup"><span data-stu-id="44e1c-356">Maxmemory policy is hello setting for how Redis selects what tooremove when `maxmemory` (hello size of hello cache offering you selected when you created hello cache) is reached.</span></span> <span data-ttu-id="44e1c-357">No tiene valor predeterminado de Hola de caché en Redis de Azure es configuración `volatile-lru`, lo que elimina las claves de hello con una expiración definida mediante un algoritmo LRU.</span><span class="sxs-lookup"><span data-stu-id="44e1c-357">With Azure Redis Cache hello default setting is `volatile-lru`, which removes hello keys with an expiration set using an LRU algorithm.</span></span> <span data-ttu-id="44e1c-358">Este valor se puede configurar en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="44e1c-358">This setting can be configured in hello Azure portal.</span></span> <span data-ttu-id="44e1c-359">Para más información, vea [Directivas de memoria](#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="44e1c-359">For more information, see [Memory policies](#memory-policies).</span></span> |
| `maxmemory-samples` |<span data-ttu-id="44e1c-360">3</span><span class="sxs-lookup"><span data-stu-id="44e1c-360">3</span></span> |<span data-ttu-id="44e1c-361">memoria de toosave, LRU y algoritmos TTL mínimo son aproximados algoritmos en lugar de algoritmos precisos.</span><span class="sxs-lookup"><span data-stu-id="44e1c-361">toosave memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span></span> <span data-ttu-id="44e1c-362">De forma predeterminada, Redis comprobaciones tres claves y recoge Hola uno que se utilizó menos recientemente.</span><span class="sxs-lookup"><span data-stu-id="44e1c-362">By default Redis checks three keys and picks hello one that was used less recently.</span></span> |
| `lua-time-limit` |<span data-ttu-id="44e1c-363">5.000</span><span class="sxs-lookup"><span data-stu-id="44e1c-363">5,000</span></span> |<span data-ttu-id="44e1c-364">Tiempo máximo de ejecución de un script Lua en milisegundos.</span><span class="sxs-lookup"><span data-stu-id="44e1c-364">Max execution time of a Lua script in milliseconds.</span></span> <span data-ttu-id="44e1c-365">Si se alcanza el tiempo de ejecución máximo de hello, Redis registra que sigue en ejecución después de hello máxima permitida de una secuencia de comandos y tooreply tooqueries inicia con un error.</span><span class="sxs-lookup"><span data-stu-id="44e1c-365">If hello maximum execution time is reached, Redis logs that a script is still in execution after hello maximum allowed time, and starts tooreply tooqueries with an error.</span></span> |
| `lua-event-limit` |<span data-ttu-id="44e1c-366">500</span><span class="sxs-lookup"><span data-stu-id="44e1c-366">500</span></span> |<span data-ttu-id="44e1c-367">Tamaño máximo de la cola de eventos de script.</span><span class="sxs-lookup"><span data-stu-id="44e1c-367">Max size of script event queue.</span></span> |
| <span data-ttu-id="44e1c-368">`client-output-buffer-limit``normalclient-output-buffer-limit``pubsub`</span><span class="sxs-lookup"><span data-stu-id="44e1c-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span></span> |<span data-ttu-id="44e1c-369">0 0 032mb 8mb 60</span><span class="sxs-lookup"><span data-stu-id="44e1c-369">0 0 032mb 8mb 60</span></span> |<span data-ttu-id="44e1c-370">Hello límites de búfer de salida de cliente se pueden utilizar tooforce desconexión de los clientes que son no leyendo los datos del servidor de hello lo suficientemente rápido por algún motivo (un motivo habitual es que un cliente de Pub/Sub no puede consumir mensajes tan rápido como Hola Editor los crea).</span><span class="sxs-lookup"><span data-stu-id="44e1c-370">hello client output buffer limits can be used tooforce disconnection of clients that are not reading data from hello server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as hello publisher can produce them).</span></span> <span data-ttu-id="44e1c-371">Para más información, vea [http://redis.io/topics/clients](http://redis.io/topics/clients).</span><span class="sxs-lookup"><span data-stu-id="44e1c-371">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span></span> |

<span data-ttu-id="44e1c-372"><a name="databases"></a>
<sup>1</sup>límite de Hola para `databases` es diferente para cada caché en Redis de Azure nivel de precios y se puede establecer al crear la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-372"><a name="databases"></a>
<sup>1</sup>hello limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span></span> <span data-ttu-id="44e1c-373">Si no hay ningún `databases` configuración se especifica durante la creación de la memoria caché, valor predeterminado de hello es 16.</span><span class="sxs-lookup"><span data-stu-id="44e1c-373">If no `databases` setting is specified during cache creation, hello default is 16.</span></span>

* <span data-ttu-id="44e1c-374">Cachés Basic y Standard</span><span class="sxs-lookup"><span data-stu-id="44e1c-374">Basic and Standard caches</span></span>
  * <span data-ttu-id="44e1c-375">C0 caché (250 MB) - seguridad too16 bases de datos</span><span class="sxs-lookup"><span data-stu-id="44e1c-375">C0 (250 MB) cache - up too16 databases</span></span>
  * <span data-ttu-id="44e1c-376">C1 caché (1 GB) - seguridad too16 bases de datos</span><span class="sxs-lookup"><span data-stu-id="44e1c-376">C1 (1 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="44e1c-377">C2 caché (2,5 GB) - seguridad too16 bases de datos</span><span class="sxs-lookup"><span data-stu-id="44e1c-377">C2 (2.5 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="44e1c-378">C3 caché (6 GB) - seguridad too16 bases de datos</span><span class="sxs-lookup"><span data-stu-id="44e1c-378">C3 (6 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="44e1c-379">C4 (13 GB) de memoria caché - seguridad too32 bases de datos</span><span class="sxs-lookup"><span data-stu-id="44e1c-379">C4 (13 GB) cache - up too32 databases</span></span>
  * <span data-ttu-id="44e1c-380">C5 caché (26 GB) - seguridad too48 bases de datos</span><span class="sxs-lookup"><span data-stu-id="44e1c-380">C5 (26 GB) cache - up too48 databases</span></span>
  * <span data-ttu-id="44e1c-381">C6 (53 GB) de memoria caché - seguridad too64 bases de datos</span><span class="sxs-lookup"><span data-stu-id="44e1c-381">C6 (53 GB) cache - up too64 databases</span></span>
* <span data-ttu-id="44e1c-382">Cachés Premium</span><span class="sxs-lookup"><span data-stu-id="44e1c-382">Premium caches</span></span>
  * <span data-ttu-id="44e1c-383">P1 (6 GB - 60 GB) - seguridad too16 bases de datos</span><span class="sxs-lookup"><span data-stu-id="44e1c-383">P1 (6 GB - 60 GB) - up too16 databases</span></span>
  * <span data-ttu-id="44e1c-384">P2 (13 GB a 130 GB) - seguridad too32 bases de datos</span><span class="sxs-lookup"><span data-stu-id="44e1c-384">P2 (13 GB - 130 GB) - up too32 databases</span></span>
  * <span data-ttu-id="44e1c-385">P3 (26 GB - 260 GB) - seguridad too48 bases de datos</span><span class="sxs-lookup"><span data-stu-id="44e1c-385">P3 (26 GB - 260 GB) - up too48 databases</span></span>
  * <span data-ttu-id="44e1c-386">P4 (53 GB - 530 GB) - seguridad too64 bases de datos</span><span class="sxs-lookup"><span data-stu-id="44e1c-386">P4 (53 GB - 530 GB) - up too64 databases</span></span>
  * <span data-ttu-id="44e1c-387">Todas las memorias caché premium con clúster de Redis habilitado - Redis clúster solo admite el uso de la base de datos 0 tan Hola `databases` limitar para cualquier caché premium con clúster de Redis habilitada es efectivamente hello y 1 [seleccione](http://redis.io/commands/select) comando no se admite.</span><span class="sxs-lookup"><span data-stu-id="44e1c-387">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so hello `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and hello [Select](http://redis.io/commands/select) command is not allowed.</span></span> <span data-ttu-id="44e1c-388">Para obtener más información, vea [¿necesito toomake cualquier toouse de aplicación de cliente de cambios toomy de agrupación en clústeres?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="44e1c-388">For more information, see [Do I need toomake any changes toomy client application toouse clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>

<span data-ttu-id="44e1c-389">Para obtener más información sobre las bases de datos, consulte el artículo [¿Cuáles son las bases de datos de Redis?](cache-faq.md#what-are-redis-databases)</span><span class="sxs-lookup"><span data-stu-id="44e1c-389">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span></span>

> [!NOTE]
> <span data-ttu-id="44e1c-390">Hola `databases` configuración se puede configurar durante la creación de cachés como solo con PowerShell, CLI u otros clientes de administración.</span><span class="sxs-lookup"><span data-stu-id="44e1c-390">hello `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span></span> <span data-ttu-id="44e1c-391">Para ver un ejemplo de configuración de `databases` al crear la memoria caché mediante PowerShell, consulte [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span><span class="sxs-lookup"><span data-stu-id="44e1c-391">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span></span>
> 
> 

<span data-ttu-id="44e1c-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` es diferente en cada plan de tarifa de Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="44e1c-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span></span>

* <span data-ttu-id="44e1c-393">Cachés Basic y Standard</span><span class="sxs-lookup"><span data-stu-id="44e1c-393">Basic and Standard caches</span></span>
  * <span data-ttu-id="44e1c-394">C0 caché (250 MB), las conexiones de too256</span><span class="sxs-lookup"><span data-stu-id="44e1c-394">C0 (250 MB) cache - up too256 connections</span></span>
  * <span data-ttu-id="44e1c-395">C1 caché (1 GB) - seguridad too1, 000 conexiones</span><span class="sxs-lookup"><span data-stu-id="44e1c-395">C1 (1 GB) cache - up too1,000 connections</span></span>
  * <span data-ttu-id="44e1c-396">C2 caché (2,5 GB) - seguridad too2, 000 conexiones</span><span class="sxs-lookup"><span data-stu-id="44e1c-396">C2 (2.5 GB) cache - up too2,000 connections</span></span>
  * <span data-ttu-id="44e1c-397">C3 caché (6 GB) - seguridad too5, 000 conexiones</span><span class="sxs-lookup"><span data-stu-id="44e1c-397">C3 (6 GB) cache - up too5,000 connections</span></span>
  * <span data-ttu-id="44e1c-398">C4 (13 GB) de memoria caché - seguridad too10, 000 conexiones</span><span class="sxs-lookup"><span data-stu-id="44e1c-398">C4 (13 GB) cache - up too10,000 connections</span></span>
  * <span data-ttu-id="44e1c-399">C5 caché (26 GB) - seguridad too15, 000 conexiones</span><span class="sxs-lookup"><span data-stu-id="44e1c-399">C5 (26 GB) cache - up too15,000 connections</span></span>
  * <span data-ttu-id="44e1c-400">C6 (53 GB) de memoria caché - seguridad too20, 000 conexiones</span><span class="sxs-lookup"><span data-stu-id="44e1c-400">C6 (53 GB) cache - up too20,000 connections</span></span>
* <span data-ttu-id="44e1c-401">Cachés Premium</span><span class="sxs-lookup"><span data-stu-id="44e1c-401">Premium caches</span></span>
  * <span data-ttu-id="44e1c-402">P1 (6 GB - 60 GB) - seguridad too7, conexiones a 500</span><span class="sxs-lookup"><span data-stu-id="44e1c-402">P1 (6 GB - 60 GB) - up too7,500 connections</span></span>
  * <span data-ttu-id="44e1c-403">P2 (13 GB a 130 GB) - seguridad too15, 000 conexiones</span><span class="sxs-lookup"><span data-stu-id="44e1c-403">P2 (13 GB - 130 GB) - up too15,000 connections</span></span>
  * <span data-ttu-id="44e1c-404">P3 (26 GB - 260 GB) - seguridad too30, 000 conexiones</span><span class="sxs-lookup"><span data-stu-id="44e1c-404">P3 (26 GB - 260 GB) - up too30,000 connections</span></span>
  * <span data-ttu-id="44e1c-405">P4 (53 GB - 530 GB) - seguridad too40, 000 conexiones</span><span class="sxs-lookup"><span data-stu-id="44e1c-405">P4 (53 GB - 530 GB) - up too40,000 connections</span></span>

> [!NOTE]
> <span data-ttu-id="44e1c-406">Aunque cada tamaño de caché permite *hasta* un cierto número de conexiones, cada tooRedis de conexión tiene sobrecarga asociado.</span><span class="sxs-lookup"><span data-stu-id="44e1c-406">While each size of cache allows *up to* a certain number of connections, each connection tooRedis has overhead associated with it.</span></span> <span data-ttu-id="44e1c-407">Un ejemplo de dicha sobrecarga podría ser el uso de memoria y CPU como resultado del cifrado TLS/SSL.</span><span class="sxs-lookup"><span data-stu-id="44e1c-407">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span></span> <span data-ttu-id="44e1c-408">límite máximo de conexiones de Hola para un tamaño de caché especificado supone una caché con poca carga.</span><span class="sxs-lookup"><span data-stu-id="44e1c-408">hello maximum connection limit for a given cache size assumes a lightly loaded cache.</span></span> <span data-ttu-id="44e1c-409">Si carga de sobrecarga de conexión *más* carga de las operaciones de cliente supera la capacidad para el sistema de Hola, caché Hola puede experimentar problemas de capacidad, incluso si no ha superado el límite de conexiones de hello para el tamaño actual de la caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="44e1c-409">If load from connection overhead *plus* load from client operations exceeds capacity for hello system, hello cache can experience capacity issues even if you have not exceeded hello connection limit for hello current cache size.</span></span>
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a><span data-ttu-id="44e1c-410">No se admiten comandos de Redis en Caché en Redis de Azure</span><span class="sxs-lookup"><span data-stu-id="44e1c-410">Redis commands not supported in Azure Redis Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="44e1c-411">Porque la configuración y administración de instancias de caché de Redis de Azure está administrado por Microsoft, hello siguientes están deshabilitados.</span><span class="sxs-lookup"><span data-stu-id="44e1c-411">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, hello following commands are disabled.</span></span> <span data-ttu-id="44e1c-412">Si intentas tooinvoke usarlas, recibirá un mensaje de error similar demasiado`"(error) ERR unknown command"`.</span><span class="sxs-lookup"><span data-stu-id="44e1c-412">If you try tooinvoke them, you receive an error message similar too`"(error) ERR unknown command"`.</span></span>
> 
> * <span data-ttu-id="44e1c-413">BGREWRITEAOF</span><span class="sxs-lookup"><span data-stu-id="44e1c-413">BGREWRITEAOF</span></span>
> * <span data-ttu-id="44e1c-414">BGSAVE</span><span class="sxs-lookup"><span data-stu-id="44e1c-414">BGSAVE</span></span>
> * <span data-ttu-id="44e1c-415">CONFIG</span><span class="sxs-lookup"><span data-stu-id="44e1c-415">CONFIG</span></span>
> * <span data-ttu-id="44e1c-416">DEBUG</span><span class="sxs-lookup"><span data-stu-id="44e1c-416">DEBUG</span></span>
> * <span data-ttu-id="44e1c-417">MIGRATE</span><span class="sxs-lookup"><span data-stu-id="44e1c-417">MIGRATE</span></span>
> * <span data-ttu-id="44e1c-418">Guardar</span><span class="sxs-lookup"><span data-stu-id="44e1c-418">SAVE</span></span>
> * <span data-ttu-id="44e1c-419">SHUTDOWN</span><span class="sxs-lookup"><span data-stu-id="44e1c-419">SHUTDOWN</span></span>
> * <span data-ttu-id="44e1c-420">SLAVEOF</span><span class="sxs-lookup"><span data-stu-id="44e1c-420">SLAVEOF</span></span>
> * <span data-ttu-id="44e1c-421">CLÚSTER: los comandos de escritura del clúster están deshabilitados, pero se permiten los comandos de solo lectura del clúster.</span><span class="sxs-lookup"><span data-stu-id="44e1c-421">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span></span>
> 
> 

<span data-ttu-id="44e1c-422">Para más información sobre los comandos de Redis, vea [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="44e1c-422">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>

## <a name="redis-console"></a><span data-ttu-id="44e1c-423">Consola de Redis</span><span class="sxs-lookup"><span data-stu-id="44e1c-423">Redis console</span></span>
<span data-ttu-id="44e1c-424">Forma segura puede emitir comandos tooyour instancias de caché en Redis de Azure con hello **Redis consola**, que está disponible en el portal de Azure para todos los niveles de caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="44e1c-424">You can securely issue commands tooyour Azure Redis Cache instances using hello **Redis Console**, which is available in hello Azure portal for all cache tiers.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="44e1c-425">Hello Redis consola no funciona con [VNET](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-425">hello Redis Console does not work with [VNET](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="44e1c-426">Cuando la memoria caché forma parte de una red virtual, solo los clientes de hello red virtual pueden tener acceso a memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="44e1c-426">When your cache is part of a VNET, only clients in hello VNET can access hello cache.</span></span> <span data-ttu-id="44e1c-427">Dado que Redis consola se ejecuta en el explorador local, que se encuentra fuera de la red virtual de hello, no puede conectarse tooyour caché.</span><span class="sxs-lookup"><span data-stu-id="44e1c-427">Because Redis Console runs in your local browser, which is outside hello VNET, it can't connect tooyour cache.</span></span>
> - <span data-ttu-id="44e1c-428">No se admiten todos los comandos de Redis en Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="44e1c-428">Not all Redis commands are supported in Azure Redis Cache.</span></span> <span data-ttu-id="44e1c-429">Para obtener una lista de comandos de Redis que se deshabilitan para caché en Redis de Azure, vea Hola anterior [Redis comandos no admitidos en caché en Redis de Azure](#redis-commands-not-supported-in-azure-redis-cache) sección.</span><span class="sxs-lookup"><span data-stu-id="44e1c-429">For a list of Redis commands that are disabled for Azure Redis Cache, see hello previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span></span> <span data-ttu-id="44e1c-430">Para más información sobre los comandos de Redis, vea [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="44e1c-430">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>
> 
> 

<span data-ttu-id="44e1c-431">Hola tooaccess Redis consola, haga clic en **consola** de hello **caché en Redis** hoja.</span><span class="sxs-lookup"><span data-stu-id="44e1c-431">tooaccess hello Redis Console, click **Console** from hello **Redis Cache** blade.</span></span>

![Consola de Redis](./media/cache-configure/redis-console-menu.png)

<span data-ttu-id="44e1c-433">comandos de tooissue en una instancia de la memoria caché, simplemente Hola de tipo deseado comando en la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="44e1c-433">tooissue commands against your cache instance, simply type hello desired command into hello console.</span></span>

![Consola de Redis](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a><span data-ttu-id="44e1c-435">Redis consola con una prima con hello en clúster caché</span><span class="sxs-lookup"><span data-stu-id="44e1c-435">Using hello Redis Console with a premium clustered cache</span></span>

<span data-ttu-id="44e1c-436">Al usar Hola consola Redis con un elevado en el clúster de caché, puede emitir tooa sola partición de memoria caché de Hola de comandos.</span><span class="sxs-lookup"><span data-stu-id="44e1c-436">When using hello Redis Console with a premium clustered cache, you can issue commands tooa single shard of hello cache.</span></span> <span data-ttu-id="44e1c-437">tooissue una partición específica de comando tooa, primero conectarse toohello de partición deseada haciendo clic en él en el selector de la partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="44e1c-437">tooissue a command tooa specific shard, first connect toohello desired shard by clicking it on hello shard picker.</span></span>

![Consola de Redis](./media/cache-configure/redis-console-premium-cluster.png)

<span data-ttu-id="44e1c-439">Si intentas tooaccess una clave que se almacena en una partición diferente de Hola particiones conectado, recibirá un toohello similar de mensaje de error siguiente mensaje.</span><span class="sxs-lookup"><span data-stu-id="44e1c-439">If you attempt tooaccess a key that is stored in a different shard than hello connected shard, you receive an error message similar toohello following message.</span></span>

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

<span data-ttu-id="44e1c-440">En el ejemplo anterior de hello, partición 1 es la partición seleccionada de hello, pero `myKey` se encuentra en la partición 0, tal como se indica por hello `(shard 0)` parte del mensaje de error de saludo.</span><span class="sxs-lookup"><span data-stu-id="44e1c-440">In hello previous example, shard 1 is hello selected shard, but `myKey` is located in shard 0, as indicated by hello `(shard 0)` portion of hello error message.</span></span> <span data-ttu-id="44e1c-441">En este ejemplo, tooaccess `myKey`, seleccione usando la partición 0 Hola selector de partición y, a continuación, comando hello deseado de problema.</span><span class="sxs-lookup"><span data-stu-id="44e1c-441">In this example, tooaccess `myKey`, select shard 0 using hello shard picker, and then issue hello desired command.</span></span>


## <a name="move-your-cache-tooa-new-subscription"></a><span data-ttu-id="44e1c-442">Mover la nueva suscripción de caché tooa</span><span class="sxs-lookup"><span data-stu-id="44e1c-442">Move your cache tooa new subscription</span></span>
<span data-ttu-id="44e1c-443">Puede mover la nueva suscripción de caché tooa haciendo clic en **mover**.</span><span class="sxs-lookup"><span data-stu-id="44e1c-443">You can move your cache tooa new subscription by clicking **Move**.</span></span>

![Traslado de Caché en Redis](./media/cache-configure/redis-cache-move.png)

<span data-ttu-id="44e1c-445">Para obtener información acerca de cómo mover los recursos de tooanother de grupo de recursos y de tooanother de una suscripción, vea [Mover grupo de recursos de toonew de recursos o suscripción](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="44e1c-445">For information on moving resources from one resource group tooanother, and from one subscription tooanother, see [Move resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="44e1c-446">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="44e1c-446">Next steps</span></span>
* <span data-ttu-id="44e1c-447">Para más información sobre cómo trabajar con los comandos de Redis, consulte [¿Cómo puedo ejecutar comandos de Redis?](cache-faq.md#how-can-i-run-redis-commands).</span><span class="sxs-lookup"><span data-stu-id="44e1c-447">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>

