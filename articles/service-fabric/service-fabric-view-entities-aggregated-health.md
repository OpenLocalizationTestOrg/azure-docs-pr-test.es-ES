---
title: "Visualización del mantenimiento agregado de entidades de Azure Service Fabric | Microsoft Docs"
description: "Se describe cómo consultar, ver y evaluar el mantenimiento agregado de entidades de Azure Service Fabric, a través de consultas de mantenimiento y consultas generales."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: b97972b1bdc28a17fb9c3a0e997738f5bd0b5d15
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="dd81f-103">Vista de los informes de estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="dd81f-103">View Service Fabric health reports</span></span>
<span data-ttu-id="dd81f-104">Azure Service Fabric presenta un [modelo de mantenimiento](service-fabric-health-introduction.md) con entidades de estado en las que componentes y guardianes del sistema pueden notificar las condiciones locales que están supervisando.</span><span class="sxs-lookup"><span data-stu-id="dd81f-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="dd81f-105">El [almacén de estado](service-fabric-health-introduction.md#health-store) agrega todos los datos de mantenimiento para determinar si las entidades son correctas.</span><span class="sxs-lookup"><span data-stu-id="dd81f-105">The [health store](service-fabric-health-introduction.md#health-store) aggregates all health data to determine whether entities are healthy.</span></span>

