---
title: "aaaBalance el clúster de Azure Service Fabric | Documentos de Microsoft"
description: "Un toobalancing de introducción del clúster con el servicio Administrador de recursos del clúster de tejido de Hola."
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
ms.openlocfilehash: 5f7ad2f5cf4cfb3751a860f5293b03d2d5266d99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="9e199-103">Equilibrio del clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9e199-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="9e199-104">Hola, Administrador de recursos de clúster de tejido de servicio admite cambios de carga dinámico, tooadditions reaccionando o las eliminaciones de nodos o servicios.</span><span class="sxs-lookup"><span data-stu-id="9e199-104">hello Service Fabric Cluster Resource Manager supports dynamic load changes, reacting tooadditions or removals of nodes or services.</span></span> <span data-ttu-id="9e199-105">También corrige automáticamente las infracciones de restricción y vuelve a equilibrar clúster Hola de forma proactiva.</span><span class="sxs-lookup"><span data-stu-id="9e199-105">It also automatically corrects constraint violations, and proactively rebalances hello cluster.</span></span> <span data-ttu-id="9e199-106">¿Pero con qué frecuencia se realizan estas acciones y qué las activa?</span><span class="sxs-lookup"><span data-stu-id="9e199-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="9e199-107">Hay tres categorías diferentes de trabajo que realiza el Administrador de recursos del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e199-107">There are three different categories of work that hello Cluster Resource Manager performs.</span></span> <span data-ttu-id="9e199-108">Son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="9e199-108">They are:</span></span>

1. <span data-ttu-id="9e199-109">Ubicación: esta fase tiene que ver con la colocación de las réplicas con estado o las instancias sin estado que faltan.</span><span class="sxs-lookup"><span data-stu-id="9e199-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="9e199-110">Abarca los nuevos servicios y la administración de réplicas con estado o instancias sin estado incorrectas.</span><span class="sxs-lookup"><span data-stu-id="9e199-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="9e199-111">Aquí también se administra la eliminación de réplicas o instancias.</span><span class="sxs-lookup"><span data-stu-id="9e199-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="9e199-112">Se comprueba la restricción: esta fase se comprueba y corrige las infracciones de restricciones de posición diferente de hello (reglas) en el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e199-112">Constraint Checks – this stage checks for and corrects violations of hello different placement constraints (rules) within hello system.</span></span> <span data-ttu-id="9e199-113">Algunos ejemplos de reglas son asegurarse de que los nodos no sobrepasan la capacidad y que las restricciones de selección de ubicación de un servicio se cumplen.</span><span class="sxs-lookup"><span data-stu-id="9e199-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="9e199-114">Equilibrio de esta fase se comprueba toosee si reequilibrio es necesario basándose en hello configurado nivel deseado de saldo de métricas diferentes.</span><span class="sxs-lookup"><span data-stu-id="9e199-114">Balancing – this stage checks toosee if rebalancing is necessary based on hello configured desired level of balance for different metrics.</span></span> <span data-ttu-id="9e199-115">Si lo intenta toofind una disposición en hello del clúster que es más equilibrada.</span><span class="sxs-lookup"><span data-stu-id="9e199-115">If so it attempts toofind an arrangement in hello cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="9e199-116">Configuración de temporizadores de Cluster Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9e199-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="9e199-117">Hola primer conjunto de controles de equilibrio son un conjunto de temporizadores.</span><span class="sxs-lookup"><span data-stu-id="9e199-117">hello first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="9e199-118">Estos temporizadores controlan la frecuencia con hello Administrador de recursos del clúster examina clúster hello y toma medidas correctivas.</span><span class="sxs-lookup"><span data-stu-id="9e199-118">These timers govern how often hello Cluster Resource Manager examines hello cluster and takes corrective actions.</span></span>

<span data-ttu-id="9e199-119">Cada uno de estos tipos diferentes de hello correcciones puede hacer el Administrador de recursos del clúster se controla mediante un temporizador diferentes que rige su frecuencia.</span><span class="sxs-lookup"><span data-stu-id="9e199-119">Each of these different types of corrections hello Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="9e199-120">Cuando se activa cada temporizador, se programa la tarea hello.</span><span class="sxs-lookup"><span data-stu-id="9e199-120">When each timer fires, hello task is scheduled.</span></span> <span data-ttu-id="9e199-121">De forma predeterminada Hola Administrador de recursos:</span><span class="sxs-lookup"><span data-stu-id="9e199-121">By default hello Resource Manager:</span></span>

