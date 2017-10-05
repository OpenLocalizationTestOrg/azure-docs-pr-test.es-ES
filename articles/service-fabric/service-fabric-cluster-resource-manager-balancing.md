---
title: "Equilibrio de un clúster de Azure Service Fabric | Microsoft Docs"
description: "Una introducción al equilibrio del clúster con el Administrador de recursos de clúster de Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 030b1465-6616-4c0b-8bc7-24ed47d054c0
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 34eacb29f324025c1d2803c9690600227d3ec457
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="174fe-103">Equilibrio del clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="174fe-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="174fe-104">Cluster Resource Manager de Service Fabric admite cambios dinámicos de carga, en respuesta a las incorporaciones y las eliminaciones de nodos o servicios.</span><span class="sxs-lookup"><span data-stu-id="174fe-104">The Service Fabric Cluster Resource Manager supports dynamic load changes, reacting to additions or removals of nodes or services.</span></span> <span data-ttu-id="174fe-105">También corrige automáticamente las infracciones de restricciones y reequilibra el clúster de manera proactiva.</span><span class="sxs-lookup"><span data-stu-id="174fe-105">It also automatically corrects constraint violations, and proactively rebalances the cluster.</span></span> <span data-ttu-id="174fe-106">¿Pero con qué frecuencia se realizan estas acciones y qué las activa?</span><span class="sxs-lookup"><span data-stu-id="174fe-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="174fe-107">Existen tres categorías de trabajo que Cluster Resource Manager realiza.</span><span class="sxs-lookup"><span data-stu-id="174fe-107">There are three different categories of work that the Cluster Resource Manager performs.</span></span> <span data-ttu-id="174fe-108">Son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="174fe-108">They are:</span></span>

1. <span data-ttu-id="174fe-109">Ubicación: esta fase tiene que ver con la colocación de las réplicas con estado o las instancias sin estado que faltan.</span><span class="sxs-lookup"><span data-stu-id="174fe-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="174fe-110">Abarca los nuevos servicios y la administración de réplicas con estado o instancias sin estado incorrectas.</span><span class="sxs-lookup"><span data-stu-id="174fe-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="174fe-111">Aquí también se administra la eliminación de réplicas o instancias.</span><span class="sxs-lookup"><span data-stu-id="174fe-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="174fe-112">Comprobaciones de restricciones: en esta etapa se comprueban y corrigen las infracciones (reglas) de las distintas restricciones de selección de ubicación dentro del sistema.</span><span class="sxs-lookup"><span data-stu-id="174fe-112">Constraint Checks – this stage checks for and corrects violations of the different placement constraints (rules) within the system.</span></span> <span data-ttu-id="174fe-113">Algunos ejemplos de reglas son asegurarse de que los nodos no sobrepasan la capacidad y que las restricciones de selección de ubicación de un servicio se cumplen.</span><span class="sxs-lookup"><span data-stu-id="174fe-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="174fe-114">Equilibrio: en esta fase se comprueba si se precisa reequilibrado en función del nivel deseado de equilibrio configurado para las distintas métricas.</span><span class="sxs-lookup"><span data-stu-id="174fe-114">Balancing – this stage checks to see if rebalancing is necessary based on the configured desired level of balance for different metrics.</span></span> <span data-ttu-id="174fe-115">En caso afirmativo, se intenta encontrar una disposición en el clúster que sea más equilibrada.</span><span class="sxs-lookup"><span data-stu-id="174fe-115">If so it attempts to find an arrangement in the cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="174fe-116">Configuración de temporizadores de Cluster Resource Manager</span><span class="sxs-lookup"><span data-stu-id="174fe-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="174fe-117">El primer conjunto de controles en torno al equilibrio es un conjunto de temporizadores.</span><span class="sxs-lookup"><span data-stu-id="174fe-117">The first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="174fe-118">Estos temporizadores controlan la frecuencia con la que Cluster Resource Manager examina el clúster y realiza acciones correctivas.</span><span class="sxs-lookup"><span data-stu-id="174fe-118">These timers govern how often the Cluster Resource Manager examines the cluster and takes corrective actions.</span></span>

