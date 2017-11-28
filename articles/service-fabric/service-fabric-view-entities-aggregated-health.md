---
title: aaaHow tooview Azure Service Fabric entidades agregan mantenimiento | Documentos de Microsoft
description: "Describe cómo ver tooquery y evaluar el estado de las entidades de Azure Service Fabric agregados, a través de consultas de estado y consultas generales."
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
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="08656-103">Vista de los informes de estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="08656-103">View Service Fabric health reports</span></span>
<span data-ttu-id="08656-104">Azure Service Fabric presenta un [modelo de mantenimiento](service-fabric-health-introduction.md) con entidades de estado en las que componentes y guardianes del sistema pueden notificar las condiciones locales que están supervisando.</span><span class="sxs-lookup"><span data-stu-id="08656-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="08656-105">Hola [almacén de estado](service-fabric-health-introduction.md#health-store) agrega todos los toodetermine de datos de estado si las entidades están en buen estadas.</span><span class="sxs-lookup"><span data-stu-id="08656-105">hello [health store](service-fabric-health-introduction.md#health-store) aggregates all health data toodetermine whether entities are healthy.</span></span>

<span data-ttu-id="08656-106">clúster de Hola se rellena automáticamente con los informes de estado enviados por componentes del sistema Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-106">hello cluster is automatically populated with health reports sent by hello system components.</span></span> <span data-ttu-id="08656-107">Más información, lea [tootroubleshoot de informes de mantenimiento del sistema de uso](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span><span class="sxs-lookup"><span data-stu-id="08656-107">Read more at [Use system health reports tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="08656-108">Service Fabric proporciona varias maneras tooget Hola agregado mantenimiento de entidades de hello:</span><span class="sxs-lookup"><span data-stu-id="08656-108">Service Fabric provides multiple ways tooget hello aggregated health of hello entities:</span></span>

