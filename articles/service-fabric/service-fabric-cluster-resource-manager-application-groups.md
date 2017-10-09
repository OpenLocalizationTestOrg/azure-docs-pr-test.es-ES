---
title: "aaaService Administrador de recursos de clúster de tejido - grupos de aplicaciones | Documentos de Microsoft"
description: "Información general sobre la funcionalidad de grupo de aplicaciones en el servicio Administrador de recursos del clúster de tejido de Hola Hola"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a><span data-ttu-id="dad0c-103">Introducción tooApplication grupos</span><span class="sxs-lookup"><span data-stu-id="dad0c-103">Introduction tooApplication Groups</span></span>
<span data-ttu-id="dad0c-104">Administrador de recursos del clúster de Service Fabric normalmente administra los recursos del clúster al repartir la carga de hello (representar mediante [métricas](service-fabric-cluster-resource-manager-metrics.md)) uniformemente a lo largo de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="dad0c-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading hello load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout hello cluster.</span></span> <span data-ttu-id="dad0c-105">Service Fabric administra la capacidad de Hola de nodos Hola Hola y Hola clúster como un todo a través de [capacidad](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="dad0c-105">Service Fabric manages hello capacity of hello nodes in hello cluster and hello cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span></span> <span data-ttu-id="dad0c-106">Las métricas y la capacidad funcionan muy bien con muchas cargas de trabajo diferentes, pero patrones que hacen un uso intensivo de diferentes instancias de aplicación de Service Fabric en ocasiones introducen requisitos adicionales.</span><span class="sxs-lookup"><span data-stu-id="dad0c-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span></span> <span data-ttu-id="dad0c-107">Por ejemplo, puede que desee:</span><span class="sxs-lookup"><span data-stu-id="dad0c-107">For example you may want to:</span></span>

- <span data-ttu-id="dad0c-108">Reservar cierta capacidad en nodos de hello en clúster de Hola para los servicios de hello en alguna instancia de aplicación con nombre</span><span class="sxs-lookup"><span data-stu-id="dad0c-108">Reserve some capacity on hello nodes in hello cluster for hello services within some named application instance</span></span>
- <span data-ttu-id="dad0c-109">Limitar Hola número total de nodos que se ejecutan servicios de hello dentro de una instancia con nombre de aplicación en (en lugar de distribuirlos de forma horizontal en clúster completo hello)</span><span class="sxs-lookup"><span data-stu-id="dad0c-109">Limit hello total number of nodes that hello services within a named application instance run on (instead of spreading them out over hello entire cluster)</span></span>
- <span data-ttu-id="dad0c-110">Definir las capacidades en la propia instancia de aplicación con nombre hello número de Hola de toolimit servicios o total del consumo de recursos de servicios de hello en él</span><span class="sxs-lookup"><span data-stu-id="dad0c-110">Define capacities on hello named application instance itself toolimit hello number of services or total resource consumption of hello services inside it</span></span>

<span data-ttu-id="dad0c-111">toomeet estos requisitos, Hola, Administrador de recursos de clúster de tejido de servicio admite una característica denominada grupos de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="dad0c-111">toomeet these requirements, hello Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span></span>

## <a name="limiting-hello-maximum-number-of-nodes"></a><span data-ttu-id="dad0c-112">Limitar el número máximo de Hola de nodos</span><span class="sxs-lookup"><span data-stu-id="dad0c-112">Limiting hello maximum number of nodes</span></span>
<span data-ttu-id="dad0c-113">caso de uso más simple de Hola de capacidad de la aplicación es cuando una instancia de la aplicación necesita toobe limitado tooa cierto número máximo de nodos.</span><span class="sxs-lookup"><span data-stu-id="dad0c-113">hello simplest use case for Application capacity is when an application instance needs toobe limited tooa certain maximum number of nodes.</span></span> <span data-ttu-id="dad0c-114">Todos los servicios dentro de esa instancia de aplicación se consolidan en un número establecido de máquinas.</span><span class="sxs-lookup"><span data-stu-id="dad0c-114">This consolidates all services within that application instance onto a set number of machines.</span></span> <span data-ttu-id="dad0c-115">Consolidación es útil cuando está tratando de toopredict o limitar el uso de los recursos físicos por servicios de hello en esa instancia con nombre de aplicación.</span><span class="sxs-lookup"><span data-stu-id="dad0c-115">Consolidation is useful when you're trying toopredict or cap physical resource use by hello services within that named application instance.</span></span> 