<span data-ttu-id="174fe-119">Cada uno de estos tipos diferentes de correcciones que Cluster Resource Manager puede realizar se controla mediante un temporizador diferente que determina su frecuencia.</span><span class="sxs-lookup"><span data-stu-id="174fe-119">Each of these different types of corrections the Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="174fe-120">Cuando se desencadena cada temporizador, se programa la tarea.</span><span class="sxs-lookup"><span data-stu-id="174fe-120">When each timer fires, the task is scheduled.</span></span> <span data-ttu-id="174fe-121">De forma predeterminada, Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="174fe-121">By default the Resource Manager:</span></span>

* <span data-ttu-id="174fe-122">Examina su estado y aplica las actualizaciones (por ejemplo, la grabación de que un nodo está inactivo) cada 1/10 de segundo.</span><span class="sxs-lookup"><span data-stu-id="174fe-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="174fe-123">establece la marca de comprobación de selección de ubicación.</span><span class="sxs-lookup"><span data-stu-id="174fe-123">sets the placement check flag</span></span> 
* <span data-ttu-id="174fe-124">establece la marca de comprobación de restricción cada segundo.</span><span class="sxs-lookup"><span data-stu-id="174fe-124">sets the constraint check flag every second</span></span>
* <span data-ttu-id="174fe-125">Establece el indicador de equilibrio cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="174fe-125">sets the balancing flag every five seconds.</span></span>

<span data-ttu-id="174fe-126">Seguidamente se ofrecen ejemplos de la configuración que regulan estos temporizadores:</span><span class="sxs-lookup"><span data-stu-id="174fe-126">Examples of the configuration governing these timers are below:</span></span>

