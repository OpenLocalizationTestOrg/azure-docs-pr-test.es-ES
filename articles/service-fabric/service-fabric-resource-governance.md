---
title: Regulador de recursos de tejido de servicio para los contenedores y los servicios de aaaAzure | Documentos de Microsoft
description: "Azure Service Fabric permite toospecify límites de recursos para servicios que se ejecutan dentro o fuera contenedores."
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
ms.openlocfilehash: 34e368211d98ff6b5b294c9c8b3af5ca30eeb20c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resource-governance"></a><span data-ttu-id="bb16a-103">Regulador de recursos</span><span class="sxs-lookup"><span data-stu-id="bb16a-103">Resource governance</span></span> 

<span data-ttu-id="bb16a-104">Cuando se ejecutan varios servicios en hello mismo nodo o el clúster, es posible que un servicio puede consumir más recursos privar a otros servicios.</span><span class="sxs-lookup"><span data-stu-id="bb16a-104">When running multiple services on hello same node or cluster, it is possible that one service might consume more resources starving other services.</span></span> <span data-ttu-id="bb16a-105">Este problema es tooas que se hace referencia hello-vecino.</span><span class="sxs-lookup"><span data-stu-id="bb16a-105">This problem is referred tooas hello noisy-neighbor problem.</span></span> <span data-ttu-id="bb16a-106">Service Fabric permite las reservas toospecify de desarrollador de Hola y límites por los recursos del servicio tooguarantee y limitar su uso de recursos.</span><span class="sxs-lookup"><span data-stu-id="bb16a-106">Service Fabric allows hello developer toospecify reservations and limits per service tooguarantee resources and also limit its resource usage.</span></span> 

## <a name="resource-governance-metrics"></a><span data-ttu-id="bb16a-107">Métricas de regulación de recursos</span><span class="sxs-lookup"><span data-stu-id="bb16a-107">Resource governance metrics</span></span> 

