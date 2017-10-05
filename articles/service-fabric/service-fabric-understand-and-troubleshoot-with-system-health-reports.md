---
title: "Solución de problemas con los informes de mantenimiento del sistema | Microsoft Docs"
description: "Describe los informes de estado enviados por los componentes de Azure Service Fabric y su uso para la resolución de problemas de clúster o de aplicaciones."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: 54e20146b2f1e0ca6153b66319be70c6f7c2fb59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-system-health-reports-to-troubleshoot"></a><span data-ttu-id="d1f49-103">Utilización de informes de mantenimiento del sistema para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="d1f49-103">Use system health reports to troubleshoot</span></span>
<span data-ttu-id="d1f49-104">Los componentes de Azure Service Fabric informan desde el primer momento de todas las entidades del clúster.</span><span class="sxs-lookup"><span data-stu-id="d1f49-104">Azure Service Fabric components report out of the box on all entities in the cluster.</span></span> <span data-ttu-id="d1f49-105">El [almacén de estado](service-fabric-health-introduction.md#health-store) crea y elimina entidades basándose en los informes del sistema.</span><span class="sxs-lookup"><span data-stu-id="d1f49-105">The [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on the system reports.</span></span> <span data-ttu-id="d1f49-106">También las organiza en una jerarquía que captura las interacciones de la entidad.</span><span class="sxs-lookup"><span data-stu-id="d1f49-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="d1f49-107">Para comprender los conceptos relacionados con el mantenimiento, obtenga más información sobre el [modelo de mantenimiento de Service Fabric](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d1f49-107">To understand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="d1f49-108">Los informes de mantenimiento del sistema proporcionan visibilidad en el clúster y funcionalidad de la aplicación, así como indican problemas a través del mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="d1f49-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="d1f49-109">Para aplicaciones y servicios, los informes de mantenimiento del sistema comprueban que las entidades se implementan y que se comportan correctamente desde la perspectiva de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d1f49-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from the Service Fabric perspective.</span></span> <span data-ttu-id="d1f49-110">Los informes no proporcionan ninguna supervisión del mantenimiento de la lógica empresarial del servicio o de la detección de los procesos bloqueados.</span><span class="sxs-lookup"><span data-stu-id="d1f49-110">The reports do not provide any health monitoring of the business logic of the service or detection of hung processes.</span></span> <span data-ttu-id="d1f49-111">Los servicios de usuario pueden enriquecer los datos de mantenimiento con información específica de su lógica.</span><span class="sxs-lookup"><span data-stu-id="d1f49-111">User services can enrich the health data with information specific to their logic.</span></span>

> [!NOTE]
> <span data-ttu-id="d1f49-112">Solo son visibles los informes de mantenimiento de los guardianes *después* de que los componentes del sistema hayan creado la entidad.</span><span class="sxs-lookup"><span data-stu-id="d1f49-112">Watchdogs health reports are visible only *after* the system components create an entity.</span></span> <span data-ttu-id="d1f49-113">Cuando se elimina una entidad, el almacén de estado elimina automáticamente todos los informes de mantenimiento asociados a ella.</span><span class="sxs-lookup"><span data-stu-id="d1f49-113">When an entity is deleted, the health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="d1f49-114">Lo mismo sucede cuando se crea una nueva instancia de la entidad (por ejemplo, se crea una nueva instancia de la réplica del servicio con estado y persistente).</span><span class="sxs-lookup"><span data-stu-id="d1f49-114">The same is true when a new instance of the entity is created (for example, a new stateful persisted service replica instance is created).</span></span> <span data-ttu-id="d1f49-115">Todos los informes asociados a la instancia anterior se eliminan y se limpian del almacén.</span><span class="sxs-lookup"><span data-stu-id="d1f49-115">All reports associated with the old instance are deleted and cleaned up from the store.</span></span>
> 
> 

<span data-ttu-id="d1f49-116">Los informes de los componentes del sistema se identifican mediante el origen, que comienza por el prefijo "**System.**"</span><span class="sxs-lookup"><span data-stu-id="d1f49-116">The system component reports are identified by the source, which starts with the "**System.**"</span></span> <span data-ttu-id="d1f49-117">.</span><span class="sxs-lookup"><span data-stu-id="d1f49-117">prefix.</span></span> <span data-ttu-id="d1f49-118">Los guardianes no pueden utilizar el mismo prefijo para sus orígenes, ya que los informes con parámetros no válidos se rechazan.</span><span class="sxs-lookup"><span data-stu-id="d1f49-118">Watchdogs can't use the same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="d1f49-119">Veamos algunos informes de sistema para entender qué los desencadena y cómo corregir los posibles problemas que representan.</span><span class="sxs-lookup"><span data-stu-id="d1f49-119">Let's look at some system reports to understand what triggers them and how to correct the possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="d1f49-120">Service Fabric sigue agregando informes de condiciones de interés que mejoran la visibilidad de lo que sucede en el clúster y la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d1f49-120">Service Fabric continues to add reports on conditions of interest that improve visibility into what is happening in the cluster and application.</span></span> <span data-ttu-id="d1f49-121">También se pueden mejorar los informes existentes con más detalles para ayudar a solucionar el problema con mayor rapidez.</span><span class="sxs-lookup"><span data-stu-id="d1f49-121">Existing reports can also be enhanced with more details to help troubleshoot the problem faster.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="d1f49-122">Informes de mantenimiento del sistema de clúster</span><span class="sxs-lookup"><span data-stu-id="d1f49-122">Cluster system health reports</span></span>
<span data-ttu-id="d1f49-123">La entidad de mantenimiento del clúster se crea automáticamente en el Almacén de estado.</span><span class="sxs-lookup"><span data-stu-id="d1f49-123">The cluster health entity is created automatically in the health store.</span></span> <span data-ttu-id="d1f49-124">Si todo funciona correctamente, no tiene un informe del sistema.</span><span class="sxs-lookup"><span data-stu-id="d1f49-124">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="d1f49-125">Pérdida de entorno</span><span class="sxs-lookup"><span data-stu-id="d1f49-125">Neighborhood loss</span></span>
<span data-ttu-id="d1f49-126">**System.Federation** notifica un error cuando detecta una pérdida de entorno.</span><span class="sxs-lookup"><span data-stu-id="d1f49-126">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="d1f49-127">El informe procede de los nodos individuales y el identificador de nodo está incluido en el nombre de la propiedad.</span><span class="sxs-lookup"><span data-stu-id="d1f49-127">The report is from individual nodes, and the node ID is included in the property name.</span></span> <span data-ttu-id="d1f49-128">Si hay una pérdida de entorno en todo el anillo de Service Fabric, puede esperar dos eventos (se notifican ambos lados del intervalo).</span><span class="sxs-lookup"><span data-stu-id="d1f49-128">If one neighborhood is lost in the entire Service Fabric ring, you can typically expect two events (both sides of the gap report).</span></span> <span data-ttu-id="d1f49-129">Si se pierden más entornos, se producen más eventos.</span><span class="sxs-lookup"><span data-stu-id="d1f49-129">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="d1f49-130">El informe especifica el tiempo de espera de concesión global como período de vida.</span><span class="sxs-lookup"><span data-stu-id="d1f49-130">The report specifies the global lease timeout as the time to live.</span></span> <span data-ttu-id="d1f49-131">El informe se vuelve a enviar una vez transcurrida la mitad de la duración del período de vida siempre y cuando la condición permanezca activa.</span><span class="sxs-lookup"><span data-stu-id="d1f49-131">The report is resent every half of the TTL duration for as long as the condition remains active.</span></span> <span data-ttu-id="d1f49-132">El evento se quita automáticamente cuando haya expirado.</span><span class="sxs-lookup"><span data-stu-id="d1f49-132">The event is automatically removed when it expires.</span></span> <span data-ttu-id="d1f49-133">El comportamiento de eliminación cuando caduca garantiza que el informe se limpie del Almacén de estado correctamente, incluso si el nodo de informes está inactivo.</span><span class="sxs-lookup"><span data-stu-id="d1f49-133">Remove when expired behavior ensures that the report is cleaned up from the health store correctly, even if the reporting node is down.</span></span>

* <span data-ttu-id="d1f49-134">**SourceId**: System.Federation</span><span class="sxs-lookup"><span data-stu-id="d1f49-134">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="d1f49-135">**Propiedad**: comienza por **Neighborhood** e incluye información sobre el nodo.</span><span class="sxs-lookup"><span data-stu-id="d1f49-135">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="d1f49-136">**Pasos siguientes**: investigue por qué se pierde el entorno (por ejemplo, compruebe la comunicación entre los nodos del clúster).</span><span class="sxs-lookup"><span data-stu-id="d1f49-136">**Next steps**: Investigate why the neighborhood is lost (for example, check the communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="d1f49-137">Informes de mantenimiento del sistema de nodos</span><span class="sxs-lookup"><span data-stu-id="d1f49-137">Node system health reports</span></span>
<span data-ttu-id="d1f49-138">**System.FM**, que representa el servicio Administrador de conmutación por error, es la autoridad que administra la información acerca de los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="d1f49-138">**System.FM**, which represents the Failover Manager service, is the authority that manages information about cluster nodes.</span></span> <span data-ttu-id="d1f49-139">Todos los nodos deben tener un informe de System.FM que muestre el estado.</span><span class="sxs-lookup"><span data-stu-id="d1f49-139">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="d1f49-140">Las entidades de nodo se quitan cuando se quita el estado del nodo (consulte [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span><span class="sxs-lookup"><span data-stu-id="d1f49-140">The node entities are removed when the node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="d1f49-141">Nodo activo o inactivo</span><span class="sxs-lookup"><span data-stu-id="d1f49-141">Node up/down</span></span>
<span data-ttu-id="d1f49-142">System.FM notifica que está todo correcto cuando el nodo se une al anillo (está en funcionamiento).</span><span class="sxs-lookup"><span data-stu-id="d1f49-142">System.FM reports as OK when the node joins the ring (it's up and running).</span></span> <span data-ttu-id="d1f49-143">Notifica un error cuando el nodo sale del anillo (no funciona, ya sea porque se está actualizando o simplemente porque no pudo).</span><span class="sxs-lookup"><span data-stu-id="d1f49-143">It reports an error when the node departs the ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="d1f49-144">La jerarquía de mantenimiento generada por el almacén de estado realiza una acción sobre las entidades implementadas en correlación con los informes de nodo de System.FM.</span><span class="sxs-lookup"><span data-stu-id="d1f49-144">The health hierarchy built by the health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="d1f49-145">Considera el nodo como un elemento primario virtual de todas las entidades implementadas.</span><span class="sxs-lookup"><span data-stu-id="d1f49-145">It considers the node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="d1f49-146">Las entidades implementadas en ese nodo se exponen a través de las consultas si System.FM notifica que el nodo está activo, con la misma instancia que la instancia asociada a las entidades.</span><span class="sxs-lookup"><span data-stu-id="d1f49-146">The deployed entities on that node are exposed through queries if the node is reported as up by System.FM, with the same instance as the instance associated with the entities.</span></span> <span data-ttu-id="d1f49-147">Cuando System.FM notifica que el nodo está inactivo o que se ha reiniciado (una nueva instancia), el almacén de estado limpia automáticamente las entidades implementadas que solo pueden existir en el nodo inactivo o en la instancia anterior del nodo.</span><span class="sxs-lookup"><span data-stu-id="d1f49-147">When System.FM reports that the node is down or restarted (a new instance), the health store automatically cleans up the deployed entities that can exist only on the down node or on the previous instance of the node.</span></span>

* <span data-ttu-id="d1f49-148">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="d1f49-148">**SourceId**: System.FM</span></span>
* <span data-ttu-id="d1f49-149">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="d1f49-149">**Property**: State</span></span>
* <span data-ttu-id="d1f49-150">**Pasos siguientes**: si el nodo está inactivo durante una actualización, debería volver a estar activo una vez que se haya actualizado.</span><span class="sxs-lookup"><span data-stu-id="d1f49-150">**Next steps**: If the node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="d1f49-151">En este caso, se debe cambiar el estado de mantenimiento a Correcto.</span><span class="sxs-lookup"><span data-stu-id="d1f49-151">In this case, the health state should switch back to OK.</span></span> <span data-ttu-id="d1f49-152">Si el nodo no recupera ese estado o se produce un error, deberá investigar más el problema.</span><span class="sxs-lookup"><span data-stu-id="d1f49-152">If the node doesn't come back or it fails, the problem needs more investigation.</span></span>

<span data-ttu-id="d1f49-153">El ejemplo siguiente muestra el evento System.FM con el estado de mantenimiento Correcto para el nodo activo:</span><span class="sxs-lookup"><span data-stu-id="d1f49-153">The following example shows the System.FM event with a health state of OK for node up:</span></span>

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a><span data-ttu-id="d1f49-154">Caducidad del certificado</span><span class="sxs-lookup"><span data-stu-id="d1f49-154">Certificate expiration</span></span>
<span data-ttu-id="d1f49-155">**System.FabricNode** notifica una advertencia cuando los certificados usados por el nodo están a punto de expirar.</span><span class="sxs-lookup"><span data-stu-id="d1f49-155">**System.FabricNode** reports a warning when certificates used by the node are near expiration.</span></span> <span data-ttu-id="d1f49-156">Hay tres certificados por nodo: **Certificate_cluster**, **Certificate_server** y **Certificate_default_client**.</span><span class="sxs-lookup"><span data-stu-id="d1f49-156">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="d1f49-157">Si faltan más de dos semanas para expirar, el estado de mantenimiento del informe es Correcto.</span><span class="sxs-lookup"><span data-stu-id="d1f49-157">When the expiration is at least two weeks away, the report health state is OK.</span></span> <span data-ttu-id="d1f49-158">Si faltan menos de dos semanas, el tipo de informe es una advertencia.</span><span class="sxs-lookup"><span data-stu-id="d1f49-158">When the expiration is within two weeks, the report type is a warning.</span></span> <span data-ttu-id="d1f49-159">El TTL de estos eventos es infinito y se quitan cuando un nodo deja el clúster.</span><span class="sxs-lookup"><span data-stu-id="d1f49-159">TTL of these events is infinite, and they are removed when a node leaves the cluster.</span></span>

* <span data-ttu-id="d1f49-160">**SourceId**: System.FabricNode</span><span class="sxs-lookup"><span data-stu-id="d1f49-160">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="d1f49-161">**Property**: comienza por **Certificate** y contiene más información sobre el tipo de certificado.</span><span class="sxs-lookup"><span data-stu-id="d1f49-161">**Property**: Starts with **Certificate** and contains more information about the certificate type</span></span>
* <span data-ttu-id="d1f49-162">**Pasos siguientes**: actualice los certificados si están a punto de expirar.</span><span class="sxs-lookup"><span data-stu-id="d1f49-162">**Next steps**: Update the certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="d1f49-163">Infracción de la capacidad de carga</span><span class="sxs-lookup"><span data-stu-id="d1f49-163">Load capacity violation</span></span>
<span data-ttu-id="d1f49-164">El equilibrador de carga de Service Fabric notifica una advertencia cuando detecta una infracción de la capacidad del nodo.</span><span class="sxs-lookup"><span data-stu-id="d1f49-164">The Service Fabric Load Balancer reports a warning when it detects a node capacity violation.</span></span>

* <span data-ttu-id="d1f49-165">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="d1f49-165">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="d1f49-166">**Property**: comienza por **Capacity**.</span><span class="sxs-lookup"><span data-stu-id="d1f49-166">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="d1f49-167">**Pasos siguientes**: compruebe las métricas proporcionadas y vea la capacidad actual en el nodo.</span><span class="sxs-lookup"><span data-stu-id="d1f49-167">**Next steps**: Check provided metrics and view the current capacity on the node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="d1f49-168">Informes de mantenimiento del sistema de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d1f49-168">Application system health reports</span></span>
<span data-ttu-id="d1f49-169">**System.CM**, que representa el servicio Administrador de clústeres, es la autoridad que administra la información acerca de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="d1f49-169">**System.CM**, which represents the Cluster Manager service, is the authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="d1f49-170">Estado</span><span class="sxs-lookup"><span data-stu-id="d1f49-170">State</span></span>
<span data-ttu-id="d1f49-171">System.CM notifica un estado Correcto cuando se ha creado o actualizado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d1f49-171">System.CM reports as OK when the application has been created or updated.</span></span> <span data-ttu-id="d1f49-172">Informa al almacén de estado cuando se ha eliminado la aplicación, por lo que puede quitarse del almacén.</span><span class="sxs-lookup"><span data-stu-id="d1f49-172">It informs the health store when the application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="d1f49-173">**SourceId**: System.CM</span><span class="sxs-lookup"><span data-stu-id="d1f49-173">**SourceId**: System.CM</span></span>
* <span data-ttu-id="d1f49-174">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="d1f49-174">**Property**: State</span></span>
* <span data-ttu-id="d1f49-175">**Pasos siguientes**: si se ha creado o actualizado la aplicación, debe incluir el informe de mantenimiento de Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="d1f49-175">**Next steps**: If the application has been created or updated, it should include the Cluster Manager health report.</span></span> <span data-ttu-id="d1f49-176">De lo contrario, compruebe el estado de la aplicación mediante el envío de una consulta (por ejemplo, el cmdlet de PowerShell **Get-ServiceFabricApplication -ApplicationName *nombreAplicación***).</span><span class="sxs-lookup"><span data-stu-id="d1f49-176">Otherwise, check the state of the application by issuing a query (for example, the PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span></span>

<span data-ttu-id="d1f49-177">El ejemplo siguiente muestra el evento de estado en la aplicación **fabric:/WordCount** :</span><span class="sxs-lookup"><span data-stu-id="d1f49-177">The following example shows the state event on the **fabric:/WordCount** application:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a><span data-ttu-id="d1f49-178">Informes de mantenimiento del sistema de servicio</span><span class="sxs-lookup"><span data-stu-id="d1f49-178">Service system health reports</span></span>
<span data-ttu-id="d1f49-179">**System.FM**, que representa el servicio Administrador de conmutación por error, es la autoridad que administra la información acerca de los servicios.</span><span class="sxs-lookup"><span data-stu-id="d1f49-179">**System.FM**, which represents the Failover Manager service, is the authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="d1f49-180">Estado</span><span class="sxs-lookup"><span data-stu-id="d1f49-180">State</span></span>
<span data-ttu-id="d1f49-181">System.FM notifica un estado Correcto cuando se ha creado el servicio.</span><span class="sxs-lookup"><span data-stu-id="d1f49-181">System.FM reports as OK when the service has been created.</span></span> <span data-ttu-id="d1f49-182">Elimina la entidad del almacén de estado cuando se ha eliminado el servicio.</span><span class="sxs-lookup"><span data-stu-id="d1f49-182">It deletes the entity from the health store when the service has been deleted.</span></span>

* <span data-ttu-id="d1f49-183">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="d1f49-183">**SourceId**: System.FM</span></span>
* <span data-ttu-id="d1f49-184">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="d1f49-184">**Property**: State</span></span>

<span data-ttu-id="d1f49-185">El ejemplo siguiente muestra el evento de estado en el servicio **fabric:/WordCount/WordCountService**:</span><span class="sxs-lookup"><span data-stu-id="d1f49-185">The following example shows the state event on the service **fabric:/WordCount/WordCountWebService**:</span></span>

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a><span data-ttu-id="d1f49-186">Error de correlación de servicio</span><span class="sxs-lookup"><span data-stu-id="d1f49-186">Service correlation error</span></span>
<span data-ttu-id="d1f49-187">**System.PLB** notifica un error cuando detecta que la actualización de un servicio que se va a correlacionar con otro crea una cadena de afinidad.</span><span class="sxs-lookup"><span data-stu-id="d1f49-187">**System.PLB** reports an error when it detects that updating a service to be correlated with another service creates an affinity chain.</span></span> <span data-ttu-id="d1f49-188">El informe se borra cuando se produce una actualización correcta.</span><span class="sxs-lookup"><span data-stu-id="d1f49-188">The report is cleared when successful update happens.</span></span>

* <span data-ttu-id="d1f49-189">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="d1f49-189">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="d1f49-190">**Propiedad**: ServiceDescription</span><span class="sxs-lookup"><span data-stu-id="d1f49-190">**Property**: ServiceDescription</span></span>
* <span data-ttu-id="d1f49-191">**Pasos siguientes**: compruebe las descripciones de servicios correlacionados.</span><span class="sxs-lookup"><span data-stu-id="d1f49-191">**Next steps**: Check the correlated service descriptions.</span></span>

## <a name="partition-system-health-reports"></a><span data-ttu-id="d1f49-192">Informes de mantenimiento del sistema de partición</span><span class="sxs-lookup"><span data-stu-id="d1f49-192">Partition system health reports</span></span>
<span data-ttu-id="d1f49-193">**System.FM**, que representa el servicio Administrador de conmutación por error, es la autoridad que administra la información acerca de las particiones del servicio.</span><span class="sxs-lookup"><span data-stu-id="d1f49-193">**System.FM**, which represents the Failover Manager service, is the authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="d1f49-194">Estado</span><span class="sxs-lookup"><span data-stu-id="d1f49-194">State</span></span>
<span data-ttu-id="d1f49-195">System.FM notifica un estado Correcto cuando la partición se ha creado y es correcta.</span><span class="sxs-lookup"><span data-stu-id="d1f49-195">System.FM reports as OK when the partition has been created and is healthy.</span></span> <span data-ttu-id="d1f49-196">Elimina la entidad del almacén de estado cuando se ha eliminado la partición.</span><span class="sxs-lookup"><span data-stu-id="d1f49-196">It deletes the entity from the health store when the partition is deleted.</span></span>

<span data-ttu-id="d1f49-197">Si la partición es inferior al recuento mínimo de réplicas, notifica un error.</span><span class="sxs-lookup"><span data-stu-id="d1f49-197">If the partition is below the minimum replica count, it reports an error.</span></span> <span data-ttu-id="d1f49-198">Si la partición no es inferior al recuento mínimo de réplicas, pero es inferior al recuento objetivo de réplicas, notifica una advertencia.</span><span class="sxs-lookup"><span data-stu-id="d1f49-198">If the partition is not below the minimum replica count, but it is below the target replica count, it reports a warning.</span></span> <span data-ttu-id="d1f49-199">Si la partición está en situación de pérdida de cuórum, System.FM notifica un error.</span><span class="sxs-lookup"><span data-stu-id="d1f49-199">If the partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="d1f49-200">Otros eventos importantes incluyen una advertencia cuando la reconfiguración tarda más tiempo de lo esperado y cuando la compilación tarda más de lo previsto.</span><span class="sxs-lookup"><span data-stu-id="d1f49-200">Other important events include a warning when the reconfiguration takes longer than expected and when the build takes longer than expected.</span></span> <span data-ttu-id="d1f49-201">Los tiempos de compilación o reconfiguración previstos se pueden configurar en función de los escenarios de servicio.</span><span class="sxs-lookup"><span data-stu-id="d1f49-201">The expected times for the build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="d1f49-202">Por ejemplo, si un servicio tiene un terabyte de estado como, por ejemplo, SQL Database, la compilación tarda más tiempo del que tardaría para un servicio con una pequeña cantidad de estado.</span><span class="sxs-lookup"><span data-stu-id="d1f49-202">For example, if a service has a terabyte of state, such as SQL Database, the build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="d1f49-203">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="d1f49-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="d1f49-204">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="d1f49-204">**Property**: State</span></span>
* <span data-ttu-id="d1f49-205">**Pasos siguientes**: si el estado de mantenimiento no es correcto, es posible que algunas réplicas no se hayan creado, abierto o promocionado a principales o secundarias de manera correcta.</span><span class="sxs-lookup"><span data-stu-id="d1f49-205">**Next steps**: If the health state is not OK, it's possible that some replicas have not been created, opened, or promoted to primary or secondary correctly.</span></span> <span data-ttu-id="d1f49-206">En muchos casos, la causa raíz es un error de servicio en la implementación del rol de apertura o cambio.</span><span class="sxs-lookup"><span data-stu-id="d1f49-206">In many instances, the root cause is a service bug in the open or change-role implementation.</span></span>

<span data-ttu-id="d1f49-207">El ejemplo siguiente muestra una partición correcta:</span><span class="sxs-lookup"><span data-stu-id="d1f49-207">The following example shows a healthy partition:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="d1f49-208">El ejemplo siguiente muestra el mantenimiento de una partición que es inferior al recuento objetivo de réplicas.</span><span class="sxs-lookup"><span data-stu-id="d1f49-208">The following example shows the health of a partition that is below target replica count.</span></span> <span data-ttu-id="d1f49-209">El paso siguiente consiste en obtener la descripción de la partición, que muestra cómo se ha configurado: **MinReplicaSetSize** es tres y **TargetReplicaSetSize** es siete.</span><span class="sxs-lookup"><span data-stu-id="d1f49-209">The next step is to get the partition description, which shows how it is configured: **MinReplicaSetSize** is three and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="d1f49-210">Después, obtenga el número de nodos del clúster: cinco.</span><span class="sxs-lookup"><span data-stu-id="d1f49-210">Then get the number of nodes in the cluster: five.</span></span> <span data-ttu-id="d1f49-211">En este caso, por lo tanto, no se pueden colocar dos réplicas porque el número de réplicas de destino es mayor que el número de nodos disponibles.</span><span class="sxs-lookup"><span data-stu-id="d1f49-211">So in this case, two replicas can't be placed because the target number of replicas is higher than the number of nodes available.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
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
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a><span data-ttu-id="d1f49-212">Infracción de restricción de réplica</span><span class="sxs-lookup"><span data-stu-id="d1f49-212">Replica constraint violation</span></span>
<span data-ttu-id="d1f49-213">**System.PLB** notifica una advertencia si detecta una infracción de restricción de réplica y no se pueden colocar todas las réplicas de la partición.</span><span class="sxs-lookup"><span data-stu-id="d1f49-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place all partition replicas.</span></span> <span data-ttu-id="d1f49-214">Los detalles del informe muestran qué restricciones y propiedades evitan la ubicación de las réplicas.</span><span class="sxs-lookup"><span data-stu-id="d1f49-214">The report details show which constraints and properties prevent the replica placement.</span></span>

* <span data-ttu-id="d1f49-215">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="d1f49-215">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="d1f49-216">**Property**: comienza por **ReplicaConstraintViolation**.</span><span class="sxs-lookup"><span data-stu-id="d1f49-216">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="d1f49-217">Informes de mantenimiento del sistema de replica</span><span class="sxs-lookup"><span data-stu-id="d1f49-217">Replica system health reports</span></span>
<span data-ttu-id="d1f49-218">**System.RA**, que representa el componente del agente de reconfiguración, es la autoridad para el estado de la réplica.</span><span class="sxs-lookup"><span data-stu-id="d1f49-218">**System.RA**, which represents the reconfiguration agent component, is the authority for the replica state.</span></span>

### <a name="state"></a><span data-ttu-id="d1f49-219">Estado</span><span class="sxs-lookup"><span data-stu-id="d1f49-219">State</span></span>
<span data-ttu-id="d1f49-220">**System.RA** notifica un estado Correcto cuando se ha creado la réplica.</span><span class="sxs-lookup"><span data-stu-id="d1f49-220">**System.RA** reports OK when the replica has been created.</span></span>

* <span data-ttu-id="d1f49-221">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="d1f49-221">**SourceId**: System.RA</span></span>
* <span data-ttu-id="d1f49-222">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="d1f49-222">**Property**: State</span></span>

<span data-ttu-id="d1f49-223">El ejemplo siguiente muestra una réplica correcta:</span><span class="sxs-lookup"><span data-stu-id="d1f49-223">The following example shows a healthy replica:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a><span data-ttu-id="d1f49-224">Estado de apertura de réplica</span><span class="sxs-lookup"><span data-stu-id="d1f49-224">Replica open status</span></span>
<span data-ttu-id="d1f49-225">La descripción de este informe de mantenimiento contiene la hora de inicio (hora universal coordinada) de cuando se ha invocado la llamada API.</span><span class="sxs-lookup"><span data-stu-id="d1f49-225">The description of this health report contains the start time (Coordinated Universal Time) when the API call was invoked.</span></span>

<span data-ttu-id="d1f49-226">**System.RA** notifica una advertencia si la apertura de la réplica tarda más tiempo del configurado (valor predeterminado: 30 minutos).</span><span class="sxs-lookup"><span data-stu-id="d1f49-226">**System.RA** reports a warning if the replica open takes longer than the configured period (default: 30 minutes).</span></span> <span data-ttu-id="d1f49-227">Si la API afecta a la disponibilidad de servicio, el informe se emite con mayor rapidez (intervalo configurable, valor predeterminado de 30 segundos).</span><span class="sxs-lookup"><span data-stu-id="d1f49-227">If the API impacts service availability, the report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="d1f49-228">El tiempo medido incluye el tiempo necesario para la apertura del replicador y del servicio.</span><span class="sxs-lookup"><span data-stu-id="d1f49-228">The time measured includes the time taken for the replicator open and the service open.</span></span> <span data-ttu-id="d1f49-229">La propiedad cambia a Correcto si se completa la apertura.</span><span class="sxs-lookup"><span data-stu-id="d1f49-229">The property changes to OK if the open completes.</span></span>

* <span data-ttu-id="d1f49-230">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="d1f49-230">**SourceId**: System.RA</span></span>
* <span data-ttu-id="d1f49-231">**Property**: **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="d1f49-231">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="d1f49-232">**Pasos siguientes**: si el estado de mantenimiento no es Correcto, compruebe por qué la apertura de la réplica tarda más de lo previsto.</span><span class="sxs-lookup"><span data-stu-id="d1f49-232">**Next steps**: If the health state is not OK, investigate why the replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="d1f49-233">Llamada a la API de servicio lenta</span><span class="sxs-lookup"><span data-stu-id="d1f49-233">Slow service API call</span></span>
<span data-ttu-id="d1f49-234">**System.RAP** y **System.Replicator** notifican una advertencia si una llamada al código de servicio de usuario tarda más tiempo del configurado.</span><span class="sxs-lookup"><span data-stu-id="d1f49-234">**System.RAP** and **System.Replicator** report a warning if a call to the user service code takes longer than the configured time.</span></span> <span data-ttu-id="d1f49-235">La advertencia se borra cuando finaliza la llamada.</span><span class="sxs-lookup"><span data-stu-id="d1f49-235">The warning is cleared when the call completes.</span></span>

* <span data-ttu-id="d1f49-236">**SourceId**: System.RAP o System.Replicator</span><span class="sxs-lookup"><span data-stu-id="d1f49-236">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="d1f49-237">**Property**: el nombre de la API lenta.</span><span class="sxs-lookup"><span data-stu-id="d1f49-237">**Property**: The name of the slow API.</span></span> <span data-ttu-id="d1f49-238">La descripción proporciona más detalles sobre el tiempo que la API ha estado pendiente.</span><span class="sxs-lookup"><span data-stu-id="d1f49-238">The description provides more details about the time the API has been pending.</span></span>
* <span data-ttu-id="d1f49-239">**Pasos siguientes**: investigue por qué la llamada tarda más de lo previsto.</span><span class="sxs-lookup"><span data-stu-id="d1f49-239">**Next steps**: Investigate why the call takes longer than expected.</span></span>

<span data-ttu-id="d1f49-240">El ejemplo siguiente muestra una partición en la pérdida de quórum, así como los pasos de investigación realizados para descubrir el motivo.</span><span class="sxs-lookup"><span data-stu-id="d1f49-240">The following example shows a partition in quorum loss, and the investigation steps done to figure out why.</span></span> <span data-ttu-id="d1f49-241">Una de las réplicas tiene un estado de mantenimiento de advertencia, por tanto, ya conoce su estado.</span><span class="sxs-lookup"><span data-stu-id="d1f49-241">One of the replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="d1f49-242">Muestra que la operación de servicio tarda más de lo previsto, un evento notificado por System.RAP.</span><span class="sxs-lookup"><span data-stu-id="d1f49-242">It shows that the service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="d1f49-243">Después de recibir esta información, el paso siguiente es examinar el código de servicio e investigar.</span><span class="sxs-lookup"><span data-stu-id="d1f49-243">After this information is received, the next step is to look at the service code and investigate there.</span></span> <span data-ttu-id="d1f49-244">En este caso, la implementación de **RunAsync** del servicio con estado produce una excepción no controlada.</span><span class="sxs-lookup"><span data-stu-id="d1f49-244">For this case, the **RunAsync** implementation of the stateful service throws an unhandled exception.</span></span> <span data-ttu-id="d1f49-245">Las réplicas se reciclan, por lo que quizás no pueda ver ninguna réplica en estado de advertencia.</span><span class="sxs-lookup"><span data-stu-id="d1f49-245">The replicas are recycling, so you may not see any replicas in the warning state.</span></span> <span data-ttu-id="d1f49-246">Puede intentar obtener de nuevo el estado de mantenimiento y buscar las diferencias en el identificador de réplica.</span><span class="sxs-lookup"><span data-stu-id="d1f49-246">You can retry getting the health state and look for any differences in the replica ID.</span></span> <span data-ttu-id="d1f49-247">En algunos casos, los reintentos pueden proporcionar pistas.</span><span class="sxs-lookup"><span data-stu-id="d1f49-247">In certain cases, the retries can give you clues.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

<span data-ttu-id="d1f49-248">Al iniciar la aplicación defectuosa en el depurador, las ventanas de eventos de diagnóstico muestran la excepción de RunAsync:</span><span class="sxs-lookup"><span data-stu-id="d1f49-248">When you start the faulty application under the debugger, the diagnostic events windows show the exception thrown from RunAsync:</span></span>

![Eventos de diagnóstico de Visual Studio 2015: Error de RunAsync en fabric:/HelloWorldStatefulApplication.][1]

<span data-ttu-id="d1f49-250">Eventos de diagnóstico de Visual Studio 2015: Error de RunAsync en **fabric:/HelloWorldStatefulApplication**.</span><span class="sxs-lookup"><span data-stu-id="d1f49-250">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="d1f49-251">Cola de replicación completa</span><span class="sxs-lookup"><span data-stu-id="d1f49-251">Replication queue full</span></span>
<span data-ttu-id="d1f49-252">**System.Replicator** notifica una advertencia cuando la cola de replicación está llena.</span><span class="sxs-lookup"><span data-stu-id="d1f49-252">**System.Replicator** reports a warning when the replication queue is full.</span></span> <span data-ttu-id="d1f49-253">En la réplica principal, la cola de replicación suele llenarse porque una o varias réplicas secundarias son lentas a la hora de confirmar las operaciones.</span><span class="sxs-lookup"><span data-stu-id="d1f49-253">On the primary, replication queue usually becomes full because one or more secondary replicas are slow to acknowledge operations.</span></span> <span data-ttu-id="d1f49-254">En la secundaria, esto suele ocurrir cuando el servicio es lento en aplicar las operaciones.</span><span class="sxs-lookup"><span data-stu-id="d1f49-254">On the secondary, this usually happens when the service is slow to apply the operations.</span></span> <span data-ttu-id="d1f49-255">La advertencia se borra cuando la cola ya no está llena.</span><span class="sxs-lookup"><span data-stu-id="d1f49-255">The warning is cleared when the queue is no longer full.</span></span>

* <span data-ttu-id="d1f49-256">**SourceId**: System.Replicator</span><span class="sxs-lookup"><span data-stu-id="d1f49-256">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="d1f49-257">**Property**: **PrimaryReplicationQueueStatus** o **SecondaryReplicationQueueStatus**, según el rol de réplica.</span><span class="sxs-lookup"><span data-stu-id="d1f49-257">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on the replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="d1f49-258">Operaciones de nomenclatura lentas</span><span class="sxs-lookup"><span data-stu-id="d1f49-258">Slow Naming operations</span></span>
<span data-ttu-id="d1f49-259">**System.NamingService** informa del estado en su réplica principal cuando una operación de nomenclatura tarda más de lo aceptable.</span><span class="sxs-lookup"><span data-stu-id="d1f49-259">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="d1f49-260">[CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) o [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) son ejemplos de operaciones de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="d1f49-260">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="d1f49-261">En FabricClient pueden encontrarse más métodos, como en [métodos de administración de servicios](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) o [métodos de administración de propiedades](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span><span class="sxs-lookup"><span data-stu-id="d1f49-261">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="d1f49-262">El servicio de nombres resuelve los nombres de servicio en una ubicación del clúster y permite a los usuarios administrar las propiedades y los nombres de servicio.</span><span class="sxs-lookup"><span data-stu-id="d1f49-262">The Naming service resolves service names to a location in the cluster and enables users to manage service names and properties.</span></span> <span data-ttu-id="d1f49-263">Se trata de un servicio guardado con particiones de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d1f49-263">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="d1f49-264">Una de las particiones representa a Authority Owner, que contiene metadatos sobre todos los nombres y servicios de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d1f49-264">One of the partitions represents the Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="d1f49-265">Los nombres de Service Fabric se asignan a particiones diferentes, denominadas particiones Name Owner, por lo que el servicio se puede ampliar.</span><span class="sxs-lookup"><span data-stu-id="d1f49-265">The Service Fabric names are mapped to different partitions, called Name Owner partitions, so the service is extensible.</span></span> <span data-ttu-id="d1f49-266">Obtenga más información sobre el [servicio de nomenclatura](service-fabric-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="d1f49-266">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="d1f49-267">Cuando una operación de nomenclatura tarda más de lo esperado, la operación se marca con un informe de advertencia en la *réplica principal de la partición del servicio de nomenclatura que se usa para la operación*.</span><span class="sxs-lookup"><span data-stu-id="d1f49-267">When a Naming operation takes longer than expected, the operation is flagged with a Warning report on the *primary replica of the Naming service partition that serves the operation*.</span></span> <span data-ttu-id="d1f49-268">Si la operación se completa correctamente, la advertencia se elimina.</span><span class="sxs-lookup"><span data-stu-id="d1f49-268">If the operation completes successfully, the Warning is cleared.</span></span> <span data-ttu-id="d1f49-269">Si la operación se completa con un error, el informe de estado incluye detalles sobre el error.</span><span class="sxs-lookup"><span data-stu-id="d1f49-269">If the operation completes with an error, the health report includes details about the error.</span></span>

* <span data-ttu-id="d1f49-270">**SourceId**: System.NamingService</span><span class="sxs-lookup"><span data-stu-id="d1f49-270">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="d1f49-271">**Property**: comienza con el prefijo **Duration_** e identifica la operación lenta y el nombre de Service Fabric en el que se aplica la operación.</span><span class="sxs-lookup"><span data-stu-id="d1f49-271">**Property**: Starts with prefix **Duration_** and identifies the slow operation and the Service Fabric name on which the operation is applied.</span></span> <span data-ttu-id="d1f49-272">Por ejemplo, si el servicio de creación en el nombre fabric:/MyApp/MyService tarda demasiado, la propiedad es Duration_AOCreateService.fabric:/MyApp/MyService.</span><span class="sxs-lookup"><span data-stu-id="d1f49-272">For example, if create service at name fabric:/MyApp/MyService takes too long, the property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="d1f49-273">AO apunta al rol de la partición de nomenclatura para este nombre y operación.</span><span class="sxs-lookup"><span data-stu-id="d1f49-273">AO points to the role of the Naming partition for this name and operation.</span></span>
* <span data-ttu-id="d1f49-274">**Pasos siguientes**: compruebe por qué se produce un error en la operación de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="d1f49-274">**Next steps**: Check why the Naming operation fails.</span></span> <span data-ttu-id="d1f49-275">Cada operación puede tener diferentes causas.</span><span class="sxs-lookup"><span data-stu-id="d1f49-275">Each operation can have different root causes.</span></span> <span data-ttu-id="d1f49-276">Por ejemplo, el servicio de eliminación puede estar atascado en un nodo debido a que el host de la aplicación se bloquee continuamente en un nodo por un error de usuario en el código del servicio.</span><span class="sxs-lookup"><span data-stu-id="d1f49-276">For example, delete service may be stuck on a node because the application host keeps crashing on a node due to a user bug in the service code.</span></span>

<span data-ttu-id="d1f49-277">El ejemplo siguiente muestra una operación de servicio de creación.</span><span class="sxs-lookup"><span data-stu-id="d1f49-277">The following example shows a create service operation.</span></span> <span data-ttu-id="d1f49-278">La operación tardó más de la duración configurada.</span><span class="sxs-lookup"><span data-stu-id="d1f49-278">The operation took longer than the configured duration.</span></span> <span data-ttu-id="d1f49-279">AO vuelve a intentarlo y envía trabajo a NO.</span><span class="sxs-lookup"><span data-stu-id="d1f49-279">AO retries and sends work to NO.</span></span> <span data-ttu-id="d1f49-280">NO completó la última operación con tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="d1f49-280">NO completed the last operation with Timeout.</span></span> <span data-ttu-id="d1f49-281">En este caso, la misma réplica es la principal tanto para el rol de AO como para el de NO.</span><span class="sxs-lookup"><span data-stu-id="d1f49-281">In this case, the same replica is primary for both the AO and NO roles.</span></span>

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : The AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : The NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="d1f49-282">Informes de mantenimiento del sistema DeployedApplication</span><span class="sxs-lookup"><span data-stu-id="d1f49-282">DeployedApplication system health reports</span></span>
<span data-ttu-id="d1f49-283">**System.Hosting** es la autoridad en las entidades implementadas.</span><span class="sxs-lookup"><span data-stu-id="d1f49-283">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="d1f49-284">Activación</span><span class="sxs-lookup"><span data-stu-id="d1f49-284">Activation</span></span>
<span data-ttu-id="d1f49-285">System.Hosting notifica un estado Correcto cuando una aplicación se ha activado correctamente en el nodo.</span><span class="sxs-lookup"><span data-stu-id="d1f49-285">System.Hosting reports as OK when an application has been successfully activated on the node.</span></span> <span data-ttu-id="d1f49-286">De lo contrario, notifica un error.</span><span class="sxs-lookup"><span data-stu-id="d1f49-286">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="d1f49-287">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="d1f49-287">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="d1f49-288">**Property**: Activation, incluida la versión de lanzamiento.</span><span class="sxs-lookup"><span data-stu-id="d1f49-288">**Property**: Activation, including the rollout version</span></span>
* <span data-ttu-id="d1f49-289">**Pasos siguientes**: si el mantenimiento de la aplicación es incorrecto, investigue el motivo del error de la activación.</span><span class="sxs-lookup"><span data-stu-id="d1f49-289">**Next steps**: If the application is unhealthy, investigate why the activation failed.</span></span>

<span data-ttu-id="d1f49-290">El ejemplo siguiente muestra una activación correcta:</span><span class="sxs-lookup"><span data-stu-id="d1f49-290">The following example shows successful activation:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="d1f49-291">Descargar</span><span class="sxs-lookup"><span data-stu-id="d1f49-291">Download</span></span>
<span data-ttu-id="d1f49-292">**System.Hosting** notifica un error si se produjo un error al descargar el paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="d1f49-292">**System.Hosting** reports an error if the application package download fails.</span></span>

* <span data-ttu-id="d1f49-293">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="d1f49-293">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="d1f49-294">**Property**: **Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="d1f49-294">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="d1f49-295">**Pasos siguientes**: investigue el motivo del error de descarga en el nodo.</span><span class="sxs-lookup"><span data-stu-id="d1f49-295">**Next steps**: Investigate why the download failed on the node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="d1f49-296">Informes de mantenimiento del sistema DeployedServicePackage</span><span class="sxs-lookup"><span data-stu-id="d1f49-296">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="d1f49-297">**System.Hosting** es la autoridad en las entidades implementadas.</span><span class="sxs-lookup"><span data-stu-id="d1f49-297">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="d1f49-298">Activación de paquete de servicio</span><span class="sxs-lookup"><span data-stu-id="d1f49-298">Service package activation</span></span>
<span data-ttu-id="d1f49-299">System.Hosting notifica un estado Correcto si la activación del paquete de servicio en el nodo se ha realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="d1f49-299">System.Hosting reports as OK if the service package activation on the node is successful.</span></span> <span data-ttu-id="d1f49-300">De lo contrario, notifica un error.</span><span class="sxs-lookup"><span data-stu-id="d1f49-300">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="d1f49-301">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="d1f49-301">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="d1f49-302">**Property**: Activation.</span><span class="sxs-lookup"><span data-stu-id="d1f49-302">**Property**: Activation</span></span>
* <span data-ttu-id="d1f49-303">**Pasos siguientes**: investigue el motivo del error de la activación.</span><span class="sxs-lookup"><span data-stu-id="d1f49-303">**Next steps**: Investigate why the activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="d1f49-304">Activación del paquete de código</span><span class="sxs-lookup"><span data-stu-id="d1f49-304">Code package activation</span></span>
<span data-ttu-id="d1f49-305">**System.Hosting** notifica un estado Correcto para cada paquete de código si la activación se ha realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="d1f49-305">**System.Hosting** reports as OK for each code package if the activation is successful.</span></span> <span data-ttu-id="d1f49-306">Si se produce un error en la activación, notifica una advertencia tal y como está configurado.</span><span class="sxs-lookup"><span data-stu-id="d1f49-306">If the activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="d1f49-307">Si **CodePackage** no se puede activar o finaliza con un error mayor que el configurado **CodePackageHealthErrorThreshold**, el hospedaje notifica un error.</span><span class="sxs-lookup"><span data-stu-id="d1f49-307">If **CodePackage** fails to activate or terminates with an error greater than the configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="d1f49-308">Si hay varios paquetes de código en un paquete de servicios, se genera un informe de activación para cada uno.</span><span class="sxs-lookup"><span data-stu-id="d1f49-308">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="d1f49-309">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="d1f49-309">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="d1f49-310">**Property**: usa el prefijo **CodePackageActivation** y contiene el nombre del paquete de código y el punto de entrada como **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (por ejemplo, **CodePackageActivation:Code:SetupEntryPoint**).</span><span class="sxs-lookup"><span data-stu-id="d1f49-310">**Property**: Uses the prefix **CodePackageActivation** and contains the name of the code package and the entry point as **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="d1f49-311">Registro del tipo de servicio</span><span class="sxs-lookup"><span data-stu-id="d1f49-311">Service type registration</span></span>
<span data-ttu-id="d1f49-312">**System.Hosting** notifica un estado Correcto si el tipo de servicio se ha registrado correctamente.</span><span class="sxs-lookup"><span data-stu-id="d1f49-312">**System.Hosting** reports as OK if the service type has been registered successfully.</span></span> <span data-ttu-id="d1f49-313">Notifica un error si el registro no se ha realizado a tiempo (tal y como se ha configurado mediante **ServiceTypeRegistrationTimeout**).</span><span class="sxs-lookup"><span data-stu-id="d1f49-313">It reports an error if the registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="d1f49-314">Si se cierra el tiempo de ejecución, el tipo de servicio no está registrado en el nodo y Hosting notifica una advertencia.</span><span class="sxs-lookup"><span data-stu-id="d1f49-314">If the runtime is closed, the service type is unregistered from the node and Hosting reports a warning.</span></span>

* <span data-ttu-id="d1f49-315">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="d1f49-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="d1f49-316">**Property**: usa el prefijo **ServiceTypeRegistration** y contiene el nombre del tipo de servicio (por ejemplo, **ServiceTypeRegistration:FileStoreServiceType**).</span><span class="sxs-lookup"><span data-stu-id="d1f49-316">**Property**: Uses the prefix **ServiceTypeRegistration** and contains the service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="d1f49-317">El ejemplo siguiente muestra un paquete de servicio implementado con mantenimiento correcto:</span><span class="sxs-lookup"><span data-stu-id="d1f49-317">The following example shows a healthy deployed service package:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="d1f49-318">Descargar</span><span class="sxs-lookup"><span data-stu-id="d1f49-318">Download</span></span>
<span data-ttu-id="d1f49-319">**System.Hosting** notifica un error si se produce un error en la descarga del paquete de servicio.</span><span class="sxs-lookup"><span data-stu-id="d1f49-319">**System.Hosting** reports an error if the service package download fails.</span></span>

* <span data-ttu-id="d1f49-320">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="d1f49-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="d1f49-321">**Property**: **Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="d1f49-321">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="d1f49-322">**Pasos siguientes**: investigue el motivo del error de descarga en el nodo.</span><span class="sxs-lookup"><span data-stu-id="d1f49-322">**Next steps**: Investigate why the download failed on the node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="d1f49-323">Validación de actualización</span><span class="sxs-lookup"><span data-stu-id="d1f49-323">Upgrade validation</span></span>
<span data-ttu-id="d1f49-324">**System.Hosting** notifica un error si se produce un error de validación durante la actualización o si se produce un error de actualización en el nodo.</span><span class="sxs-lookup"><span data-stu-id="d1f49-324">**System.Hosting** reports an error if validation during the upgrade fails or if the upgrade fails on the node.</span></span>

* <span data-ttu-id="d1f49-325">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="d1f49-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="d1f49-326">**Property**: usa el prefijo **FabricUpgradeValidation** y contiene la versión de actualización.</span><span class="sxs-lookup"><span data-stu-id="d1f49-326">**Property**: Uses the prefix **FabricUpgradeValidation** and contains the upgrade version</span></span>
* <span data-ttu-id="d1f49-327">**Description**: señala el error encontrado.</span><span class="sxs-lookup"><span data-stu-id="d1f49-327">**Description**: Points to the error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1f49-328">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d1f49-328">Next steps</span></span>
[<span data-ttu-id="d1f49-329">Vista de los informes de estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d1f49-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="d1f49-330">Notificación y comprobación del estado del servicio</span><span class="sxs-lookup"><span data-stu-id="d1f49-330">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="d1f49-331">Supervisión y diagnóstico de los servicios localmente</span><span class="sxs-lookup"><span data-stu-id="d1f49-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="d1f49-332">Actualización de la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d1f49-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