<span data-ttu-id="174fe-127">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="174fe-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="174fe-128">a través de ClusterConfig.json para las implementaciones independientes o Template.json para los clústeres hospedados en Azure:</span><span class="sxs-lookup"><span data-stu-id="174fe-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PLBRefreshGap",
          "value": "0.10"
      },
      {
          "name": "MinPlacementInterval",
          "value": "1.0"
      },
      {
          "name": "MinConstraintCheckInterval",
          "value": "1.0"
      },
      {
          "name": "MinLoadBalancingInterval",
          "value": "5.0"
      }
    ]
  }
]
```

<span data-ttu-id="174fe-129">Ahora, Cluster Resource Manager solo realiza estas acciones una a una, de forma secuencial.</span><span class="sxs-lookup"><span data-stu-id="174fe-129">Today the Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="174fe-130">Por esto nos referimos a estos temporizadores como “intervalos mínimos” y a las acciones que se realizan cuando los temporizadores se desactivan "marcas de establecimiento".</span><span class="sxs-lookup"><span data-stu-id="174fe-130">This is why we refer to these timers as “minimum intervals” and the actions that get taken when the timers go off as "setting flags".</span></span> <span data-ttu-id="174fe-131">Por ejemplo, Cluster Resource Manager se encarga de las solicitudes pendientes para crear servicios antes de equilibrar el clúster.</span><span class="sxs-lookup"><span data-stu-id="174fe-131">For example, the Cluster Resource Manager takes care of pending requests to create services before balancing the cluster.</span></span> <span data-ttu-id="174fe-132">Como puede ver por los intervalos de tiempo predeterminados especificados, Cluster Resource Manager examina y comprueba con frecuencia si hay algo que deba hacer.</span><span class="sxs-lookup"><span data-stu-id="174fe-132">As you can see by the default time intervals specified, the Cluster Resource Manager scans for anything it needs to do frequently.</span></span> <span data-ttu-id="174fe-133">Normalmente, esto significa que el conjunto de cambios realizados durante cada paso es pequeño.</span><span class="sxs-lookup"><span data-stu-id="174fe-133">Normally this means that the set of changes made during each step is small.</span></span> <span data-ttu-id="174fe-134">Realizar pequeños cambios con frecuencia permite que Cluster Resource Manager responda a los eventos que se producen en el clúster.</span><span class="sxs-lookup"><span data-stu-id="174fe-134">Making small changes frequently allows the Cluster Resource Manager to be responsive when things happen in the cluster.</span></span> <span data-ttu-id="174fe-135">Los temporizadores predeterminados proporcionan algún procesamiento por lotes porque muchos eventos del mismo tipo tienden a producirse al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="174fe-135">The default timers provide some batching since many of the same types of events tend to occur simultaneously.</span></span> 

<span data-ttu-id="174fe-136">Por ejemplo, cuando los nodos no funcionan pueden provocar que todos los dominios dejen de funcionar a la vez.</span><span class="sxs-lookup"><span data-stu-id="174fe-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="174fe-137">Tos estos errores se capturan durante la siguiente actualización de estado después de *PLBRefreshGap*.</span><span class="sxs-lookup"><span data-stu-id="174fe-137">All these failures are captured during the next state update after the *PLBRefreshGap*.</span></span> <span data-ttu-id="174fe-138">Las correcciones se determinan durante las siguientes ejecuciones de selección de ubicación, comprobación de restricciones y equilibrio.</span><span class="sxs-lookup"><span data-stu-id="174fe-138">The corrections are determined during the following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="174fe-139">De forma predeterminada, Cluster Resource Manager no realiza exámenes durante las horas de cambios en el clúster e intenta abordar todos los cambios al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="174fe-139">By default the Cluster Resource Manager is not scanning through hours of changes in the cluster and trying to address all changes at once.</span></span> <span data-ttu-id="174fe-140">Hacerlo produciría ráfagas de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="174fe-140">Doing so would lead to bursts of churn.</span></span>

<span data-ttu-id="174fe-141">Cluster Resource Manager también necesita información adicional para determinar si el clúster está desequilibrado.</span><span class="sxs-lookup"><span data-stu-id="174fe-141">The Cluster Resource Manager also needs some additional information to determine if the cluster imbalanced.</span></span> <span data-ttu-id="174fe-142">Para ello se cuenta con dos elementos de configuración: *BalancingThresholds* y *ActivityThresholds*.</span><span class="sxs-lookup"><span data-stu-id="174fe-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="174fe-143">Umbrales de equilibrio</span><span class="sxs-lookup"><span data-stu-id="174fe-143">Balancing thresholds</span></span>
<span data-ttu-id="174fe-144">Un umbral de equilibrio es el control principal para la activación del reequilibrado.</span><span class="sxs-lookup"><span data-stu-id="174fe-144">A Balancing Threshold is the main control for triggering rebalancing.</span></span> <span data-ttu-id="174fe-145">El umbral de equilibrio de una métrica es una _proporción_.</span><span class="sxs-lookup"><span data-stu-id="174fe-145">The Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="174fe-146">Si la carga de una métrica en el nodo más cargado dividida entre la cantidad de carga en el nodo menos cargado supera el valor de *BalancingThreshold* de la métrica, el clúster está desequilibrado.</span><span class="sxs-lookup"><span data-stu-id="174fe-146">If the load for a metric on the most loaded node divided by the amount of load on the least loaded node exceeds that metric's *BalancingThreshold*, then the cluster is imbalanced.</span></span> <span data-ttu-id="174fe-147">Como resultado, se activa el equilibrado durante la próxima comprobación de Cluster Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="174fe-147">As a result balancing is triggered the next time the Cluster Resource Manager checks.</span></span> <span data-ttu-id="174fe-148">El temporizador *MinLoadBalancingInterval* determina la frecuencia con la que Cluster Resource Manager debe comprobar si es necesario realizar el reequilibrado.</span><span class="sxs-lookup"><span data-stu-id="174fe-148">The *MinLoadBalancingInterval* timer defines how often the Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="174fe-149">La comprobación no significa que suceda nada.</span><span class="sxs-lookup"><span data-stu-id="174fe-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="174fe-150">Los umbrales de equilibrio se definen por métrica como parte de la definición de clúster.</span><span class="sxs-lookup"><span data-stu-id="174fe-150">Balancing Thresholds are defined on a per-metric basis as a part of the cluster definition.</span></span> <span data-ttu-id="174fe-151">Para más información sobre las métricas, consulte [este artículo](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="174fe-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="174fe-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="174fe-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="174fe-153">a través de ClusterConfig.json para las implementaciones independientes o Template.json para los clústeres hospedados en Azure:</span><span class="sxs-lookup"><span data-stu-id="174fe-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricBalancingThresholds",
    "parameters": [
      {
          "name": "MetricName1",
          "value": "2"
      },
      {
          "name": "MetricName2",
          "value": "3.5"
      }
    ]
  }
]
```

