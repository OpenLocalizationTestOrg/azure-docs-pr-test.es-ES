---
title: 'Cluster Resource Manager de Service Fabric: costo de movimiento | Microsoft Docs'
description: "Información general del costo de movimiento de los servicios de Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 65d4ac73efffcf7b25b1e95da6f9012a9238cb75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-movement-cost"></a><span data-ttu-id="8467b-103">Costo del movimiento del servicio</span><span class="sxs-lookup"><span data-stu-id="8467b-103">Service movement cost</span></span>
<span data-ttu-id="8467b-104">Un factor que Hola Administrador de recursos de clúster de tejido de servicio tiene en cuenta al intentar toodetermine qué clúster de tooa toomake de cambios es el costo de Hola de esos cambios.</span><span class="sxs-lookup"><span data-stu-id="8467b-104">A factor that hello Service Fabric Cluster Resource Manager considers when trying toodetermine what changes toomake tooa cluster is hello cost of those changes.</span></span> <span data-ttu-id="8467b-105">noción de Hola de "costo" es sopesar con respecto a cuánto clúster Hola se puede mejorar.</span><span class="sxs-lookup"><span data-stu-id="8467b-105">hello notion of "cost" is traded off against how much hello cluster can be improved.</span></span> <span data-ttu-id="8467b-106">El costo se tiene en cuenta al mover los servicios por cuestiones de equilibrio, desfragmentación y otros requisitos.</span><span class="sxs-lookup"><span data-stu-id="8467b-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span></span> <span data-ttu-id="8467b-107">objetivo de Hello es toomeet requisitos de Hola Hola menos forma perjudiciales o costosa.</span><span class="sxs-lookup"><span data-stu-id="8467b-107">hello goal is toomeet hello requirements in hello least disruptive or expensive way.</span></span> 

<span data-ttu-id="8467b-108">Mover servicios supone unos costos mínimos de tiempo de CPU y ancho de banda de red.</span><span class="sxs-lookup"><span data-stu-id="8467b-108">Moving services costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="8467b-109">Para los servicios con estado, requiere copiar estado Hola de dichos servicios, consumiendo memoria adicional y disco.</span><span class="sxs-lookup"><span data-stu-id="8467b-109">For stateful services, it requires copying hello state of those services, consuming additional memory and disk.</span></span> <span data-ttu-id="8467b-110">Minimizan los costos de Hola de soluciones que Hola Administrador de recursos de clúster de Azure Service Fabric aparece con la ayuda a garantizar que no se invierte en recursos del clúster de hello innecesariamente.</span><span class="sxs-lookup"><span data-stu-id="8467b-110">Minimizing hello cost of solutions that hello Azure Service Fabric Cluster Resource Manager comes up with helps ensure that hello cluster's resources aren't spent unnecessarily.</span></span> <span data-ttu-id="8467b-111">Sin embargo, también prefiere no tooignore soluciones que podrían mejorar notablemente asignación Hola de recursos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="8467b-111">However, you also don’t want tooignore solutions that would significantly improve hello allocation of resources in hello cluster.</span></span>

<span data-ttu-id="8467b-112">Hola, Administrador de recursos del clúster tiene dos maneras de calcular los costos y limita su acceso mientras lo intenta de clúster de hello toomanage.</span><span class="sxs-lookup"><span data-stu-id="8467b-112">hello Cluster Resource Manager has two ways of computing costs and limiting them while it tries toomanage hello cluster.</span></span> <span data-ttu-id="8467b-113">primer mecanismo de Hello simplemente está contando cada movimiento que sería.</span><span class="sxs-lookup"><span data-stu-id="8467b-113">hello first mechanism is simply counting every move that it would make.</span></span> <span data-ttu-id="8467b-114">Si se generan dos soluciones con hello mismo equilibrar (puntuación), a continuación, Hola, Administrador de recursos de clúster prefiere Hola uno con hello menor coste (número total de movimientos).</span><span class="sxs-lookup"><span data-stu-id="8467b-114">If two solutions are generated with about hello same balance (score), then hello Cluster Resource Manager prefers hello one with hello lowest cost (total number of moves).</span></span>

<span data-ttu-id="8467b-115">Esta estrategia da buenos resultados.</span><span class="sxs-lookup"><span data-stu-id="8467b-115">This strategy works well.</span></span> <span data-ttu-id="8467b-116">Pero, al igual que con cargas predeterminadas o estáticas, es poco probable que en cualquier sistema complejo todos los movimientos sean iguales.</span><span class="sxs-lookup"><span data-stu-id="8467b-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="8467b-117">Algunas son probablemente toobe mucho más caro.</span><span class="sxs-lookup"><span data-stu-id="8467b-117">Some are likely toobe much more expensive.</span></span>