* <span data-ttu-id="08656-109">[Explorador de Service Fabric](service-fabric-visualizing-your-cluster.md) y otras herramientas de visualización</span><span class="sxs-lookup"><span data-stu-id="08656-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="08656-110">Consultas de mantenimiento (a través de PowerShell, API o REST)</span><span class="sxs-lookup"><span data-stu-id="08656-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="08656-111">General, las consultas que devuelven una lista de entidades que tienen el estado como una de las propiedades de hello (a través de PowerShell, API o REST)</span><span class="sxs-lookup"><span data-stu-id="08656-111">General queries that return a list of entities that have health as one of hello properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="08656-112">toodemonstrate estas opciones, vamos a usar un clúster local con cinco nodos y hello [fabric: / aplicación WordCount](http://aka.ms/servicefabric-wordcountapp).</span><span class="sxs-lookup"><span data-stu-id="08656-112">toodemonstrate these options, let's use a local cluster with five nodes and hello [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="08656-113">Hola **fabric: / WordCount** aplicación contiene dos servicios de manera predeterminada, un servicio con estado de tipo `WordCountServiceType`y un servicio sin estado de tipo `WordCountWebServiceType`.</span><span class="sxs-lookup"><span data-stu-id="08656-113">hello **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="08656-114">He cambiado hello `ApplicationManifest.xml` toorequire siete réplicas de destino para el servicio con estado hello y una partición.</span><span class="sxs-lookup"><span data-stu-id="08656-114">I changed hello `ApplicationManifest.xml` toorequire seven target replicas for hello stateful service and one partition.</span></span> <span data-ttu-id="08656-115">Porque hay solo cinco nodos en clúster de hello, componentes del sistema Hola notificar una advertencia en la partición de servicio de hello porque es inferior al recuento de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-115">Because there are only five nodes in hello cluster, hello system components report a warning on hello service partition because it is below hello target count.</span></span>

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

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="08656-116">Mantenimiento del Explorador de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="08656-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="08656-117">Explorador de Service Fabric proporciona una vista visual de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-117">Service Fabric Explorer provides a visual view of hello cluster.</span></span> <span data-ttu-id="08656-118">En la imagen de hello siguiente, puede ver que:</span><span class="sxs-lookup"><span data-stu-id="08656-118">In hello image below, you can see that:</span></span>

* <span data-ttu-id="08656-119">Hola aplicación **fabric: / WordCount** está en rojo (en error) porque tiene un evento de error notificado por **MyWatchdog** para la propiedad de hello **disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="08656-119">hello application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for hello property **Availability**.</span></span>
* <span data-ttu-id="08656-120">Uno de sus servicios, **fabric:/WordCount/WordCountService** está en amarillo (en advertencia).</span><span class="sxs-lookup"><span data-stu-id="08656-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="08656-121">Hola servicio está configurado con siete réplicas y clúster de hello tiene cinco nodos, por lo que no se puede colocar dos repicas.</span><span class="sxs-lookup"><span data-stu-id="08656-121">hello service is configured with seven replicas and hello cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="08656-122">Aunque no se muestra aquí, la partición de servicio de hello es amarilla debido a un informe del sistema de `System.FM` que indique que `Partition is below target replica or instance count`.</span><span class="sxs-lookup"><span data-stu-id="08656-122">Although it's not shown here, hello service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="08656-123">desencadenadores de partición amarillo Hola Hola servicio amarillo.</span><span class="sxs-lookup"><span data-stu-id="08656-123">hello yellow partition triggers hello yellow service.</span></span>
* <span data-ttu-id="08656-124">clúster de Hello es rojo debido a la aplicación hello rojo.</span><span class="sxs-lookup"><span data-stu-id="08656-124">hello cluster is red because of hello red application.</span></span>

<span data-ttu-id="08656-125">evaluación de Hello usa las directivas predeterminadas de manifiesto de clúster de Hola y el manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="08656-125">hello evaluation uses default policies from hello cluster manifest and application manifest.</span></span> <span data-ttu-id="08656-126">Son directivas estrictas y no toleran ningún error.</span><span class="sxs-lookup"><span data-stu-id="08656-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="08656-127">Vista de clúster de hello con Service Fabric Explorer:</span><span class="sxs-lookup"><span data-stu-id="08656-127">View of hello cluster with Service Fabric Explorer:</span></span>

![Vista de clúster de hello con Service Fabric Explorer.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="08656-129">Obtenga más información sobre el [Explorador de Service Fabric](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="08656-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="08656-130">Consultas de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="08656-130">Health queries</span></span>
<span data-ttu-id="08656-131">Service Fabric expone consultas de estado para cada uno de hello admitida [tipos de entidad](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span><span class="sxs-lookup"><span data-stu-id="08656-131">Service Fabric exposes health queries for each of hello supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="08656-132">Son accesibles a través de API, utilizando los métodos en hello [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), cmdlets de PowerShell y REST.</span><span class="sxs-lookup"><span data-stu-id="08656-132">They can be accessed through hello API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="08656-133">Estas consultas devuelven información de estado acerca de la entidad de hello: Hola agrega el estado, los eventos de estado de entidad, Estados de mantenimiento de elemento secundario (si procede), evaluaciones en mal estado (cuando la entidad de hello no es correcto) y las estadísticas de estado de los elementos secundarios (cuando aplicable).</span><span class="sxs-lookup"><span data-stu-id="08656-133">These queries return complete health information about hello entity: hello aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when hello entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="08656-134">Una entidad de estado se devuelve cuando se completa en el almacén de estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-134">A health entity is returned when it is fully populated in hello health store.</span></span> <span data-ttu-id="08656-135">entidad de Hello debe estar activo (no eliminado) y tiene un informe de sistema.</span><span class="sxs-lookup"><span data-stu-id="08656-135">hello entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="08656-136">Sus entidades primario en la cadena de jerarquía de hello también deben tener informes del sistema.</span><span class="sxs-lookup"><span data-stu-id="08656-136">Its parent entities on hello hierarchy chain must also have system reports.</span></span> <span data-ttu-id="08656-137">Si no se cumple alguna de estas condiciones, mantenimiento de hello las consultas devuelven un [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) con [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` que muestra por qué no se devuelve la entidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-137">If any of these conditions are not satisfied, hello health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why hello entity is not returned.</span></span>
>
>

<span data-ttu-id="08656-138">consultas de estado de Hello deben pasar el identificador de entidad de hello, que depende del tipo de entidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-138">hello health queries must pass in hello entity identifier, which depends on hello entity type.</span></span> <span data-ttu-id="08656-139">las consultas de Hello aceptan parámetros de la directiva de mantenimiento opcional.</span><span class="sxs-lookup"><span data-stu-id="08656-139">hello queries accept optional health policy parameters.</span></span> <span data-ttu-id="08656-140">Si no se especifica ninguna directiva de mantenimiento, Hola [las directivas de mantenimiento](service-fabric-health-introduction.md#health-policies) del manifiesto de clúster o una aplicación Hola se usan para la evaluación.</span><span class="sxs-lookup"><span data-stu-id="08656-140">If no health policies are specified, hello [health policies](service-fabric-health-introduction.md#health-policies) from hello cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="08656-141">Si Hola manifiestos no contienen una definición de las directivas de mantenimiento, directivas de mantenimiento de hello predeterminadas se usan para la evaluación.</span><span class="sxs-lookup"><span data-stu-id="08656-141">If hello manifests don't contain a definition for health policies, hello default health policies are used for evaluation.</span></span> <span data-ttu-id="08656-142">las directivas de mantenimiento de Hello predeterminado no tolerar los errores.</span><span class="sxs-lookup"><span data-stu-id="08656-142">hello default health policies do not tolerate any failures.</span></span> <span data-ttu-id="08656-143">las consultas de Hello también aceptan filtros para devolver solo los elementos secundarios parciales o eventos--hello las que respetan Hola filtros especificados.</span><span class="sxs-lookup"><span data-stu-id="08656-143">hello queries also accept filters for returning only partial children or events--hello ones that respect hello specified filters.</span></span> <span data-ttu-id="08656-144">Otro filtro permite excluir las estadísticas de los elementos secundarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-144">Another filter allows excluding hello children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="08656-145">se aplican los filtros de salida de Hello en servidor hello, por lo que se reduce el tamaño de respuesta del mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-145">hello output filters are applied on hello server side, so hello message reply size is reduced.</span></span> <span data-ttu-id="08656-146">Se recomienda que utilice los filtros de salida de hello toolimit Hola datos devuelven, en lugar de aplican filtros en el lado del cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-146">We recommended that you use hello output filters toolimit hello data returned, rather than apply filters on hello client side.</span></span>
>
>

<span data-ttu-id="08656-147">Contiene el mantenimiento de la entidad:</span><span class="sxs-lookup"><span data-stu-id="08656-147">An entity's health contains:</span></span>

* <span data-ttu-id="08656-148">Hola estado agregado de entidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-148">hello aggregated health state of hello entity.</span></span> <span data-ttu-id="08656-149">Calculado por el almacén de estado de hello basándose en los informes de estado de entidad, Estados de mantenimiento de elemento secundario (si procede) y las directivas de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="08656-149">Computed by hello health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="08656-150">Lea más sobre la [evaluación del mantenimiento de entidades](service-fabric-health-introduction.md#health-evaluation).</span><span class="sxs-lookup"><span data-stu-id="08656-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="08656-151">Hola eventos de estado de una entidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-151">hello health events on hello entity.</span></span>
* <span data-ttu-id="08656-152">colección de Hola de Estados de mantenimiento de todos los elementos secundarios para las entidades de Hola que pueden tener elementos secundarios.</span><span class="sxs-lookup"><span data-stu-id="08656-152">hello collection of health states of all children for hello entities that can have children.</span></span> <span data-ttu-id="08656-153">Estados de mantenimiento de Hello contienen los identificadores de entidad y Hola estado agregado.</span><span class="sxs-lookup"><span data-stu-id="08656-153">hello health states contain entity identifiers and hello aggregated health state.</span></span> <span data-ttu-id="08656-154">tooget estado para un elemento secundario, llamar a estado de consulta de hello para el tipo de entidad de secundarios de Hola y pase identificador secundario de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-154">tooget complete health for a child, call hello query health for hello child entity type and pass in hello child identifier.</span></span>
* <span data-ttu-id="08656-155">evaluaciones en mal estado Hello toohello de ese punto de informes que desencadenan estado de Hola de entidad de hello, si Hola entidad no es correcto.</span><span class="sxs-lookup"><span data-stu-id="08656-155">hello unhealthy evaluations that point toohello report that triggered hello state of hello entity, if hello entity is not healthy.</span></span> <span data-ttu-id="08656-156">las evaluaciones de Hello son recursivos, que contiene evaluaciones del mantenimiento de los elementos secundarios Hola que desencadenó el estado de mantenimiento actual.</span><span class="sxs-lookup"><span data-stu-id="08656-156">hello evaluations are recursive, containing hello children health evaluations that triggered current health state.</span></span> <span data-ttu-id="08656-157">Por ejemplo, un guardián notificó un error en una réplica.</span><span class="sxs-lookup"><span data-stu-id="08656-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="08656-158">estado de la aplicación Hello muestra una evaluación incorrecto debido tooan servicio incorrecto; servicio de Hello está en mal estado vencimiento partición tooa error; partición de Hello está en mal estado vencimiento réplica tooa error; réplica de Hello está en mal estado debido a informes de estado de error de guardián toohello.</span><span class="sxs-lookup"><span data-stu-id="08656-158">hello application health shows an unhealthy evaluation due tooan unhealthy service; hello service is unhealthy due tooa partition in error; hello partition is unhealthy due tooa replica in error; hello replica is unhealthy due toohello watchdog error health report.</span></span>
* <span data-ttu-id="08656-159">estadísticas de estado de Hola para todos los tipos de elementos secundarios de entidades de Hola que tienen elementos secundarios.</span><span class="sxs-lookup"><span data-stu-id="08656-159">hello health statistics for all children types of hello entities that have children.</span></span> <span data-ttu-id="08656-160">Por ejemplo, el estado del clúster muestra el número total de Hola de aplicaciones, servicios, particiones, las réplicas e implementa entidades de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-160">For example, cluster health shows hello total number of applications, services, partitions, replicas, and deployed entities in hello cluster.</span></span> <span data-ttu-id="08656-161">Estado del servicio muestra el número total de Hola de particiones y réplicas en hello servicio especificado.</span><span class="sxs-lookup"><span data-stu-id="08656-161">Service health shows hello total number of partitions and replicas under hello specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="08656-162">Obtención del mantenimiento de clúster</span><span class="sxs-lookup"><span data-stu-id="08656-162">Get cluster health</span></span>
<span data-ttu-id="08656-163">Devuelve Hola mantenimiento de entidad de clúster de Hola y contiene los Estados de mantenimiento de Hola de aplicaciones y nodos (elementos secundarios del clúster de hello).</span><span class="sxs-lookup"><span data-stu-id="08656-163">Returns hello health of hello cluster entity and contains hello health states of applications and nodes (children of hello cluster).</span></span> <span data-ttu-id="08656-164">Entrada:</span><span class="sxs-lookup"><span data-stu-id="08656-164">Input:</span></span>

* <span data-ttu-id="08656-165">Directiva de mantenimiento de clúster [opcional] Hola utiliza nodos de hello tooevaluate y eventos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-165">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="08656-166">Asignación de directiva de mantenimiento de aplicación Hola [opcional], con las directivas de mantenimiento de hello usa directivas de manifiesto de aplicación de Hola de toooverride.</span><span class="sxs-lookup"><span data-stu-id="08656-166">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="08656-167">[Opcional] Filtros de eventos, nodos y aplicaciones que especifican las entradas que son de interés y se deben devolver en el resultado de hello (por ejemplo, únicamente, los errores o las advertencias y errores).</span><span class="sxs-lookup"><span data-stu-id="08656-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="08656-168">Todos los eventos, nodos y aplicaciones son mantenimiento de entidad agregado hello tooevaluate usado, independientemente del filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-168">All events, nodes, and applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="08656-169">[Opcional] Filtrar las estadísticas de estado de tooexclude.</span><span class="sxs-lookup"><span data-stu-id="08656-169">[Optional] Filter tooexclude health statistics.</span></span>
* <span data-ttu-id="08656-170">[Opcional] Filtrar tooinclude fabric: / Hola de las estadísticas de estado del sistema en las estadísticas de estado.</span><span class="sxs-lookup"><span data-stu-id="08656-170">[Optional] Filter tooinclude fabric:/System health statistics in hello health statistics.</span></span> <span data-ttu-id="08656-171">Solo se aplica cuando no se excluyen las estadísticas de estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-171">Only applicable when hello health statistics are not excluded.</span></span> <span data-ttu-id="08656-172">De forma predeterminada, las estadísticas de estado de Hola incluyen solo las estadísticas de las aplicaciones de usuario y aplicación del sistema no Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-172">By default, hello health statistics include only statistics for user applications and not hello System application.</span></span>

### <a name="api"></a><span data-ttu-id="08656-173">API</span><span class="sxs-lookup"><span data-stu-id="08656-173">API</span></span>
<span data-ttu-id="08656-174">tooget estado del clúster, cree una `FabricClient` llamada hello y [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) método en su **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="08656-174">tooget cluster health, create a `FabricClient` and call hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="08656-175">Hello llamada siguiente obtiene el estado del clúster hello:</span><span class="sxs-lookup"><span data-stu-id="08656-175">hello following call gets hello cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="08656-176">Hola código siguiente obtiene el estado del clúster hello mediante una directiva de mantenimiento de clúster personalizado y filtra los nodos y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="08656-176">hello following code gets hello cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="08656-177">Especifica que las estadísticas de estado de hello incluyen tejido hello: / estadísticas del sistema.</span><span class="sxs-lookup"><span data-stu-id="08656-177">It specifies that hello health statistics include hello fabric:/System statistics.</span></span> <span data-ttu-id="08656-178">Crea [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), que contiene información de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains hello input information.</span></span>

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

### <a name="powershell"></a><span data-ttu-id="08656-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08656-179">PowerShell</span></span>
<span data-ttu-id="08656-180">es el estado de clúster de Hola Hola cmdlet tooget [ServiceFabricClusterHealth Get](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="08656-180">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="08656-181">En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="08656-181">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="08656-182">Hola estado del clúster de hello es cinco nodos, la aplicación de sistema de Hola y fabric: / WordCount configurado como se describe.</span><span class="sxs-lookup"><span data-stu-id="08656-182">hello state of hello cluster is five nodes, hello system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="08656-183">Hola siguiendo el cmdlet Obtiene el estado del clúster mediante el uso de directivas de mantenimiento de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="08656-183">hello following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="08656-184">Hello estado agregado una advertencia, ya que Hola fabric: / aplicación WordCount produce una advertencia.</span><span class="sxs-lookup"><span data-stu-id="08656-184">hello aggregated health state is warning, because hello fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="08656-185">Tenga en cuenta cómo evaluaciones en mal estado Hola proporcionan detalles de las condiciones de Hola que desencadenó Hola agregado mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="08656-185">Note how hello unhealthy evaluations provide details on hello conditions that triggered hello aggregated health.</span></span>

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

<span data-ttu-id="08656-186">Hello siguiente cmdlet de PowerShell obtiene Hola mantenimiento de clúster de hello mediante una directiva de aplicación personalizada.</span><span class="sxs-lookup"><span data-stu-id="08656-186">hello following PowerShell cmdlet gets hello health of hello cluster by using a custom application policy.</span></span> <span data-ttu-id="08656-187">Filtra los resultados tooget sólo las aplicaciones y los nodos de error o advertencia.</span><span class="sxs-lookup"><span data-stu-id="08656-187">It filters results tooget only applications and nodes in error or warning.</span></span> <span data-ttu-id="08656-188">Como resultado, no se devuelve ningún nodo, ya que todos son correctos.</span><span class="sxs-lookup"><span data-stu-id="08656-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="08656-189">Hola solo fabric: / aplicación WordCount respeta el filtro de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-189">Only hello fabric:/WordCount application respects hello applications filter.</span></span> <span data-ttu-id="08656-190">Directiva personalizada de hello especifica tooconsider advertencias como errores de tejido de hello: / aplicación WordCount, aplicación hello se evalúa como erróneo y, por lo que es clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-190">Because hello custom policy specifies tooconsider warnings as errors for hello fabric:/WordCount application, hello application is evaluated as in error, and so is hello cluster.</span></span>

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

### <a name="rest"></a><span data-ttu-id="08656-191">REST</span><span class="sxs-lookup"><span data-stu-id="08656-191">REST</span></span>
<span data-ttu-id="08656-192">Puede obtener el estado del clúster con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) que incluye las directivas de mantenimiento que se describe en el cuerpo de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="08656-193">Obtención del mantenimiento de nodo</span><span class="sxs-lookup"><span data-stu-id="08656-193">Get node health</span></span>
<span data-ttu-id="08656-194">Devuelve Hola estado de una entidad del nodo y contiene eventos de estado de hello notificados en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-194">Returns hello health of a node entity and contains hello health events reported on hello node.</span></span> <span data-ttu-id="08656-195">Entrada:</span><span class="sxs-lookup"><span data-stu-id="08656-195">Input:</span></span>

* <span data-ttu-id="08656-196">Nombre de nodo de hello [obligatorio] que identifica el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-196">[Required] hello node name that identifies hello node.</span></span>
* <span data-ttu-id="08656-197">Configuración de directiva de mantenimiento de clúster de hello [opcional] usa tooevaluate mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="08656-197">[Optional] hello cluster health policy settings used tooevaluate health.</span></span>
* <span data-ttu-id="08656-198">[Opcional] Filtros para los eventos que especifican las entradas que son de interés y se deben devolver en el resultado de hello (por ejemplo, únicamente, los errores o las advertencias y errores).</span><span class="sxs-lookup"><span data-stu-id="08656-198">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="08656-199">Todos los eventos son mantenimiento de entidad agregado hello tooevaluate usado, independientemente del filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-199">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="08656-200">API</span><span class="sxs-lookup"><span data-stu-id="08656-200">API</span></span>
<span data-ttu-id="08656-201">estado de nodo de tooget a través de hello API, cree un `FabricClient` llamada hello y [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) método en su HealthManager.</span><span class="sxs-lookup"><span data-stu-id="08656-201">tooget node health through hello API, create a `FabricClient` and call hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="08656-202">Hello código siguiente obtiene mantenimiento de nodo de hello para el nombre del nodo especificado de hello:</span><span class="sxs-lookup"><span data-stu-id="08656-202">hello following code gets hello node health for hello specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="08656-203">Hello código siguiente obtiene el estado del nodo de Hola para hello especificado nombre de nodo y pasa en el filtro de eventos y una directiva personalizada a través de [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="08656-203">hello following code gets hello node health for hello specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="08656-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08656-204">PowerShell</span></span>
<span data-ttu-id="08656-205">el estado del nodo Hola cmdlet tooget hello es [ServiceFabricNodeHealth Get](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span><span class="sxs-lookup"><span data-stu-id="08656-205">hello cmdlet tooget hello node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="08656-206">En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="08656-206">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="08656-207">Hola siguiente cmdlet Obtiene el mantenimiento de nodo de hello mediante el uso de directivas de mantenimiento de manera predeterminada:</span><span class="sxs-lookup"><span data-stu-id="08656-207">hello following cmdlet gets hello node health by using default health policies:</span></span>

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

<span data-ttu-id="08656-208">Hello siguiente cmdlet obtiene Hola mantenimiento de todos los nodos de clúster de hello:</span><span class="sxs-lookup"><span data-stu-id="08656-208">hello following cmdlet gets hello health of all nodes in hello cluster:</span></span>

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

### <a name="rest"></a><span data-ttu-id="08656-209">REST</span><span class="sxs-lookup"><span data-stu-id="08656-209">REST</span></span>
<span data-ttu-id="08656-210">Puede obtener el estado de nodo con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) que incluye las directivas de mantenimiento que se describe en el cuerpo de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="08656-211">Obtención del mantenimiento de la aplicación</span><span class="sxs-lookup"><span data-stu-id="08656-211">Get application health</span></span>
<span data-ttu-id="08656-212">Devuelve el estado de saludo de una entidad de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="08656-212">Returns hello health of an application entity.</span></span> <span data-ttu-id="08656-213">Contiene los Estados de mantenimiento de Hola de aplicación hello implementado y elementos secundarios de servicio.</span><span class="sxs-lookup"><span data-stu-id="08656-213">It contains hello health states of hello deployed application and service children.</span></span> <span data-ttu-id="08656-214">Entrada:</span><span class="sxs-lookup"><span data-stu-id="08656-214">Input:</span></span>

* <span data-ttu-id="08656-215">Hola [obligatorio] nombre de la aplicación (URI) que identifica la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="08656-215">[Required] hello application name (URI) that identifies hello application.</span></span>
* <span data-ttu-id="08656-216">Directiva de mantenimiento de aplicación Hola [opcional] usa directivas de manifiesto de aplicación de Hola de toooverride.</span><span class="sxs-lookup"><span data-stu-id="08656-216">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="08656-217">[Opcional] Filtros de eventos, servicios y aplicaciones implementadas que especifican las entradas que son de interés y se deben devolver en el resultado de hello (por ejemplo, únicamente, los errores o las advertencias y errores).</span><span class="sxs-lookup"><span data-stu-id="08656-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="08656-218">Todos los eventos, servicios y aplicaciones implementadas son mantenimiento de entidad agregado hello tooevaluate usado, independientemente del filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-218">All events, services, and deployed applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="08656-219">[Opcional] Filtrar las estadísticas de estado de hello tooexclude.</span><span class="sxs-lookup"><span data-stu-id="08656-219">[Optional] Filter tooexclude hello health statistics.</span></span> <span data-ttu-id="08656-220">Si no se especifica, las estadísticas de estado de hello incluyen Aceptar hello, de advertencia y de recuento de errores para todos los elementos secundarios de la aplicación: servicios, particiones, las réplicas, las aplicaciones implementadas y paquetes de servicio implementados.</span><span class="sxs-lookup"><span data-stu-id="08656-220">If not specified, hello health statistics include hello ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="08656-221">API</span><span class="sxs-lookup"><span data-stu-id="08656-221">API</span></span>
<span data-ttu-id="08656-222">estado de la aplicación de tooget, crear un `FabricClient` llamada hello y [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) método en su HealthManager.</span><span class="sxs-lookup"><span data-stu-id="08656-222">tooget application health, create a `FabricClient` and call hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="08656-223">Hello código siguiente obtiene el estado de aplicaciones de hello para el nombre de aplicación especificado hello (URI):</span><span class="sxs-lookup"><span data-stu-id="08656-223">hello following code gets hello application health for hello specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="08656-224">Hello código siguiente obtiene el estado de aplicaciones de hello para el nombre de aplicación especificado hello (URI), con los filtros y las directivas personalizadas especifican a través de [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="08656-224">hello following code gets hello application health for hello specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

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

### <a name="powershell"></a><span data-ttu-id="08656-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08656-225">PowerShell</span></span>
<span data-ttu-id="08656-226">es el estado de aplicaciones de Hola Hola cmdlet tooget [ServiceFabricApplicationHealth Get](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="08656-226">hello cmdlet tooget hello application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="08656-227">En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="08656-227">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="08656-228">Hello siguiente cmdlet devuelve mantenimiento Hola de hello **fabric: / WordCount** aplicación:</span><span class="sxs-lookup"><span data-stu-id="08656-228">hello following cmdlet returns hello health of hello **fabric:/WordCount** application:</span></span>

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

<span data-ttu-id="08656-229">Hola siguiendo los pasos de cmdlet de PowerShell de directivas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="08656-229">hello following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="08656-230">También filtra los elementos secundarios y los eventos.</span><span class="sxs-lookup"><span data-stu-id="08656-230">It also filters children and events.</span></span>

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

### <a name="rest"></a><span data-ttu-id="08656-231">REST</span><span class="sxs-lookup"><span data-stu-id="08656-231">REST</span></span>
<span data-ttu-id="08656-232">Puede obtener el estado de aplicación con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) que incluye las directivas de mantenimiento que se describe en el cuerpo de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="08656-233">Obtención del mantenimiento del servicio</span><span class="sxs-lookup"><span data-stu-id="08656-233">Get service health</span></span>
<span data-ttu-id="08656-234">Devuelve el estado de saludo de una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="08656-234">Returns hello health of a service entity.</span></span> <span data-ttu-id="08656-235">Contiene los Estados de mantenimiento de partición Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-235">It contains hello partition health states.</span></span> <span data-ttu-id="08656-236">Entrada:</span><span class="sxs-lookup"><span data-stu-id="08656-236">Input:</span></span>

* <span data-ttu-id="08656-237">Hola [obligatorio] nombre del servicio (URI) que identifica el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-237">[Required] hello service name (URI) that identifies hello service.</span></span>
* <span data-ttu-id="08656-238">Directiva de mantenimiento de aplicación Hola [opcional] usa la directiva del manifiesto de aplicación toooverride Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-238">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="08656-239">[Opcional] Filtros de eventos y las particiones que especifican las entradas que son de interés y se deben devolver en el resultado de hello (por ejemplo, únicamente, los errores o las advertencias y errores).</span><span class="sxs-lookup"><span data-stu-id="08656-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="08656-240">Todos los eventos y las particiones son mantenimiento de entidad agregado hello tooevaluate usado, independientemente del filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-240">All events and partitions are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="08656-241">[Opcional] Filtrar las estadísticas de estado de tooexclude.</span><span class="sxs-lookup"><span data-stu-id="08656-241">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="08656-242">Si no se especifica, Hola Hola de mostrar las estadísticas de estado correcto, advertencia y error de recuento de todas las particiones y réplicas de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-242">If not specified, hello health statistics show hello ok, warning, and error count for all partitions and replicas of hello service.</span></span>

### <a name="api"></a><span data-ttu-id="08656-243">API</span><span class="sxs-lookup"><span data-stu-id="08656-243">API</span></span>
<span data-ttu-id="08656-244">estado del servicio tooget a través de hello API, cree un `FabricClient` llamada hello y [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) método en su HealthManager.</span><span class="sxs-lookup"><span data-stu-id="08656-244">tooget service health through hello API, create a `FabricClient` and call hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="08656-245">Hello en el ejemplo siguiente se obtiene Hola mantenimiento de un servicio con el nombre de servicio especificado (URI):</span><span class="sxs-lookup"><span data-stu-id="08656-245">hello following example gets hello health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="08656-246">Hello código siguiente obtiene Hola estado del servicio para el nombre de servicio especificado de hello (URI), especificar filtros y una directiva personalizada a través de [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="08656-246">hello following code gets hello service health for hello specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="08656-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08656-247">PowerShell</span></span>
<span data-ttu-id="08656-248">es el estado del servicio de Hello cmdlet tooget hello [ServiceFabricServiceHealth Get](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span><span class="sxs-lookup"><span data-stu-id="08656-248">hello cmdlet tooget hello service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="08656-249">En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="08656-249">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="08656-250">Hola siguiendo el cmdlet Obtiene el estado del servicio de hello mediante el uso de directivas de mantenimiento de manera predeterminada:</span><span class="sxs-lookup"><span data-stu-id="08656-250">hello following cmdlet gets hello service health by using default health policies:</span></span>

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

### <a name="rest"></a><span data-ttu-id="08656-251">REST</span><span class="sxs-lookup"><span data-stu-id="08656-251">REST</span></span>
<span data-ttu-id="08656-252">Puede obtener el estado del servicio con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) que incluye las directivas de mantenimiento que se describe en el cuerpo de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="08656-253">Obtención del mantenimiento de partición</span><span class="sxs-lookup"><span data-stu-id="08656-253">Get partition health</span></span>
<span data-ttu-id="08656-254">Devuelve el estado de saludo de una entidad de la partición.</span><span class="sxs-lookup"><span data-stu-id="08656-254">Returns hello health of a partition entity.</span></span> <span data-ttu-id="08656-255">Contiene los Estados de mantenimiento de réplica de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-255">It contains hello replica health states.</span></span> <span data-ttu-id="08656-256">Entrada:</span><span class="sxs-lookup"><span data-stu-id="08656-256">Input:</span></span>

* <span data-ttu-id="08656-257">Partición de hello [obligatorio] identificador (GUID) que identifica la partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-257">[Required] hello partition ID (GUID) that identifies hello partition.</span></span>
* <span data-ttu-id="08656-258">Directiva de mantenimiento de aplicación Hola [opcional] usa la directiva del manifiesto de aplicación toooverride Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-258">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="08656-259">[Opcional] Filtros de eventos y las réplicas que especifican las entradas que son de interés y se deben devolver en el resultado de hello (por ejemplo, únicamente, los errores o las advertencias y errores).</span><span class="sxs-lookup"><span data-stu-id="08656-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="08656-260">Todos los eventos y réplicas son mantenimiento de entidad agregado hello tooevaluate usado, independientemente del filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-260">All events and replicas are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="08656-261">[Opcional] Filtrar las estadísticas de estado de tooexclude.</span><span class="sxs-lookup"><span data-stu-id="08656-261">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="08656-262">Si no se especifica, muestran las estadísticas de estado de hello cuántas réplicas están en Aceptar, advertencia y error de Estados.</span><span class="sxs-lookup"><span data-stu-id="08656-262">If not specified, hello health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="08656-263">API</span><span class="sxs-lookup"><span data-stu-id="08656-263">API</span></span>
<span data-ttu-id="08656-264">estado de la partición de tooget a través de hello API, cree un `FabricClient` llamada hello y [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) método en su HealthManager.</span><span class="sxs-lookup"><span data-stu-id="08656-264">tooget partition health through hello API, create a `FabricClient` and call hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="08656-265">crear parámetros opcionales toospecify [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="08656-265">toospecify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="08656-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08656-266">PowerShell</span></span>
<span data-ttu-id="08656-267">Mantenimiento de partición de Hello cmdlet tooget hello es [ServiceFabricPartitionHealth Get](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span><span class="sxs-lookup"><span data-stu-id="08656-267">hello cmdlet tooget hello partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="08656-268">En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="08656-268">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="08656-269">Hello siguiente obtiene mantenimiento Hola para todas las particiones de hello **fabric: / WordCount/WordCountService** servicio y filtra los Estados de mantenimiento de réplica:</span><span class="sxs-lookup"><span data-stu-id="08656-269">hello following cmdlet gets hello health for all partitions of hello **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

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
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
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

### <a name="rest"></a><span data-ttu-id="08656-270">REST</span><span class="sxs-lookup"><span data-stu-id="08656-270">REST</span></span>
<span data-ttu-id="08656-271">Puede obtener el estado de la partición con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) que incluye las directivas de mantenimiento que se describe en el cuerpo de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="08656-272">Obtención del mantenimiento de réplica</span><span class="sxs-lookup"><span data-stu-id="08656-272">Get replica health</span></span>
<span data-ttu-id="08656-273">Devuelve el estado de saludo de una réplica de servicio con estado o una instancia de servicio sin estado.</span><span class="sxs-lookup"><span data-stu-id="08656-273">Returns hello health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="08656-274">Entrada:</span><span class="sxs-lookup"><span data-stu-id="08656-274">Input:</span></span>

* <span data-ttu-id="08656-275">[Obligatorio] Hola identificador (GUID) y la réplica Id. de partición que identifica la réplica de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-275">[Required] hello partition ID (GUID) and replica ID that identifies hello replica.</span></span>
* <span data-ttu-id="08656-276">Parámetros de la directiva de mantenimiento de hello [opcional] aplicación utilizan directivas de manifiesto de aplicación de Hola de toooverride.</span><span class="sxs-lookup"><span data-stu-id="08656-276">[Optional] hello application health policy parameters used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="08656-277">[Opcional] Filtros para los eventos que especifican las entradas que son de interés y se deben devolver en el resultado de hello (por ejemplo, únicamente, los errores o las advertencias y errores).</span><span class="sxs-lookup"><span data-stu-id="08656-277">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="08656-278">Todos los eventos son mantenimiento de entidad agregado hello tooevaluate usado, independientemente del filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-278">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="08656-279">API</span><span class="sxs-lookup"><span data-stu-id="08656-279">API</span></span>
<span data-ttu-id="08656-280">Mantenimiento de réplica de hello tooget a través de hello API, cree un `FabricClient` llamada hello y [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) método en su HealthManager.</span><span class="sxs-lookup"><span data-stu-id="08656-280">tooget hello replica health through hello API, create a `FabricClient` and call hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="08656-281">parámetros avanzados, uso de toospecify [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="08656-281">toospecify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="08656-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08656-282">PowerShell</span></span>
<span data-ttu-id="08656-283">el estado de réplica de Hola Hola cmdlet tooget es [ServiceFabricReplicaHealth Get](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span><span class="sxs-lookup"><span data-stu-id="08656-283">hello cmdlet tooget hello replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="08656-284">En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="08656-284">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="08656-285">Hello siguiente cmdlet obtiene Hola mantenimiento de réplica principal de Hola para todas las particiones del servicio de hello:</span><span class="sxs-lookup"><span data-stu-id="08656-285">hello following cmdlet gets hello health of hello primary replica for all partitions of hello service:</span></span>

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

### <a name="rest"></a><span data-ttu-id="08656-286">REST</span><span class="sxs-lookup"><span data-stu-id="08656-286">REST</span></span>
<span data-ttu-id="08656-287">Puede obtener el estado de réplica con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) que incluye las directivas de mantenimiento que se describe en el cuerpo de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="08656-288">Obtención del mantenimiento de la aplicación implementada</span><span class="sxs-lookup"><span data-stu-id="08656-288">Get deployed application health</span></span>
<span data-ttu-id="08656-289">Devuelve el estado de saludo de una aplicación implementada en una entidad del nodo.</span><span class="sxs-lookup"><span data-stu-id="08656-289">Returns hello health of an application deployed on a node entity.</span></span> <span data-ttu-id="08656-290">Contiene Estados de mantenimiento de paquete de servicio de hello implementado.</span><span class="sxs-lookup"><span data-stu-id="08656-290">It contains hello deployed service package health states.</span></span> <span data-ttu-id="08656-291">Entrada:</span><span class="sxs-lookup"><span data-stu-id="08656-291">Input:</span></span>

* <span data-ttu-id="08656-292">Nombre de la aplicación hello [obligatorio] (URI) y el nombre de nodo (cadena) que identifican Hola implementan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="08656-292">[Required] hello application name (URI) and node name (string) that identify hello deployed application.</span></span>
* <span data-ttu-id="08656-293">Directiva de mantenimiento de aplicación Hola [opcional] usa directivas de manifiesto de aplicación de Hola de toooverride.</span><span class="sxs-lookup"><span data-stu-id="08656-293">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="08656-294">[Opcional] Filtros de eventos y paquetes de servicio implementado que especifican las entradas que son de interés y se deben devolver en el resultado de hello (por ejemplo, únicamente, los errores o las advertencias y errores).</span><span class="sxs-lookup"><span data-stu-id="08656-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="08656-295">Todos los eventos y paquetes de servicio implementados son mantenimiento de entidad agregado hello tooevaluate usado, independientemente del filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-295">All events and deployed service packages are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="08656-296">[Opcional] Filtrar las estadísticas de estado de tooexclude.</span><span class="sxs-lookup"><span data-stu-id="08656-296">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="08656-297">Si no se especifica, las estadísticas de estado de hello mostrarán número de Hola de paquetes de servicio implementados en los Estados de mantenimiento de Aceptar, advertencia y error.</span><span class="sxs-lookup"><span data-stu-id="08656-297">If not specified, hello health statistics show hello number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="08656-298">API</span><span class="sxs-lookup"><span data-stu-id="08656-298">API</span></span>
<span data-ttu-id="08656-299">estado de hello tooget de una aplicación implementada en un nodo a través de hello API, cree un `FabricClient` llamada hello y [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) método en su HealthManager.</span><span class="sxs-lookup"><span data-stu-id="08656-299">tooget hello health of an application deployed on a node through hello API, create a `FabricClient` and call hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="08656-300">toospecify parámetros opcionales, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="08656-300">toospecify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="08656-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08656-301">PowerShell</span></span>
<span data-ttu-id="08656-302">Hola estado de la aplicación de cmdlet tooget Hola implementado es [ServiceFabricDeployedApplicationHealth Get](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="08656-302">hello cmdlet tooget hello deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="08656-303">En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="08656-303">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="08656-304">toofind out donde se implementa una aplicación, ejecutar [ServiceFabricApplicationHealth Get](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) y vistazo Hola implementa elementos secundarios de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="08656-304">toofind out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed application children.</span></span>

<span data-ttu-id="08656-305">Hello siguiente obtiene mantenimiento Hola de hello **fabric: / WordCount** aplicación implementada en **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="08656-305">hello following cmdlet gets hello health of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

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
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="08656-306">REST</span><span class="sxs-lookup"><span data-stu-id="08656-306">REST</span></span>
<span data-ttu-id="08656-307">Puede obtener el estado de la aplicación implementada con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) que incluye las directivas de mantenimiento que se describe en el cuerpo de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="08656-308">Obtención del mantenimiento del paquete de servicio implementado</span><span class="sxs-lookup"><span data-stu-id="08656-308">Get deployed service package health</span></span>
<span data-ttu-id="08656-309">Devuelve Hola estado de una entidad de paquete de servicio implementado.</span><span class="sxs-lookup"><span data-stu-id="08656-309">Returns hello health of a deployed service package entity.</span></span> <span data-ttu-id="08656-310">Entrada:</span><span class="sxs-lookup"><span data-stu-id="08656-310">Input:</span></span>

* <span data-ttu-id="08656-311">Nombre de la aplicación hello [obligatorio] (URI), nombre de nodo (cadena) y el nombre de manifiesto de servicio (cadena) que identifican Hola implementan el paquete de servicio.</span><span class="sxs-lookup"><span data-stu-id="08656-311">[Required] hello application name (URI), node name (string), and service manifest name (string) that identify hello deployed service package.</span></span>
* <span data-ttu-id="08656-312">Directiva de mantenimiento de aplicación Hola [opcional] usa la directiva del manifiesto de aplicación toooverride Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-312">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="08656-313">[Opcional] Filtros para los eventos que especifican las entradas que son de interés y se deben devolver en el resultado de hello (por ejemplo, únicamente, los errores o las advertencias y errores).</span><span class="sxs-lookup"><span data-stu-id="08656-313">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="08656-314">Todos los eventos son mantenimiento de entidad agregado hello tooevaluate usado, independientemente del filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-314">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="08656-315">API</span><span class="sxs-lookup"><span data-stu-id="08656-315">API</span></span>
<span data-ttu-id="08656-316">estado de hello tooget de un paquete de servicio implementado a través de hello API, cree un `FabricClient` llamada hello y [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) método en su HealthManager.</span><span class="sxs-lookup"><span data-stu-id="08656-316">tooget hello health of a deployed service package through hello API, create a `FabricClient` and call hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="08656-317">toospecify parámetros opcionales, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="08656-317">toospecify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="08656-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08656-318">PowerShell</span></span>
<span data-ttu-id="08656-319">Hola mantenimiento del paquete de servicio de cmdlet tooget Hola implementado es [ServiceFabricDeployedServicePackageHealth Get](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span><span class="sxs-lookup"><span data-stu-id="08656-319">hello cmdlet tooget hello deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="08656-320">En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="08656-320">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="08656-321">toosee donde se implementa una aplicación, ejecutar [ServiceFabricApplicationHealth Get](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) y ver las aplicaciones de hello implementado.</span><span class="sxs-lookup"><span data-stu-id="08656-321">toosee where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed applications.</span></span> <span data-ttu-id="08656-322">toosee que los paquetes de servicio están en una aplicación, busque en hello implementa elementos secundarios de paquete de servicio en hello [ServiceFabricDeployedApplicationHealth Get](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) salida.</span><span class="sxs-lookup"><span data-stu-id="08656-322">toosee which service packages are in an application, look at hello deployed service package children in hello [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="08656-323">Hello siguiente obtiene mantenimiento Hola de hello **WordCountServicePkg** paquete del servicio de hello **fabric: / WordCount** aplicación implementada en **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="08656-323">hello following cmdlet gets hello health of hello **WordCountServicePkg** service package of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="08656-324">entidad de Hello tiene **System.Hosting** informes para una activación correcta del paquete de servicio y punto de entrada y el registro de tipo de servicio correcta.</span><span class="sxs-lookup"><span data-stu-id="08656-324">hello entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

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
                             Description           : hello ServicePackage was activated successfully.
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
                             Description           : hello CodePackage was activated successfully.
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
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="08656-325">REST</span><span class="sxs-lookup"><span data-stu-id="08656-325">REST</span></span>
<span data-ttu-id="08656-326">Puede obtener el estado del paquete de servicio implementado con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) que incluye las directivas de mantenimiento que se describe en el cuerpo de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="08656-327">Consultas de fragmentos de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="08656-327">Health chunk queries</span></span>
<span data-ttu-id="08656-328">las consultas de fragmento de mantenimiento de Hello pueden devolver a elementos secundarios de clúster de varios niveles (recursivamente), por los filtros de entrada.</span><span class="sxs-lookup"><span data-stu-id="08656-328">hello health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="08656-329">Admite filtros avanzados que permiten una gran flexibilidad al elegir elementos secundarios de hello toobe devuelto.</span><span class="sxs-lookup"><span data-stu-id="08656-329">It supports advanced filters that allow a lot of flexibility in choosing hello children toobe returned.</span></span> <span data-ttu-id="08656-330">los filtros de Hello pueden especificar a elementos secundarios por identificador único de Hola o por otros identificadores de grupo o Estados de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="08656-330">hello filters can specify children by hello unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="08656-331">De forma predeterminada, ningún elemento secundario se incluyen, como comandos de toohealth lugar que siempre incluyen a elementos secundarios de primer nivel.</span><span class="sxs-lookup"><span data-stu-id="08656-331">By default, no children are included, as opposed toohealth commands that always include first-level children.</span></span>

<span data-ttu-id="08656-332">Hola [consultas de estado](service-fabric-view-entities-aggregated-health.md#health-queries) devueltos elementos secundarios de primer nivel sólo de hello especificado entidad por filtros necesarios.</span><span class="sxs-lookup"><span data-stu-id="08656-332">hello [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of hello specified entity per required filters.</span></span> <span data-ttu-id="08656-333">Hola tooget los elementos secundarios de elementos secundarios de hello, debe llamar a las API de estado adicional para cada entidad de interés.</span><span class="sxs-lookup"><span data-stu-id="08656-333">tooget hello children of hello children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="08656-334">De forma similar, mantenimiento de hello tooget de entidades específicas, debe llamar a mantenimiento de una API para cada entidad deseada.</span><span class="sxs-lookup"><span data-stu-id="08656-334">Similarly, tooget hello health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="08656-335">Hello fragmento consulta filtrado avanzado permite toorequest varios elementos de interés en una sola consulta, lo que minimiza el tamaño del mensaje de Hola y número de Hola de mensajes.</span><span class="sxs-lookup"><span data-stu-id="08656-335">hello chunk query advanced filtering allows you toorequest multiple items of interest in one query, minimizing hello message size and hello number of messages.</span></span>

<span data-ttu-id="08656-336">valor de Hola de consulta de fragmento de hello es que puede obtener el estado más entidades de clúster (potencialmente todas las entidades de clúster a partir de raíz necesario) en una llamada.</span><span class="sxs-lookup"><span data-stu-id="08656-336">hello value of hello chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="08656-337">Puede expresar consultas de mantenimiento complejas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="08656-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="08656-338">Devolver solo las aplicaciones con error y, para esas aplicaciones, incluir todos los servicios con advertencias o errores.</span><span class="sxs-lookup"><span data-stu-id="08656-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="08656-339">Para los servicios devueltos, incluir todas las particiones.</span><span class="sxs-lookup"><span data-stu-id="08656-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="08656-340">Devolver solo el estado de Hola de cuatro aplicaciones, especificado por sus nombres.</span><span class="sxs-lookup"><span data-stu-id="08656-340">Return only hello health of four applications, specified by their names.</span></span>
* <span data-ttu-id="08656-341">Devolver solo Hola estado de las aplicaciones de un tipo de aplicación que desee.</span><span class="sxs-lookup"><span data-stu-id="08656-341">Return only hello health of applications of a desired application type.</span></span>
* <span data-ttu-id="08656-342">Devolver todas las entidades implementadas en un nodo.</span><span class="sxs-lookup"><span data-stu-id="08656-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="08656-343">Devuelve todas las aplicaciones, todas las aplicaciones implementadas en el nodo especificado hello y todos los paquetes de servicio de hello implementado en ese nodo.</span><span class="sxs-lookup"><span data-stu-id="08656-343">Returns all applications, all deployed applications on hello specified node and all hello deployed service packages on that node.</span></span>
* <span data-ttu-id="08656-344">Devolver todas las réplicas con error.</span><span class="sxs-lookup"><span data-stu-id="08656-344">Return all replicas in error.</span></span> <span data-ttu-id="08656-345">Devuelve todas las aplicaciones, los servicios, las particiones y solo las réplicas con error.</span><span class="sxs-lookup"><span data-stu-id="08656-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="08656-346">Devolver todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="08656-346">Return all applications.</span></span> <span data-ttu-id="08656-347">Para un servicio especificado, incluir todas las particiones.</span><span class="sxs-lookup"><span data-stu-id="08656-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="08656-348">Actualmente, la consulta de fragmento de mantenimiento de Hola se expone solo para la entidad de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-348">Currently, hello health chunk query is exposed only for hello cluster entity.</span></span> <span data-ttu-id="08656-349">Devuelve un fragmento de estado del clúster, que contiene:</span><span class="sxs-lookup"><span data-stu-id="08656-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="08656-350">estado de mantenimiento de clúster agregado Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-350">hello cluster aggregated health state.</span></span>
* <span data-ttu-id="08656-351">lista de fragmento del estado de mantenimiento Hola de nodos que respeta los filtros de entrada.</span><span class="sxs-lookup"><span data-stu-id="08656-351">hello health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="08656-352">lista de fragmento del estado de mantenimiento Hola de aplicaciones que respetan los filtros de entrada.</span><span class="sxs-lookup"><span data-stu-id="08656-352">hello health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="08656-353">Cada fragmento de estado de mantenimiento de aplicación contiene una lista de fragmentos con todos los servicios que respetan los filtros de entrada y una lista de fragmentos con todas las aplicaciones implementadas que respeta los filtros de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect hello filters.</span></span> <span data-ttu-id="08656-354">Igual para los elementos secundarios de hello de servicios y las aplicaciones implementadas.</span><span class="sxs-lookup"><span data-stu-id="08656-354">Same for hello children of services and deployed applications.</span></span> <span data-ttu-id="08656-355">De esta manera, todas las entidades de clúster de hello pueden devolverse potencialmente si solicita de forma jerárquica.</span><span class="sxs-lookup"><span data-stu-id="08656-355">This way, all entities in hello cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="08656-356">Consulta de fragmentos de mantenimiento del clúster</span><span class="sxs-lookup"><span data-stu-id="08656-356">Cluster health chunk query</span></span>
<span data-ttu-id="08656-357">Devuelve Hola mantenimiento de entidad de clúster de Hola y contiene fragmentos de estado de mantenimiento jerárquica Hola de los elementos secundarios necesarios.</span><span class="sxs-lookup"><span data-stu-id="08656-357">Returns hello health of hello cluster entity and contains hello hierarchical health state chunks of required children.</span></span> <span data-ttu-id="08656-358">Entrada:</span><span class="sxs-lookup"><span data-stu-id="08656-358">Input:</span></span>

* <span data-ttu-id="08656-359">Directiva de mantenimiento de clúster [opcional] Hola utiliza nodos de hello tooevaluate y eventos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-359">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="08656-360">Asignación de directiva de mantenimiento de aplicación Hola [opcional], con las directivas de mantenimiento de hello usa directivas de manifiesto de aplicación de Hola de toooverride.</span><span class="sxs-lookup"><span data-stu-id="08656-360">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="08656-361">[Opcional] Filtros para los nodos y las aplicaciones que especifican las entradas que son de interés y se deben devolver en el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="08656-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in hello result.</span></span> <span data-ttu-id="08656-362">Hola filtros son tooan específico/grupo de entidad de entidades o entidades tooall aplicables en ese nivel.</span><span class="sxs-lookup"><span data-stu-id="08656-362">hello filters are specific tooan entity/group of entities or are applicable tooall entities at that level.</span></span> <span data-ttu-id="08656-363">lista de Hola de filtros puede contener un filtro general o filtros para entidades de toofine detalle específico de identificadores devueltos por la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-363">hello list of filters can contain one general filter and/or filters for specific identifiers toofine-grain entities returned by hello query.</span></span> <span data-ttu-id="08656-364">Si está vacío, no se devuelven los elementos secundarios de Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="08656-364">If empty, hello children are not returned by default.</span></span>
  <span data-ttu-id="08656-365">Obtenga más información sobre filtros de hello en [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) y [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span><span class="sxs-lookup"><span data-stu-id="08656-365">Read more about hello filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="08656-366">recursivamente de Hello aplicación filtros puede especificar filtros avanzados para los elementos secundarios.</span><span class="sxs-lookup"><span data-stu-id="08656-366">hello application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="08656-367">resultado del fragmento de Hello incluye a los elementos secundarios de hello respetan los filtros de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-367">hello chunk result includes hello children that respect hello filters.</span></span>

<span data-ttu-id="08656-368">Actualmente, consulta de fragmento de hello no devolver evaluaciones en mal estado o los eventos de la entidad.</span><span class="sxs-lookup"><span data-stu-id="08656-368">Currently, hello chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="08656-369">Esa información adicional se puede obtener mediante la consulta del estado de clúster existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-369">That extra information can be obtained using hello existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="08656-370">API</span><span class="sxs-lookup"><span data-stu-id="08656-370">API</span></span>
<span data-ttu-id="08656-371">estado del clúster tooget los fragmentos, cree un `FabricClient` llamada hello y [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) método en su **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="08656-371">tooget cluster health chunk, create a `FabricClient` and call hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="08656-372">Se puede pasar en [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) las directivas de mantenimiento de toodescribe y filtros avanzados.</span><span class="sxs-lookup"><span data-stu-id="08656-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe health policies and advanced filters.</span></span>

<span data-ttu-id="08656-373">Hello código siguiente obtiene fragmentos de mantenimiento de clúster con filtros avanzados.</span><span class="sxs-lookup"><span data-stu-id="08656-373">hello following code gets cluster health chunk with advanced filters.</span></span>

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

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="08656-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08656-374">PowerShell</span></span>
<span data-ttu-id="08656-375">es el estado de clúster de Hola Hola cmdlet tooget [ServiceFabricClusterChunkHealth Get](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span><span class="sxs-lookup"><span data-stu-id="08656-375">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="08656-376">En primer lugar, conectar toohello clúster mediante el uso de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="08656-376">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="08656-377">Hello código siguiente obtiene nodos solo si están en Error excepto para un nodo específico, que siempre se debe devolver.</span><span class="sxs-lookup"><span data-stu-id="08656-377">hello following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
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

<span data-ttu-id="08656-378">Hola siguiendo el cmdlet obtiene fragmentos de clúster con los filtros de aplicación.</span><span class="sxs-lookup"><span data-stu-id="08656-378">hello following cmdlet gets cluster chunk with application filters.</span></span>

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

<span data-ttu-id="08656-379">Hello siguiente cmdlet devuelve implementadas todas las entidades en un nodo.</span><span class="sxs-lookup"><span data-stu-id="08656-379">hello following cmdlet returns all deployed entities on a node.</span></span>

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

### <a name="rest"></a><span data-ttu-id="08656-380">REST</span><span class="sxs-lookup"><span data-stu-id="08656-380">REST</span></span>
<span data-ttu-id="08656-381">Puede obtener el fragmento de estado del clúster con un [solicitud GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) o un [solicitud POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) que incluye las directivas de mantenimiento y los filtros avanzados se describe en el cuerpo de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in hello body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="08656-382">Consultas generales</span><span class="sxs-lookup"><span data-stu-id="08656-382">General queries</span></span>
<span data-ttu-id="08656-383">Las consultas generales devuelven una lista de entidades de Service Fabric de un tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="08656-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="08656-384">Estas propiedades se exponen a través de la API de hello (mediante los métodos de hello en **FabricClient.QueryManager**), cmdlets de PowerShell y REST.</span><span class="sxs-lookup"><span data-stu-id="08656-384">They are exposed through hello API (via hello methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="08656-385">Estas consultas agregan subconsultas de varios componentes.</span><span class="sxs-lookup"><span data-stu-id="08656-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="08656-386">Uno de ellos es hello [almacén de estado](service-fabric-health-introduction.md#health-store), que rellena Hola agrega el estado de mantenimiento para cada resultado de la consulta.</span><span class="sxs-lookup"><span data-stu-id="08656-386">One of them is hello [health store](service-fabric-health-introduction.md#health-store), which populates hello aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="08656-387">Consultas generales devuelven Hola agregado el estado de entidad de hello y no contienen datos de estado enriquecido.</span><span class="sxs-lookup"><span data-stu-id="08656-387">General queries return hello aggregated health state of hello entity and do not contain rich health data.</span></span> <span data-ttu-id="08656-388">Si una entidad no es correcto, puede seguir con estado consultas tooget toda su información de estado, incluidos los eventos y Estados de mantenimiento de secundarios, evaluaciones en mal estado.</span><span class="sxs-lookup"><span data-stu-id="08656-388">If an entity is not healthy, you can follow up with health queries tooget all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="08656-389">Si las consultas generales devuelven un estado desconocido para una entidad, es posible que ese almacén de estado de hello no tiene datos completos sobre la entidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-389">If general queries return an unknown health state for an entity, it's possible that hello health store doesn't have complete data about hello entity.</span></span> <span data-ttu-id="08656-390">También es posible que un almacén de estado de subconsulta toohello no era correcta (por ejemplo, se produjo un error de comunicación o se limitó el almacén de estado de hello).</span><span class="sxs-lookup"><span data-stu-id="08656-390">It's also possible that a subquery toohello health store wasn't successful (for example, there was a communication error, or hello health store was throttled).</span></span> <span data-ttu-id="08656-391">Realizar un seguimiento con una consulta de estado de entidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-391">Follow up with a health query for hello entity.</span></span> <span data-ttu-id="08656-392">Si la subconsulta Hola detectó errores transitorios, como problemas de red, es posible que pueda realizar esta consulta de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="08656-392">If hello subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="08656-393">Pueden también proporcionan más detalles de hello health store sobre por qué no se expone la entidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-393">It may also give you more details from hello health store about why hello entity is not exposed.</span></span>

<span data-ttu-id="08656-394">Hola las consultas que contienen **HealthState** para las entidades son:</span><span class="sxs-lookup"><span data-stu-id="08656-394">hello queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="08656-395">Lista de nodos: devuelve nodos de la lista de hello en clúster hello (paginado).</span><span class="sxs-lookup"><span data-stu-id="08656-395">Node list: Returns hello list nodes in hello cluster (paged).</span></span>
  * <span data-ttu-id="08656-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="08656-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="08656-397">PowerShell: Get-ServiceFabricNode.</span><span class="sxs-lookup"><span data-stu-id="08656-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="08656-398">Lista de aplicaciones: devuelve una lista de aplicaciones en clúster de hello (paginado) Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-398">Application list: Returns hello list of applications in hello cluster (paged).</span></span>
  * <span data-ttu-id="08656-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="08656-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="08656-400">PowerShell: Get-ServiceFabricApplication.</span><span class="sxs-lookup"><span data-stu-id="08656-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="08656-401">Lista de servicios: devuelve la lista de hello de servicios en una aplicación (paginado).</span><span class="sxs-lookup"><span data-stu-id="08656-401">Service list: Returns hello list of services in an application (paged).</span></span>
  * <span data-ttu-id="08656-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="08656-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="08656-403">PowerShell: Get-ServiceFabricService.</span><span class="sxs-lookup"><span data-stu-id="08656-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="08656-404">Lista de particiones: devuelve la lista de Hola de particiones en un servicio (paginado).</span><span class="sxs-lookup"><span data-stu-id="08656-404">Partition list: Returns hello list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="08656-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="08656-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="08656-406">PowerShell: Get-ServiceFabricPartition.</span><span class="sxs-lookup"><span data-stu-id="08656-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="08656-407">La lista de réplicas: devuelve la lista de Hola de réplicas de una partición (paginado).</span><span class="sxs-lookup"><span data-stu-id="08656-407">Replica list: Returns hello list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="08656-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="08656-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="08656-409">PowerShell: Get-ServiceFabricReplica.</span><span class="sxs-lookup"><span data-stu-id="08656-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="08656-410">Implementa la lista de aplicaciones: devuelve una lista de las aplicaciones implementadas en un nodo Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-410">Deployed application list: Returns hello list of deployed applications on a node.</span></span>
  * <span data-ttu-id="08656-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="08656-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="08656-412">PowerShell: Get-ServiceFabricDeployedApplication.</span><span class="sxs-lookup"><span data-stu-id="08656-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="08656-413">Implementa lista de paquetes de servicio: devuelve una lista de paquetes de servicio en una aplicación implementada Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-413">Deployed service package list: Returns hello list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="08656-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="08656-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="08656-415">PowerShell: Get-ServiceFabricDeployedApplication.</span><span class="sxs-lookup"><span data-stu-id="08656-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="08656-416">Algunas de las consultas de hello devuelven resultados paginados.</span><span class="sxs-lookup"><span data-stu-id="08656-416">Some of hello queries return paged results.</span></span> <span data-ttu-id="08656-417">Hello devuelto de estas consultas es una lista que se deriva de [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span><span class="sxs-lookup"><span data-stu-id="08656-417">hello return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="08656-418">Si los resultados de hello no ajustan a un mensaje, se devuelve solo una página y un ContinuationToken que realiza un seguimiento de dónde ha detenido la enumeración.</span><span class="sxs-lookup"><span data-stu-id="08656-418">If hello results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="08656-419">Continuar toocall Hola igual de consulta y pase un token de continuación de Hola de hello anterior tooget siguientes resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="08656-419">Continue toocall hello same query and pass in hello continuation token from hello previous query tooget next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="08656-420">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="08656-420">Examples</span></span>
<span data-ttu-id="08656-421">Hello código siguiente obtiene aplicaciones en mal estado hello en clúster de hello:</span><span class="sxs-lookup"><span data-stu-id="08656-421">hello following code gets hello unhealthy applications in hello cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="08656-422">Hello siguiente cmdlet obtiene los detalles de la aplicación hello para el tejido de hello: / aplicación WordCount.</span><span class="sxs-lookup"><span data-stu-id="08656-422">hello following cmdlet gets hello application details for hello fabric:/WordCount application.</span></span> <span data-ttu-id="08656-423">Observe que el estado de mantenimiento está en advertencia.</span><span class="sxs-lookup"><span data-stu-id="08656-423">Notice that health state is at warning.</span></span>

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

<span data-ttu-id="08656-424">Hello siguiente cmdlet obtiene servicios Hola con un estado de error:</span><span class="sxs-lookup"><span data-stu-id="08656-424">hello following cmdlet gets hello services with a health state of error:</span></span>

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

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="08656-425">Actualización de clústeres y aplicaciones</span><span class="sxs-lookup"><span data-stu-id="08656-425">Cluster and application upgrades</span></span>
<span data-ttu-id="08656-426">Durante una actualización supervisada de clúster de Hola y de aplicación, Service Fabric comprueba tooensure de mantenimiento que todo es correcto.</span><span class="sxs-lookup"><span data-stu-id="08656-426">During a monitored upgrade of hello cluster and application, Service Fabric checks health tooensure that everything remains healthy.</span></span> <span data-ttu-id="08656-427">Si una entidad está en mal estada según se ha evaluado mediante el uso de las directivas de mantenimiento configurada, actualización Hola aplica siguiente acción de directivas específicas de la actualización toodetermine Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-427">If an entity is unhealthy as evaluated by using configured health policies, hello upgrade applies upgrade-specific policies toodetermine hello next action.</span></span> <span data-ttu-id="08656-428">actualización de Hello puede ser tooallow en pausa interacción del usuario (por ejemplo, corregir las condiciones de error o cambiar las directivas) o lo puede revierten automáticamente toohello de versión anterior válida.</span><span class="sxs-lookup"><span data-stu-id="08656-428">hello upgrade may be paused tooallow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back toohello previous good version.</span></span>

<span data-ttu-id="08656-429">Durante una *clúster* actualización, puede obtener estado de actualización de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-429">During a *cluster* upgrade, you can get hello cluster upgrade status.</span></span> <span data-ttu-id="08656-430">estado de actualización de Hello incluye evaluaciones en mal estado, qué toowhat punto está en mal estado en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-430">hello upgrade status includes unhealthy evaluations, which point toowhat is unhealthy in hello cluster.</span></span> <span data-ttu-id="08656-431">Si se revierte la actualización Hola debido a problemas de toohealth, estado de actualización de hello recuerda a motivos de mal estado último Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-431">If hello upgrade is rolled back due toohealth issues, hello upgrade status remembers hello last unhealthy reasons.</span></span> <span data-ttu-id="08656-432">Esta información puede ayudar a los administradores a investigar qué salió mal después de la actualización de hello revertido o detenido.</span><span class="sxs-lookup"><span data-stu-id="08656-432">This information can help administrators investigate what went wrong after hello upgrade rolled back or stopped.</span></span>

<span data-ttu-id="08656-433">De forma similar, durante un *aplicación* actualización, las evaluaciones en mal estado se encuentran en estado de actualización de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in hello application upgrade status.</span></span>

<span data-ttu-id="08656-434">Hello siguiente muestra estado de actualización de aplicación Hola de un tejido modificado: / aplicación WordCount.</span><span class="sxs-lookup"><span data-stu-id="08656-434">hello following shows hello application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="08656-435">Un guardián ha informado de un error en una de sus réplicas.</span><span class="sxs-lookup"><span data-stu-id="08656-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="08656-436">actualización de Hello es gradual porque no se respeten la hello las comprobaciones de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="08656-436">hello upgrade is rolling back because hello health checks are not respected.</span></span>

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

<span data-ttu-id="08656-437">Obtener más información acerca de hello [actualización de la aplicación de Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="08656-437">Read more about hello [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-tootroubleshoot"></a><span data-ttu-id="08656-438">Usar tootroubleshoot de evaluaciones de estado</span><span class="sxs-lookup"><span data-stu-id="08656-438">Use health evaluations tootroubleshoot</span></span>
<span data-ttu-id="08656-439">Siempre que haya un problema con el clúster de Hola o una aplicación, mire toopinpoint de mantenimiento de clúster o una aplicación Hola cuál es el problema.</span><span class="sxs-lookup"><span data-stu-id="08656-439">Whenever there is an issue with hello cluster or an application, look at hello cluster or application health toopinpoint what is wrong.</span></span> <span data-ttu-id="08656-440">evaluaciones en mal estado Hola proporcionan detalles sobre qué Hola desencadenadas mal estado actual.</span><span class="sxs-lookup"><span data-stu-id="08656-440">hello unhealthy evaluations provide details about what triggered hello current unhealthy state.</span></span> <span data-ttu-id="08656-441">Si necesita, puede profundizar en mal estado secundario entidades tooidentify Hola causa.</span><span class="sxs-lookup"><span data-stu-id="08656-441">If you need to, you can drill down into unhealthy child entities tooidentify hello root cause.</span></span>

<span data-ttu-id="08656-442">Por ejemplo, considere una aplicación con un estado incorrecto porque hay un informe de errores en una de sus réplicas.</span><span class="sxs-lookup"><span data-stu-id="08656-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="08656-443">Hello siguiente cmdlet de Powershell muestra evaluaciones en mal estado hello:</span><span class="sxs-lookup"><span data-stu-id="08656-443">hello following Powershell cmdlet shows hello unhealthy evaluations:</span></span>

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

<span data-ttu-id="08656-444">Puede mirar Hola réplica tooget obtener más información:</span><span class="sxs-lookup"><span data-stu-id="08656-444">You can look at hello replica tooget more information:</span></span>

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
> <span data-ttu-id="08656-445">Hello evaluaciones en mal estado Mostrar hello primer motivo Hola entidad es evalúa toocurrent estado de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="08656-445">hello unhealthy evaluations show hello first reason hello entity is evaluated toocurrent health state.</span></span> <span data-ttu-id="08656-446">Puede haber varios otros eventos que desencadenan este estado, pero no se reflejan en las evaluaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-446">There may be multiple other events that trigger this state, but they are not be reflected in hello evaluations.</span></span> <span data-ttu-id="08656-447">tooget obtener más información, explorar en profundidad en hello mantenimiento entidades toofigure todos los informes de hello incorrecto en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="08656-447">tooget more information, drill down into hello health entities toofigure out all hello unhealthy reports in hello cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="08656-448">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="08656-448">Next steps</span></span>
[<span data-ttu-id="08656-449">Usar tootroubleshoot de informes de estado de sistema</span><span class="sxs-lookup"><span data-stu-id="08656-449">Use system health reports tootroubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="08656-450">Incorporación de informes de mantenimiento de Service Fabric personalizados</span><span class="sxs-lookup"><span data-stu-id="08656-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="08656-451">¿Cómo tooreport y comprobación de estado de servicio</span><span class="sxs-lookup"><span data-stu-id="08656-451">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="08656-452">Supervisión y diagnóstico de los servicios localmente</span><span class="sxs-lookup"><span data-stu-id="08656-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="08656-453">Actualización de la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="08656-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