<span data-ttu-id="bb16a-108">Service Fabric admite la regulación de recursos en función del [paquete de servicio](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="bb16a-108">Resource governance is supported in Service Fabric per [Service Package](service-fabric-application-model.md).</span></span> <span data-ttu-id="bb16a-109">recursos de Hello asignados tooService paquete pueden dividirse aún más entre los paquetes de código.</span><span class="sxs-lookup"><span data-stu-id="bb16a-109">hello resources that are assigned tooService Package can be further divided between code packages.</span></span> <span data-ttu-id="bb16a-110">límites de recursos de Hello especificados también significan una reserva Hola de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb16a-110">hello resource limits specified also mean hello reservation of hello resources.</span></span> <span data-ttu-id="bb16a-111">Service Fabric admite la determinación de CPU y memoria por cada paquete de servicio mediante la utilización de dos [métricas](service-fabric-cluster-resource-manager-metrics.md) integradas:</span><span class="sxs-lookup"><span data-stu-id="bb16a-111">Service Fabric supports specifying CPU and Memory per service package, using two built-in [metrics](service-fabric-cluster-resource-manager-metrics.md):</span></span>

* <span data-ttu-id="bb16a-112">CPU (nombre de la métrica `ServiceFabric:/_CpuCores`): un núcleo es un núcleo lógico que está disponible en el equipo de host de Hola y todos los núcleos en todos los nodos se ponderan Hola igual.</span><span class="sxs-lookup"><span data-stu-id="bb16a-112">CPU (metric name `ServiceFabric:/_CpuCores`): A core is a logical core that is available on hello host machine, and all cores across all nodes are weighted hello same.</span></span>
* <span data-ttu-id="bb16a-113">Memoria (nombre de la métrica `ServiceFabric:/_MemoryInMB`): memoria se expresa en megabytes y se asigna memoria toophysical que está disponible en la máquina de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb16a-113">Memory (metric name `ServiceFabric:/_MemoryInMB`): Memory is expressed in megabytes, and it maps toophysical memory that is available on hello machine.</span></span>

<span data-ttu-id="bb16a-114">Solo las garantías de reserva de software son siempre - en tiempo de ejecución de hello rechaza la apertura del nuevo servicio se superan los recursos disponibles de paquetes.</span><span class="sxs-lookup"><span data-stu-id="bb16a-114">Only soft reservation guarantees are provided - hello runtime rejects opening of new service packages available resources are exceeded.</span></span> <span data-ttu-id="bb16a-115">Sin embargo, si otro archivo ejecutable o contenedor se coloca en el nodo de hello, que pueden infringir las garantías de reserva original Hola.</span><span class="sxs-lookup"><span data-stu-id="bb16a-115">However, if another executable or container is placed on hello node, that may violate hello original reservation guarantees.</span></span>

<span data-ttu-id="bb16a-116">Para estos dos métricas Hola [Administrador de recursos del clúster](service-fabric-cluster-resource-manager-cluster-description.md) realiza un seguimiento de la capacidad total en el clúster, carga de hello en cada nodo de clúster de hello, y, quedan recursos en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb16a-116">For these two metrics, hello [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) tracks total cluster capacity, hello load on each node in hello cluster, and, remaining resources in hello cluster.</span></span> <span data-ttu-id="bb16a-117">Estos dos métricas es equivalente tooany otro usuario o una métrica personalizada y todas las características existentes pueden usarse con ellos:</span><span class="sxs-lookup"><span data-stu-id="bb16a-117">These two metrics are equivalent tooany other user or custom metric and all existing features can be used with them:</span></span>
* <span data-ttu-id="bb16a-118">Puede ser clúster [equilibrada](service-fabric-cluster-resource-manager-balancing.md) según las métricas de toothese dos (comportamiento predeterminado).</span><span class="sxs-lookup"><span data-stu-id="bb16a-118">Cluster can be [balanced](service-fabric-cluster-resource-manager-balancing.md) according toothese two metrics (default behavior).</span></span>
* <span data-ttu-id="bb16a-119">Puede ser clúster [desfragmentados](service-fabric-cluster-resource-manager-defragmentation-metrics.md) según las métricas de toothese dos.</span><span class="sxs-lookup"><span data-stu-id="bb16a-119">Cluster can be [defragmented](service-fabric-cluster-resource-manager-defragmentation-metrics.md) according toothese two metrics.</span></span>
* <span data-ttu-id="bb16a-120">Para [describir un clúster](service-fabric-cluster-resource-manager-cluster-description.md), se puede establecer la capacidad de almacenamiento en búfer para estas dos métricas.</span><span class="sxs-lookup"><span data-stu-id="bb16a-120">When [describing a cluster](service-fabric-cluster-resource-manager-cluster-description.md), buffered capacity can be set for these two metrics.</span></span>

<span data-ttu-id="bb16a-121">El [informe de carga dinámica](service-fabric-cluster-resource-manager-metrics.md) no es compatible con estas métricas, y las cargas para estas métricas se definen en el momento de la creación.</span><span class="sxs-lookup"><span data-stu-id="bb16a-121">[Dynamic load reporting](service-fabric-cluster-resource-manager-metrics.md) is not supported for these metrics, and loads for these metrics are defined at creation time.</span></span>

## <a name="cluster-set-up-for-enabling-resource-governance"></a><span data-ttu-id="bb16a-122">Configuración del clúster para habilitar la regulación de recursos</span><span class="sxs-lookup"><span data-stu-id="bb16a-122">Cluster set up for enabling resource governance</span></span>

<span data-ttu-id="bb16a-123">Capacidad debe definirse manualmente en cada tipo de nodo de clúster de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="bb16a-123">Capacity should be defined manually in each node type in hello cluster as follows:</span></span>

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
<span data-ttu-id="bb16a-124">La regulación de recursos solo se admite en servicios de usuario y no en todos los servicios de sistema.</span><span class="sxs-lookup"><span data-stu-id="bb16a-124">Resource governance is allowed only on user services and not on any system services.</span></span> <span data-ttu-id="bb16a-125">Al especificar la capacidad, algunos núcleos y la memoria deben dejarse desasignados para los servicios de sistema.</span><span class="sxs-lookup"><span data-stu-id="bb16a-125">When specifying capacity, some cores and memory must be left unallocated for system services.</span></span> <span data-ttu-id="bb16a-126">Para obtener un rendimiento óptimo, Hola después de la configuración debe también activarse en el manifiesto de clúster de hello:</span><span class="sxs-lookup"><span data-stu-id="bb16a-126">For optimal performance, hello following setting should also be turned on in hello cluster manifest:</span></span> 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a><span data-ttu-id="bb16a-127">Definición de la regulación de recursos</span><span class="sxs-lookup"><span data-stu-id="bb16a-127">Specifying resource governance</span></span> 

<span data-ttu-id="bb16a-128">Límites de regulación de recursos se especifican en el manifiesto de aplicación Hola (sección ServiceManifestImport) como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="bb16a-128">Resource governance limits are specified in hello application manifest (ServiceManifestImport section) as shown in hello following example:</span></span>

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has hello number of CPU cores defined, but doesn't have hello MemoryInMB defined.
  In this case, Service Fabric will sum hello limits on code packages and uses hello sum as 
  hello overall ServicePackage limit.
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
  
<span data-ttu-id="bb16a-129">En este ejemplo, el paquete de servicio ServicePackageA Obtiene un núcleo en nodos de Hola donde se coloca.</span><span class="sxs-lookup"><span data-stu-id="bb16a-129">In this example, service package ServicePackageA gets one core on hello nodes where it is placed.</span></span> <span data-ttu-id="bb16a-130">Este paquete de servicio contiene dos paquetes de código (CodeA1 y CodeA2), y ambos especifican hello `CpuShares` parámetro.</span><span class="sxs-lookup"><span data-stu-id="bb16a-130">This service package contains two code packages (CodeA1 and CodeA2), and both specify hello `CpuShares` parameter.</span></span> <span data-ttu-id="bb16a-131">proporción de Hola de CpuShares 512:256 divide core Hola a todos los paquetes de código de hello dos.</span><span class="sxs-lookup"><span data-stu-id="bb16a-131">hello proportion of CpuShares 512:256  divides hello core across hello two code packages.</span></span> <span data-ttu-id="bb16a-132">Por lo tanto, en este ejemplo, CodeA1 obtiene dos tercios de un núcleo y CodeA2 Obtiene una tercera parte de un núcleo (y Hola una reserva de garantía de software del mismo).</span><span class="sxs-lookup"><span data-stu-id="bb16a-132">Thus, in this example, CodeA1 gets two-thirds of a core, and  CodeA2 gets one-third of a core (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="bb16a-133">En caso de que cuando CpuShares no se especifican para los paquetes de código, Service Fabric divide núcleos Hola equitativamente entre ellos.</span><span class="sxs-lookup"><span data-stu-id="bb16a-133">In case when CpuShares are not specified for code packages, Service Fabric divides hello cores equally among them.</span></span>

<span data-ttu-id="bb16a-134">Límites de memoria están absolutos, por lo que ambos paquetes de código too1024 limitado MB de memoria (y una reserva de garantía de software del mismo Hola).</span><span class="sxs-lookup"><span data-stu-id="bb16a-134">Memory limits are absolute, so both code packages are limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="bb16a-135">Paquetes de código (contenedores o procesos) no son tooallocate capaz de más memoria que este límite e intentar toodo que se producirá una excepción de memoria insuficiente.</span><span class="sxs-lookup"><span data-stu-id="bb16a-135">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="bb16a-136">Para toowork de cumplimiento del límite de recursos, todos los paquetes de código dentro de un paquete de servicio deben tener límites de memoria especificados.</span><span class="sxs-lookup"><span data-stu-id="bb16a-136">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bb16a-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bb16a-137">Next steps</span></span>
* <span data-ttu-id="bb16a-138">toolearn más sobre recursos Administrador de clústeres, lea esta [artículo](service-fabric-cluster-resource-manager-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bb16a-138">toolearn more about Cluster Resource Manager, read this [article](service-fabric-cluster-resource-manager-introduction.md).</span></span>
* <span data-ttu-id="bb16a-139">toolearn más información sobre el modelo de aplicación, paquetes de servicio, paquetes de código y cómo asignan las réplicas toothem lea esta [artículo](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="bb16a-139">toolearn more about application model, service packages, code packages and how replicas map toothem read this [article](service-fabric-application-model.md).</span></span>