## <a name="setting-move-costs"></a><span data-ttu-id="8467b-118">Establecimiento de los costos de movimiento</span><span class="sxs-lookup"><span data-stu-id="8467b-118">Setting Move Costs</span></span> 
<span data-ttu-id="8467b-119">Puede especificar el costo de movimiento de hello predeterminado para un servicio cuando se crea:</span><span class="sxs-lookup"><span data-stu-id="8467b-119">You can specify hello default move cost for a service when it is created:</span></span>

<span data-ttu-id="8467b-120">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8467b-120">PowerShell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

<span data-ttu-id="8467b-121">C#:</span><span class="sxs-lookup"><span data-stu-id="8467b-121">C#:</span></span> 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="8467b-122">También puede especificar o actualizar MoveCost dinámicamente para un servicio después de que se ha creado el servicio de hello:</span><span class="sxs-lookup"><span data-stu-id="8467b-122">You can also specify or update MoveCost dynamically for a service after hello service has been created:</span></span> 

<span data-ttu-id="8467b-123">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8467b-123">PowerShell:</span></span> 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

<span data-ttu-id="8467b-124">C#:</span><span class="sxs-lookup"><span data-stu-id="8467b-124">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a><span data-ttu-id="8467b-125">Especificación de forma dinámica del costo de movimiento por réplica</span><span class="sxs-lookup"><span data-stu-id="8467b-125">Dynamically specifying move cost on a per-replica basis</span></span>

<span data-ttu-id="8467b-126">Hello fragmentos de código anteriores son todos para especificar MoveCost para un servicio completo al mismo tiempo desde el propio servicio Hola exterior.</span><span class="sxs-lookup"><span data-stu-id="8467b-126">hello preceding snippets are all for specifying MoveCost for a whole service at once from outside hello service itself.</span></span> <span data-ttu-id="8467b-127">Sin embargo, mover el costo es más útil es cuando cambia el costo de movimiento de Hola de un objeto de servicio específico sobre su duración.</span><span class="sxs-lookup"><span data-stu-id="8467b-127">However, move cost is most useful is when hello move cost of a specific service object changes over its lifespan.</span></span> <span data-ttu-id="8467b-128">Puesto que Hola servicios por sí mismos, probablemente tiene Hola mejor idea de cómo costosos son toomove un momento dado, hay una API para tooreport servicios su propios movimiento individual de costo en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="8467b-128">Since hello services themselves probably have hello best idea of how costly they are toomove a given time, there's an API for services tooreport their own individual move cost during runtime.</span></span> 

<span data-ttu-id="8467b-129">C#:</span><span class="sxs-lookup"><span data-stu-id="8467b-129">C#:</span></span>

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a><span data-ttu-id="8467b-130">Impacto del costo de movimiento</span><span class="sxs-lookup"><span data-stu-id="8467b-130">Impact of move cost</span></span>
<span data-ttu-id="8467b-131">El valor MoveCost tiene cuatro niveles: Zero (Cero), Low (Bajo), Medium (Medio) y High (Alto).</span><span class="sxs-lookup"><span data-stu-id="8467b-131">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="8467b-132">MoveCosts son relativa tooeach otro, excepto cero.</span><span class="sxs-lookup"><span data-stu-id="8467b-132">MoveCosts are relative tooeach other, except for Zero.</span></span> <span data-ttu-id="8467b-133">Cero costo de movimiento significa que el movimiento es gratuito y no debe contar con la puntuación de Hola de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="8467b-133">Zero move cost means that movement is free and should not count against hello score of hello solution.</span></span> <span data-ttu-id="8467b-134">Configuración de su movimiento costo tooHigh *no* garantiza que la réplica Hola permanece en un solo lugar.</span><span class="sxs-lookup"><span data-stu-id="8467b-134">Setting your move cost tooHigh does *not* guarantee that hello replica stays in one place.</span></span>