* <span data-ttu-id="9e199-122">Examina su estado y aplica las actualizaciones (por ejemplo, la grabación de que un nodo está inactivo) cada 1/10 de segundo.</span><span class="sxs-lookup"><span data-stu-id="9e199-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="9e199-123">establece la marca de verificación de selección de ubicación de Hola</span><span class="sxs-lookup"><span data-stu-id="9e199-123">sets hello placement check flag</span></span> 
* <span data-ttu-id="9e199-124">establece la marca de verificación de restricción de hello cada segundo</span><span class="sxs-lookup"><span data-stu-id="9e199-124">sets hello constraint check flag every second</span></span>
* <span data-ttu-id="9e199-125">establece Hola equilibrio marca cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="9e199-125">sets hello balancing flag every five seconds.</span></span>

<span data-ttu-id="9e199-126">Ejemplos de configuración de Hola que rigen estos temporizadores son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="9e199-126">Examples of hello configuration governing these timers are below:</span></span>

<span data-ttu-id="9e199-127">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="9e199-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="9e199-128">a través de ClusterConfig.json para las implementaciones independientes o Template.json para los clústeres hospedados en Azure:</span><span class="sxs-lookup"><span data-stu-id="9e199-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="9e199-129">Hoy en día Hola, Administrador de recursos del clúster sólo realiza una de estas acciones a la vez, secuencialmente.</span><span class="sxs-lookup"><span data-stu-id="9e199-129">Today hello Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="9e199-130">Se trata de por qué se hacen referencia los temporizadores de toothese como "intervalos mínimos" y Hola medidas que obtengan tomar al temporizadores Hola apagarán "marcadores de configuración".</span><span class="sxs-lookup"><span data-stu-id="9e199-130">This is why we refer toothese timers as “minimum intervals” and hello actions that get taken when hello timers go off as "setting flags".</span></span> <span data-ttu-id="9e199-131">Por ejemplo, Hola, Administrador de recursos del clúster se encarga de pendiente solicita toocreate services antes de hello clúster de equilibrio.</span><span class="sxs-lookup"><span data-stu-id="9e199-131">For example, hello Cluster Resource Manager takes care of pending requests toocreate services before balancing hello cluster.</span></span> <span data-ttu-id="9e199-132">Como puede ver por intervalos de tiempo predeterminado de hello especificados, Hola, Administrador de recursos del clúster analiza para cualquier elemento necesidades toodo con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="9e199-132">As you can see by hello default time intervals specified, hello Cluster Resource Manager scans for anything it needs toodo frequently.</span></span> <span data-ttu-id="9e199-133">Normalmente esto significa que el conjunto de Hola de los cambios realizados durante cada paso es pequeño.</span><span class="sxs-lookup"><span data-stu-id="9e199-133">Normally this means that hello set of changes made during each step is small.</span></span> <span data-ttu-id="9e199-134">Realizar pequeños cambios con frecuencia permite hello toobe del Administrador de recursos de clúster responda cuando ocurren cosas en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e199-134">Making small changes frequently allows hello Cluster Resource Manager toobe responsive when things happen in hello cluster.</span></span> <span data-ttu-id="9e199-135">Hello temporizadores predeterminados proporcionan algún procesamiento por lotes desde muchos Hola mismo tipos de eventos suelen toooccur al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="9e199-135">hello default timers provide some batching since many of hello same types of events tend toooccur simultaneously.</span></span> 

<span data-ttu-id="9e199-136">Por ejemplo, cuando los nodos no funcionan pueden provocar que todos los dominios dejen de funcionar a la vez.</span><span class="sxs-lookup"><span data-stu-id="9e199-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="9e199-137">Todos estos errores se capturan durante el siguiente estado de hello actualización después de hello *PLBRefreshGap*.</span><span class="sxs-lookup"><span data-stu-id="9e199-137">All these failures are captured during hello next state update after hello *PLBRefreshGap*.</span></span> <span data-ttu-id="9e199-138">correcciones de Hola se determinan durante Hola después de selección de ubicación, comprobación de restricción y el equilibrio de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="9e199-138">hello corrections are determined during hello following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="9e199-139">Hola predeterminado Administrador de recursos del clúster no está analizando horas de cambios en el clúster de Hola e intentar tooaddress todos los cambios a la vez.</span><span class="sxs-lookup"><span data-stu-id="9e199-139">By default hello Cluster Resource Manager is not scanning through hours of changes in hello cluster and trying tooaddress all changes at once.</span></span> <span data-ttu-id="9e199-140">Si lo hace, provocaría toobursts de renovación.</span><span class="sxs-lookup"><span data-stu-id="9e199-140">Doing so would lead toobursts of churn.</span></span>