<span data-ttu-id="174fe-154"><center>
![Ejemplo de umbral de equilibrio][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="174fe-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="174fe-155">En este ejemplo, cada servicio solo consume una unidad de alguna métrica.</span><span class="sxs-lookup"><span data-stu-id="174fe-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="174fe-156">En el ejemplo superior, la carga máxima en un nodo es cinco y la mínima es dos.</span><span class="sxs-lookup"><span data-stu-id="174fe-156">In the top example, the maximum load on a node is five and the minimum is two.</span></span> <span data-ttu-id="174fe-157">Supongamos que el umbral de equilibrio de esta métrica es tres.</span><span class="sxs-lookup"><span data-stu-id="174fe-157">Let’s say that the balancing threshold for this metric is three.</span></span> <span data-ttu-id="174fe-158">Puesto que la proporción del clúster es 5/2 = 2,5, que es menor que el umbral de equilibrio especificado de tres, el clúster está equilibrado.</span><span class="sxs-lookup"><span data-stu-id="174fe-158">Since the ratio in the cluster is 5/2 = 2.5 and that is less than the specified balancing threshold of three, the cluster is balanced.</span></span> <span data-ttu-id="174fe-159">El equilibrado no se activa durante la comprobación de Cluster Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="174fe-159">No balancing is triggered when the Cluster Resource Manager checks.</span></span>

<span data-ttu-id="174fe-160">En el ejemplo de abajo, la carga máxima en un nodo es 10, mientras que la mínima es dos, lo que da lugar a una proporción de cinco.</span><span class="sxs-lookup"><span data-stu-id="174fe-160">In the bottom example, the maximum load on a node is 10, while the minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="174fe-161">Cinco es mayor que el umbral de equilibrio establecido en tres para esa métrica.</span><span class="sxs-lookup"><span data-stu-id="174fe-161">Five is greater than the designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="174fe-162">Como resultado, la próxima vez que el temporizador de equilibrio se active, se programará un reequilibrado.</span><span class="sxs-lookup"><span data-stu-id="174fe-162">As a result, a rebalancing run will be scheduled next time the balancing timer fires.</span></span> <span data-ttu-id="174fe-163">En una situación como esta, parte de la carga suele distribuirse a Node3.</span><span class="sxs-lookup"><span data-stu-id="174fe-163">In a situation like this some load is usually distributed to Node3.</span></span> <span data-ttu-id="174fe-164">Como el enfoque de Cluster Resource Manager de Service Fabric no es ambicioso, también podría distribuir cierta carga a Node2.</span><span class="sxs-lookup"><span data-stu-id="174fe-164">Because the Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed to Node2.</span></span> 

<span data-ttu-id="174fe-165"><center>
![Acciones de ejemplo de umbral de equilibrio][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="174fe-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="174fe-166">"Equilibrio" controla dos estrategias distintas para administrar la carga del clúster.</span><span class="sxs-lookup"><span data-stu-id="174fe-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="174fe-167">La estrategia predeterminada que usa Cluster Resource Manager consiste en distribuir la carga entre los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="174fe-167">The default strategy that the Cluster Resource Manager uses is to distribute load across the nodes in the cluster.</span></span> <span data-ttu-id="174fe-168">La otra estrategia es la [desfragmentación](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="174fe-168">The other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="174fe-169">La desfragmentación se realiza durante la misma ejecución del equilibrio.</span><span class="sxs-lookup"><span data-stu-id="174fe-169">Defragmentation is performed during the same balancing run.</span></span> <span data-ttu-id="174fe-170">Las estrategias de equilibrio y desfragmentación se pueden usar con distintas métricas en un mismo clúster.</span><span class="sxs-lookup"><span data-stu-id="174fe-170">The balancing and defragmentation strategies can be used for different metrics within the same cluster.</span></span> <span data-ttu-id="174fe-171">Un servicio puede tener métricas de equilibrio y desfragmentación.</span><span class="sxs-lookup"><span data-stu-id="174fe-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="174fe-172">En cuanto a las métricas de desfragmentación, la proporción de las cargas del clúster activa el reequilibrado cuando es _inferior_ al umbral de equilibrio.</span><span class="sxs-lookup"><span data-stu-id="174fe-172">For defragmentation metrics, the ratio of the loads in the cluster triggers rebalancing when it is _below_ the balancing threshold.</span></span> 
>

<span data-ttu-id="174fe-173">El objetivo explícito no es estar por debajo del umbral de equilibrio.</span><span class="sxs-lookup"><span data-stu-id="174fe-173">Getting below the balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="174fe-174">Los umbrales de equilibrio son tan solo un *desencadenador*.</span><span class="sxs-lookup"><span data-stu-id="174fe-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="174fe-175">Cuando se ejecuta el equilibrio, Cluster Resource Manager determina qué mejoras puede realizar, si hay alguna.</span><span class="sxs-lookup"><span data-stu-id="174fe-175">When balancing runs, the Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="174fe-176">El inicio de una búsqueda de equilibrio no significa que nada cambie.</span><span class="sxs-lookup"><span data-stu-id="174fe-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="174fe-177">A veces, el clúster está desequilibrado pero tiene demasiadas restricciones para que se corrija.</span><span class="sxs-lookup"><span data-stu-id="174fe-177">Sometimes the cluster is imbalanced but too constrained to correct.</span></span> <span data-ttu-id="174fe-178">Otra posibilidad es que las mejoras requieran movimientos que resulten demasiado [costosos](service-fabric-cluster-resource-manager-movement-cost.md).</span><span class="sxs-lookup"><span data-stu-id="174fe-178">Alternatively, the improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="174fe-179">umbrales de actividad</span><span class="sxs-lookup"><span data-stu-id="174fe-179">Activity thresholds</span></span>
<span data-ttu-id="174fe-180">En ocasiones, aunque los nodos están relativamente desequilibrados, la cantidad de carga *total* en el clúster es baja.</span><span class="sxs-lookup"><span data-stu-id="174fe-180">Sometimes, although nodes are relatively imbalanced, the *total* amount of load in the cluster is low.</span></span> <span data-ttu-id="174fe-181">La falta de carga puede deberse a una caída transitoria, o porque el clúster es nuevo y se acaba de arrancar.</span><span class="sxs-lookup"><span data-stu-id="174fe-181">The lack of load could be a transient dip, or because the cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="174fe-182">En cualquier caso, no querrá perder tiempo en equilibrar el clúster porque no hay mucho que ganar.</span><span class="sxs-lookup"><span data-stu-id="174fe-182">In either case, you may not want to spend time balancing the cluster because there’s little to be gained.</span></span> <span data-ttu-id="174fe-183">Si el clúster se somete a un equilibrado, se invertirían recursos de red y de proceso para realizar cambios que no suponen *ninguna* diferencia.</span><span class="sxs-lookup"><span data-stu-id="174fe-183">If the cluster underwent balancing, you’d spend network and compute resources to move things around without making any large *absolute* difference.</span></span> <span data-ttu-id="174fe-184">Para evitar movimientos innecesarios, hay otro control conocido como umbrales de actividad.</span><span class="sxs-lookup"><span data-stu-id="174fe-184">To avoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="174fe-185">Los umbrales de actividad permiten especificar un límite inferior absoluto para la actividad.</span><span class="sxs-lookup"><span data-stu-id="174fe-185">Activity Thresholds allows you to specify some absolute lower bound for activity.</span></span> <span data-ttu-id="174fe-186">Si ningún nodo se encuentra por encima de umbral, el equilibrado no se desencadena aunque se alcance el umbral de equilibrio.</span><span class="sxs-lookup"><span data-stu-id="174fe-186">If no node is over this threshold, balancing isn't triggered even if the Balancing Threshold is met.</span></span>

<span data-ttu-id="174fe-187">Supongamos que se mantiene el umbral de equilibrio de tres para esta métrica.</span><span class="sxs-lookup"><span data-stu-id="174fe-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="174fe-188">Supongamos también que se tiene un umbral de actividad de 1536.</span><span class="sxs-lookup"><span data-stu-id="174fe-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="174fe-189">En el primer caso, aunque el clúster está desequilibrado según el umbral de equilibrio, ningún nodo llega al umbral mínimo de actividad, por lo que no sucede nada.</span><span class="sxs-lookup"><span data-stu-id="174fe-189">In the first case, while the cluster is imbalanced per the Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="174fe-190">En el ejemplo de abajo, Node1 supera el umbral de actividad.</span><span class="sxs-lookup"><span data-stu-id="174fe-190">In the bottom example, Node1 is over the Activity Threshold.</span></span> <span data-ttu-id="174fe-191">Puesto que se superan el umbral de equilibrio y el umbral de actividad para la métrica, se programa el equilibrado.</span><span class="sxs-lookup"><span data-stu-id="174fe-191">Since both the Balancing Threshold and the Activity Threshold for the metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="174fe-192">Como ejemplo, observemos el diagrama siguiente.</span><span class="sxs-lookup"><span data-stu-id="174fe-192">As an example, let's look at the following diagram:</span></span> 

<span data-ttu-id="174fe-193"><center>
![Ejemplo de umbral de actividad][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="174fe-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="174fe-194">Al igual que los umbrales de equilibrio, los umbrales de actividad se definen por métrica a través de la definición de clúster:</span><span class="sxs-lookup"><span data-stu-id="174fe-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via the cluster definition:</span></span>

<span data-ttu-id="174fe-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="174fe-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="174fe-196">mediante ClusterConfig.json para las implementaciones independientes o Template.json para los clústeres hospedados en Azure:</span><span class="sxs-lookup"><span data-stu-id="174fe-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricActivityThresholds",
    "parameters": [
      {
          "name": "Memory",
          "value": "1536"
      }
    ]
  }
]
```

<span data-ttu-id="174fe-197">Observe que los umbrales de equilibrio y actividad están vinculados a la métrica; el equilibrado solo se desencadenará si se superan los umbrales de equilibrio y actividad de la misma métrica.</span><span class="sxs-lookup"><span data-stu-id="174fe-197">Balancing and activity thresholds are both tied to a specific metric - balancing is triggered only if both the Balancing Threshold and Activity Threshold is exceeded for the same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="174fe-198">Equilibrio conjunto de los servicios</span><span class="sxs-lookup"><span data-stu-id="174fe-198">Balancing services together</span></span>
<span data-ttu-id="174fe-199">La decisión de si el clúster está desequilibrado o no afecta a todo el clúster.</span><span class="sxs-lookup"><span data-stu-id="174fe-199">Whether the cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="174fe-200">Sin embargo, para corregirlo movemos instancias y réplicas de servicio individuales.</span><span class="sxs-lookup"><span data-stu-id="174fe-200">However, the way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="174fe-201">Tiene sentido, ¿no?</span><span class="sxs-lookup"><span data-stu-id="174fe-201">This makes sense, right?</span></span> <span data-ttu-id="174fe-202">Si la memoria está apilada en un nodo, podría haber varias réplicas o instancias contribuyendo a ella.</span><span class="sxs-lookup"><span data-stu-id="174fe-202">If memory is stacked up on one node, multiple replicas or instances could be contributing to it.</span></span> <span data-ttu-id="174fe-203">Para corregir el desequilibrio podría ser necesario mover cualquiera de las réplicas con estado o instancias sin estado que utiliza la métrica desequilibrada.</span><span class="sxs-lookup"><span data-stu-id="174fe-203">Fixing the imbalance could require moving any of the stateful replicas or stateless instances that use the imbalanced metric.</span></span>

<span data-ttu-id="174fe-204">Aunque, a veces, se mueve un servicio que no estaba desequilibrado (recuerde la explicación anterior sobre ponderaciones locales y globales).</span><span class="sxs-lookup"><span data-stu-id="174fe-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember the discussion of local and global weights earlier).</span></span> <span data-ttu-id="174fe-205">¿Por qué habría de moverse un servicio si todas sus métricas están equilibradas?</span><span class="sxs-lookup"><span data-stu-id="174fe-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="174fe-206">Veamos un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="174fe-206">Let’s see an example:</span></span>

- <span data-ttu-id="174fe-207">Supongamos que hay cuatro servicios, Service1, Service2, Service3 y Service4.</span><span class="sxs-lookup"><span data-stu-id="174fe-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="174fe-208">Service1 informa de las métricas Metric1 y Metric2.</span><span class="sxs-lookup"><span data-stu-id="174fe-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="174fe-209">Service2 informa de las métricas Metric2 y Metric3.</span><span class="sxs-lookup"><span data-stu-id="174fe-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="174fe-210">Service3 informa de las métricas Metric3 y Metric4.</span><span class="sxs-lookup"><span data-stu-id="174fe-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="174fe-211">Service4 informa de la Metric99.</span><span class="sxs-lookup"><span data-stu-id="174fe-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="174fe-212">Seguramente puede ver adónde queremos llegar: hay una cadena.</span><span class="sxs-lookup"><span data-stu-id="174fe-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="174fe-213">En realidad no tenemos cuatro servicios independientes, sino tres servicios que están relacionados y uno que va por su cuenta.</span><span class="sxs-lookup"><span data-stu-id="174fe-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="174fe-214"><center>
![Equilibrio conjunto de los servicios][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="174fe-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="174fe-215">Debido a esta cadena, es posible que un desequilibrio en las métrica 1-4 provoque el movimiento de las réplicas o instancias que pertenecen a los servicios 1-3.</span><span class="sxs-lookup"><span data-stu-id="174fe-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging to services 1-3 to move around.</span></span> <span data-ttu-id="174fe-216">También sabemos que un desequilibrio en las métricas 1, 2 o 3 no puede ocasionar movimientos en Service4.</span><span class="sxs-lookup"><span data-stu-id="174fe-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="174fe-217">No tendría sentido porque mover las réplicas o instancias que pertenecen a Service4 no afectará al equilibrio de las métricas 1-3.</span><span class="sxs-lookup"><span data-stu-id="174fe-217">There would be no point since moving the replicas or instances belonging to Service4 around can do absolutely nothing to impact the balance of Metrics 1-3.</span></span>

<span data-ttu-id="174fe-218">Cluster Resource Manager averigua automáticamente qué servicios están relacionados.</span><span class="sxs-lookup"><span data-stu-id="174fe-218">The Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="174fe-219">La incorporación, eliminación o modificación de las métricas de los servicios puede afectar a sus relaciones.</span><span class="sxs-lookup"><span data-stu-id="174fe-219">Adding, removing, or changing the metrics for services can impact their relationships.</span></span> <span data-ttu-id="174fe-220">Por ejemplo, entre dos ejecuciones de equilibrado, puede que Service2 se haya actualizado y quitado Metric2.</span><span class="sxs-lookup"><span data-stu-id="174fe-220">For example, between two runs of balancing Service2 may have been updated to remove Metric2.</span></span> <span data-ttu-id="174fe-221">Esto rompe la cadena entre el Servicio1 y el Servicio2.</span><span class="sxs-lookup"><span data-stu-id="174fe-221">This breaks the chain between Service1 and Service2.</span></span> <span data-ttu-id="174fe-222">Ahora, en lugar de dos grupos de servicios relacionados, hay tres:</span><span class="sxs-lookup"><span data-stu-id="174fe-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="174fe-223"><center>
![Equilibrio conjunto de los servicios][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="174fe-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="174fe-224">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="174fe-224">Next steps</span></span>
* <span data-ttu-id="174fe-225">Las métricas son el modo en que el Administrador de recursos de clúster de Service Fabric administra la capacidad y el consumo en el clúster.</span><span class="sxs-lookup"><span data-stu-id="174fe-225">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span></span> <span data-ttu-id="174fe-226">Para más información sobre las métricas y cómo configurarlas, consulte [este artículo](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="174fe-226">To learn more about metrics and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="174fe-227">El costo del movimiento es una forma de señalizar al Administrador de recursos de clúster que determinados servicios son más caros de mover que otros.</span><span class="sxs-lookup"><span data-stu-id="174fe-227">Movement Cost is one way of signaling to the Cluster Resource Manager that certain services are more expensive to move than others.</span></span> <span data-ttu-id="174fe-228">Para más información sobre el coste del movimiento, consulte [este artículo](service-fabric-cluster-resource-manager-movement-cost.md)</span><span class="sxs-lookup"><span data-stu-id="174fe-228">For more about movement cost, refer to [this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="174fe-229">El Administrador de recursos de clúster presenta varias limitaciones que se pueden configurar para ralentizar la renovación del clúster.</span><span class="sxs-lookup"><span data-stu-id="174fe-229">The Cluster Resource Manager has several throttles that you can configure to slow down churn in the cluster.</span></span> <span data-ttu-id="174fe-230">Aunque no son normalmente necesarias, si las necesita, puede encontrar información sobre ellas [aquí](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="174fe-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
