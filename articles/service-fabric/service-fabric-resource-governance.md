---
title: "Regulación de recursos de Azure Service Fabric para contenedores y servicios | Microsoft Docs"
description: "Azure Service Fabric permite especificar los límites de recursos de servicios que se ejecutan dentro o fuera de contenedores."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 88d44953ad83f9e7401fd087a39842e4a3790124
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="resource-governance"></a><span data-ttu-id="c0469-103">Regulador de recursos</span><span class="sxs-lookup"><span data-stu-id="c0469-103">Resource governance</span></span> 

<span data-ttu-id="c0469-104">Cuando se ejecutan varios servicios en el mismo clúster o nodo, es posible que un servicio pueda consumir más recursos y privar así a otros servicios.</span><span class="sxs-lookup"><span data-stu-id="c0469-104">When running multiple services on the same node or cluster, it is possible that one service might consume more resources starving other services.</span></span> <span data-ttu-id="c0469-105">A este problema se le conoce como el problema del entorno ruidoso.</span><span class="sxs-lookup"><span data-stu-id="c0469-105">This problem is referred to as the noisy-neighbor problem.</span></span> <span data-ttu-id="c0469-106">Service Fabric permite al desarrollador establecer reservas y límites por servicio, a fin de garantizar la disponibilidad de recursos y, además, limita el uso de recursos.</span><span class="sxs-lookup"><span data-stu-id="c0469-106">Service Fabric allows the developer to specify reservations and limits per service to guarantee resources and also limit its resource usage.</span></span> 

## <a name="resource-governance-metrics"></a><span data-ttu-id="c0469-107">Métricas de regulación de recursos</span><span class="sxs-lookup"><span data-stu-id="c0469-107">Resource governance metrics</span></span> 