<span data-ttu-id="8467b-135"><center>
![Costo de movimiento como un factor en la selección de réplicas para el movimiento][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="8467b-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="8467b-136">MoveCost le ayuda a encontrar soluciones de Hola que causa Hola menor interrupción general y es más fácil tooachieve mientras todavía que llegan al saldo equivalente.</span><span class="sxs-lookup"><span data-stu-id="8467b-136">MoveCost helps you find hello solutions that cause hello least disruption overall and are easiest tooachieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="8467b-137">Noción de un servicio de costo puede ser relativa toomany cosas.</span><span class="sxs-lookup"><span data-stu-id="8467b-137">A service’s notion of cost can be relative toomany things.</span></span> <span data-ttu-id="8467b-138">Hello factores más comunes para calcular el costo de movimiento son:</span><span class="sxs-lookup"><span data-stu-id="8467b-138">hello most common factors in calculating your move cost are:</span></span>

- <span data-ttu-id="8467b-139">cantidad de Hola de estado o los datos que el servicio de hello tiene toomove.</span><span class="sxs-lookup"><span data-stu-id="8467b-139">hello amount of state or data that hello service has toomove.</span></span>
- <span data-ttu-id="8467b-140">costo de Hola de desconexión de los clientes.</span><span class="sxs-lookup"><span data-stu-id="8467b-140">hello cost of disconnection of clients.</span></span> <span data-ttu-id="8467b-141">Mover una réplica principal es normalmente más elevado que el costo de Hola de mover una réplica secundaria.</span><span class="sxs-lookup"><span data-stu-id="8467b-141">Moving a primary replica is usually more costly than hello cost of moving a secondary replica.</span></span>
- <span data-ttu-id="8467b-142">costo de Hola de interrumpir una operación en curso.</span><span class="sxs-lookup"><span data-stu-id="8467b-142">hello cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="8467b-143">Nivel de almacén de algunas operaciones en datos de Hola o las operaciones realizadas en la llamada de cliente de respuesta tooa son costosas.</span><span class="sxs-lookup"><span data-stu-id="8467b-143">Some operations at hello data store level or operations performed in response tooa client call are costly.</span></span> <span data-ttu-id="8467b-144">Después de un punto determinado, no desea toostop en caso de que no es necesario.</span><span class="sxs-lookup"><span data-stu-id="8467b-144">After a certain point, you don’t want toostop them if you don’t have to.</span></span> <span data-ttu-id="8467b-145">Por lo tanto mientras la operación de hello está sucediendo, aumentar costo de movimiento de Hola de esta probabilidad de Hola de tooreduce de objeto de servicio que se desplaza.</span><span class="sxs-lookup"><span data-stu-id="8467b-145">So while hello operation is going on, you increase hello move cost of this service object tooreduce hello likelihood that it moves.</span></span> <span data-ttu-id="8467b-146">Cuando se realiza la operación de hello, establezca Hola costo atrás toonormal.</span><span class="sxs-lookup"><span data-stu-id="8467b-146">When hello operation is done, you set hello cost back toonormal.</span></span>

## <a name="enabling-move-cost-in-your-cluster"></a><span data-ttu-id="8467b-147">Habilitación del costo de movimiento en el clúster</span><span class="sxs-lookup"><span data-stu-id="8467b-147">Enabling move cost in your cluster</span></span>
<span data-ttu-id="8467b-148">En orden para Hola más granular toobe MoveCosts tener en cuenta, MoveCost debe estar habilitada en el clúster.</span><span class="sxs-lookup"><span data-stu-id="8467b-148">In order for hello more granular MoveCosts toobe taken into account, MoveCost must be enabled in your cluster.</span></span> <span data-ttu-id="8467b-149">Sin esta configuración, se utiliza el modo de predeterminado de Hola de recuento de movimientos para calcular MoveCost y MoveCost informes se omiten.</span><span class="sxs-lookup"><span data-stu-id="8467b-149">Without this setting, hello default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span></span>


<span data-ttu-id="8467b-150">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="8467b-150">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

<span data-ttu-id="8467b-151">a través de ClusterConfig.json para las implementaciones independientes o Template.json para los clústeres hospedados en Azure:</span><span class="sxs-lookup"><span data-stu-id="8467b-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="8467b-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8467b-152">Next steps</span></span>
- <span data-ttu-id="8467b-153">Administrador de recursos de clúster de tejido de servicio utiliza métricas toomanage consumo y la capacidad de clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="8467b-153">Service Fabric Cluster Resource Manger uses metrics toomanage consumption and capacity in hello cluster.</span></span> <span data-ttu-id="8467b-154">toolearn más información acerca de las métricas y cómo tooconfigure, visite [consumo de recursos de administración y carga de Service Fabric con métricas](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="8467b-154">toolearn more about metrics and how tooconfigure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
- <span data-ttu-id="8467b-155">toolearn acerca de cómo Hola, Administrador de recursos del clúster administra y equilibra la carga en el clúster de hello, visite [equilibrio su clúster de Service Fabric](service-fabric-cluster-resource-manager-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="8467b-155">toolearn about how hello Cluster Resource Manager manages and balances load in hello cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