<span data-ttu-id="dd81f-106">El clúster se rellena automáticamente con informes de estado enviados por los componentes del sistema.</span><span class="sxs-lookup"><span data-stu-id="dd81f-106">The cluster is automatically populated with health reports sent by the system components.</span></span> <span data-ttu-id="dd81f-107">Lea más en [Uso de informes de mantenimiento del sistema para solucionar problemas](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span><span class="sxs-lookup"><span data-stu-id="dd81f-107">Read more at [Use system health reports to troubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="dd81f-108">Service Fabric proporciona varias maneras de obtener el mantenimiento agregado de las entidades:</span><span class="sxs-lookup"><span data-stu-id="dd81f-108">Service Fabric provides multiple ways to get the aggregated health of the entities:</span></span>

* <span data-ttu-id="dd81f-109">[Explorador de Service Fabric](service-fabric-visualizing-your-cluster.md) y otras herramientas de visualización</span><span class="sxs-lookup"><span data-stu-id="dd81f-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="dd81f-110">Consultas de mantenimiento (a través de PowerShell, API o REST)</span><span class="sxs-lookup"><span data-stu-id="dd81f-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="dd81f-111">Consultas generales que devuelven una lista de entidades con el estado como una de las propiedades (a través de PowerShell, API o REST)</span><span class="sxs-lookup"><span data-stu-id="dd81f-111">General queries that return a list of entities that have health as one of the properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="dd81f-112">Para demostrar estas opciones, vamos a usar un clúster local con los nodos y la [aplicación fabric:/WordCount](http://aka.ms/servicefabric-wordcountapp).</span><span class="sxs-lookup"><span data-stu-id="dd81f-112">To demonstrate these options, let's use a local cluster with five nodes and the [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="dd81f-113">La aplicación **fabric:/WordCount** contiene dos servicios predeterminados, uno con estado de tipo `WordCountServiceType` y otro sin estado de tipo `WordCountWebServiceType`.</span><span class="sxs-lookup"><span data-stu-id="dd81f-113">The **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="dd81f-114">He cambiado el archivo `ApplicationManifest.xml` para requerir siete réplicas de destino para el servicio con estado y una partición.</span><span class="sxs-lookup"><span data-stu-id="dd81f-114">I changed the `ApplicationManifest.xml` to require seven target replicas for the stateful service and one partition.</span></span> <span data-ttu-id="dd81f-115">Dado que hay solo cinco nodos en el clúster, los componentes del sistema notifican una advertencia en la partición del servicio porque está por debajo del número de destino.</span><span class="sxs-lookup"><span data-stu-id="dd81f-115">Because there are only five nodes in the cluster, the system components report a warning on the service partition because it is below the target count.</span></span>

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="dd81f-116">Mantenimiento del Explorador de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="dd81f-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="dd81f-117">El Explorador de Service Fabric proporciona una vista visual del clúster.</span><span class="sxs-lookup"><span data-stu-id="dd81f-117">Service Fabric Explorer provides a visual view of the cluster.</span></span> <span data-ttu-id="dd81f-118">En la imagen siguiente, puede ver que:</span><span class="sxs-lookup"><span data-stu-id="dd81f-118">In the image below, you can see that:</span></span>

* <span data-ttu-id="dd81f-119">La aplicación **fabric:/WordCount** está en rojo (en error) porque tiene un evento de error notificado por **MyWatchdog** para la propiedad **Availability**.</span><span class="sxs-lookup"><span data-stu-id="dd81f-119">The application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for the property **Availability**.</span></span>
* <span data-ttu-id="dd81f-120">Uno de sus servicios, **fabric:/WordCount/WordCountService** está en amarillo (en advertencia).</span><span class="sxs-lookup"><span data-stu-id="dd81f-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="dd81f-121">El servicio está configurado con siete réplicas y el clúster tiene cinco nodos, por lo que no se pueden colocar dos réplicas.</span><span class="sxs-lookup"><span data-stu-id="dd81f-121">The service is configured with seven replicas and the cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="dd81f-122">Aunque no se muestra aquí, la partición de servicio está en amarillo debido al informe del sistema de `System.FM` que indica que `Partition is below target replica or instance count` (la partición está por debajo del número de instancias o réplicas de destino).</span><span class="sxs-lookup"><span data-stu-id="dd81f-122">Although it's not shown here, the service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="dd81f-123">La partición en amarillo desencadena el servicio en amarillo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-123">The yellow partition triggers the yellow service.</span></span>
* <span data-ttu-id="dd81f-124">El clúster está en rojo debido a la aplicación en rojo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-124">The cluster is red because of the red application.</span></span>

<span data-ttu-id="dd81f-125">La evaluación usa las directivas predeterminadas del manifiesto de clúster y el manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd81f-125">The evaluation uses default policies from the cluster manifest and application manifest.</span></span> <span data-ttu-id="dd81f-126">Son directivas estrictas y no toleran ningún error.</span><span class="sxs-lookup"><span data-stu-id="dd81f-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="dd81f-127">Vista del clúster con el Explorador de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="dd81f-127">View of the cluster with Service Fabric Explorer:</span></span>

![Vista del clúster con el Explorador de Service Fabric.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="dd81f-129">Obtenga más información sobre el [Explorador de Service Fabric](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="dd81f-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="dd81f-130">Consultas de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="dd81f-130">Health queries</span></span>
<span data-ttu-id="dd81f-131">Service Fabric expone las consultas de mantenimiento para cada uno de los [tipos de entidad](service-fabric-health-introduction.md#health-entities-and-hierarchy)admitidos.</span><span class="sxs-lookup"><span data-stu-id="dd81f-131">Service Fabric exposes health queries for each of the supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="dd81f-132">Se puede acceder a ellas mediante la API, con los métodos de [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), los cmdlets de PowerShell y REST.</span><span class="sxs-lookup"><span data-stu-id="dd81f-132">They can be accessed through the API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="dd81f-133">Estas consultas devuelven información completa de mantenimiento sobre la entidad: el estado de mantenimiento agregado, los eventos de mantenimiento de la entidad, los estados de mantenimiento de los elementos secundarios (si procede), las evaluaciones de estado incorrecto y las estadísticas de mantenimiento de los elementos secundarios (cuando corresponde).</span><span class="sxs-lookup"><span data-stu-id="dd81f-133">These queries return complete health information about the entity: the aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when the entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="dd81f-134">Se devuelve una entidad de mantenimiento cuando se rellena completamente en el Almacén de estado.</span><span class="sxs-lookup"><span data-stu-id="dd81f-134">A health entity is returned when it is fully populated in the health store.</span></span> <span data-ttu-id="dd81f-135">La entidad debe estar activa (no eliminada) y tener un informe de sistema.</span><span class="sxs-lookup"><span data-stu-id="dd81f-135">The entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="dd81f-136">Sus entidades primarias en la cadena de jerarquía deben tener también informes del sistema.</span><span class="sxs-lookup"><span data-stu-id="dd81f-136">Its parent entities on the hierarchy chain must also have system reports.</span></span> <span data-ttu-id="dd81f-137">Si no se cumple alguna de estas condiciones, las consultas de mantenimiento devuelven una excepción [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) con el código [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` que muestra por qué no se devuelve la entidad.</span><span class="sxs-lookup"><span data-stu-id="dd81f-137">If any of these conditions are not satisfied, the health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why the entity is not returned.</span></span>
>
>

<span data-ttu-id="dd81f-138">Las consultas de mantenimiento requieren pasar el identificador de entidad, que depende del tipo de entidad.</span><span class="sxs-lookup"><span data-stu-id="dd81f-138">The health queries must pass in the entity identifier, which depends on the entity type.</span></span> <span data-ttu-id="dd81f-139">Las consultas aceptan parámetros de directivas de mantenimiento opcionales.</span><span class="sxs-lookup"><span data-stu-id="dd81f-139">The queries accept optional health policy parameters.</span></span> <span data-ttu-id="dd81f-140">Si no se especifican directivas de mantenimiento, se usan para la evaluación las [directivas de mantenimiento](service-fabric-health-introduction.md#health-policies) del manifiesto de aplicación o de clúster.</span><span class="sxs-lookup"><span data-stu-id="dd81f-140">If no health policies are specified, the [health policies](service-fabric-health-introduction.md#health-policies) from the cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="dd81f-141">Si los manifiestos no contienen una definición de las directivas de mantenimiento, para la evaluación se usan las predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="dd81f-141">If the manifests don't contain a definition for health policies, the default health policies are used for evaluation.</span></span> <span data-ttu-id="dd81f-142">Las directivas de mantenimiento predeterminadas no toleran errores.</span><span class="sxs-lookup"><span data-stu-id="dd81f-142">The default health policies do not tolerate any failures.</span></span> <span data-ttu-id="dd81f-143">También aceptan filtros para devolver solo los elementos secundarios o eventos parciales, los que respetan los filtros especificados.</span><span class="sxs-lookup"><span data-stu-id="dd81f-143">The queries also accept filters for returning only partial children or events--the ones that respect the specified filters.</span></span> <span data-ttu-id="dd81f-144">Otro filtro permite excluir las estadísticas de los elementos secundarios.</span><span class="sxs-lookup"><span data-stu-id="dd81f-144">Another filter allows excluding the children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="dd81f-145">Los filtros de salida se aplican en el servidor, por lo que se reduce el tamaño de la respuesta del mensaje.</span><span class="sxs-lookup"><span data-stu-id="dd81f-145">The output filters are applied on the server side, so the message reply size is reduced.</span></span> <span data-ttu-id="dd81f-146">Recomendamos usar los filtros de salida para limitar los datos devueltos en lugar de aplicar filtros en el cliente.</span><span class="sxs-lookup"><span data-stu-id="dd81f-146">We recommended that you use the output filters to limit the data returned, rather than apply filters on the client side.</span></span>
>
>

<span data-ttu-id="dd81f-147">Contiene el mantenimiento de la entidad:</span><span class="sxs-lookup"><span data-stu-id="dd81f-147">An entity's health contains:</span></span>

* <span data-ttu-id="dd81f-148">El estado de mantenimiento agregado de la entidad.</span><span class="sxs-lookup"><span data-stu-id="dd81f-148">The aggregated health state of the entity.</span></span> <span data-ttu-id="dd81f-149">El Almacén de estado lo calcula en función de los informes de mantenimiento de la entidad, los estados de mantenimiento de los elementos secundarios (si procede) y las directivas de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="dd81f-149">Computed by the health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="dd81f-150">Lea más sobre la [evaluación del mantenimiento de entidades](service-fabric-health-introduction.md#health-evaluation).</span><span class="sxs-lookup"><span data-stu-id="dd81f-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="dd81f-151">Eventos de mantenimiento de la entidad.</span><span class="sxs-lookup"><span data-stu-id="dd81f-151">The health events on the entity.</span></span>
* <span data-ttu-id="dd81f-152">La colección de los estados de mantenimiento de todos los elementos secundarios de las entidades que pueden tener elementos secundarios.</span><span class="sxs-lookup"><span data-stu-id="dd81f-152">The collection of health states of all children for the entities that can have children.</span></span> <span data-ttu-id="dd81f-153">Los estados de mantenimiento contienen identificadores de entidad y el estado de mantenimiento agregado.</span><span class="sxs-lookup"><span data-stu-id="dd81f-153">The health states contain entity identifiers and the aggregated health state.</span></span> <span data-ttu-id="dd81f-154">Para obtener el mantenimiento completo de un elemento secundario, llame al mantenimiento de consultas del tipo de entidad secundaria y pase el identificador de elementos secundarios.</span><span class="sxs-lookup"><span data-stu-id="dd81f-154">To get complete health for a child, call the query health for the child entity type and pass in the child identifier.</span></span>
* <span data-ttu-id="dd81f-155">Si la entidad no es correcta, las evaluaciones de mantenimiento incorrecto apuntan al informe que desencadenó el estado de la entidad.</span><span class="sxs-lookup"><span data-stu-id="dd81f-155">The unhealthy evaluations that point to the report that triggered the state of the entity, if the entity is not healthy.</span></span> <span data-ttu-id="dd81f-156">Las evaluaciones son recursivas, contienen las evaluaciones de mantenimiento de los elementos secundarios que desencadenaron el estado de mantenimiento actual.</span><span class="sxs-lookup"><span data-stu-id="dd81f-156">The evaluations are recursive, containing the children health evaluations that triggered current health state.</span></span> <span data-ttu-id="dd81f-157">Por ejemplo, un guardián notificó un error en una réplica.</span><span class="sxs-lookup"><span data-stu-id="dd81f-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="dd81f-158">El estado de la aplicación muestra una evaluación de estado incorrecto debido a un servicio con un estado incorrecto; este estado del servicio se debe a que una partición tiene un error; el estado de la partición es incorrecto debido a que una réplica tiene otro error; el estado de la réplica es incorrecto debido al informe de estado de error del guardián.</span><span class="sxs-lookup"><span data-stu-id="dd81f-158">The application health shows an unhealthy evaluation due to an unhealthy service; the service is unhealthy due to a partition in error; the partition is unhealthy due to a replica in error; the replica is unhealthy due to the watchdog error health report.</span></span>
* <span data-ttu-id="dd81f-159">Las estadísticas de estado de todos los tipos de elementos secundarios de las entidades que los tienen.</span><span class="sxs-lookup"><span data-stu-id="dd81f-159">The health statistics for all children types of the entities that have children.</span></span> <span data-ttu-id="dd81f-160">Por ejemplo, el estado del clúster muestra el número total de aplicaciones, servicios, particiones, réplicas y entidades implementadas en el clúster.</span><span class="sxs-lookup"><span data-stu-id="dd81f-160">For example, cluster health shows the total number of applications, services, partitions, replicas, and deployed entities in the cluster.</span></span> <span data-ttu-id="dd81f-161">El estado del servicio muestra el número total de particiones y réplicas en el servicio especificado.</span><span class="sxs-lookup"><span data-stu-id="dd81f-161">Service health shows the total number of partitions and replicas under the specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="dd81f-162">Obtención del mantenimiento de clúster</span><span class="sxs-lookup"><span data-stu-id="dd81f-162">Get cluster health</span></span>
<span data-ttu-id="dd81f-163">Devuelve el mantenimiento de la entidad del clúster y contiene los estados de mantenimiento de aplicaciones y nodos (elementos secundarios del clúster).</span><span class="sxs-lookup"><span data-stu-id="dd81f-163">Returns the health of the cluster entity and contains the health states of applications and nodes (children of the cluster).</span></span> <span data-ttu-id="dd81f-164">Entrada:</span><span class="sxs-lookup"><span data-stu-id="dd81f-164">Input:</span></span>

* <span data-ttu-id="dd81f-165">[Opcional] La directiva de mantenimiento del clúster utilizada para evaluar los nodos y los eventos del clúster.</span><span class="sxs-lookup"><span data-stu-id="dd81f-165">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="dd81f-166">[Opcional] La asignación de directivas de mantenimiento de aplicaciones, con las directivas de mantenimiento usadas para invalidar las directivas de manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd81f-166">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="dd81f-167">[Opcional] Filtros para eventos, nodos y aplicaciones que especifican las entradas que son de interés y se deben devolver en el resultado (por ejemplo, únicamente los errores o advertencias y errores).</span><span class="sxs-lookup"><span data-stu-id="dd81f-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="dd81f-168">Todos los eventos, nodos y aplicaciones se utilizan para evaluar el mantenimiento agregado de la entidad, independientemente del filtro.</span><span class="sxs-lookup"><span data-stu-id="dd81f-168">All events, nodes, and applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="dd81f-169">[Opcional] Filtro para excluir las estadísticas de estado.</span><span class="sxs-lookup"><span data-stu-id="dd81f-169">[Optional] Filter to exclude health statistics.</span></span>
* <span data-ttu-id="dd81f-170">[Opcional] Filtro para incluir las estadísticas de estado fabric:/System.</span><span class="sxs-lookup"><span data-stu-id="dd81f-170">[Optional] Filter to include fabric:/System health statistics in the health statistics.</span></span> <span data-ttu-id="dd81f-171">Solo se pude aplicar cuando no se excluyen las estadísticas de estado.</span><span class="sxs-lookup"><span data-stu-id="dd81f-171">Only applicable when the health statistics are not excluded.</span></span> <span data-ttu-id="dd81f-172">De forma predeterminada, las estadísticas de estado incluyen solo las estadísticas de las aplicaciones de usuario y no la aplicación del sistema.</span><span class="sxs-lookup"><span data-stu-id="dd81f-172">By default, the health statistics include only statistics for user applications and not the System application.</span></span>

### <a name="api"></a><span data-ttu-id="dd81f-173">API</span><span class="sxs-lookup"><span data-stu-id="dd81f-173">API</span></span>
<span data-ttu-id="dd81f-174">Para obtener el mantenimiento del clúster, cree una instancia de `FabricClient` y llame al método [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) en su instancia de **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="dd81f-174">To get cluster health, create a `FabricClient` and call the [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="dd81f-175">La siguiente llamada obtiene el mantenimiento del clúster:</span><span class="sxs-lookup"><span data-stu-id="dd81f-175">The following call gets the cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="dd81f-176">El código siguiente obtiene el mantenimiento del clúster mediante una directiva de mantenimiento personalizada del clúster y filtros para nodos y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="dd81f-176">The following code gets the cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="dd81f-177">Especifica que las estadísticas de estado incluyen las de tipo fabric:/System.</span><span class="sxs-lookup"><span data-stu-id="dd81f-177">It specifies that the health statistics include the fabric:/System statistics.</span></span> <span data-ttu-id="dd81f-178">Crea la clase [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), que contiene toda la información de entrada.</span><span class="sxs-lookup"><span data-stu-id="dd81f-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains the input information.</span></span>

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="dd81f-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd81f-179">PowerShell</span></span>
<span data-ttu-id="dd81f-180">El cmdlet para obtener el mantenimiento del clúster es [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="dd81f-180">The cmdlet to get the cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="dd81f-181">Conéctese primero al clúster mediante el cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="dd81f-181">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="dd81f-182">El estado del clúster es igual a cinco nodos, la aplicación del sistema y fabric:/WordCount se configuran tal como se ha descrito.</span><span class="sxs-lookup"><span data-stu-id="dd81f-182">The state of the cluster is five nodes, the system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="dd81f-183">El siguiente cmdlet obtiene el mantenimiento del clúster con directivas de mantenimiento predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="dd81f-183">The following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="dd81f-184">El estado de mantenimiento agregado está en advertencia, porque también lo está la aplicación fabric:/WordCount.</span><span class="sxs-lookup"><span data-stu-id="dd81f-184">The aggregated health state is warning, because the fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="dd81f-185">Observe cómo las evaluaciones de mantenimiento incorrecto muestran detalles de las condiciones que desencadenaron el mantenimiento agregado.</span><span class="sxs-lookup"><span data-stu-id="dd81f-185">Note how the unhealthy evaluations provide details on the conditions that triggered the aggregated health.</span></span>

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

<span data-ttu-id="dd81f-186">El siguiente cmdlet de PowerShell obtiene el mantenimiento del clúster mediante una directiva de aplicación personalizada.</span><span class="sxs-lookup"><span data-stu-id="dd81f-186">The following PowerShell cmdlet gets the health of the cluster by using a custom application policy.</span></span> <span data-ttu-id="dd81f-187">Filtra los resultados para obtener solo los nodos y las aplicaciones con error o advertencia.</span><span class="sxs-lookup"><span data-stu-id="dd81f-187">It filters results to get only applications and nodes in error or warning.</span></span> <span data-ttu-id="dd81f-188">Como resultado, no se devuelve ningún nodo, ya que todos son correctos.</span><span class="sxs-lookup"><span data-stu-id="dd81f-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="dd81f-189">Solo la aplicación fabric:/WordCount respeta el filtro de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="dd81f-189">Only the fabric:/WordCount application respects the applications filter.</span></span> <span data-ttu-id="dd81f-190">Puesto que la directiva personalizada especifica que hay que considerar que las advertencias son errores en la aplicación fabric:/WordCount, la aplicación se evalúa como en error y lo mismo el clúster.</span><span class="sxs-lookup"><span data-stu-id="dd81f-190">Because the custom policy specifies to consider warnings as errors for the fabric:/WordCount application, the application is evaluated as in error, and so is the cluster.</span></span>

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a><span data-ttu-id="dd81f-191">REST</span><span class="sxs-lookup"><span data-stu-id="dd81f-191">REST</span></span>
<span data-ttu-id="dd81f-192">Puede obtener el mantenimiento del clúster con una [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) o una [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) que incluye las directivas de mantenimiento descritas en el cuerpo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="dd81f-193">Obtención del mantenimiento de nodo</span><span class="sxs-lookup"><span data-stu-id="dd81f-193">Get node health</span></span>
<span data-ttu-id="dd81f-194">Devuelve el mantenimiento de una entidad del nodo y contiene los eventos de mantenimiento notificados en el nodo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-194">Returns the health of a node entity and contains the health events reported on the node.</span></span> <span data-ttu-id="dd81f-195">Entrada:</span><span class="sxs-lookup"><span data-stu-id="dd81f-195">Input:</span></span>

* <span data-ttu-id="dd81f-196">[Obligatorio] El nombre de nodo que identifica al nodo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-196">[Required] The node name that identifies the node.</span></span>
* <span data-ttu-id="dd81f-197">[Opcional] La configuración de la directiva de mantenimiento del clúster usada para evaluar el mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="dd81f-197">[Optional] The cluster health policy settings used to evaluate health.</span></span>
* <span data-ttu-id="dd81f-198">[Opcional] Filtros para eventos que especifican las entradas que son de interés y se deben devolver en el resultado (por ejemplo, únicamente errores o advertencias y errores).</span><span class="sxs-lookup"><span data-stu-id="dd81f-198">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="dd81f-199">Todos los eventos se utilizan para evaluar el mantenimiento agregado de la entidad, independientemente del filtro.</span><span class="sxs-lookup"><span data-stu-id="dd81f-199">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="dd81f-200">API</span><span class="sxs-lookup"><span data-stu-id="dd81f-200">API</span></span>
<span data-ttu-id="dd81f-201">Para obtener el mantenimiento del nodo mediante la API, cree una instancia de `FabricClient` y llame al método [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) en su instancia de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="dd81f-201">To get node health through the API, create a `FabricClient` and call the [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="dd81f-202">El código siguiente obtiene el mantenimiento del nodo para el nombre de nodo especificado:</span><span class="sxs-lookup"><span data-stu-id="dd81f-202">The following code gets the node health for the specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="dd81f-203">El código siguiente obtiene el mantenimiento del nodo para el nombre de nodo especificado, y pasa un filtro de eventos y la directiva personalizada mediante [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="dd81f-203">The following code gets the node health for the specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="dd81f-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd81f-204">PowerShell</span></span>
<span data-ttu-id="dd81f-205">El cmdlet para obtener el mantenimiento del nodo es [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span><span class="sxs-lookup"><span data-stu-id="dd81f-205">The cmdlet to get the node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="dd81f-206">Conéctese primero al clúster mediante el cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="dd81f-206">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="dd81f-207">El siguiente cmdlet obtiene el mantenimiento del nodo mediante directivas de mantenimiento predeterminadas:</span><span class="sxs-lookup"><span data-stu-id="dd81f-207">The following cmdlet gets the node health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="dd81f-208">El siguiente cmdlet obtiene el mantenimiento de todos los nodos del clúster:</span><span class="sxs-lookup"><span data-stu-id="dd81f-208">The following cmdlet gets the health of all nodes in the cluster:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a><span data-ttu-id="dd81f-209">REST</span><span class="sxs-lookup"><span data-stu-id="dd81f-209">REST</span></span>
<span data-ttu-id="dd81f-210">Puede obtener el mantenimiento del nodo con una [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) o una [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) que incluye las directivas de mantenimiento descritas en el cuerpo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="dd81f-211">Obtención del mantenimiento de la aplicación</span><span class="sxs-lookup"><span data-stu-id="dd81f-211">Get application health</span></span>
<span data-ttu-id="dd81f-212">Devuelve el mantenimiento de una entidad de aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd81f-212">Returns the health of an application entity.</span></span> <span data-ttu-id="dd81f-213">Contiene los estados de mantenimiento de la aplicación implementada y de los elementos secundarios del servicio.</span><span class="sxs-lookup"><span data-stu-id="dd81f-213">It contains the health states of the deployed application and service children.</span></span> <span data-ttu-id="dd81f-214">Entrada:</span><span class="sxs-lookup"><span data-stu-id="dd81f-214">Input:</span></span>

* <span data-ttu-id="dd81f-215">[Obligatorio] El nombre de la aplicación (URI) que identifica la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd81f-215">[Required] The application name (URI) that identifies the application.</span></span>
* <span data-ttu-id="dd81f-216">[Opcional] La directiva de mantenimiento de aplicación usada para invalidar las directivas de manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd81f-216">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="dd81f-217">[Opcional] Filtros para eventos, servicios y aplicaciones implementadas que especifican las entradas que son de interés y se deben devolver en el resultado (por ejemplo, únicamente errores o advertencias y errores).</span><span class="sxs-lookup"><span data-stu-id="dd81f-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="dd81f-218">Todos los eventos, servicios y aplicaciones implementadas se utilizan para evaluar el mantenimiento agregado de la entidad, independientemente del filtro.</span><span class="sxs-lookup"><span data-stu-id="dd81f-218">All events, services, and deployed applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="dd81f-219">[Opcional] Filtro para excluir las estadísticas de estado.</span><span class="sxs-lookup"><span data-stu-id="dd81f-219">[Optional] Filter to exclude the health statistics.</span></span> <span data-ttu-id="dd81f-220">Si no se especifica, las estadísticas de estado incluyen los estados correcto, de advertencia y recuento de errores para todos los elementos secundarios de la aplicación: servicios, particiones, réplicas, aplicaciones implementadas y paquetes de servicio implementados.</span><span class="sxs-lookup"><span data-stu-id="dd81f-220">If not specified, the health statistics include the ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="dd81f-221">API</span><span class="sxs-lookup"><span data-stu-id="dd81f-221">API</span></span>
<span data-ttu-id="dd81f-222">Para obtener el mantenimiento de la aplicación, cree una instancia de `FabricClient` y llame al método [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) en su instancia de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="dd81f-222">To get application health, create a `FabricClient` and call the [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="dd81f-223">El código siguiente obtiene el mantenimiento de la aplicación para el nombre de aplicación especificado (URI):</span><span class="sxs-lookup"><span data-stu-id="dd81f-223">The following code gets the application health for the specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="dd81f-224">El código siguiente obtiene el mantenimiento de la aplicación para el nombre de aplicación especificado (URI), con filtros y directivas personalizadas especificados mediante [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="dd81f-224">The following code gets the application health for the specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="dd81f-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd81f-225">PowerShell</span></span>
<span data-ttu-id="dd81f-226">El cmdlet para obtener el mantenimiento de la aplicación es [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="dd81f-226">The cmdlet to get the application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="dd81f-227">Conéctese primero al clúster mediante el cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="dd81f-227">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="dd81f-228">El siguiente cmdlet devuelve el mantenimiento de la aplicación **fabric:/WordCount** :</span><span class="sxs-lookup"><span data-stu-id="dd81f-228">The following cmdlet returns the health of the **fabric:/WordCount** application:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

<span data-ttu-id="dd81f-229">El siguiente cmdlet de PowerShell pasa directivas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="dd81f-229">The following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="dd81f-230">También filtra los elementos secundarios y los eventos.</span><span class="sxs-lookup"><span data-stu-id="dd81f-230">It also filters children and events.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a><span data-ttu-id="dd81f-231">REST</span><span class="sxs-lookup"><span data-stu-id="dd81f-231">REST</span></span>
<span data-ttu-id="dd81f-232">Puede obtener el mantenimiento de la aplicación con una [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) o una [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) que incluye las directivas de mantenimiento descritas en el cuerpo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="dd81f-233">Obtención del mantenimiento del servicio</span><span class="sxs-lookup"><span data-stu-id="dd81f-233">Get service health</span></span>
<span data-ttu-id="dd81f-234">Devuelve el mantenimiento de una entidad del servicio.</span><span class="sxs-lookup"><span data-stu-id="dd81f-234">Returns the health of a service entity.</span></span> <span data-ttu-id="dd81f-235">Contiene los estados de mantenimiento de la partición.</span><span class="sxs-lookup"><span data-stu-id="dd81f-235">It contains the partition health states.</span></span> <span data-ttu-id="dd81f-236">Entrada:</span><span class="sxs-lookup"><span data-stu-id="dd81f-236">Input:</span></span>

* <span data-ttu-id="dd81f-237">[Obligatorio] El nombre del servicio (URI) que identifica el servicio.</span><span class="sxs-lookup"><span data-stu-id="dd81f-237">[Required] The service name (URI) that identifies the service.</span></span>
* <span data-ttu-id="dd81f-238">[Opcional] La directiva de mantenimiento de aplicación usada para invalidar la directiva de manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd81f-238">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="dd81f-239">[Opcional] Filtros para eventos y particiones que especifican las entradas que son de interés y se deben devolver en el resultado (por ejemplo, únicamente errores o advertencias y errores).</span><span class="sxs-lookup"><span data-stu-id="dd81f-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="dd81f-240">Todos los eventos y particiones se utilizan para evaluar el mantenimiento agregado de la entidad, independientemente del filtro.</span><span class="sxs-lookup"><span data-stu-id="dd81f-240">All events and partitions are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="dd81f-241">[Opcional] Filtro para excluir las estadísticas de estado.</span><span class="sxs-lookup"><span data-stu-id="dd81f-241">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="dd81f-242">Si no se especifica, las estadísticas de estado muestran el estado correcto, de advertencia y recuento de errores para todas las particiones y réplicas del servicio.</span><span class="sxs-lookup"><span data-stu-id="dd81f-242">If not specified, the health statistics show the ok, warning, and error count for all partitions and replicas of the service.</span></span>

### <a name="api"></a><span data-ttu-id="dd81f-243">API</span><span class="sxs-lookup"><span data-stu-id="dd81f-243">API</span></span>
<span data-ttu-id="dd81f-244">Para obtener el mantenimiento del servicio mediante la API, cree una instancia de `FabricClient` y llame al método [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) en su instancia de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="dd81f-244">To get service health through the API, create a `FabricClient` and call the [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="dd81f-245">En el ejemplo siguiente se obtiene el mantenimiento de un servicio con el nombre de servicio especificado (URI):</span><span class="sxs-lookup"><span data-stu-id="dd81f-245">The following example gets the health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="dd81f-246">El código siguiente obtiene el mantenimiento del servicio para el nombre de servicio especificado (URI), mediante la especificación de filtros y directivas personalizadas con la clase [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="dd81f-246">The following code gets the service health for the specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="dd81f-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd81f-247">PowerShell</span></span>
<span data-ttu-id="dd81f-248">El cmdlet para obtener el mantenimiento del servicio es [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span><span class="sxs-lookup"><span data-stu-id="dd81f-248">The cmdlet to get the service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="dd81f-249">Conéctese primero al clúster mediante el cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="dd81f-249">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="dd81f-250">El siguiente cmdlet obtiene el mantenimiento del servicio con directivas de mantenimiento predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="dd81f-250">The following cmdlet gets the service health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="dd81f-251">REST</span><span class="sxs-lookup"><span data-stu-id="dd81f-251">REST</span></span>
<span data-ttu-id="dd81f-252">Puede obtener el mantenimiento del servicio con una [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) o una [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) que incluye las directivas de mantenimiento descritas en el cuerpo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="dd81f-253">Obtención del mantenimiento de partición</span><span class="sxs-lookup"><span data-stu-id="dd81f-253">Get partition health</span></span>
<span data-ttu-id="dd81f-254">Devuelve el mantenimiento de una entidad de partición.</span><span class="sxs-lookup"><span data-stu-id="dd81f-254">Returns the health of a partition entity.</span></span> <span data-ttu-id="dd81f-255">Contiene los estados de mantenimiento de la réplica.</span><span class="sxs-lookup"><span data-stu-id="dd81f-255">It contains the replica health states.</span></span> <span data-ttu-id="dd81f-256">Entrada:</span><span class="sxs-lookup"><span data-stu-id="dd81f-256">Input:</span></span>

* <span data-ttu-id="dd81f-257">[Obligatorio] El identificador de partición (GUID) que identifica la partición.</span><span class="sxs-lookup"><span data-stu-id="dd81f-257">[Required] The partition ID (GUID) that identifies the partition.</span></span>
* <span data-ttu-id="dd81f-258">[Opcional] La directiva de mantenimiento de aplicación usada para invalidar la directiva de manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd81f-258">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="dd81f-259">[Opcional] Filtros de eventos y réplicas que especifican las entradas que son de interés y se deben devolver en el resultado (por ejemplo, únicamente errores o advertencias y errores).</span><span class="sxs-lookup"><span data-stu-id="dd81f-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="dd81f-260">Todos los eventos y réplicas se utilizan para evaluar el mantenimiento agregado de la entidad, independientemente del filtro.</span><span class="sxs-lookup"><span data-stu-id="dd81f-260">All events and replicas are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="dd81f-261">[Opcional] Filtro para excluir las estadísticas de estado.</span><span class="sxs-lookup"><span data-stu-id="dd81f-261">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="dd81f-262">Si no se especifica, las estadísticas de estado muestran cuántas réplicas están en estado correcto, de advertencia y de error.</span><span class="sxs-lookup"><span data-stu-id="dd81f-262">If not specified, the health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="dd81f-263">API</span><span class="sxs-lookup"><span data-stu-id="dd81f-263">API</span></span>
<span data-ttu-id="dd81f-264">Para obtener el mantenimiento de la partición mediante la API, cree una instancia de `FabricClient` y llame al método [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) en su instancia de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="dd81f-264">To get partition health through the API, create a `FabricClient` and call the [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="dd81f-265">Para especificar parámetros opcionales, cree [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="dd81f-265">To specify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="dd81f-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd81f-266">PowerShell</span></span>
<span data-ttu-id="dd81f-267">El cmdlet para obtener el mantenimiento de la partición es [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span><span class="sxs-lookup"><span data-stu-id="dd81f-267">The cmdlet to get the partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="dd81f-268">Conéctese primero al clúster mediante el cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="dd81f-268">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="dd81f-269">El siguiente cmdlet obtiene el estado de todas las particiones del servicio **fabric:/WordCount/WordCountService** y filtra los estados de mantenimiento de las réplicas:</span><span class="sxs-lookup"><span data-stu-id="dd81f-269">The following cmdlet gets the health for all partitions of the **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
                        TTL                   : 00:01:05
                        Description           : The Load Balancer was unable to find a placement for one or more of the Service's Replicas:
                        Secondary replica could not be placed due to the following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="dd81f-270">REST</span><span class="sxs-lookup"><span data-stu-id="dd81f-270">REST</span></span>
<span data-ttu-id="dd81f-271">Puede obtener el mantenimiento de la partición con una [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) o una [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) que incluye las directivas de mantenimiento descritas en el cuerpo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="dd81f-272">Obtención del mantenimiento de réplica</span><span class="sxs-lookup"><span data-stu-id="dd81f-272">Get replica health</span></span>
<span data-ttu-id="dd81f-273">Devuelve el mantenimiento de una réplica de servicio con estado o una instancia de servicio sin estado.</span><span class="sxs-lookup"><span data-stu-id="dd81f-273">Returns the health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="dd81f-274">Entrada:</span><span class="sxs-lookup"><span data-stu-id="dd81f-274">Input:</span></span>

* <span data-ttu-id="dd81f-275">[Obligatorio] El identificador de partición (GUID) y el identificador de réplica que identifica a la réplica.</span><span class="sxs-lookup"><span data-stu-id="dd81f-275">[Required] The partition ID (GUID) and replica ID that identifies the replica.</span></span>
* <span data-ttu-id="dd81f-276">[Opcional] Los parámetros de la directiva de mantenimiento de aplicación usados para invalidar las directivas de manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd81f-276">[Optional] The application health policy parameters used to override the application manifest policies.</span></span>
* <span data-ttu-id="dd81f-277">[Opcional] Filtros para eventos que especifican las entradas que son de interés y se deben devolver en el resultado (por ejemplo, únicamente errores o advertencias y errores).</span><span class="sxs-lookup"><span data-stu-id="dd81f-277">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="dd81f-278">Todos los eventos se utilizan para evaluar el mantenimiento agregado de la entidad, independientemente del filtro.</span><span class="sxs-lookup"><span data-stu-id="dd81f-278">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="dd81f-279">API</span><span class="sxs-lookup"><span data-stu-id="dd81f-279">API</span></span>
<span data-ttu-id="dd81f-280">Para obtener el mantenimiento de la réplica mediante la API, cree una instancia de `FabricClient` y llame al método [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) en su instancia de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="dd81f-280">To get the replica health through the API, create a `FabricClient` and call the [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="dd81f-281">Para especificar parámetros avanzados, utilice [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="dd81f-281">To specify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="dd81f-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd81f-282">PowerShell</span></span>
<span data-ttu-id="dd81f-283">El cmdlet para obtener el mantenimiento de la réplica es [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span><span class="sxs-lookup"><span data-stu-id="dd81f-283">The cmdlet to get the replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="dd81f-284">Conéctese primero al clúster mediante el cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="dd81f-284">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="dd81f-285">El cmdlet siguiente obtiene el mantenimiento de la réplica principal para todas las particiones del servicio:</span><span class="sxs-lookup"><span data-stu-id="dd81f-285">The following cmdlet gets the health of the primary replica for all partitions of the service:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="dd81f-286">REST</span><span class="sxs-lookup"><span data-stu-id="dd81f-286">REST</span></span>
<span data-ttu-id="dd81f-287">Puede obtener el mantenimiento de la réplica con una [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) o una[solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) que incluye las directivas de mantenimiento descritas en el cuerpo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="dd81f-288">Obtención del mantenimiento de la aplicación implementada</span><span class="sxs-lookup"><span data-stu-id="dd81f-288">Get deployed application health</span></span>
<span data-ttu-id="dd81f-289">Devuelve el mantenimiento de una aplicación implementada en una actividad del nodo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-289">Returns the health of an application deployed on a node entity.</span></span> <span data-ttu-id="dd81f-290">Contiene los estados de mantenimiento del paquete de servicio implementado.</span><span class="sxs-lookup"><span data-stu-id="dd81f-290">It contains the deployed service package health states.</span></span> <span data-ttu-id="dd81f-291">Entrada:</span><span class="sxs-lookup"><span data-stu-id="dd81f-291">Input:</span></span>

* <span data-ttu-id="dd81f-292">[Obligatorio] El nombre de la aplicación (URI) y el nombre del nodo (cadena) que identifican a la aplicación implementada</span><span class="sxs-lookup"><span data-stu-id="dd81f-292">[Required] The application name (URI) and node name (string) that identify the deployed application.</span></span>
* <span data-ttu-id="dd81f-293">[Opcional] La directiva de mantenimiento de aplicación usada para invalidar las directivas de manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd81f-293">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="dd81f-294">[Opcional] Filtros de eventos y paquetes de servicio implementados que especifican las entradas que son de interés y se deben devolver en el resultado (por ejemplo, únicamente errores o advertencias y errores).</span><span class="sxs-lookup"><span data-stu-id="dd81f-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="dd81f-295">Todos los eventos y paquetes de servicio implementados se utilizan para evaluar el mantenimiento agregado de la entidad, independientemente del filtro.</span><span class="sxs-lookup"><span data-stu-id="dd81f-295">All events and deployed service packages are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="dd81f-296">[Opcional] Filtro para excluir las estadísticas de estado.</span><span class="sxs-lookup"><span data-stu-id="dd81f-296">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="dd81f-297">Si no se especifica, las estadísticas de estado muestran el número de paquetes de servicio implementados en los estados de mantenimiento correcto, de advertencia y de error.</span><span class="sxs-lookup"><span data-stu-id="dd81f-297">If not specified, the health statistics show the number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="dd81f-298">API</span><span class="sxs-lookup"><span data-stu-id="dd81f-298">API</span></span>
<span data-ttu-id="dd81f-299">Para obtener el mantenimiento de una aplicación implementada en un nodo mediante la API, cree una instancia de `FabricClient` y llame al método [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) en su instancia de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="dd81f-299">To get the health of an application deployed on a node through the API, create a `FabricClient` and call the [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="dd81f-300">Para especificar parámetros opcionales, utilice [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="dd81f-300">To specify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="dd81f-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd81f-301">PowerShell</span></span>
<span data-ttu-id="dd81f-302">El cmdlet para obtener el mantenimiento de la aplicación implementada es [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="dd81f-302">The cmdlet to get the deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="dd81f-303">Conéctese primero al clúster mediante el cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="dd81f-303">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="dd81f-304">Para averiguar dónde está implementada una aplicación, ejecute [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) y observe los elementos secundarios de la aplicación implementada.</span><span class="sxs-lookup"><span data-stu-id="dd81f-304">To find out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed application children.</span></span>

<span data-ttu-id="dd81f-305">El siguiente cmdlet obtiene el mantenimiento de la aplicación **fabric:/WordCount** implementada en **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="dd81f-305">The following cmdlet gets the health of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="dd81f-306">REST</span><span class="sxs-lookup"><span data-stu-id="dd81f-306">REST</span></span>
<span data-ttu-id="dd81f-307">Puede obtener el mantenimiento de la aplicación implementada con una [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) o una [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) que incluye las directivas de mantenimiento descritas en el cuerpo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="dd81f-308">Obtención del mantenimiento del paquete de servicio implementado</span><span class="sxs-lookup"><span data-stu-id="dd81f-308">Get deployed service package health</span></span>
<span data-ttu-id="dd81f-309">Devuelve el mantenimiento de una entidad de paquete de servicio implementado.</span><span class="sxs-lookup"><span data-stu-id="dd81f-309">Returns the health of a deployed service package entity.</span></span> <span data-ttu-id="dd81f-310">Entrada:</span><span class="sxs-lookup"><span data-stu-id="dd81f-310">Input:</span></span>

* <span data-ttu-id="dd81f-311">[Obligatorio] El nombre de la aplicación (URI), el nombre del nodo (cadena) y el nombre del manifiesto de servicio (cadena) que identifican al paquete de servicio implementado.</span><span class="sxs-lookup"><span data-stu-id="dd81f-311">[Required] The application name (URI), node name (string), and service manifest name (string) that identify the deployed service package.</span></span>
* <span data-ttu-id="dd81f-312">[Opcional] La directiva de mantenimiento de aplicación usada para invalidar la directiva de manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd81f-312">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="dd81f-313">[Opcional] Filtros para eventos que especifican las entradas que son de interés y se deben devolver en el resultado (por ejemplo, únicamente errores o advertencias y errores).</span><span class="sxs-lookup"><span data-stu-id="dd81f-313">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="dd81f-314">Todos los eventos se utilizan para evaluar el mantenimiento agregado de la entidad, independientemente del filtro.</span><span class="sxs-lookup"><span data-stu-id="dd81f-314">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="dd81f-315">API</span><span class="sxs-lookup"><span data-stu-id="dd81f-315">API</span></span>
<span data-ttu-id="dd81f-316">Para obtener el mantenimiento de un paquete de servicio implementado mediante la API, cree una instancia de `FabricClient` y llame al método [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) en su instancia de HealthManager.</span><span class="sxs-lookup"><span data-stu-id="dd81f-316">To get the health of a deployed service package through the API, create a `FabricClient` and call the [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="dd81f-317">Para especificar parámetros opcionales, utilice [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="dd81f-317">To specify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="dd81f-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd81f-318">PowerShell</span></span>
<span data-ttu-id="dd81f-319">El cmdlet para obtener el mantenimiento del paquete de servicio implementado es [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span><span class="sxs-lookup"><span data-stu-id="dd81f-319">The cmdlet to get the deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="dd81f-320">Conéctese primero al clúster mediante el cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="dd81f-320">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="dd81f-321">Para averiguar dónde está implementada una aplicación, ejecute [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) y examine las aplicaciones implementadas.</span><span class="sxs-lookup"><span data-stu-id="dd81f-321">To see where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed applications.</span></span> <span data-ttu-id="dd81f-322">Para ver qué paquetes de servicio están en una aplicación, examine los elementos secundarios del paquete de servicio implementado en la salida de [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="dd81f-322">To see which service packages are in an application, look at the deployed service package children in the [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="dd81f-323">El siguiente cmdlet obtiene el mantenimiento del paquete de servicio **WordCountServicePkg** de la aplicación **fabric:/WordCount** implementada en **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="dd81f-323">The following cmdlet gets the health of the **WordCountServicePkg** service package of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="dd81f-324">La entidad tiene informes **System.Hosting** para la activación correcta del paquete de servicio y del punto de entrada, y para el registro correcto del tipo de servicio.</span><span class="sxs-lookup"><span data-stu-id="dd81f-324">The entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="dd81f-325">REST</span><span class="sxs-lookup"><span data-stu-id="dd81f-325">REST</span></span>
<span data-ttu-id="dd81f-326">Puede obtener el mantenimiento del paquete de servicio implementado con una [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) o una [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) que incluye las directivas de mantenimiento descritas en el cuerpo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="dd81f-327">Consultas de fragmentos de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="dd81f-327">Health chunk queries</span></span>
<span data-ttu-id="dd81f-328">Las consultas de fragmentos de mantenimiento pueden devolver elementos secundarios de clúster de varios niveles (recursivamente), según los filtros de entrada.</span><span class="sxs-lookup"><span data-stu-id="dd81f-328">The health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="dd81f-329">Admite filtros avanzados que permiten una gran flexibilidad al elegir los elementos secundarios que se devuelven.</span><span class="sxs-lookup"><span data-stu-id="dd81f-329">It supports advanced filters that allow a lot of flexibility in choosing the children to be returned.</span></span> <span data-ttu-id="dd81f-330">Los filtros pueden especificar elementos secundarios por el identificador único o por otros identificadores de grupo o estados de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="dd81f-330">The filters can specify children by the unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="dd81f-331">De forma predeterminada, no se incluye ningún elemento secundario, a diferencia de los comandos de mantenimiento que siempre incluyen elementos secundarios de primer nivel.</span><span class="sxs-lookup"><span data-stu-id="dd81f-331">By default, no children are included, as opposed to health commands that always include first-level children.</span></span>

<span data-ttu-id="dd81f-332">Las [consultas de mantenimiento](service-fabric-view-entities-aggregated-health.md#health-queries) solo devuelven elementos secundarios de primer nivel de la entidad especificada, según los filtros necesarios.</span><span class="sxs-lookup"><span data-stu-id="dd81f-332">The [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of the specified entity per required filters.</span></span> <span data-ttu-id="dd81f-333">Para obtener los elementos secundarios de los elementos secundarios, debe llamar a las API de mantenimiento adicionales para cada entidad que sea de interés.</span><span class="sxs-lookup"><span data-stu-id="dd81f-333">To get the children of the children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="dd81f-334">De igual forma, para obtener el mantenimiento de entidades específicas, debe llamar a una API de mantenimiento para cada entidad deseada.</span><span class="sxs-lookup"><span data-stu-id="dd81f-334">Similarly, to get the health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="dd81f-335">El filtrado avanzado de consultas de fragmentos le permite solicitar varios elementos de interés en una consulta, lo que reduce el tamaño del mensaje y el número de mensajes.</span><span class="sxs-lookup"><span data-stu-id="dd81f-335">The chunk query advanced filtering allows you to request multiple items of interest in one query, minimizing the message size and the number of messages.</span></span>

<span data-ttu-id="dd81f-336">El valor de la consulta de fragmentos es que puede obtener el estado de mantenimiento para más entidades del clúster (posiblemente todas las entidades del clúster que comienzan en la raíz requerida) en una llamada.</span><span class="sxs-lookup"><span data-stu-id="dd81f-336">The value of the chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="dd81f-337">Puede expresar consultas de mantenimiento complejas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dd81f-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="dd81f-338">Devolver solo las aplicaciones con error y, para esas aplicaciones, incluir todos los servicios con advertencias o errores.</span><span class="sxs-lookup"><span data-stu-id="dd81f-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="dd81f-339">Para los servicios devueltos, incluir todas las particiones.</span><span class="sxs-lookup"><span data-stu-id="dd81f-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="dd81f-340">Devolver solo el mantenimiento de cuatro aplicaciones, especificadas por sus nombres.</span><span class="sxs-lookup"><span data-stu-id="dd81f-340">Return only the health of four applications, specified by their names.</span></span>
* <span data-ttu-id="dd81f-341">Devolver solo el mantenimiento de aplicaciones de un tipo de aplicación deseado.</span><span class="sxs-lookup"><span data-stu-id="dd81f-341">Return only the health of applications of a desired application type.</span></span>
* <span data-ttu-id="dd81f-342">Devolver todas las entidades implementadas en un nodo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="dd81f-343">Devuelve todas las aplicaciones, todas las aplicaciones implementadas en el nodo especificado y todos los paquetes de servicio implementados en ese nodo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-343">Returns all applications, all deployed applications on the specified node and all the deployed service packages on that node.</span></span>
* <span data-ttu-id="dd81f-344">Devolver todas las réplicas con error.</span><span class="sxs-lookup"><span data-stu-id="dd81f-344">Return all replicas in error.</span></span> <span data-ttu-id="dd81f-345">Devuelve todas las aplicaciones, los servicios, las particiones y solo las réplicas con error.</span><span class="sxs-lookup"><span data-stu-id="dd81f-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="dd81f-346">Devolver todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="dd81f-346">Return all applications.</span></span> <span data-ttu-id="dd81f-347">Para un servicio especificado, incluir todas las particiones.</span><span class="sxs-lookup"><span data-stu-id="dd81f-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="dd81f-348">Actualmente, la consulta de fragmentos de mantenimiento se expone solo para la entidad del clúster.</span><span class="sxs-lookup"><span data-stu-id="dd81f-348">Currently, the health chunk query is exposed only for the cluster entity.</span></span> <span data-ttu-id="dd81f-349">Devuelve un fragmento de estado del clúster, que contiene:</span><span class="sxs-lookup"><span data-stu-id="dd81f-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="dd81f-350">El estado de mantenimiento agregado del clúster.</span><span class="sxs-lookup"><span data-stu-id="dd81f-350">The cluster aggregated health state.</span></span>
* <span data-ttu-id="dd81f-351">La lista de fragmentos de estado de mantenimiento de nodos que respetan los filtros de entrada.</span><span class="sxs-lookup"><span data-stu-id="dd81f-351">The health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="dd81f-352">La lista de fragmentos de estado de mantenimiento de aplicaciones que respetan los filtros de entrada.</span><span class="sxs-lookup"><span data-stu-id="dd81f-352">The health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="dd81f-353">Cada fragmento de estado de mantenimiento de aplicación contiene una lista de fragmentos con todos los servicios que respetan los filtros de entrada y una lista de fragmentos con todas las aplicaciones implementadas que respetan los filtros.</span><span class="sxs-lookup"><span data-stu-id="dd81f-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect the filters.</span></span> <span data-ttu-id="dd81f-354">Igual para los elementos secundarios de servicios y aplicaciones implementadas.</span><span class="sxs-lookup"><span data-stu-id="dd81f-354">Same for the children of services and deployed applications.</span></span> <span data-ttu-id="dd81f-355">De este modo, todas las entidades del clúster pueden devolverse potencialmente si se solicitan, de una manera jerárquica.</span><span class="sxs-lookup"><span data-stu-id="dd81f-355">This way, all entities in the cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="dd81f-356">Consulta de fragmentos de mantenimiento del clúster</span><span class="sxs-lookup"><span data-stu-id="dd81f-356">Cluster health chunk query</span></span>
<span data-ttu-id="dd81f-357">Devuelve el mantenimiento de la entidad del clúster y contiene los fragmentos del estado de mantenimiento jerárquico de los elementos secundarios necesarios.</span><span class="sxs-lookup"><span data-stu-id="dd81f-357">Returns the health of the cluster entity and contains the hierarchical health state chunks of required children.</span></span> <span data-ttu-id="dd81f-358">Entrada:</span><span class="sxs-lookup"><span data-stu-id="dd81f-358">Input:</span></span>

* <span data-ttu-id="dd81f-359">[Opcional] La directiva de mantenimiento del clúster utilizada para evaluar los nodos y los eventos del clúster.</span><span class="sxs-lookup"><span data-stu-id="dd81f-359">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="dd81f-360">[Opcional] La asignación de directivas de mantenimiento de aplicaciones, con las directivas de mantenimiento usadas para invalidar las directivas de manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd81f-360">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="dd81f-361">[Opcional] Filtros para nodos y aplicaciones que especifican las entradas que son de interés y se deben devolver en el resultado.</span><span class="sxs-lookup"><span data-stu-id="dd81f-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in the result.</span></span> <span data-ttu-id="dd81f-362">Los filtros son específicos de una entidad o grupo de entidades o son aplicables a todas las entidades de ese nivel.</span><span class="sxs-lookup"><span data-stu-id="dd81f-362">The filters are specific to an entity/group of entities or are applicable to all entities at that level.</span></span> <span data-ttu-id="dd81f-363">La lista de filtros puede contener un filtro general o filtros para identificadores específicos a fin de precisar más las entidades devueltas por la consulta.</span><span class="sxs-lookup"><span data-stu-id="dd81f-363">The list of filters can contain one general filter and/or filters for specific identifiers to fine-grain entities returned by the query.</span></span> <span data-ttu-id="dd81f-364">Si está vacía, no se devuelven los elementos secundarios de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="dd81f-364">If empty, the children are not returned by default.</span></span>
  <span data-ttu-id="dd81f-365">Más información sobre los filtros en [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) y [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span><span class="sxs-lookup"><span data-stu-id="dd81f-365">Read more about the filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="dd81f-366">Los filtros de aplicación pueden especificar de forma recursiva filtros avanzados para elementos secundarios.</span><span class="sxs-lookup"><span data-stu-id="dd81f-366">The application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="dd81f-367">El resultado del fragmento incluye los elementos secundarios que respetan los filtros.</span><span class="sxs-lookup"><span data-stu-id="dd81f-367">The chunk result includes the children that respect the filters.</span></span>

<span data-ttu-id="dd81f-368">Actualmente, la consulta de fragmentos no devuelve evaluaciones de mantenimiento incorrecto o eventos de entidad.</span><span class="sxs-lookup"><span data-stu-id="dd81f-368">Currently, the chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="dd81f-369">Esta información adicional puede obtenerse mediante la consulta de mantenimiento del clúster existente.</span><span class="sxs-lookup"><span data-stu-id="dd81f-369">That extra information can be obtained using the existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="dd81f-370">API</span><span class="sxs-lookup"><span data-stu-id="dd81f-370">API</span></span>
<span data-ttu-id="dd81f-371">Para obtener fragmentos de mantenimiento del clúster, cree una instancia de `FabricClient` y llame al método [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) en su instancia de **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="dd81f-371">To get cluster health chunk, create a `FabricClient` and call the [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="dd81f-372">Puede pasar [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) para describir directivas de mantenimiento y filtros avanzados.</span><span class="sxs-lookup"><span data-stu-id="dd81f-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) to describe health policies and advanced filters.</span></span>

<span data-ttu-id="dd81f-373">El código siguiente obtiene fragmentos de mantenimiento del clúster con filtros avanzados.</span><span class="sxs-lookup"><span data-stu-id="dd81f-373">The following code gets cluster health chunk with advanced filters.</span></span>

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except the ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="dd81f-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd81f-374">PowerShell</span></span>
<span data-ttu-id="dd81f-375">El cmdlet para obtener el mantenimiento del clúster es [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span><span class="sxs-lookup"><span data-stu-id="dd81f-375">The cmdlet to get the cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="dd81f-376">Conéctese primero al clúster mediante el cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="dd81f-376">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="dd81f-377">El código siguiente obtiene los nodos solo si se encuentran en estado de error, a excepción de un nodo específico, que se debe devolver siempre.</span><span class="sxs-lookup"><span data-stu-id="dd81f-377">The following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in the cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

<span data-ttu-id="dd81f-378">El siguiente cmdlet obtiene fragmentos del clúster con filtros de aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd81f-378">The following cmdlet gets cluster chunk with application filters.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

<span data-ttu-id="dd81f-379">El siguiente cmdlet devuelve todas las entidades implementadas en un nodo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-379">The following cmdlet returns all deployed entities on a node.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a><span data-ttu-id="dd81f-380">REST</span><span class="sxs-lookup"><span data-stu-id="dd81f-380">REST</span></span>
<span data-ttu-id="dd81f-381">Puede obtener fragmentos de mantenimiento del clúster con una [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) o una [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) que incluye las directivas de mantenimiento y filtros avanzados descritos en el cuerpo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in the body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="dd81f-382">Consultas generales</span><span class="sxs-lookup"><span data-stu-id="dd81f-382">General queries</span></span>
<span data-ttu-id="dd81f-383">Las consultas generales devuelven una lista de entidades de Service Fabric de un tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="dd81f-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="dd81f-384">Se exponen mediante la API (por medio de los métodos de **FabricClient.QueryManager**), los cmdlets de PowerShell y REST.</span><span class="sxs-lookup"><span data-stu-id="dd81f-384">They are exposed through the API (via the methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="dd81f-385">Estas consultas agregan subconsultas de varios componentes.</span><span class="sxs-lookup"><span data-stu-id="dd81f-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="dd81f-386">Uno de ellos es el [Almacén de estado](service-fabric-health-introduction.md#health-store), que rellena el estado de mantenimiento agregado para cada resultado de consulta.</span><span class="sxs-lookup"><span data-stu-id="dd81f-386">One of them is the [health store](service-fabric-health-introduction.md#health-store), which populates the aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="dd81f-387">Las consultas generales devuelven el estado de mantenimiento agregado de la entidad y no contienen los datos completos de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="dd81f-387">General queries return the aggregated health state of the entity and do not contain rich health data.</span></span> <span data-ttu-id="dd81f-388">Si el mantenimiento de una entidad no es correcto, puede seguir con las consultas de mantenimiento para obtener toda su información de mantenimiento, como eventos, estados de mantenimiento de los elementos secundarios y evaluaciones de mantenimiento incorrecto.</span><span class="sxs-lookup"><span data-stu-id="dd81f-388">If an entity is not healthy, you can follow up with health queries to get all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="dd81f-389">Si las consultas generales devuelven un estado de mantenimiento desconocido para una entidad, es posible que el almacén de estado no tenga datos completos sobre la entidad.</span><span class="sxs-lookup"><span data-stu-id="dd81f-389">If general queries return an unknown health state for an entity, it's possible that the health store doesn't have complete data about the entity.</span></span> <span data-ttu-id="dd81f-390">También es posible que una subconsulta al almacén de estado no fuera correcta (por ejemplo, se produjo un error de comunicación o se limitó el almacén de estado).</span><span class="sxs-lookup"><span data-stu-id="dd81f-390">It's also possible that a subquery to the health store wasn't successful (for example, there was a communication error, or the health store was throttled).</span></span> <span data-ttu-id="dd81f-391">Realice un seguimiento con una consulta de mantenimiento para la entidad.</span><span class="sxs-lookup"><span data-stu-id="dd81f-391">Follow up with a health query for the entity.</span></span> <span data-ttu-id="dd81f-392">Si la subconsulta se encontró con errores transitorios, como problemas de red, esta consulta de seguimiento puede ser de ayuda.</span><span class="sxs-lookup"><span data-stu-id="dd81f-392">If the subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="dd81f-393">También le puede proporcionar más detalles del almacén de estado sobre por qué no se expone la entidad.</span><span class="sxs-lookup"><span data-stu-id="dd81f-393">It may also give you more details from the health store about why the entity is not exposed.</span></span>

<span data-ttu-id="dd81f-394">Las consultas que contienen **HealthState** para las entidades son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="dd81f-394">The queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="dd81f-395">Lista de nodos: devuelve los nodos de la lista del clúster (paginada).</span><span class="sxs-lookup"><span data-stu-id="dd81f-395">Node list: Returns the list nodes in the cluster (paged).</span></span>
  * <span data-ttu-id="dd81f-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="dd81f-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="dd81f-397">PowerShell: Get-ServiceFabricNode.</span><span class="sxs-lookup"><span data-stu-id="dd81f-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="dd81f-398">Lista de aplicaciones: devuelve la lista de aplicaciones del clúster (paginada).</span><span class="sxs-lookup"><span data-stu-id="dd81f-398">Application list: Returns the list of applications in the cluster (paged).</span></span>
  * <span data-ttu-id="dd81f-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="dd81f-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="dd81f-400">PowerShell: Get-ServiceFabricApplication.</span><span class="sxs-lookup"><span data-stu-id="dd81f-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="dd81f-401">Lista de servicios: devuelve la lista de servicios de una aplicación (paginada).</span><span class="sxs-lookup"><span data-stu-id="dd81f-401">Service list: Returns the list of services in an application (paged).</span></span>
  * <span data-ttu-id="dd81f-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="dd81f-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="dd81f-403">PowerShell: Get-ServiceFabricService.</span><span class="sxs-lookup"><span data-stu-id="dd81f-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="dd81f-404">Lista de particiones: devuelve la lista de particiones de un servicio (paginada).</span><span class="sxs-lookup"><span data-stu-id="dd81f-404">Partition list: Returns the list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="dd81f-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="dd81f-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="dd81f-406">PowerShell: Get-ServiceFabricPartition.</span><span class="sxs-lookup"><span data-stu-id="dd81f-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="dd81f-407">Lista de réplicas: devuelve la lista de réplicas de una partición (paginada).</span><span class="sxs-lookup"><span data-stu-id="dd81f-407">Replica list: Returns the list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="dd81f-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="dd81f-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="dd81f-409">PowerShell: Get-ServiceFabricReplica.</span><span class="sxs-lookup"><span data-stu-id="dd81f-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="dd81f-410">Lista de aplicaciones implementadas: devuelve la lista de aplicaciones implementadas en un nodo.</span><span class="sxs-lookup"><span data-stu-id="dd81f-410">Deployed application list: Returns the list of deployed applications on a node.</span></span>
  * <span data-ttu-id="dd81f-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="dd81f-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="dd81f-412">PowerShell: Get-ServiceFabricDeployedApplication.</span><span class="sxs-lookup"><span data-stu-id="dd81f-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="dd81f-413">Lista de paquetes de servicio implementados: devuelve la lista de paquetes de servicio de una aplicación implementada.</span><span class="sxs-lookup"><span data-stu-id="dd81f-413">Deployed service package list: Returns the list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="dd81f-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="dd81f-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="dd81f-415">PowerShell: Get-ServiceFabricDeployedApplication.</span><span class="sxs-lookup"><span data-stu-id="dd81f-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="dd81f-416">Algunas de las consultas devuelven resultados paginados.</span><span class="sxs-lookup"><span data-stu-id="dd81f-416">Some of the queries return paged results.</span></span> <span data-ttu-id="dd81f-417">La devolución de estas consultas es una lista que se deriva de [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span><span class="sxs-lookup"><span data-stu-id="dd81f-417">The return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="dd81f-418">Si los resultados no caben en un mensaje, solo se devuelve una página y ContinuationToken, que realiza el seguimiento de dónde se detuvo la enumeración.</span><span class="sxs-lookup"><span data-stu-id="dd81f-418">If the results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="dd81f-419">Continúe llamando a la misma consulta y pase el token de continuación de la consulta anterior para obtener los siguientes resultados.</span><span class="sxs-lookup"><span data-stu-id="dd81f-419">Continue to call the same query and pass in the continuation token from the previous query to get next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="dd81f-420">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="dd81f-420">Examples</span></span>
<span data-ttu-id="dd81f-421">El código siguiente obtiene las aplicaciones incorrectas en el clúster:</span><span class="sxs-lookup"><span data-stu-id="dd81f-421">The following code gets the unhealthy applications in the cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="dd81f-422">El siguiente cmdlet obtiene los detalles de la aplicación fabric:/WordCount.</span><span class="sxs-lookup"><span data-stu-id="dd81f-422">The following cmdlet gets the application details for the fabric:/WordCount application.</span></span> <span data-ttu-id="dd81f-423">Observe que el estado de mantenimiento está en advertencia.</span><span class="sxs-lookup"><span data-stu-id="dd81f-423">Notice that health state is at warning.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

<span data-ttu-id="dd81f-424">El siguiente cmdlet obtiene los servicios con un estado de mantenimiento de error:</span><span class="sxs-lookup"><span data-stu-id="dd81f-424">The following cmdlet gets the services with a health state of error:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="dd81f-425">Actualización de clústeres y aplicaciones</span><span class="sxs-lookup"><span data-stu-id="dd81f-425">Cluster and application upgrades</span></span>
<span data-ttu-id="dd81f-426">Durante una actualización supervisada del clúster y la aplicación, Service Fabric comprueba el mantenimiento para asegurarse de que todo está correcto.</span><span class="sxs-lookup"><span data-stu-id="dd81f-426">During a monitored upgrade of the cluster and application, Service Fabric checks health to ensure that everything remains healthy.</span></span> <span data-ttu-id="dd81f-427">Si una entidad es incorrecta según se ha evaluado mediante las directivas de mantenimiento configuradas, la actualización aplica directivas específicas de actualización para determinar la próxima acción.</span><span class="sxs-lookup"><span data-stu-id="dd81f-427">If an entity is unhealthy as evaluated by using configured health policies, the upgrade applies upgrade-specific policies to determine the next action.</span></span> <span data-ttu-id="dd81f-428">La actualización se puede poner en pausa para permitir la interacción de los usuarios (por ejemplo, corregir las condiciones de error o cambiar las directivas), o se puede revertir automáticamente a la versión buena anterior.</span><span class="sxs-lookup"><span data-stu-id="dd81f-428">The upgrade may be paused to allow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back to the previous good version.</span></span>

<span data-ttu-id="dd81f-429">Durante la actualización de un *clúster* , puede obtener su estado de actualización.</span><span class="sxs-lookup"><span data-stu-id="dd81f-429">During a *cluster* upgrade, you can get the cluster upgrade status.</span></span> <span data-ttu-id="dd81f-430">El estado de actualización incluye las evaluaciones de mantenimiento incorrecto, que señalan lo que está mal en el clúster.</span><span class="sxs-lookup"><span data-stu-id="dd81f-430">The upgrade status includes unhealthy evaluations, which point to what is unhealthy in the cluster.</span></span> <span data-ttu-id="dd81f-431">Si se revierte la actualización debido a problemas de mantenimiento, el estado de actualización recuerda las razones del último mantenimiento incorrecto.</span><span class="sxs-lookup"><span data-stu-id="dd81f-431">If the upgrade is rolled back due to health issues, the upgrade status remembers the last unhealthy reasons.</span></span> <span data-ttu-id="dd81f-432">Esta información puede ayudar a los administradores a investigar qué salió mal después de que se revirtiera o detuviera la actualización.</span><span class="sxs-lookup"><span data-stu-id="dd81f-432">This information can help administrators investigate what went wrong after the upgrade rolled back or stopped.</span></span>

<span data-ttu-id="dd81f-433">De igual forma, durante la actualización de una *aplicación* , las evaluaciones de mantenimiento incorrecto están contenidas en el estado de actualización de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd81f-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in the application upgrade status.</span></span>

<span data-ttu-id="dd81f-434">A continuación se muestra el estado de actualización de la aplicación para una aplicación fabric/WordCount modificada.</span><span class="sxs-lookup"><span data-stu-id="dd81f-434">The following shows the application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="dd81f-435">Un guardián ha informado de un error en una de sus réplicas.</span><span class="sxs-lookup"><span data-stu-id="dd81f-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="dd81f-436">La actualización se revierte porque no se respetan las comprobaciones de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="dd81f-436">The upgrade is rolling back because the health checks are not respected.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

<span data-ttu-id="dd81f-437">Más información sobre la [actualización de aplicaciones de Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="dd81f-437">Read more about the [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-to-troubleshoot"></a><span data-ttu-id="dd81f-438">Uso de las evaluaciones de mantenimiento para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="dd81f-438">Use health evaluations to troubleshoot</span></span>
<span data-ttu-id="dd81f-439">Siempre que haya un problema con el clúster o una aplicación, consulte el mantenimiento del clúster o de la aplicación para analizar lo que pasa.</span><span class="sxs-lookup"><span data-stu-id="dd81f-439">Whenever there is an issue with the cluster or an application, look at the cluster or application health to pinpoint what is wrong.</span></span> <span data-ttu-id="dd81f-440">Las evaluaciones de mantenimiento incorrecto proporcionan detalles sobre lo que activó el estado incorrecto actual.</span><span class="sxs-lookup"><span data-stu-id="dd81f-440">The unhealthy evaluations provide details about what triggered the current unhealthy state.</span></span> <span data-ttu-id="dd81f-441">Si lo necesita, puede explorar en profundidad las entidades secundarias incorrectas para identificar la causa principal.</span><span class="sxs-lookup"><span data-stu-id="dd81f-441">If you need to, you can drill down into unhealthy child entities to identify the root cause.</span></span>

<span data-ttu-id="dd81f-442">Por ejemplo, considere una aplicación con un estado incorrecto porque hay un informe de errores en una de sus réplicas.</span><span class="sxs-lookup"><span data-stu-id="dd81f-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="dd81f-443">El siguiente cmdlet de Powershell muestra las evaluaciones de estado incorrecto:</span><span class="sxs-lookup"><span data-stu-id="dd81f-443">The following Powershell cmdlet shows the unhealthy evaluations:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

<span data-ttu-id="dd81f-444">Puede mirar la réplica para obtener más información:</span><span class="sxs-lookup"><span data-stu-id="dd81f-444">You can look at the replica to get more information:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="dd81f-445">Las evaluaciones de mantenimiento incorrecto muestran la razón principal de que la entidad se evaluara con el estado de mantenimiento actual.</span><span class="sxs-lookup"><span data-stu-id="dd81f-445">The unhealthy evaluations show the first reason the entity is evaluated to current health state.</span></span> <span data-ttu-id="dd81f-446">Puede haber muchos otros eventos que desencadenen este estado pero no se reflejan en las evaluaciones.</span><span class="sxs-lookup"><span data-stu-id="dd81f-446">There may be multiple other events that trigger this state, but they are not be reflected in the evaluations.</span></span> <span data-ttu-id="dd81f-447">Para más información, explore en profundidad las entidades de mantenimiento para averiguar todos los informes de mantenimiento incorrecto en el clúster.</span><span class="sxs-lookup"><span data-stu-id="dd81f-447">To get more information, drill down into the health entities to figure out all the unhealthy reports in the cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="dd81f-448">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dd81f-448">Next steps</span></span>
[<span data-ttu-id="dd81f-449">Utilización de informes de mantenimiento del sistema para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="dd81f-449">Use system health reports to troubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="dd81f-450">Incorporación de informes de mantenimiento de Service Fabric personalizados</span><span class="sxs-lookup"><span data-stu-id="dd81f-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="dd81f-451">Notificación y comprobación del estado del servicio</span><span class="sxs-lookup"><span data-stu-id="dd81f-451">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="dd81f-452">Supervisión y diagnóstico de los servicios localmente</span><span class="sxs-lookup"><span data-stu-id="dd81f-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="dd81f-453">Actualización de la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="dd81f-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