<span data-ttu-id="c0469-108">Service Fabric admite la regulación de recursos en función del [paquete de servicio](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="c0469-108">Resource governance is supported in Service Fabric per [Service Package](service-fabric-application-model.md).</span></span> <span data-ttu-id="c0469-109">Los recursos asignados al paquete de servicio pueden dividirse además entre paquetes de código.</span><span class="sxs-lookup"><span data-stu-id="c0469-109">The resources that are assigned to Service Package can be further divided between code packages.</span></span> <span data-ttu-id="c0469-110">Los límites de recursos especificados también suponen la reserva de los recursos.</span><span class="sxs-lookup"><span data-stu-id="c0469-110">The resource limits specified also mean the reservation of the resources.</span></span> <span data-ttu-id="c0469-111">Service Fabric admite la determinación de CPU y memoria por cada paquete de servicio mediante la utilización de dos [métricas](service-fabric-cluster-resource-manager-metrics.md) integradas:</span><span class="sxs-lookup"><span data-stu-id="c0469-111">Service Fabric supports specifying CPU and Memory per service package, using two built-in [metrics](service-fabric-cluster-resource-manager-metrics.md):</span></span>

* <span data-ttu-id="c0469-112">CPU (nombre de métrica `ServiceFabric:/_CpuCores`): un núcleo es un núcleo lógico que se encuentra disponible en el equipo host, y todos los núcleos de todos los nodos se ponderan de la misma forma.</span><span class="sxs-lookup"><span data-stu-id="c0469-112">CPU (metric name `ServiceFabric:/_CpuCores`): A core is a logical core that is available on the host machine, and all cores across all nodes are weighted the same.</span></span>
* <span data-ttu-id="c0469-113">Memoria (nombre de métrica `ServiceFabric:/_MemoryInMB`): la memoria se expresa en megabytes y se asigna a la memoria física que está disponible en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c0469-113">Memory (metric name `ServiceFabric:/_MemoryInMB`): Memory is expressed in megabytes, and it maps to physical memory that is available on the machine.</span></span>

<span data-ttu-id="c0469-114">Solo se ofrecen garantías de reserva flexible; el runtime rechaza la apertura de los nuevos paquetes de servicio en los que se superan los recursos disponibles.</span><span class="sxs-lookup"><span data-stu-id="c0469-114">Only soft reservation guarantees are provided - the runtime rejects opening of new service packages available resources are exceeded.</span></span> <span data-ttu-id="c0469-115">Sin embargo, si se coloca otro archivo ejecutable o contenedor en el nodo, se pueden infringir las garantías de reserva originales.</span><span class="sxs-lookup"><span data-stu-id="c0469-115">However, if another executable or container is placed on the node, that may violate the original reservation guarantees.</span></span>

<span data-ttu-id="c0469-116">Para estas dos métricas, el [Administrador de recursos de clúster](service-fabric-cluster-resource-manager-cluster-description.md) realiza un seguimiento de la capacidad total del clúster, la carga de cada nodo del clúster y los recursos restantes del clúster.</span><span class="sxs-lookup"><span data-stu-id="c0469-116">For these two metrics, the [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) tracks total cluster capacity, the load on each node in the cluster, and, remaining resources in the cluster.</span></span> <span data-ttu-id="c0469-117">Estas dos métricas son equivalentes a cualquier otra métrica de usuario o personalizada, por lo que todas las características existentes se pueden usar con ellas:</span><span class="sxs-lookup"><span data-stu-id="c0469-117">These two metrics are equivalent to any other user or custom metric and all existing features can be used with them:</span></span>
* <span data-ttu-id="c0469-118">El clúster puede [equilibrarse](service-fabric-cluster-resource-manager-balancing.md) en función de estas dos métricas (comportamiento predeterminado).</span><span class="sxs-lookup"><span data-stu-id="c0469-118">Cluster can be [balanced](service-fabric-cluster-resource-manager-balancing.md) according to these two metrics (default behavior).</span></span>
* <span data-ttu-id="c0469-119">El clúster puede [desfragmentarse](service-fabric-cluster-resource-manager-defragmentation-metrics.md) en función de estas dos métricas.</span><span class="sxs-lookup"><span data-stu-id="c0469-119">Cluster can be [defragmented](service-fabric-cluster-resource-manager-defragmentation-metrics.md) according to these two metrics.</span></span>
* <span data-ttu-id="c0469-120">Para [describir un clúster](service-fabric-cluster-resource-manager-cluster-description.md), se puede establecer la capacidad de almacenamiento en búfer para estas dos métricas.</span><span class="sxs-lookup"><span data-stu-id="c0469-120">When [describing a cluster](service-fabric-cluster-resource-manager-cluster-description.md), buffered capacity can be set for these two metrics.</span></span>

<span data-ttu-id="c0469-121">El [informe de carga dinámica](service-fabric-cluster-resource-manager-metrics.md) no es compatible con estas métricas, y las cargas para estas métricas se definen en el momento de la creación.</span><span class="sxs-lookup"><span data-stu-id="c0469-121">[Dynamic load reporting](service-fabric-cluster-resource-manager-metrics.md) is not supported for these metrics, and loads for these metrics are defined at creation time.</span></span>

## <a name="cluster-set-up-for-enabling-resource-governance"></a><span data-ttu-id="c0469-122">Configuración del clúster para habilitar la regulación de recursos</span><span class="sxs-lookup"><span data-stu-id="c0469-122">Cluster set up for enabling resource governance</span></span>

<span data-ttu-id="c0469-123">La capacidad debe definirse manualmente en cada tipo de nodo del clúster como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="c0469-123">Capacity should be defined manually in each node type in the cluster as follows:</span></span>

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
<span data-ttu-id="c0469-124">La regulación de recursos solo se admite en servicios de usuario y no en todos los servicios de sistema.</span><span class="sxs-lookup"><span data-stu-id="c0469-124">Resource governance is allowed only on user services and not on any system services.</span></span> <span data-ttu-id="c0469-125">Al especificar la capacidad, algunos núcleos y la memoria deben dejarse desasignados para los servicios de sistema.</span><span class="sxs-lookup"><span data-stu-id="c0469-125">When specifying capacity, some cores and memory must be left unallocated for system services.</span></span> <span data-ttu-id="c0469-126">Para obtener un rendimiento óptimo, también es necesario activar la siguiente configuración en el manifiesto de clúster:</span><span class="sxs-lookup"><span data-stu-id="c0469-126">For optimal performance, the following setting should also be turned on in the cluster manifest:</span></span> 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a><span data-ttu-id="c0469-127">Definición de la regulación de recursos</span><span class="sxs-lookup"><span data-stu-id="c0469-127">Specifying resource governance</span></span> 

<span data-ttu-id="c0469-128">Los límites de la regulación de recursos se especifican en el manifiesto de aplicación (sección ServiceManifestImport) como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c0469-128">Resource governance limits are specified in the application manifest (ServiceManifestImport section) as shown in the following example:</span></span>

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has the number of CPU cores defined, but doesn't have the MemoryInMB defined.
  In this case, Service Fabric will sum the limits on code packages and uses the sum as 
  the overall ServicePackage limit.
  -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName='ServicePackageA' ServiceManifestVersion='v1'/>
    <Policies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="CodeA1" CpuShares="512" MemoryInMB="1000" />
      <ResourceGovernancePolicy CodePackageRef="CodeA2" CpuShares="256" MemoryInMB="1000" />
    </Policies>
  </ServiceManifestImport>
```
  
<span data-ttu-id="c0469-129">En este ejemplo, el paquete de servicio ServicePackageA obtiene un núcleo de los nodos en que se encuentra.</span><span class="sxs-lookup"><span data-stu-id="c0469-129">In this example, service package ServicePackageA gets one core on the nodes where it is placed.</span></span> <span data-ttu-id="c0469-130">Este paquete de servicio contiene dos paquetes de código (CodeA1 y CodeA2), y ambos especifican el parámetro `CpuShares`.</span><span class="sxs-lookup"><span data-stu-id="c0469-130">This service package contains two code packages (CodeA1 and CodeA2), and both specify the `CpuShares` parameter.</span></span> <span data-ttu-id="c0469-131">La proporción de CpuShares 512:256 divide el núcleo entre los dos paquetes de código.</span><span class="sxs-lookup"><span data-stu-id="c0469-131">The proportion of CpuShares 512:256  divides the core across the two code packages.</span></span> <span data-ttu-id="c0469-132">Por lo tanto, en este ejemplo, CodeA1 obtiene dos tercios de un núcleo y CodeA2 obtiene una tercera parte de un núcleo (y una reserva de garantía flexible del mismo).</span><span class="sxs-lookup"><span data-stu-id="c0469-132">Thus, in this example, CodeA1 gets two-thirds of a core, and  CodeA2 gets one-third of a core (and a soft-guarantee reservation of the same).</span></span> <span data-ttu-id="c0469-133">En caso de que no se especifiquen las proporciones de CpuShares para los paquetes de código, Service Fabric divide los núcleos equitativamente entre ellos.</span><span class="sxs-lookup"><span data-stu-id="c0469-133">In case when CpuShares are not specified for code packages, Service Fabric divides the cores equally among them.</span></span>

<span data-ttu-id="c0469-134">Los límites de memoria son absolutos, por lo que ambos paquetes de código están limitados a 1024 MB de memoria (con una reserva de garantía flexible de dicha capacidad).</span><span class="sxs-lookup"><span data-stu-id="c0469-134">Memory limits are absolute, so both code packages are limited to 1024 MB of memory (and a soft-guarantee reservation of the same).</span></span> <span data-ttu-id="c0469-135">Los paquetes de código (contenedores o procesos) no pueden asignar más memoria de la que establece este límite; si se intenta, el resultado es una excepción de memoria insuficiente.</span><span class="sxs-lookup"><span data-stu-id="c0469-135">Code packages (containers or processes) are not able to allocate more memory than this limit, and attempting to do so results in an out-of-memory exception.</span></span> <span data-ttu-id="c0469-136">Para que la aplicación del límite de recursos funcione, es necesario haber definido límites de memoria en todos los paquetes de código de un paquete de servicio.</span><span class="sxs-lookup"><span data-stu-id="c0469-136">For resource limit enforcement to work, all code packages within a service package should have memory limits specified.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c0469-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c0469-137">Next steps</span></span>
* <span data-ttu-id="c0469-138">Para más información sobre el Administrador de recursos de clúster, lea este [artículo](service-fabric-cluster-resource-manager-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c0469-138">To learn more about Cluster Resource Manager, read this [article](service-fabric-cluster-resource-manager-introduction.md).</span></span>
* <span data-ttu-id="c0469-139">Para más información sobre el modelo de aplicación, los paquetes de servicio, los paquetes de código y cómo se les asignan las réplicas, lea este [artículo](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="c0469-139">To learn more about application model, service packages, code packages and how replicas map to them read this [article](service-fabric-application-model.md).</span></span>