<span data-ttu-id="dad0c-116">Hello siguiente imagen muestra una instancia de la aplicación con y sin un número máximo de nodos definidos:</span><span class="sxs-lookup"><span data-stu-id="dad0c-116">hello following image shows an application instance with and without a maximum number of nodes defined:</span></span>

<span data-ttu-id="dad0c-117"><center>
![Definición del número máximo de nodos para la instancia de aplicación][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="dad0c-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span></span>

<span data-ttu-id="dad0c-118">En el ejemplo de Hola a izquierda, aplicación hello no tiene un número máximo de nodos definidos y tiene tres servicios.</span><span class="sxs-lookup"><span data-stu-id="dad0c-118">In hello left example, hello application doesn’t have a maximum number of nodes defined, and it has three services.</span></span> <span data-ttu-id="dad0c-119">Hola, Administrador de recursos del clúster se reparten todas las réplicas a través de seis nodos disponibles tooachieve Hola mejor equilibrio en clúster de hello (comportamiento predeterminado de Hola).</span><span class="sxs-lookup"><span data-stu-id="dad0c-119">hello Cluster Resource Manager has spread out all replicas across six available nodes tooachieve hello best balance in hello cluster (hello default behavior).</span></span> <span data-ttu-id="dad0c-120">En el ejemplo de Hola a derecha, vemos Hola misma aplicación limitada toothree nodos.</span><span class="sxs-lookup"><span data-stu-id="dad0c-120">In hello right example, we see hello same application limited toothree nodes.</span></span>

<span data-ttu-id="dad0c-121">parámetro de Hola que controla este comportamiento se denomina MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="dad0c-121">hello parameter that controls this behavior is called MaximumNodes.</span></span> <span data-ttu-id="dad0c-122">Este parámetro se puede establecer durante la creación de la aplicación, o actualizarse con una instancia de la aplicación que ya se estaba ejecutando.</span><span class="sxs-lookup"><span data-stu-id="dad0c-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span></span>

<span data-ttu-id="dad0c-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dad0c-123">Powershell</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

<span data-ttu-id="dad0c-124">C#</span><span class="sxs-lookup"><span data-stu-id="dad0c-124">C#</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

<span data-ttu-id="dad0c-125">En el conjunto de Hola de nodos, Hola, Administrador de recursos del clúster no garantiza qué objetos de servicio se asignarán juntos o qué nodos se usan.</span><span class="sxs-lookup"><span data-stu-id="dad0c-125">Within hello set of nodes, hello Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span></span>

## <a name="application-metrics-load-and-capacity"></a><span data-ttu-id="dad0c-126">Métrica, carga y capacidad de aplicación</span><span class="sxs-lookup"><span data-stu-id="dad0c-126">Application Metrics, Load, and Capacity</span></span>
<span data-ttu-id="dad0c-127">Grupos de aplicaciones le permiten métricas de toodefine asociadas a una instancia de aplicación con nombre determinada y la capacidad de la instancia de esa aplicación para esas métricas.</span><span class="sxs-lookup"><span data-stu-id="dad0c-127">Application Groups also allow you toodefine metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span></span> <span data-ttu-id="dad0c-128">Las métricas de aplicación permiten tootrack, reserva y limitar el consumo de recursos de servicios de hello dentro de esa instancia de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="dad0c-128">Application metrics allow you tootrack, reserve, and limit hello resource consumption of hello services inside that application instance.</span></span>

<span data-ttu-id="dad0c-129">En cada métrica de la aplicación, hay dos valores que se pueden establecer:</span><span class="sxs-lookup"><span data-stu-id="dad0c-129">For each application metric, there are two values that can be set:</span></span>

- <span data-ttu-id="dad0c-130">**Total de capacidad de la aplicación** : esta opción representa la capacidad total de Hola de aplicación hello para una métrica concreta.</span><span class="sxs-lookup"><span data-stu-id="dad0c-130">**Total Application Capacity** – This setting represents hello total capacity of hello application for a particular metric.</span></span> <span data-ttu-id="dad0c-131">Hola, Administrador de recursos del clúster no permite la creación de hello de los nuevos servicios en la instancia de aplicación que puede provocar que la carga total tooexceed este valor.</span><span class="sxs-lookup"><span data-stu-id="dad0c-131">hello Cluster Resource Manager disallows hello creation of any new services within this application instance that would cause total load tooexceed this value.</span></span> <span data-ttu-id="dad0c-132">Por ejemplo, supongamos que tuviera una capacidad de 10 de instancia de la aplicación hello y ya tenía la carga de cinco.</span><span class="sxs-lookup"><span data-stu-id="dad0c-132">For example, let's say hello application instance had a capacity of 10 and already had load of five.</span></span> <span data-ttu-id="dad0c-133">creación de Hello de un servicio con una carga total predeterminado de 10 circunstancias no está permitida.</span><span class="sxs-lookup"><span data-stu-id="dad0c-133">hello creation of a service with a total default load of 10 would be disallowed.</span></span>
- <span data-ttu-id="dad0c-134">**Capacidad máxima de nodo** : esta configuración especifica la carga total máxima de hello para la aplicación hello en un único nodo.</span><span class="sxs-lookup"><span data-stu-id="dad0c-134">**Maximum Node Capacity** – This setting specifies hello maximum total load for hello application on a single node.</span></span> <span data-ttu-id="dad0c-135">Si carga supera esta capacidad, Hola, Administrador de recursos de clúster mueve nodos de tooother de réplicas para que reduzca la hello carga.</span><span class="sxs-lookup"><span data-stu-id="dad0c-135">If load goes over this capacity, hello Cluster Resource Manager moves replicas tooother nodes so that hello load decreases.</span></span>


<span data-ttu-id="dad0c-136">Powershell:</span><span class="sxs-lookup"><span data-stu-id="dad0c-136">Powershell:</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

<span data-ttu-id="dad0c-137">C#:</span><span class="sxs-lookup"><span data-stu-id="dad0c-137">C#:</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a><span data-ttu-id="dad0c-138">Reserva de capacidad</span><span class="sxs-lookup"><span data-stu-id="dad0c-138">Reserving Capacity</span></span>
<span data-ttu-id="dad0c-139">Otro uso común para los grupos de aplicaciones es tooensure que recursos dentro de Hola clúster están reservados para una instancia de aplicación determinada.</span><span class="sxs-lookup"><span data-stu-id="dad0c-139">Another common use for application groups is tooensure that resources within hello cluster are reserved for a given application instance.</span></span> <span data-ttu-id="dad0c-140">Cuando se crea la instancia de la aplicación hello, se reserva siempre Hola espacio.</span><span class="sxs-lookup"><span data-stu-id="dad0c-140">hello space is always reserved when hello application instance is created.</span></span>

<span data-ttu-id="dad0c-141">La reserva de espacio en el clúster de hello para la aplicación hello ocurre inmediatamente, incluso cuando:</span><span class="sxs-lookup"><span data-stu-id="dad0c-141">Reserving space in hello cluster for hello application happens immediately even when:</span></span>
- <span data-ttu-id="dad0c-142">instancia de la aplicación Hello se ha creado pero aún no tiene ningún servicio dentro de él</span><span class="sxs-lookup"><span data-stu-id="dad0c-142">hello application instance is created but doesn't have any services within it yet</span></span>
- <span data-ttu-id="dad0c-143">número de Hello de servicios dentro de la instancia de la aplicación hello cambia cada vez</span><span class="sxs-lookup"><span data-stu-id="dad0c-143">hello number of services within hello application instance changes every time</span></span> 
- <span data-ttu-id="dad0c-144">Servicios de Hello existen pero no están consumiendo recursos Hola</span><span class="sxs-lookup"><span data-stu-id="dad0c-144">hello services exist but aren't consuming hello resources</span></span> 

<span data-ttu-id="dad0c-145">Para reservar recursos para una instancia de aplicación, es necesario especificar dos parámetros adicionales: *MinimumNodes* y *NodeReservationCapacity* .</span><span class="sxs-lookup"><span data-stu-id="dad0c-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span></span>

- <span data-ttu-id="dad0c-146">**MinimumNodes** -define el número mínimo de Hola de nodos que Hola aplicación instancia debe ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="dad0c-146">**MinimumNodes** - Defines hello minimum number of nodes that hello application instance should run on.</span></span>  
- <span data-ttu-id="dad0c-147">**NodeReservationCapacity** -esta configuración es por métrica para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="dad0c-147">**NodeReservationCapacity** - This setting is per metric for hello application.</span></span> <span data-ttu-id="dad0c-148">valor de Hello es la cantidad de Hola de esa métrica reservada para la aplicación hello en cualquier nodo en los que se Hola servicios en ejecución de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dad0c-148">hello value is hello amount of that metric reserved for hello application on any node where that hello services in that application run.</span></span>

<span data-ttu-id="dad0c-149">Combinar **MinimumNodes** y **NodeReservationCapacity** garantiza una reserva de carga mínima para la aplicación hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="dad0c-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for hello application within hello cluster.</span></span> <span data-ttu-id="dad0c-150">Si hay menos restantes capacidad en Hola de clúster que reserva total Hola necesaria, se produce un error en la creación de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="dad0c-150">If there's less remaining capacity in hello cluster than hello total reservation required, creation of hello application fails.</span></span> 

<span data-ttu-id="dad0c-151">Veamos un ejemplo de la reserva de capacidad:</span><span class="sxs-lookup"><span data-stu-id="dad0c-151">Let's look at an example of capacity reservation:</span></span>

<span data-ttu-id="dad0c-152"><center>
![Definición de la capacidad reservada para la instancia de aplicación][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="dad0c-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span></span>

<span data-ttu-id="dad0c-153">En el ejemplo de Hola a izquierda, las aplicaciones no tiene ninguna capacidad de aplicación definida.</span><span class="sxs-lookup"><span data-stu-id="dad0c-153">In hello left example, applications do not have any Application Capacity defined.</span></span> <span data-ttu-id="dad0c-154">Hola, Administrador de recursos del clúster equilibra todos los elementos según las reglas de toonormal.</span><span class="sxs-lookup"><span data-stu-id="dad0c-154">hello Cluster Resource Manager balances everything according toonormal rules.</span></span>

<span data-ttu-id="dad0c-155">En el ejemplo de Hola en hello derecho, supongamos que Application1 se creó con hello después de configuración:</span><span class="sxs-lookup"><span data-stu-id="dad0c-155">In hello example on hello right, let's say that Application1 was created with hello following settings:</span></span>

- <span data-ttu-id="dad0c-156">MinimumNodes establecer tootwo</span><span class="sxs-lookup"><span data-stu-id="dad0c-156">MinimumNodes set tootwo</span></span>
- <span data-ttu-id="dad0c-157">Una aplicación métrica definida con</span><span class="sxs-lookup"><span data-stu-id="dad0c-157">An application Metric defined with</span></span>
  - <span data-ttu-id="dad0c-158">NodeReservationCapacity de 20</span><span class="sxs-lookup"><span data-stu-id="dad0c-158">NodeReservationCapacity of 20</span></span>

<span data-ttu-id="dad0c-159">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dad0c-159">Powershell</span></span>

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

<span data-ttu-id="dad0c-160">C#</span><span class="sxs-lookup"><span data-stu-id="dad0c-160">C#</span></span>

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

<span data-ttu-id="dad0c-161">Service Fabric reserva capacidad en dos nodos para Application1 y no permite los servicios de Application2 tooconsume esa capacidad incluso si no hay que ninguna carga utilizada por servicios de hello dentro Application1 en tiempo de presentación.</span><span class="sxs-lookup"><span data-stu-id="dad0c-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 tooconsume that capacity even if there are no load is being consumed by hello services inside Application1 at hello time.</span></span> <span data-ttu-id="dad0c-162">Se considera que esta capacidad reservada aplicación consumido y se descuenta de hello capacidad en ese nodo y en clúster de hello restante.</span><span class="sxs-lookup"><span data-stu-id="dad0c-162">This reserved application capacity is considered consumed  and counts against hello remaining capacity on that node and within hello cluster.</span></span>  <span data-ttu-id="dad0c-163">reserva de Hola se deduce de hello restantes capacidad clúster inmediatamente, pero Hola reservado consumo se deduce del capacidad Hola de un nodo específico solo cuando al menos un servicio se ponen en él.</span><span class="sxs-lookup"><span data-stu-id="dad0c-163">hello reservation is deducted from hello remaining cluster capacity immediately, however hello reserved consumption is deducted from hello capacity of a specific node only when at least one service object is placed on it.</span></span> <span data-ttu-id="dad0c-164">Esta reserva posterior permite flexibilidad y una mejor utilización de recursos, ya que solo se reservan recursos en nodos cuando resulta necesario.</span><span class="sxs-lookup"><span data-stu-id="dad0c-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span></span>

## <a name="obtaining-hello-application-load-information"></a><span data-ttu-id="dad0c-165">Obtener información de carga de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="dad0c-165">Obtaining hello application load information</span></span>
<span data-ttu-id="dad0c-166">Para cada aplicación que tiene una capacidad de aplicación definidos para una o varias métricas puede obtener información de hello acerca de la carga global Hola notificado por las réplicas de sus servicios.</span><span class="sxs-lookup"><span data-stu-id="dad0c-166">For each application that has an Application Capacity defined for one or more metrics you can obtain hello information about hello aggregate load reported by replicas of its services.</span></span>

<span data-ttu-id="dad0c-167">Powershell:</span><span class="sxs-lookup"><span data-stu-id="dad0c-167">Powershell:</span></span>

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

<span data-ttu-id="dad0c-168">C#</span><span class="sxs-lookup"><span data-stu-id="dad0c-168">C#</span></span>

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

<span data-ttu-id="dad0c-169">consulta de Hello ApplicationLoad devuelve información básica de hello acerca de la capacidad de las aplicaciones que se especificó para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="dad0c-169">hello ApplicationLoad query returns hello basic information about Application Capacity that was specified for hello application.</span></span> <span data-ttu-id="dad0c-170">Esta información incluye información de nodos de mínimo y máximo de Hola y número de Hola que actualmente está ocupando aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="dad0c-170">This information includes hello Minimum Nodes and Maximum Nodes info, and hello number that hello application is currently occupying.</span></span> <span data-ttu-id="dad0c-171">También incluye información de cada métrica de carga de la aplicación, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dad0c-171">It also includes information about each application load metric, including:</span></span>

* <span data-ttu-id="dad0c-172">Nombre de la métrica: El nombre de métrica de Hola.</span><span class="sxs-lookup"><span data-stu-id="dad0c-172">Metric Name: Name of hello metric.</span></span>
* <span data-ttu-id="dad0c-173">Capacidad de reserva: Capacidad de clúster que está reservada en clúster de Hola para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="dad0c-173">Reservation Capacity: Cluster Capacity that is reserved in hello cluster for this Application.</span></span>
* <span data-ttu-id="dad0c-174">Carga de la aplicación: carga total de las réplicas secundarias de esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="dad0c-174">Application Load: Total Load of this Application’s child replicas.</span></span>
* <span data-ttu-id="dad0c-175">Capacidad de aplicación: valor máximo permitido de la carga de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dad0c-175">Application Capacity: Maximum permitted value of Application Load.</span></span>

## <a name="removing-application-capacity"></a><span data-ttu-id="dad0c-176">Eliminación de la capacidad de aplicación</span><span class="sxs-lookup"><span data-stu-id="dad0c-176">Removing Application Capacity</span></span>
<span data-ttu-id="dad0c-177">Una vez que los parámetros de la capacidad de las aplicaciones de Hola se establecen para una aplicación, puede quitar mediante cmdlets de PowerShell o las API de aplicación de actualización.</span><span class="sxs-lookup"><span data-stu-id="dad0c-177">Once hello Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span></span> <span data-ttu-id="dad0c-178">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dad0c-178">For example:</span></span>

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

<span data-ttu-id="dad0c-179">Este comando quita todos los parámetros de administración de capacidad de aplicación de la instancia de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="dad0c-179">This command removes all Application capacity management parameters from hello application instance.</span></span> <span data-ttu-id="dad0c-180">Esto incluye MinimumNodes, MaximumNodes y métricas de la aplicación hello, si lo hay.</span><span class="sxs-lookup"><span data-stu-id="dad0c-180">This includes MinimumNodes, MaximumNodes, and hello Application's metrics, if any.</span></span> <span data-ttu-id="dad0c-181">efecto de Hola de comando hello es inmediata.</span><span class="sxs-lookup"><span data-stu-id="dad0c-181">hello effect of hello command is immediate.</span></span> <span data-ttu-id="dad0c-182">Una vez completado este comando, Hola, Administrador de recursos del clúster usa un comportamiento de hello predeterminado para administrar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="dad0c-182">After this command completes, hello Cluster Resource Manager uses hello default behavior for managing applications.</span></span> <span data-ttu-id="dad0c-183">Los parámetros de la capacidad de aplicación se pueden especificar de nuevo mediante `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span><span class="sxs-lookup"><span data-stu-id="dad0c-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span></span>

### <a name="restrictions-on-application-capacity"></a><span data-ttu-id="dad0c-184">Restricciones en la capacidad de aplicación</span><span class="sxs-lookup"><span data-stu-id="dad0c-184">Restrictions on Application Capacity</span></span>
<span data-ttu-id="dad0c-185">Existen varias restricciones en los parámetros de capacidad de aplicación que se deben respetar.</span><span class="sxs-lookup"><span data-stu-id="dad0c-185">There are several restrictions on Application Capacity parameters that must be respected.</span></span> <span data-ttu-id="dad0c-186">Si hay errores de validación, no se producirá ningún cambio.</span><span class="sxs-lookup"><span data-stu-id="dad0c-186">If there are validation errors no changes take place.</span></span>

- <span data-ttu-id="dad0c-187">Todos los parámetros de número entero deben ser números no negativos.</span><span class="sxs-lookup"><span data-stu-id="dad0c-187">All integer parameters must be non-negative numbers.</span></span>
- <span data-ttu-id="dad0c-188">MinimumNodes nunca debe ser mayor que MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="dad0c-188">MinimumNodes must never be greater than MaximumNodes.</span></span>
- <span data-ttu-id="dad0c-189">Si se definen capacidades para una métrica de carga, deben seguir estas reglas:</span><span class="sxs-lookup"><span data-stu-id="dad0c-189">If capacities for a load metric are defined, then they must follow these rules:</span></span>
  - <span data-ttu-id="dad0c-190">La capacidad de reserva del nodo no debe ser superior a la capacidad máxima del nodo.</span><span class="sxs-lookup"><span data-stu-id="dad0c-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span></span> <span data-ttu-id="dad0c-191">Por ejemplo, no puede limitar la capacidad de Hola de métrica de Hola "CPU" en las unidades de tootwo del nodo de Hola e intente tooreserve tres unidades en cada nodo.</span><span class="sxs-lookup"><span data-stu-id="dad0c-191">For example, you cannot limit hello capacity for hello metric “CPU” on hello node tootwo units and try tooreserve three units on each node.</span></span>
  - <span data-ttu-id="dad0c-192">Si se especifica MaximumNodes, producto Hola de MaximumNodes y la capacidad máxima de nodo no debe ser mayor que la capacidad Total de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dad0c-192">If MaximumNodes is specified, then hello product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span></span> <span data-ttu-id="dad0c-193">Por ejemplo, supongamos que la capacidad máxima de nodo de métrica de carga "CPU" se establece tooeight Hola.</span><span class="sxs-lookup"><span data-stu-id="dad0c-193">For example, let's say hello Maximum Node Capacity for load metric “CPU” is set tooeight.</span></span> <span data-ttu-id="dad0c-194">Supongamos también que establece hello too10 de nodos máximos.</span><span class="sxs-lookup"><span data-stu-id="dad0c-194">Let's also say you set hello Maximum Nodes too10.</span></span> <span data-ttu-id="dad0c-195">En este caso, la capacidad total de aplicación debe ser mayor que 80 en esta métrica de carga.</span><span class="sxs-lookup"><span data-stu-id="dad0c-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span></span>

<span data-ttu-id="dad0c-196">se aplican restricciones de Hello tanto durante la creación de aplicaciones y actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="dad0c-196">hello restrictions are enforced both during application creation and updates.</span></span>

## <a name="how-not-toouse-application-capacity"></a><span data-ttu-id="dad0c-197">Cómo no toouse capacidad de aplicación</span><span class="sxs-lookup"><span data-stu-id="dad0c-197">How not toouse Application Capacity</span></span>
- <span data-ttu-id="dad0c-198">No intente toouse Hola grupo de aplicaciones características tooconstrain Hola aplicación tooa _específico_ subconjunto de nodos.</span><span class="sxs-lookup"><span data-stu-id="dad0c-198">Do not try toouse hello Application Group features tooconstrain hello application tooa _specific_ subset of nodes.</span></span> <span data-ttu-id="dad0c-199">En otras palabras, puede especificar que la aplicación hello se ejecuta en al menos cinco nodos, pero no qué cinco nodos específicos en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="dad0c-199">In other words, you can specify that hello application runs on at most five nodes, but not which specific five nodes in hello cluster.</span></span> <span data-ttu-id="dad0c-200">Restringir una aplicación toospecific nodos pueden lograrse mediante las restricciones de posición para los servicios.</span><span class="sxs-lookup"><span data-stu-id="dad0c-200">Constraining an application toospecific nodes can be achieved using placement constraints for services.</span></span>
- <span data-ttu-id="dad0c-201">No intente tooensure de capacidad de la aplicación hello toouse que dos servicios de hello misma aplicación se colocan en Hola los mismos nodos.</span><span class="sxs-lookup"><span data-stu-id="dad0c-201">Do not try toouse hello Application Capacity tooensure that two services from hello same application are placed on hello same nodes.</span></span> <span data-ttu-id="dad0c-202">En su lugar use la [afinidad](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) o las [restricciones de colocación](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span><span class="sxs-lookup"><span data-stu-id="dad0c-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dad0c-203">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dad0c-203">Next steps</span></span>
- <span data-ttu-id="dad0c-204">Para más información sobre la configuración de servicios, vaya a [este vínculo](service-fabric-cluster-resource-manager-configure-services.md).</span><span class="sxs-lookup"><span data-stu-id="dad0c-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>
- <span data-ttu-id="dad0c-205">toofind out acerca de cómo Hola, Administrador de recursos del clúster administra y equilibra la carga en el clúster de hello, desproteger artículo hello en [equilibrio de carga](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="dad0c-205">toofind out about how hello Cluster Resource Manager manages and balances load in hello cluster, check out hello article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="dad0c-206">Desde el principio de Hola y [obtener un servicio Administrador de recursos del clúster de tejido de toohello de introducción](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="dad0c-206">Start from hello beginning and [get an Introduction toohello Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="dad0c-207">Para más información sobre cómo funcionan las métricas en general, lea el artículo [Administración de consumo y carga de recursos en Service Fabric con métricas](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="dad0c-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="dad0c-208">Hola, Administrador de recursos del clúster tiene muchas opciones para describir el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="dad0c-208">hello Cluster Resource Manager has many options for describing hello cluster.</span></span> <span data-ttu-id="dad0c-209">toofind más información acerca de ellos, consulte este artículo en [que describe un clúster de Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="dad0c-209">toofind out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