<span data-ttu-id="9e199-141">Hola, Administrador de recursos del clúster también necesita algunos toodetermine información adicional si hello en clúster equilibrado.</span><span class="sxs-lookup"><span data-stu-id="9e199-141">hello Cluster Resource Manager also needs some additional information toodetermine if hello cluster imbalanced.</span></span> <span data-ttu-id="9e199-142">Para ello se cuenta con dos elementos de configuración: *BalancingThresholds* y *ActivityThresholds*.</span><span class="sxs-lookup"><span data-stu-id="9e199-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="9e199-143">Umbrales de equilibrio</span><span class="sxs-lookup"><span data-stu-id="9e199-143">Balancing thresholds</span></span>
<span data-ttu-id="9e199-144">Un umbral de equilibrio es control principal de hello para la activación de reequilibrio.</span><span class="sxs-lookup"><span data-stu-id="9e199-144">A Balancing Threshold is hello main control for triggering rebalancing.</span></span> <span data-ttu-id="9e199-145">Hola equilibrio de umbral de una métrica es un _proporción_.</span><span class="sxs-lookup"><span data-stu-id="9e199-145">hello Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="9e199-146">Si carga Hola para una métrica en hello más carga nodo dividido por volumen Hola de carga Hola menos cargado nodo supera esa métrica *BalancingThreshold*, clúster de hello es desequilibrado.</span><span class="sxs-lookup"><span data-stu-id="9e199-146">If hello load for a metric on hello most loaded node divided by hello amount of load on hello least loaded node exceeds that metric's *BalancingThreshold*, then hello cluster is imbalanced.</span></span> <span data-ttu-id="9e199-147">Como resultado equilibrio es Hola Hola desencadenadas de tiempo siguiente comprueba el Administrador de recursos del clúster.</span><span class="sxs-lookup"><span data-stu-id="9e199-147">As a result balancing is triggered hello next time hello Cluster Resource Manager checks.</span></span> <span data-ttu-id="9e199-148">Hola *MinLoadBalancingInterval* temporizador define la frecuencia con hello Administrador de recursos del clúster debe comprobar si el nuevo equilibrio es necesario.</span><span class="sxs-lookup"><span data-stu-id="9e199-148">hello *MinLoadBalancingInterval* timer defines how often hello Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="9e199-149">La comprobación no significa que suceda nada.</span><span class="sxs-lookup"><span data-stu-id="9e199-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="9e199-150">Se han definido umbrales de equilibrio de forma por métrica como parte de la definición del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e199-150">Balancing Thresholds are defined on a per-metric basis as a part of hello cluster definition.</span></span> <span data-ttu-id="9e199-151">Para más información sobre las métricas, consulte [este artículo](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="9e199-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="9e199-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="9e199-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="9e199-153">a través de ClusterConfig.json para las implementaciones independientes o Template.json para los clústeres hospedados en Azure:</span><span class="sxs-lookup"><span data-stu-id="9e199-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="9e199-154"><center>
![Ejemplo de umbral de equilibrio][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="9e199-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="9e199-155">En este ejemplo, cada servicio solo consume una unidad de alguna métrica.</span><span class="sxs-lookup"><span data-stu-id="9e199-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="9e199-156">En el ejemplo de Hola superior, carga máxima de hello en un nodo es cinco y mínimo de hello es dos.</span><span class="sxs-lookup"><span data-stu-id="9e199-156">In hello top example, hello maximum load on a node is five and hello minimum is two.</span></span> <span data-ttu-id="9e199-157">Supongamos que Hola equilibrio umbral para esta métrica es tres.</span><span class="sxs-lookup"><span data-stu-id="9e199-157">Let’s say that hello balancing threshold for this metric is three.</span></span> <span data-ttu-id="9e199-158">Puesto que la proporción de hello en clúster de hello es 5/2 = 2.5 y que es menor que la especificada de hello equilibrio umbral de tres, clúster de hello está equilibrada.</span><span class="sxs-lookup"><span data-stu-id="9e199-158">Since hello ratio in hello cluster is 5/2 = 2.5 and that is less than hello specified balancing threshold of three, hello cluster is balanced.</span></span> <span data-ttu-id="9e199-159">Equilibrio no se desencadena cuando comprueba Hola, Administrador de recursos del clúster.</span><span class="sxs-lookup"><span data-stu-id="9e199-159">No balancing is triggered when hello Cluster Resource Manager checks.</span></span>

<span data-ttu-id="9e199-160">En el ejemplo de la parte inferior de hello, carga máxima de hello en un nodo es 10, mientras mínimo hello es dos, como resultado una relación de cinco.</span><span class="sxs-lookup"><span data-stu-id="9e199-160">In hello bottom example, hello maximum load on a node is 10, while hello minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="9e199-161">Cinco es mayor que el umbral de equilibrio designado de Hola de tres para esa métrica.</span><span class="sxs-lookup"><span data-stu-id="9e199-161">Five is greater than hello designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="9e199-162">Como resultado, una ejecución de reequilibrio será programada Hola tiempo siguiente equilibrio se activa de temporizador.</span><span class="sxs-lookup"><span data-stu-id="9e199-162">As a result, a rebalancing run will be scheduled next time hello balancing timer fires.</span></span> <span data-ttu-id="9e199-163">En una situación como ésta cierta carga es tooNode3 normalmente distribuida.</span><span class="sxs-lookup"><span data-stu-id="9e199-163">In a situation like this some load is usually distributed tooNode3.</span></span> <span data-ttu-id="9e199-164">Porque Hola, Administrador de recursos de clúster de tejido de servicio no usa un enfoque expansivo, cierta carga también podría ser tooNode2 distribuida.</span><span class="sxs-lookup"><span data-stu-id="9e199-164">Because hello Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed tooNode2.</span></span> 

<span data-ttu-id="9e199-165"><center>
![Acciones de ejemplo de umbral de equilibrio][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="9e199-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="9e199-166">"Equilibrio" controla dos estrategias distintas para administrar la carga del clúster.</span><span class="sxs-lookup"><span data-stu-id="9e199-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="9e199-167">estrategia de predeterminada Hola Hola usos del Administrador de recursos de clúster es toodistribute carga en todos los nodos de hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e199-167">hello default strategy that hello Cluster Resource Manager uses is toodistribute load across hello nodes in hello cluster.</span></span> <span data-ttu-id="9e199-168">Hola otra estrategia es [desfragmentación](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="9e199-168">hello other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="9e199-169">La desfragmentación se realiza durante Hola equilibrio mismo ejecutar.</span><span class="sxs-lookup"><span data-stu-id="9e199-169">Defragmentation is performed during hello same balancing run.</span></span> <span data-ttu-id="9e199-170">Hello las estrategias de desfragmentación y equilibrio pueden utilizarse para diferentes métricas dentro de hello mismo clúster.</span><span class="sxs-lookup"><span data-stu-id="9e199-170">hello balancing and defragmentation strategies can be used for different metrics within hello same cluster.</span></span> <span data-ttu-id="9e199-171">Un servicio puede tener métricas de equilibrio y desfragmentación.</span><span class="sxs-lookup"><span data-stu-id="9e199-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="9e199-172">Para las métricas de desfragmentación, carga proporción de Hola de hello en los desencadenadores de clúster de hello reequilibrio cuando sea _a continuación_ Hola equilibrio umbral.</span><span class="sxs-lookup"><span data-stu-id="9e199-172">For defragmentation metrics, hello ratio of hello loads in hello cluster triggers rebalancing when it is _below_ hello balancing threshold.</span></span> 
>

<span data-ttu-id="9e199-173">Introducción a continuación Hola equilibrio umbral no es un objetivo explícito.</span><span class="sxs-lookup"><span data-stu-id="9e199-173">Getting below hello balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="9e199-174">Los umbrales de equilibrio son tan solo un *desencadenador*.</span><span class="sxs-lookup"><span data-stu-id="9e199-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="9e199-175">Cuando equilibrio se ejecuta, Hola, Administrador de recursos del clúster determina qué mejoras puede ralentizar, si lo hay.</span><span class="sxs-lookup"><span data-stu-id="9e199-175">When balancing runs, hello Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="9e199-176">El inicio de una búsqueda de equilibrio no significa que nada cambie.</span><span class="sxs-lookup"><span data-stu-id="9e199-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="9e199-177">A veces hello clúster es toocorrect desequilibrado pero demasiado limitada.</span><span class="sxs-lookup"><span data-stu-id="9e199-177">Sometimes hello cluster is imbalanced but too constrained toocorrect.</span></span> <span data-ttu-id="9e199-178">Como alternativa, mejoras de hello necesitan movimientos que son demasiado [costoso](service-fabric-cluster-resource-manager-movement-cost.md)).</span><span class="sxs-lookup"><span data-stu-id="9e199-178">Alternatively, hello improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="9e199-179">umbrales de actividad</span><span class="sxs-lookup"><span data-stu-id="9e199-179">Activity thresholds</span></span>
<span data-ttu-id="9e199-180">A veces, aunque los nodos son relativamente desequilibrados, Hola *total* cantidad de carga en el clúster de hello es baja.</span><span class="sxs-lookup"><span data-stu-id="9e199-180">Sometimes, although nodes are relatively imbalanced, hello *total* amount of load in hello cluster is low.</span></span> <span data-ttu-id="9e199-181">falta de Hola de carga podría ser una dip transitoria, o porque clúster hello ' s new and simplemente Introducción al iniciar.</span><span class="sxs-lookup"><span data-stu-id="9e199-181">hello lack of load could be a transient dip, or because hello cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="9e199-182">En cualquier caso, no puede tiempo toospend Hola clúster con equilibrio porque hay poca toobe adquirida.</span><span class="sxs-lookup"><span data-stu-id="9e199-182">In either case, you may not want toospend time balancing hello cluster because there’s little toobe gained.</span></span> <span data-ttu-id="9e199-183">Clúster Hola hayan sufrido equilibrio, se invierte en red y proceso recursos toomove cosas sin realizar cualquier grandes *absoluta* diferencia.</span><span class="sxs-lookup"><span data-stu-id="9e199-183">If hello cluster underwent balancing, you’d spend network and compute resources toomove things around without making any large *absolute* difference.</span></span> <span data-ttu-id="9e199-184">se mueve tooavoid innecesario, hay otro control que se conoce como umbrales de actividad.</span><span class="sxs-lookup"><span data-stu-id="9e199-184">tooavoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="9e199-185">Umbrales de actividad le permite toospecify límite algunos inferior absoluta para la actividad.</span><span class="sxs-lookup"><span data-stu-id="9e199-185">Activity Thresholds allows you toospecify some absolute lower bound for activity.</span></span> <span data-ttu-id="9e199-186">Si ningún nodo se encuentra sobre este umbral, equilibrio no desencadena incluso si hello equilibrio umbral se cumple.</span><span class="sxs-lookup"><span data-stu-id="9e199-186">If no node is over this threshold, balancing isn't triggered even if hello Balancing Threshold is met.</span></span>

<span data-ttu-id="9e199-187">Supongamos que se mantiene el umbral de equilibrio de tres para esta métrica.</span><span class="sxs-lookup"><span data-stu-id="9e199-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="9e199-188">Supongamos también que se tiene un umbral de actividad de 1536.</span><span class="sxs-lookup"><span data-stu-id="9e199-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="9e199-189">En el primer caso de hello, mientras está equilibrado por hello clúster Hola equilibrio umbral existe no es ningún nodo cumple ese umbral de actividad, nada por lo que ocurre.</span><span class="sxs-lookup"><span data-stu-id="9e199-189">In hello first case, while hello cluster is imbalanced per hello Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="9e199-190">En el ejemplo de la parte inferior de hello, Nodo1 está por encima de hello umbral de actividad.</span><span class="sxs-lookup"><span data-stu-id="9e199-190">In hello bottom example, Node1 is over hello Activity Threshold.</span></span> <span data-ttu-id="9e199-191">Dado que ambos Hola umbral de equilibrio y se superan Hola actividad umbral de métrica de Hola, equilibrio está programado.</span><span class="sxs-lookup"><span data-stu-id="9e199-191">Since both hello Balancing Threshold and hello Activity Threshold for hello metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="9e199-192">Por ejemplo, echemos un vistazo a Hola siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="9e199-192">As an example, let's look at hello following diagram:</span></span> 

<span data-ttu-id="9e199-193"><center>
![Ejemplo de umbral de actividad][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="9e199-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="9e199-194">Igual que los umbrales de equilibrio, umbrales de actividad son definidos por métrica a través de la definición del clúster hello:</span><span class="sxs-lookup"><span data-stu-id="9e199-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via hello cluster definition:</span></span>

<span data-ttu-id="9e199-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="9e199-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="9e199-196">a través de ClusterConfig.json para las implementaciones independientes o Template.json para los clústeres hospedados en Azure:</span><span class="sxs-lookup"><span data-stu-id="9e199-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="9e199-197">Umbrales de equilibrio y actividad son ambos métrica específica tooa ligada - equilibrio se activa sólo si ambos Hola umbral de equilibrio y se supera el umbral de actividad para hello misma métrica.</span><span class="sxs-lookup"><span data-stu-id="9e199-197">Balancing and activity thresholds are both tied tooa specific metric - balancing is triggered only if both hello Balancing Threshold and Activity Threshold is exceeded for hello same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="9e199-198">Equilibrio conjunto de los servicios</span><span class="sxs-lookup"><span data-stu-id="9e199-198">Balancing services together</span></span>
<span data-ttu-id="9e199-199">Si el clúster de hello es desequilibrado o no es una decisión de todo el clúster.</span><span class="sxs-lookup"><span data-stu-id="9e199-199">Whether hello cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="9e199-200">Sin embargo, manera Hola decidimos acerca de la solución refiere a instancias alrededor y réplicas de servicio individuales.</span><span class="sxs-lookup"><span data-stu-id="9e199-200">However, hello way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="9e199-201">Tiene sentido, ¿no?</span><span class="sxs-lookup"><span data-stu-id="9e199-201">This makes sense, right?</span></span> <span data-ttu-id="9e199-202">Si la memoria es apilada en un nodo, varias réplicas o instancias podrían contribuir tooit.</span><span class="sxs-lookup"><span data-stu-id="9e199-202">If memory is stacked up on one node, multiple replicas or instances could be contributing tooit.</span></span> <span data-ttu-id="9e199-203">Corrección desequilibrio Hola podría ser necesario mover cualquiera de las réplicas con estado de Hola o instancias sin estado que utiliza Hola desequilibrado métrica.</span><span class="sxs-lookup"><span data-stu-id="9e199-203">Fixing hello imbalance could require moving any of hello stateful replicas or stateless instances that use hello imbalanced metric.</span></span>

<span data-ttu-id="9e199-204">Sin embargo, en ocasiones obtiene mueve un servicio que no sea propio desequilibrado (recuerde discusión Hola de local y global pondera anteriormente).</span><span class="sxs-lookup"><span data-stu-id="9e199-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember hello discussion of local and global weights earlier).</span></span> <span data-ttu-id="9e199-205">¿Por qué habría de moverse un servicio si todas sus métricas están equilibradas?</span><span class="sxs-lookup"><span data-stu-id="9e199-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="9e199-206">Veamos un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9e199-206">Let’s see an example:</span></span>

- <span data-ttu-id="9e199-207">Supongamos que hay cuatro servicios, Service1, Service2, Service3 y Service4.</span><span class="sxs-lookup"><span data-stu-id="9e199-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="9e199-208">Service1 informa de las métricas Metric1 y Metric2.</span><span class="sxs-lookup"><span data-stu-id="9e199-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="9e199-209">Service2 informa de las métricas Metric2 y Metric3.</span><span class="sxs-lookup"><span data-stu-id="9e199-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="9e199-210">Service3 informa de las métricas Metric3 y Metric4.</span><span class="sxs-lookup"><span data-stu-id="9e199-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="9e199-211">Service4 informa de la Metric99.</span><span class="sxs-lookup"><span data-stu-id="9e199-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="9e199-212">Seguramente puede ver adónde queremos llegar: hay una cadena.</span><span class="sxs-lookup"><span data-stu-id="9e199-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="9e199-213">En realidad no tenemos cuatro servicios independientes, sino tres servicios que están relacionados y uno que va por su cuenta.</span><span class="sxs-lookup"><span data-stu-id="9e199-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="9e199-214"><center>
![Equilibrio conjunto de los servicios][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="9e199-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="9e199-215">Debido a esta cadena, es posible que un desequilibrio en las métricas de 1 a 4 puede hacer que las réplicas o instancias que pertenecen tooservices toomove de 1 a 3 alrededor.</span><span class="sxs-lookup"><span data-stu-id="9e199-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging tooservices 1-3 toomove around.</span></span> <span data-ttu-id="9e199-216">También sabemos que un desequilibrio en las métricas 1, 2 o 3 no puede ocasionar movimientos en Service4.</span><span class="sxs-lookup"><span data-stu-id="9e199-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="9e199-217">No habría ningún punto desde mover réplicas de Hola o instancias que pertenecen tooService4 alrededor puede no aportan nada tooimpact Hola equilibrio entre las métricas de 1 a 3.</span><span class="sxs-lookup"><span data-stu-id="9e199-217">There would be no point since moving hello replicas or instances belonging tooService4 around can do absolutely nothing tooimpact hello balance of Metrics 1-3.</span></span>

<span data-ttu-id="9e199-218">Hola, Administrador de recursos del clúster imagina automáticamente qué servicios están relacionados.</span><span class="sxs-lookup"><span data-stu-id="9e199-218">hello Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="9e199-219">Agregar, quitar o cambian las métricas de Hola para servicios pueden afectar a las relaciones entre ellas.</span><span class="sxs-lookup"><span data-stu-id="9e199-219">Adding, removing, or changing hello metrics for services can impact their relationships.</span></span> <span data-ttu-id="9e199-220">Por ejemplo, entre las dos ejecuciones de equilibrio Service2 se haya actualizado tooremove Metric2.</span><span class="sxs-lookup"><span data-stu-id="9e199-220">For example, between two runs of balancing Service2 may have been updated tooremove Metric2.</span></span> <span data-ttu-id="9e199-221">Esto interrumpe la cadena de hello entre Service1 y Service2.</span><span class="sxs-lookup"><span data-stu-id="9e199-221">This breaks hello chain between Service1 and Service2.</span></span> <span data-ttu-id="9e199-222">Ahora, en lugar de dos grupos de servicios relacionados, hay tres:</span><span class="sxs-lookup"><span data-stu-id="9e199-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="9e199-223"><center>
![Equilibrio conjunto de los servicios][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="9e199-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="9e199-224">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9e199-224">Next steps</span></span>
* <span data-ttu-id="9e199-225">Las métricas son cómo Hola, Administrador de recursos de clúster de tejido de servicio administra capacidad en clúster de Hola y consumo.</span><span class="sxs-lookup"><span data-stu-id="9e199-225">Metrics are how hello Service Fabric Cluster Resource Manger manages consumption and capacity in hello cluster.</span></span> <span data-ttu-id="9e199-226">toolearn más información acerca de las métricas y cómo tooconfigure, visite [este artículo](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="9e199-226">toolearn more about metrics and how tooconfigure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="9e199-227">Coste del movimiento es una manera de señalización toohello Administrador de recursos del clúster que determinados servicios estén toomove más cara que otras.</span><span class="sxs-lookup"><span data-stu-id="9e199-227">Movement Cost is one way of signaling toohello Cluster Resource Manager that certain services are more expensive toomove than others.</span></span> <span data-ttu-id="9e199-228">Para obtener más información sobre el coste del movimiento, consulte demasiado[este artículo](service-fabric-cluster-resource-manager-movement-cost.md)</span><span class="sxs-lookup"><span data-stu-id="9e199-228">For more about movement cost, refer too[this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="9e199-229">Hola, Administrador de recursos del clúster tiene varias limitaciones que se puede configurar tooslow hacia abajo renovación en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e199-229">hello Cluster Resource Manager has several throttles that you can configure tooslow down churn in hello cluster.</span></span> <span data-ttu-id="9e199-230">Aunque no son normalmente necesarias, si las necesita, puede encontrar información sobre ellas [aquí](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="9e199-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
