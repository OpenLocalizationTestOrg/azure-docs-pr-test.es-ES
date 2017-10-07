---
title: aaaTroubleshoot con informes de mantenimiento del sistema | Documentos de Microsoft
description: "Describe los informes de mantenimiento de hello enviados por los componentes del tejido de servicio de Azure y su uso de clúster para solucionar problemas o problemas de la aplicación."
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
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a><span data-ttu-id="b3db3-103">Usar tootroubleshoot de informes de estado de sistema</span><span class="sxs-lookup"><span data-stu-id="b3db3-103">Use system health reports tootroubleshoot</span></span>
<span data-ttu-id="b3db3-104">Azure Service Fabric componentes informe fuera del cuadro de hello en todas las entidades de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-104">Azure Service Fabric components report out of hello box on all entities in hello cluster.</span></span> <span data-ttu-id="b3db3-105">Hola [almacén de estado](service-fabric-health-introduction.md#health-store) crea y elimina las entidades basándose en los informes del sistema Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-105">hello [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on hello system reports.</span></span> <span data-ttu-id="b3db3-106">También las organiza en una jerarquía que captura las interacciones de la entidad.</span><span class="sxs-lookup"><span data-stu-id="b3db3-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="b3db3-107">más información, lea los conceptos relacionados con el estado de toounderstand, [modelo de estado de Service Fabric](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b3db3-107">toounderstand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="b3db3-108">Los informes de mantenimiento del sistema proporcionan visibilidad en el clúster y funcionalidad de la aplicación, así como indican problemas a través del mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="b3db3-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="b3db3-109">Para aplicaciones y servicios, informes de mantenimiento del sistema comprueban que las entidades se implementan y se comportan correctamente desde la perspectiva de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from hello Service Fabric perspective.</span></span> <span data-ttu-id="b3db3-110">informes de Hello no proporcionan ninguna supervisión de estado de lógica de negocios de Hola de servicio de Hola o detección de procesos bloqueados.</span><span class="sxs-lookup"><span data-stu-id="b3db3-110">hello reports do not provide any health monitoring of hello business logic of hello service or detection of hung processes.</span></span> <span data-ttu-id="b3db3-111">Servicios de usuario pueden enriquecer datos de estado de hello con lógica de tootheir específico de información.</span><span class="sxs-lookup"><span data-stu-id="b3db3-111">User services can enrich hello health data with information specific tootheir logic.</span></span>

> [!NOTE]
> <span data-ttu-id="b3db3-112">Solo están visibles los informes de mantenimiento de watchdogs *después* componentes del sistema Hola crean una entidad.</span><span class="sxs-lookup"><span data-stu-id="b3db3-112">Watchdogs health reports are visible only *after* hello system components create an entity.</span></span> <span data-ttu-id="b3db3-113">Cuando se elimina una entidad, almacén de estado de hello elimina automáticamente todos los informes de estado asociados a él.</span><span class="sxs-lookup"><span data-stu-id="b3db3-113">When an entity is deleted, hello health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="b3db3-114">Hello mismo puede decirse cuando se crea una nueva instancia de entidad de hello (por ejemplo, se crea una nueva instancia de réplica de servicio persistente con estado).</span><span class="sxs-lookup"><span data-stu-id="b3db3-114">hello same is true when a new instance of hello entity is created (for example, a new stateful persisted service replica instance is created).</span></span> <span data-ttu-id="b3db3-115">Todos los informes asociados a la instancia anterior de Hola se elimina y se limpian del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-115">All reports associated with hello old instance are deleted and cleaned up from hello store.</span></span>
> 
> 

<span data-ttu-id="b3db3-116">informes de componentes de sistema Hello se identifican una origen de hello, que empieza por hello "**System.**"</span><span class="sxs-lookup"><span data-stu-id="b3db3-116">hello system component reports are identified by hello source, which starts with hello "**System.**"</span></span> <span data-ttu-id="b3db3-117">.</span><span class="sxs-lookup"><span data-stu-id="b3db3-117">prefix.</span></span> <span data-ttu-id="b3db3-118">Watchdogs no puede usar Hola igual de prefijo para sus orígenes, tal y como se rechazan los informes con parámetros no válidos.</span><span class="sxs-lookup"><span data-stu-id="b3db3-118">Watchdogs can't use hello same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="b3db3-119">Echemos un vistazo a algún sistema notifica toounderstand lo que les activa y cómo toocorrect Hola posibles problemas que representan.</span><span class="sxs-lookup"><span data-stu-id="b3db3-119">Let's look at some system reports toounderstand what triggers them and how toocorrect hello possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="b3db3-120">Service Fabric continúa tooadd informes en las condiciones de interés que mejoran la visibilidad de lo que ocurre en el clúster Hola y de aplicación.</span><span class="sxs-lookup"><span data-stu-id="b3db3-120">Service Fabric continues tooadd reports on conditions of interest that improve visibility into what is happening in hello cluster and application.</span></span> <span data-ttu-id="b3db3-121">También se pueden mejorar los informes existentes con más detalles toohelp solucionar problema Hola con mayor rapidez.</span><span class="sxs-lookup"><span data-stu-id="b3db3-121">Existing reports can also be enhanced with more details toohelp troubleshoot hello problem faster.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="b3db3-122">Informes de mantenimiento del sistema de clúster</span><span class="sxs-lookup"><span data-stu-id="b3db3-122">Cluster system health reports</span></span>
<span data-ttu-id="b3db3-123">entidad de mantenimiento del clúster de Hola se crea automáticamente en el almacén de estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-123">hello cluster health entity is created automatically in hello health store.</span></span> <span data-ttu-id="b3db3-124">Si todo funciona correctamente, no tiene un informe del sistema.</span><span class="sxs-lookup"><span data-stu-id="b3db3-124">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="b3db3-125">Pérdida de entorno</span><span class="sxs-lookup"><span data-stu-id="b3db3-125">Neighborhood loss</span></span>
<span data-ttu-id="b3db3-126">**System.Federation** notifica un error cuando detecta una pérdida de entorno.</span><span class="sxs-lookup"><span data-stu-id="b3db3-126">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="b3db3-127">informe de Hello procede de los nodos individuales e Id. de nodo de Hola se incluye en el nombre de la propiedad de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-127">hello report is from individual nodes, and hello node ID is included in hello property name.</span></span> <span data-ttu-id="b3db3-128">Si se pierde un entorno en anillo de Service Fabric todo hello, normalmente pueden esperar dos eventos (ambos lados del informe de brechas de hello).</span><span class="sxs-lookup"><span data-stu-id="b3db3-128">If one neighborhood is lost in hello entire Service Fabric ring, you can typically expect two events (both sides of hello gap report).</span></span> <span data-ttu-id="b3db3-129">Si se pierden más entornos, se producen más eventos.</span><span class="sxs-lookup"><span data-stu-id="b3db3-129">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="b3db3-130">informe de Hello especifica el tiempo de espera de hello concesión global como hora de hello toolive.</span><span class="sxs-lookup"><span data-stu-id="b3db3-130">hello report specifies hello global lease timeout as hello time toolive.</span></span> <span data-ttu-id="b3db3-131">informe de Hola se vuelve a enviar cada media de duración TTL de Hola para como condición de hello permanece activa.</span><span class="sxs-lookup"><span data-stu-id="b3db3-131">hello report is resent every half of hello TTL duration for as long as hello condition remains active.</span></span> <span data-ttu-id="b3db3-132">evento de Hola se quita automáticamente cuando esta expire.</span><span class="sxs-lookup"><span data-stu-id="b3db3-132">hello event is automatically removed when it expires.</span></span> <span data-ttu-id="b3db3-133">Quitar al comportamiento expirada garantiza que el informe de Hola se limpia del almacén de estado de hello correctamente, incluso si Hola informes nodo está inactivo.</span><span class="sxs-lookup"><span data-stu-id="b3db3-133">Remove when expired behavior ensures that hello report is cleaned up from hello health store correctly, even if hello reporting node is down.</span></span>

* <span data-ttu-id="b3db3-134">**SourceId**: System.Federation</span><span class="sxs-lookup"><span data-stu-id="b3db3-134">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="b3db3-135">**Propiedad**: comienza por **Neighborhood** e incluye información sobre el nodo.</span><span class="sxs-lookup"><span data-stu-id="b3db3-135">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="b3db3-136">**Pasos siguientes**: investigar por qué entorno Hola se pierde (por ejemplo, verificación Hola comunicación entre nodos del clúster).</span><span class="sxs-lookup"><span data-stu-id="b3db3-136">**Next steps**: Investigate why hello neighborhood is lost (for example, check hello communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="b3db3-137">Informes de mantenimiento del sistema de nodos</span><span class="sxs-lookup"><span data-stu-id="b3db3-137">Node system health reports</span></span>
<span data-ttu-id="b3db3-138">**System.FM**, que representa el servicio de administrador de conmutación por error de hello, es la autoridad de Hola que administra información acerca de los nodos de clúster.</span><span class="sxs-lookup"><span data-stu-id="b3db3-138">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about cluster nodes.</span></span> <span data-ttu-id="b3db3-139">Todos los nodos deben tener un informe de System.FM que muestre el estado.</span><span class="sxs-lookup"><span data-stu-id="b3db3-139">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="b3db3-140">entidades de nodo de Hola se quitan cuando se quita el estado del nodo hello (vea [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span><span class="sxs-lookup"><span data-stu-id="b3db3-140">hello node entities are removed when hello node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="b3db3-141">Nodo activo o inactivo</span><span class="sxs-lookup"><span data-stu-id="b3db3-141">Node up/down</span></span>
<span data-ttu-id="b3db3-142">System.FM notifica como Aceptar cuando une a nodo Hola anillo hello (está en funcionamiento).</span><span class="sxs-lookup"><span data-stu-id="b3db3-142">System.FM reports as OK when hello node joins hello ring (it's up and running).</span></span> <span data-ttu-id="b3db3-143">Notifica un error al nodo de hello sale anillo hello (no funciona, ya sea para actualizar o simplemente porque se produjo un error).</span><span class="sxs-lookup"><span data-stu-id="b3db3-143">It reports an error when hello node departs hello ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="b3db3-144">jerarquía de estado de Hello generado con el almacén de estado de hello realiza una acción sobre entidades implementadas en correlación con los informes del nodo System.FM.</span><span class="sxs-lookup"><span data-stu-id="b3db3-144">hello health hierarchy built by hello health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="b3db3-145">Considera que el nodo de Hola de un elemento primario virtual de todas las entidades implementadas.</span><span class="sxs-lookup"><span data-stu-id="b3db3-145">It considers hello node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="b3db3-146">entidades de Hello implementado en ese nodo se exponen a través de las consultas si el nodo de Hola se notifica como seguridad por System.FM, con hello misma instancia como instancia de hello asociada con entidades de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-146">hello deployed entities on that node are exposed through queries if hello node is reported as up by System.FM, with hello same instance as hello instance associated with hello entities.</span></span> <span data-ttu-id="b3db3-147">Cuando System.FM notifica ese nodo Hola está inactivo o reiniciado (una nueva instancia), almacén de estado de Hola se limpia automáticamente los entidades de hello implementado que pueden existir sólo en hello hacia abajo del nodo o en la instancia anterior de hello del nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-147">When System.FM reports that hello node is down or restarted (a new instance), hello health store automatically cleans up hello deployed entities that can exist only on hello down node or on hello previous instance of hello node.</span></span>

* <span data-ttu-id="b3db3-148">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="b3db3-148">**SourceId**: System.FM</span></span>
* <span data-ttu-id="b3db3-149">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="b3db3-149">**Property**: State</span></span>
* <span data-ttu-id="b3db3-150">**Pasos siguientes**: si el nodo de hello está inactivo para realizar una actualización, debería vuelven a estar en una vez que se ha actualizado.</span><span class="sxs-lookup"><span data-stu-id="b3db3-150">**Next steps**: If hello node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="b3db3-151">En este caso, el estado de mantenimiento de hello debería pasar tooOK atrás.</span><span class="sxs-lookup"><span data-stu-id="b3db3-151">In this case, hello health state should switch back tooOK.</span></span> <span data-ttu-id="b3db3-152">Si el nodo de hello no vuelven a estar o se produce un error, problema de hello necesita más investigación.</span><span class="sxs-lookup"><span data-stu-id="b3db3-152">If hello node doesn't come back or it fails, hello problem needs more investigation.</span></span>

<span data-ttu-id="b3db3-153">Hello en el ejemplo siguiente se muestra eventos de hello System.FM con un estado de mantenimiento de Aceptar de nodo:</span><span class="sxs-lookup"><span data-stu-id="b3db3-153">hello following example shows hello System.FM event with a health state of OK for node up:</span></span>

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


### <a name="certificate-expiration"></a><span data-ttu-id="b3db3-154">Caducidad del certificado</span><span class="sxs-lookup"><span data-stu-id="b3db3-154">Certificate expiration</span></span>
<span data-ttu-id="b3db3-155">**System.FabricNode** emite una advertencia cuando los certificados usados por nodo de hello son van a caducar.</span><span class="sxs-lookup"><span data-stu-id="b3db3-155">**System.FabricNode** reports a warning when certificates used by hello node are near expiration.</span></span> <span data-ttu-id="b3db3-156">Hay tres certificados por nodo: **Certificate_cluster**, **Certificate_server** y **Certificate_default_client**.</span><span class="sxs-lookup"><span data-stu-id="b3db3-156">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="b3db3-157">Una vez expiración Hola al menos dos semanas, estado de mantenimiento de informes de hello es correcto.</span><span class="sxs-lookup"><span data-stu-id="b3db3-157">When hello expiration is at least two weeks away, hello report health state is OK.</span></span> <span data-ttu-id="b3db3-158">Una vez expiración Hola menos de dos semanas, el tipo de informe de hello es una advertencia.</span><span class="sxs-lookup"><span data-stu-id="b3db3-158">When hello expiration is within two weeks, hello report type is a warning.</span></span> <span data-ttu-id="b3db3-159">TTL de estos eventos es infinito, y se quitan cuando sale de un nodo de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-159">TTL of these events is infinite, and they are removed when a node leaves hello cluster.</span></span>

* <span data-ttu-id="b3db3-160">**SourceId**: System.FabricNode</span><span class="sxs-lookup"><span data-stu-id="b3db3-160">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="b3db3-161">**Propiedad**: comienza con **certificado** y contiene más información sobre el tipo de certificado de Hola</span><span class="sxs-lookup"><span data-stu-id="b3db3-161">**Property**: Starts with **Certificate** and contains more information about hello certificate type</span></span>
* <span data-ttu-id="b3db3-162">**Pasos siguientes**: actualizar certificados de hello si fueran van a caducar.</span><span class="sxs-lookup"><span data-stu-id="b3db3-162">**Next steps**: Update hello certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="b3db3-163">Infracción de la capacidad de carga</span><span class="sxs-lookup"><span data-stu-id="b3db3-163">Load capacity violation</span></span>
<span data-ttu-id="b3db3-164">Hola equilibrador de carga de tejido de servicio emite una advertencia cuando detecta una infracción de la capacidad de nodo.</span><span class="sxs-lookup"><span data-stu-id="b3db3-164">hello Service Fabric Load Balancer reports a warning when it detects a node capacity violation.</span></span>

* <span data-ttu-id="b3db3-165">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="b3db3-165">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="b3db3-166">**Property**: comienza por **Capacity**.</span><span class="sxs-lookup"><span data-stu-id="b3db3-166">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="b3db3-167">**Pasos siguientes**: comprobación proporciona métricas y la vista capacidad actual de hello en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-167">**Next steps**: Check provided metrics and view hello current capacity on hello node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="b3db3-168">Informes de mantenimiento del sistema de la aplicación</span><span class="sxs-lookup"><span data-stu-id="b3db3-168">Application system health reports</span></span>
<span data-ttu-id="b3db3-169">**System.CM**, que representa el servicio de administrador de clústeres de hello, es la autoridad de Hola que administra información acerca de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="b3db3-169">**System.CM**, which represents hello Cluster Manager service, is hello authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="b3db3-170">Estado</span><span class="sxs-lookup"><span data-stu-id="b3db3-170">State</span></span>
<span data-ttu-id="b3db3-171">System.CM notifica como correcto cuando la aplicación hello se ha creado o actualizado.</span><span class="sxs-lookup"><span data-stu-id="b3db3-171">System.CM reports as OK when hello application has been created or updated.</span></span> <span data-ttu-id="b3db3-172">Informa al almacén de estado de hello cuando se ha eliminado la aplicación hello, por lo que se puede quitar del almacén.</span><span class="sxs-lookup"><span data-stu-id="b3db3-172">It informs hello health store when hello application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="b3db3-173">**SourceId**: System.CM</span><span class="sxs-lookup"><span data-stu-id="b3db3-173">**SourceId**: System.CM</span></span>
* <span data-ttu-id="b3db3-174">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="b3db3-174">**Property**: State</span></span>
* <span data-ttu-id="b3db3-175">**Pasos siguientes**: si se ha creado o actualizado aplicación hello, debe incluir el informe de mantenimiento del Administrador de clústeres de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-175">**Next steps**: If hello application has been created or updated, it should include hello Cluster Manager health report.</span></span> <span data-ttu-id="b3db3-176">En caso contrario, compruebe el estado de Hola de aplicación hello mediante la emisión de una consulta (por ejemplo, Hola cmdlet de PowerShell **ServiceFabricApplication de Get - ApplicationName *applicationName***).</span><span class="sxs-lookup"><span data-stu-id="b3db3-176">Otherwise, check hello state of hello application by issuing a query (for example, hello PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span></span>

<span data-ttu-id="b3db3-177">Hello en el ejemplo siguiente se muestra el evento de estado de hello en hello **fabric: / WordCount** aplicación:</span><span class="sxs-lookup"><span data-stu-id="b3db3-177">hello following example shows hello state event on hello **fabric:/WordCount** application:</span></span>

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

## <a name="service-system-health-reports"></a><span data-ttu-id="b3db3-178">Informes de mantenimiento del sistema de servicio</span><span class="sxs-lookup"><span data-stu-id="b3db3-178">Service system health reports</span></span>
<span data-ttu-id="b3db3-179">**System.FM**, que representa el servicio de administrador de conmutación por error de hello, es la autoridad de Hola que administra información acerca de los servicios.</span><span class="sxs-lookup"><span data-stu-id="b3db3-179">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="b3db3-180">Estado</span><span class="sxs-lookup"><span data-stu-id="b3db3-180">State</span></span>
<span data-ttu-id="b3db3-181">System.FM notifica como correcta cuando se ha creado el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-181">System.FM reports as OK when hello service has been created.</span></span> <span data-ttu-id="b3db3-182">Elimina la entidad de Hola de almacén de estado de hello, en cuando se ha eliminado el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-182">It deletes hello entity from hello health store when hello service has been deleted.</span></span>

* <span data-ttu-id="b3db3-183">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="b3db3-183">**SourceId**: System.FM</span></span>
* <span data-ttu-id="b3db3-184">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="b3db3-184">**Property**: State</span></span>

<span data-ttu-id="b3db3-185">Hello en el ejemplo siguiente se muestra eventos de estado de hello en el servicio de hello **fabric: / WordCount/WordCountWebService**:</span><span class="sxs-lookup"><span data-stu-id="b3db3-185">hello following example shows hello state event on hello service **fabric:/WordCount/WordCountWebService**:</span></span>

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

### <a name="service-correlation-error"></a><span data-ttu-id="b3db3-186">Error de correlación de servicio</span><span class="sxs-lookup"><span data-stu-id="b3db3-186">Service correlation error</span></span>
<span data-ttu-id="b3db3-187">**System.PLB** notifica un error cuando detecta que la actualización de un toobe servicio correlacionado con otro servicio crea una cadena de afinidad.</span><span class="sxs-lookup"><span data-stu-id="b3db3-187">**System.PLB** reports an error when it detects that updating a service toobe correlated with another service creates an affinity chain.</span></span> <span data-ttu-id="b3db3-188">informe de Hola se borra cuando se produce una actualización correcta.</span><span class="sxs-lookup"><span data-stu-id="b3db3-188">hello report is cleared when successful update happens.</span></span>

* <span data-ttu-id="b3db3-189">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="b3db3-189">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="b3db3-190">**Propiedad**: ServiceDescription</span><span class="sxs-lookup"><span data-stu-id="b3db3-190">**Property**: ServiceDescription</span></span>
* <span data-ttu-id="b3db3-191">**Pasos siguientes**: Hola de verificación correlacionado descripciones de servicio.</span><span class="sxs-lookup"><span data-stu-id="b3db3-191">**Next steps**: Check hello correlated service descriptions.</span></span>

## <a name="partition-system-health-reports"></a><span data-ttu-id="b3db3-192">Informes de mantenimiento del sistema de partición</span><span class="sxs-lookup"><span data-stu-id="b3db3-192">Partition system health reports</span></span>
<span data-ttu-id="b3db3-193">**System.FM**, que representa el servicio de administrador de conmutación por error de hello, es la autoridad de Hola que administra información acerca de las particiones de servicio.</span><span class="sxs-lookup"><span data-stu-id="b3db3-193">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="b3db3-194">Estado</span><span class="sxs-lookup"><span data-stu-id="b3db3-194">State</span></span>
<span data-ttu-id="b3db3-195">System.FM notifica como correcto cuando partición Hola se ha creado y está en buen estado.</span><span class="sxs-lookup"><span data-stu-id="b3db3-195">System.FM reports as OK when hello partition has been created and is healthy.</span></span> <span data-ttu-id="b3db3-196">Elimina la entidad de Hola de almacén de estado de hello, en cuando se elimina la partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-196">It deletes hello entity from hello health store when hello partition is deleted.</span></span>

<span data-ttu-id="b3db3-197">Si la partición de hello es inferior al recuento de réplica mínimo hello, notifica un error.</span><span class="sxs-lookup"><span data-stu-id="b3db3-197">If hello partition is below hello minimum replica count, it reports an error.</span></span> <span data-ttu-id="b3db3-198">Si la partición hello no es inferior al recuento de réplica mínimo hello, pero es inferior al recuento de réplica de destino de hello, emite una advertencia.</span><span class="sxs-lookup"><span data-stu-id="b3db3-198">If hello partition is not below hello minimum replica count, but it is below hello target replica count, it reports a warning.</span></span> <span data-ttu-id="b3db3-199">Si la partición de hello está en pérdida de quórum, System.FM notifica un error.</span><span class="sxs-lookup"><span data-stu-id="b3db3-199">If hello partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="b3db3-200">Otros eventos importantes incluyen una advertencia cuando una reconfiguración Hola tarda más de lo esperado y cuando la compilación de hello tarda más tiempo del esperado.</span><span class="sxs-lookup"><span data-stu-id="b3db3-200">Other important events include a warning when hello reconfiguration takes longer than expected and when hello build takes longer than expected.</span></span> <span data-ttu-id="b3db3-201">tiempos de Hello esperado para la compilación de Hola y volver a configurar son configurables basándose en los escenarios de servicio.</span><span class="sxs-lookup"><span data-stu-id="b3db3-201">hello expected times for hello build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="b3db3-202">Por ejemplo, si un servicio tiene un terabyte del estado, como la base de datos de SQL, compilación Hola tarda más de un servicio con una pequeña cantidad de estado.</span><span class="sxs-lookup"><span data-stu-id="b3db3-202">For example, if a service has a terabyte of state, such as SQL Database, hello build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="b3db3-203">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="b3db3-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="b3db3-204">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="b3db3-204">**Property**: State</span></span>
* <span data-ttu-id="b3db3-205">**Pasos siguientes**: si el estado de mantenimiento de hello no es correcto, es posible que algunas réplicas no han sido creado, abierto o promocionada tooprimary o base de datos secundaria correctamente.</span><span class="sxs-lookup"><span data-stu-id="b3db3-205">**Next steps**: If hello health state is not OK, it's possible that some replicas have not been created, opened, or promoted tooprimary or secondary correctly.</span></span> <span data-ttu-id="b3db3-206">En muchos casos, causa de hello es un error de servicio en hello abierta o la implementación de cambio de rol.</span><span class="sxs-lookup"><span data-stu-id="b3db3-206">In many instances, hello root cause is a service bug in hello open or change-role implementation.</span></span>

<span data-ttu-id="b3db3-207">Hola de ejemplo siguiente muestra una partición correcto:</span><span class="sxs-lookup"><span data-stu-id="b3db3-207">hello following example shows a healthy partition:</span></span>

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

<span data-ttu-id="b3db3-208">Hello en el ejemplo siguiente se muestra el estado de saludo de una partición que sea inferior al recuento de la réplica de destino.</span><span class="sxs-lookup"><span data-stu-id="b3db3-208">hello following example shows hello health of a partition that is below target replica count.</span></span> <span data-ttu-id="b3db3-209">Hola siguiente paso es descripción de la partición hello tooget, que muestra cómo se configura: **MinReplicaSetSize** es tres y **TargetReplicaSetSize** es siete.</span><span class="sxs-lookup"><span data-stu-id="b3db3-209">hello next step is tooget hello partition description, which shows how it is configured: **MinReplicaSetSize** is three and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="b3db3-210">A continuación, obtener el número de Hola de nodos de clúster hello: cinco.</span><span class="sxs-lookup"><span data-stu-id="b3db3-210">Then get hello number of nodes in hello cluster: five.</span></span> <span data-ttu-id="b3db3-211">En este caso, por lo que dos réplicas no se puede colocar como número de destino de Hola de réplicas es mayor que el número de Hola de nodos disponibles.</span><span class="sxs-lookup"><span data-stu-id="b3db3-211">So in this case, two replicas can't be placed because hello target number of replicas is higher than hello number of nodes available.</span></span>

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

### <a name="replica-constraint-violation"></a><span data-ttu-id="b3db3-212">Infracción de restricción de réplica</span><span class="sxs-lookup"><span data-stu-id="b3db3-212">Replica constraint violation</span></span>
<span data-ttu-id="b3db3-213">**System.PLB** notifica una advertencia si detecta una infracción de restricción de réplica y no se pueden colocar todas las réplicas de la partición.</span><span class="sxs-lookup"><span data-stu-id="b3db3-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place all partition replicas.</span></span> <span data-ttu-id="b3db3-214">Detalles del informe Hola muestran qué restricciones y propiedades de evitar que la ubicación de réplica de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-214">hello report details show which constraints and properties prevent hello replica placement.</span></span>

* <span data-ttu-id="b3db3-215">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="b3db3-215">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="b3db3-216">**Property**: comienza por **ReplicaConstraintViolation**.</span><span class="sxs-lookup"><span data-stu-id="b3db3-216">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="b3db3-217">Informes de mantenimiento del sistema de replica</span><span class="sxs-lookup"><span data-stu-id="b3db3-217">Replica system health reports</span></span>
<span data-ttu-id="b3db3-218">**System.RA**, que representa el componente del agente de reconfiguración de hello, es la autoridad de hello para el estado de réplica de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-218">**System.RA**, which represents hello reconfiguration agent component, is hello authority for hello replica state.</span></span>

### <a name="state"></a><span data-ttu-id="b3db3-219">Estado</span><span class="sxs-lookup"><span data-stu-id="b3db3-219">State</span></span>
<span data-ttu-id="b3db3-220">**System.RA** notifica Aceptar si se ha creado la réplica de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-220">**System.RA** reports OK when hello replica has been created.</span></span>

* <span data-ttu-id="b3db3-221">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="b3db3-221">**SourceId**: System.RA</span></span>
* <span data-ttu-id="b3db3-222">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="b3db3-222">**Property**: State</span></span>

<span data-ttu-id="b3db3-223">Hola de ejemplo siguiente muestra una réplica correcto:</span><span class="sxs-lookup"><span data-stu-id="b3db3-223">hello following example shows a healthy replica:</span></span>

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

### <a name="replica-open-status"></a><span data-ttu-id="b3db3-224">Estado de apertura de réplica</span><span class="sxs-lookup"><span data-stu-id="b3db3-224">Replica open status</span></span>
<span data-ttu-id="b3db3-225">Descripción de Hola de este informe de estado contiene la hora de inicio de hello (hora Universal) cuando se ha invocado Hola API llamada.</span><span class="sxs-lookup"><span data-stu-id="b3db3-225">hello description of this health report contains hello start time (Coordinated Universal Time) when hello API call was invoked.</span></span>

<span data-ttu-id="b3db3-226">**System.RA** emite una advertencia si réplica Hola abierto tarda más de período de hello configurado (valor predeterminado: 30 minutos).</span><span class="sxs-lookup"><span data-stu-id="b3db3-226">**System.RA** reports a warning if hello replica open takes longer than hello configured period (default: 30 minutes).</span></span> <span data-ttu-id="b3db3-227">Si Hola API afecta la disponibilidad de servicio, informe de Hola se emite mucho más rápido (un intervalo configurable, su valor predeterminado es 30 segundos).</span><span class="sxs-lookup"><span data-stu-id="b3db3-227">If hello API impacts service availability, hello report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="b3db3-228">tiempo de Hello medido incluye tiempo Hola de Replicador de hello abierto y el servicio de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="b3db3-228">hello time measured includes hello time taken for hello replicator open and hello service open.</span></span> <span data-ttu-id="b3db3-229">Hola propiedad cambios tooOK si abre Hola completa.</span><span class="sxs-lookup"><span data-stu-id="b3db3-229">hello property changes tooOK if hello open completes.</span></span>

* <span data-ttu-id="b3db3-230">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="b3db3-230">**SourceId**: System.RA</span></span>
* <span data-ttu-id="b3db3-231">**Property**: **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="b3db3-231">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="b3db3-232">**Pasos siguientes**: si el estado de mantenimiento de hello no es correcto, investigue por qué réplica Hola abierto tarda más de lo esperado.</span><span class="sxs-lookup"><span data-stu-id="b3db3-232">**Next steps**: If hello health state is not OK, investigate why hello replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="b3db3-233">Llamada a la API de servicio lenta</span><span class="sxs-lookup"><span data-stu-id="b3db3-233">Slow service API call</span></span>
<span data-ttu-id="b3db3-234">**System.RAP** y **System.Replicator** notificar una advertencia si un código de servicio de llamada toohello usuario tarda más tiempo de hello configurado.</span><span class="sxs-lookup"><span data-stu-id="b3db3-234">**System.RAP** and **System.Replicator** report a warning if a call toohello user service code takes longer than hello configured time.</span></span> <span data-ttu-id="b3db3-235">Advertencia de Hola se borra cuando se complete la llamada de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-235">hello warning is cleared when hello call completes.</span></span>

* <span data-ttu-id="b3db3-236">**SourceId**: System.RAP o System.Replicator</span><span class="sxs-lookup"><span data-stu-id="b3db3-236">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="b3db3-237">**Propiedad**: nombre Hola de hello lenta API.</span><span class="sxs-lookup"><span data-stu-id="b3db3-237">**Property**: hello name of hello slow API.</span></span> <span data-ttu-id="b3db3-238">Descripción de Hello proporciona más detalles sobre Hola Hola de tiempo API ha estado pendiente.</span><span class="sxs-lookup"><span data-stu-id="b3db3-238">hello description provides more details about hello time hello API has been pending.</span></span>
* <span data-ttu-id="b3db3-239">**Pasos siguientes**: investigar por qué llamada Hola tarda más tiempo del esperado.</span><span class="sxs-lookup"><span data-stu-id="b3db3-239">**Next steps**: Investigate why hello call takes longer than expected.</span></span>

<span data-ttu-id="b3db3-240">Hola de ejemplo siguiente muestra una partición de pérdida de quórum y Hola investigación pasos realiza toofigure el motivo.</span><span class="sxs-lookup"><span data-stu-id="b3db3-240">hello following example shows a partition in quorum loss, and hello investigation steps done toofigure out why.</span></span> <span data-ttu-id="b3db3-241">Una de las réplicas de hello tiene un estado de advertencia, por lo que obtiene su estado.</span><span class="sxs-lookup"><span data-stu-id="b3db3-241">One of hello replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="b3db3-242">Muestra que la operación de servicio de hello tarda más tiempo del esperado, un evento notificado por System.RAP.</span><span class="sxs-lookup"><span data-stu-id="b3db3-242">It shows that hello service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="b3db3-243">Una vez recibida esta información, Hola siguiente paso es toolook en el código del servicio de Hola e investigar no existe.</span><span class="sxs-lookup"><span data-stu-id="b3db3-243">After this information is received, hello next step is toolook at hello service code and investigate there.</span></span> <span data-ttu-id="b3db3-244">En este caso, Hola **Coredispatcher** implementación de servicio con estado Hola produce una excepción no controlada.</span><span class="sxs-lookup"><span data-stu-id="b3db3-244">For this case, hello **RunAsync** implementation of hello stateful service throws an unhandled exception.</span></span> <span data-ttu-id="b3db3-245">réplicas de Hola se reciclaje, por lo que quizás no pueda ver cualquier réplica en estado de advertencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-245">hello replicas are recycling, so you may not see any replicas in hello warning state.</span></span> <span data-ttu-id="b3db3-246">Puede vuelva a intentar obtener estado de mantenimiento de Hola y buscar las diferencias de hello Id. de réplica.</span><span class="sxs-lookup"><span data-stu-id="b3db3-246">You can retry getting hello health state and look for any differences in hello replica ID.</span></span> <span data-ttu-id="b3db3-247">En algunos casos, los reintentos de hello pueden proporcionar pistas.</span><span class="sxs-lookup"><span data-stu-id="b3db3-247">In certain cases, hello retries can give you clues.</span></span>

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

<span data-ttu-id="b3db3-248">Cuando se inicia la aplicación defectuoso hello en el depurador de hello, ventanas de eventos de diagnóstico de hello muestran excepción Hola de Coredispatcher:</span><span class="sxs-lookup"><span data-stu-id="b3db3-248">When you start hello faulty application under hello debugger, hello diagnostic events windows show hello exception thrown from RunAsync:</span></span>

![Eventos de diagnóstico de Visual Studio 2015: Error de RunAsync en fabric:/HelloWorldStatefulApplication.][1]

<span data-ttu-id="b3db3-250">Eventos de diagnóstico de Visual Studio 2015: Error de RunAsync en **fabric:/HelloWorldStatefulApplication**.</span><span class="sxs-lookup"><span data-stu-id="b3db3-250">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="b3db3-251">Cola de replicación completa</span><span class="sxs-lookup"><span data-stu-id="b3db3-251">Replication queue full</span></span>
<span data-ttu-id="b3db3-252">**System.Replicator** emite una advertencia cuando la cola de replicación de hello está llena.</span><span class="sxs-lookup"><span data-stu-id="b3db3-252">**System.Replicator** reports a warning when hello replication queue is full.</span></span> <span data-ttu-id="b3db3-253">En hello principal, cola de replicación normalmente llenarse porque una o varias réplicas secundarias son operaciones de tooacknowledge lenta.</span><span class="sxs-lookup"><span data-stu-id="b3db3-253">On hello primary, replication queue usually becomes full because one or more secondary replicas are slow tooacknowledge operations.</span></span> <span data-ttu-id="b3db3-254">En hello secundaria, esto suele ocurrir cuando el servicio de hello tooapply lenta Hola operaciones.</span><span class="sxs-lookup"><span data-stu-id="b3db3-254">On hello secondary, this usually happens when hello service is slow tooapply hello operations.</span></span> <span data-ttu-id="b3db3-255">Advertencia de Hola se borra cuando Hola cola ya no está llena.</span><span class="sxs-lookup"><span data-stu-id="b3db3-255">hello warning is cleared when hello queue is no longer full.</span></span>

* <span data-ttu-id="b3db3-256">**SourceId**: System.Replicator</span><span class="sxs-lookup"><span data-stu-id="b3db3-256">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="b3db3-257">**Propiedad**: **PrimaryReplicationQueueStatus** o **SecondaryReplicationQueueStatus**, según el rol de réplica Hola</span><span class="sxs-lookup"><span data-stu-id="b3db3-257">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on hello replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="b3db3-258">Operaciones de nomenclatura lentas</span><span class="sxs-lookup"><span data-stu-id="b3db3-258">Slow Naming operations</span></span>
<span data-ttu-id="b3db3-259">**System.NamingService** informa del estado en su réplica principal cuando una operación de nomenclatura tarda más de lo aceptable.</span><span class="sxs-lookup"><span data-stu-id="b3db3-259">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="b3db3-260">[CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) o [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) son ejemplos de operaciones de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="b3db3-260">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="b3db3-261">En FabricClient pueden encontrarse más métodos, como en [métodos de administración de servicios](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) o [métodos de administración de propiedades](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span><span class="sxs-lookup"><span data-stu-id="b3db3-261">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="b3db3-262">Hola Naming service resuelve ubicación tooa nombres del servicio de clúster de Hola y permite propiedades y los nombres de servicio de toomanage de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="b3db3-262">hello Naming service resolves service names tooa location in hello cluster and enables users toomanage service names and properties.</span></span> <span data-ttu-id="b3db3-263">Se trata de un servicio guardado con particiones de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b3db3-263">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="b3db3-264">Una de las particiones de hello representa Hola Authority Owner, que contiene metadatos sobre todos los servicios y nombres de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b3db3-264">One of hello partitions represents hello Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="b3db3-265">nombres de Service Fabric Hola son particiones de toodifferent asignadas, denominadas particiones Name Owner, por lo que el servicio de hello es extensible.</span><span class="sxs-lookup"><span data-stu-id="b3db3-265">hello Service Fabric names are mapped toodifferent partitions, called Name Owner partitions, so hello service is extensible.</span></span> <span data-ttu-id="b3db3-266">Obtenga más información sobre el [servicio de nomenclatura](service-fabric-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="b3db3-266">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="b3db3-267">Cuando una operación de escribir el nombre tiene más de lo esperado, operación Hola se marca con un informe de advertencia en hello *réplica principal de hello denominación de partición de servicio, que sirve de operación de hello*.</span><span class="sxs-lookup"><span data-stu-id="b3db3-267">When a Naming operation takes longer than expected, hello operation is flagged with a Warning report on hello *primary replica of hello Naming service partition that serves hello operation*.</span></span> <span data-ttu-id="b3db3-268">Si finaliza correctamente la operación de hello, hello advertencia está desactivada.</span><span class="sxs-lookup"><span data-stu-id="b3db3-268">If hello operation completes successfully, hello Warning is cleared.</span></span> <span data-ttu-id="b3db3-269">Si la operación de hello completa con un error, informe de mantenimiento de Hola incluye detalles sobre el error de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-269">If hello operation completes with an error, hello health report includes details about hello error.</span></span>

* <span data-ttu-id="b3db3-270">**SourceId**: System.NamingService</span><span class="sxs-lookup"><span data-stu-id="b3db3-270">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="b3db3-271">**Propiedad**: comienza con prefijo **Duration_** e identifica el funcionamiento lento de Hola y el nombre de Service Fabric hello en qué Hola se aplica la operación.</span><span class="sxs-lookup"><span data-stu-id="b3db3-271">**Property**: Starts with prefix **Duration_** and identifies hello slow operation and hello Service Fabric name on which hello operation is applied.</span></span> <span data-ttu-id="b3db3-272">Por ejemplo, si crear servicio en el tejido de nombre: / MyApp/MyService tarda demasiado, propiedad de hello es Duration_AOCreateService.fabric:/MyApp/MyService.</span><span class="sxs-lookup"><span data-stu-id="b3db3-272">For example, if create service at name fabric:/MyApp/MyService takes too long, hello property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="b3db3-273">Rol de toohello AO puntos del programa Hola a escribir el nombre de partición para este nombre y la operación.</span><span class="sxs-lookup"><span data-stu-id="b3db3-273">AO points toohello role of hello Naming partition for this name and operation.</span></span>
* <span data-ttu-id="b3db3-274">**Pasos siguientes**: ¿por qué se produce un error en la operación de nomenclatura de Hola de comprobación.</span><span class="sxs-lookup"><span data-stu-id="b3db3-274">**Next steps**: Check why hello Naming operation fails.</span></span> <span data-ttu-id="b3db3-275">Cada operación puede tener diferentes causas.</span><span class="sxs-lookup"><span data-stu-id="b3db3-275">Each operation can have different root causes.</span></span> <span data-ttu-id="b3db3-276">Por ejemplo, eliminar servicio puede haberse atascado en un nodo porque el host de la aplicación hello sigue fallando en un nodo debido a errores de usuario de tooa en el código de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-276">For example, delete service may be stuck on a node because hello application host keeps crashing on a node due tooa user bug in hello service code.</span></span>

<span data-ttu-id="b3db3-277">Hola de ejemplo siguiente muestra una operación de servicio de creación.</span><span class="sxs-lookup"><span data-stu-id="b3db3-277">hello following example shows a create service operation.</span></span> <span data-ttu-id="b3db3-278">operación de Hello ha tardado más tiempo más tiempo en ejecutarse Hola configurado.</span><span class="sxs-lookup"><span data-stu-id="b3db3-278">hello operation took longer than hello configured duration.</span></span> <span data-ttu-id="b3db3-279">AO reintenta y envía tooNO de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b3db3-279">AO retries and sends work tooNO.</span></span> <span data-ttu-id="b3db3-280">NINGUNA operación de la última Hola completada con tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="b3db3-280">NO completed hello last operation with Timeout.</span></span> <span data-ttu-id="b3db3-281">En este caso, hello misma réplica es el principal de hello AO y ningún rol.</span><span class="sxs-lookup"><span data-stu-id="b3db3-281">In this case, hello same replica is primary for both hello AO and NO roles.</span></span>

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
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
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
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="b3db3-282">Informes de mantenimiento del sistema DeployedApplication</span><span class="sxs-lookup"><span data-stu-id="b3db3-282">DeployedApplication system health reports</span></span>
<span data-ttu-id="b3db3-283">**System.Hosting** es autoridad hello en entidades implementadas.</span><span class="sxs-lookup"><span data-stu-id="b3db3-283">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="b3db3-284">Activación</span><span class="sxs-lookup"><span data-stu-id="b3db3-284">Activation</span></span>
<span data-ttu-id="b3db3-285">System.Hosting notifica como correcta cuando una aplicación se ha activado correctamente en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-285">System.Hosting reports as OK when an application has been successfully activated on hello node.</span></span> <span data-ttu-id="b3db3-286">De lo contrario, notifica un error.</span><span class="sxs-lookup"><span data-stu-id="b3db3-286">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="b3db3-287">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="b3db3-287">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="b3db3-288">**Propiedad**: activación, incluida la versión de lanzamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="b3db3-288">**Property**: Activation, including hello rollout version</span></span>
* <span data-ttu-id="b3db3-289">**Pasos siguientes**: si la aplicación hello está en mal estado, investigue el motivo del error de activación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-289">**Next steps**: If hello application is unhealthy, investigate why hello activation failed.</span></span>

<span data-ttu-id="b3db3-290">Hello en el ejemplo siguiente se muestra una activación correcta:</span><span class="sxs-lookup"><span data-stu-id="b3db3-290">hello following example shows successful activation:</span></span>

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
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="b3db3-291">Descargar</span><span class="sxs-lookup"><span data-stu-id="b3db3-291">Download</span></span>
<span data-ttu-id="b3db3-292">**System.Hosting** notifica un error si se produce un error en la descarga del paquete de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-292">**System.Hosting** reports an error if hello application package download fails.</span></span>

* <span data-ttu-id="b3db3-293">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="b3db3-293">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="b3db3-294">**Property**: **Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="b3db3-294">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="b3db3-295">**Pasos siguientes**: investigar el motivo del error de descarga de hello en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-295">**Next steps**: Investigate why hello download failed on hello node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="b3db3-296">Informes de mantenimiento del sistema DeployedServicePackage</span><span class="sxs-lookup"><span data-stu-id="b3db3-296">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="b3db3-297">**System.Hosting** es autoridad hello en entidades implementadas.</span><span class="sxs-lookup"><span data-stu-id="b3db3-297">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="b3db3-298">Activación de paquete de servicio</span><span class="sxs-lookup"><span data-stu-id="b3db3-298">Service package activation</span></span>
<span data-ttu-id="b3db3-299">System.Hosting notifica como Aceptar si la activación del paquete de servicio de hello en el nodo de hello es correcta.</span><span class="sxs-lookup"><span data-stu-id="b3db3-299">System.Hosting reports as OK if hello service package activation on hello node is successful.</span></span> <span data-ttu-id="b3db3-300">De lo contrario, notifica un error.</span><span class="sxs-lookup"><span data-stu-id="b3db3-300">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="b3db3-301">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="b3db3-301">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="b3db3-302">**Property**: Activation.</span><span class="sxs-lookup"><span data-stu-id="b3db3-302">**Property**: Activation</span></span>
* <span data-ttu-id="b3db3-303">**Pasos siguientes**: investigar el motivo del error de activación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-303">**Next steps**: Investigate why hello activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="b3db3-304">Activación del paquete de código</span><span class="sxs-lookup"><span data-stu-id="b3db3-304">Code package activation</span></span>
<span data-ttu-id="b3db3-305">**System.Hosting** notifica como Aceptar para cada paquete de código si la activación de hello es correcta.</span><span class="sxs-lookup"><span data-stu-id="b3db3-305">**System.Hosting** reports as OK for each code package if hello activation is successful.</span></span> <span data-ttu-id="b3db3-306">Si se produce un error en activación de hello, emite una advertencia conforme a la configuración.</span><span class="sxs-lookup"><span data-stu-id="b3db3-306">If hello activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="b3db3-307">Si **CodePackage** se produce un error tooactivate o se cierra con un error mayor Hola configurado **CodePackageHealthErrorThreshold**, hospedaje notifica un error.</span><span class="sxs-lookup"><span data-stu-id="b3db3-307">If **CodePackage** fails tooactivate or terminates with an error greater than hello configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="b3db3-308">Si hay varios paquetes de código en un paquete de servicios, se genera un informe de activación para cada uno.</span><span class="sxs-lookup"><span data-stu-id="b3db3-308">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="b3db3-309">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="b3db3-309">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="b3db3-310">**Propiedad**: prefijo de hello usa **CodePackageActivation** y contiene el nombre de Hola de paquete de código de hello y punto de entrada de hello como  **CodePackageActivation:* CodePackageName*:*SetupEntryPoint/EntryPoint*** (por ejemplo, **CodePackageActivation:Code:SetupEntryPoint**)</span><span class="sxs-lookup"><span data-stu-id="b3db3-310">**Property**: Uses hello prefix **CodePackageActivation** and contains hello name of hello code package and hello entry point as **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="b3db3-311">Registro del tipo de servicio</span><span class="sxs-lookup"><span data-stu-id="b3db3-311">Service type registration</span></span>
<span data-ttu-id="b3db3-312">**System.Hosting** notifica como correcto si el tipo de servicio de Hola se ha registrado correctamente.</span><span class="sxs-lookup"><span data-stu-id="b3db3-312">**System.Hosting** reports as OK if hello service type has been registered successfully.</span></span> <span data-ttu-id="b3db3-313">Notifica un error si no se realizó el registro de hello en el tiempo (según la configuración utilizando **ServiceTypeRegistrationTimeout**).</span><span class="sxs-lookup"><span data-stu-id="b3db3-313">It reports an error if hello registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="b3db3-314">Si se cierra en tiempo de ejecución de hello, tipo de servicio de Hola se anula el registro del nodo de Hola y hospedaje emite una advertencia.</span><span class="sxs-lookup"><span data-stu-id="b3db3-314">If hello runtime is closed, hello service type is unregistered from hello node and Hosting reports a warning.</span></span>

* <span data-ttu-id="b3db3-315">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="b3db3-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="b3db3-316">**Propiedad**: prefijo de hello usa **ServiceTypeRegistration** y contiene el nombre de tipo de servicio de hello (por ejemplo, **ServiceTypeRegistration:FileStoreServiceType**)</span><span class="sxs-lookup"><span data-stu-id="b3db3-316">**Property**: Uses hello prefix **ServiceTypeRegistration** and contains hello service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="b3db3-317">Hola de ejemplo siguiente muestra un paquete de servicio implementado correcto:</span><span class="sxs-lookup"><span data-stu-id="b3db3-317">hello following example shows a healthy deployed service package:</span></span>

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
                             Description           : hello ServicePackage was activated successfully.
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
                             Description           : hello CodePackage was activated successfully.
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
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="b3db3-318">Descargar</span><span class="sxs-lookup"><span data-stu-id="b3db3-318">Download</span></span>
<span data-ttu-id="b3db3-319">**System.Hosting** notifica un error si se produce un error en la descarga del paquete del servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-319">**System.Hosting** reports an error if hello service package download fails.</span></span>

* <span data-ttu-id="b3db3-320">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="b3db3-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="b3db3-321">**Property**: **Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="b3db3-321">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="b3db3-322">**Pasos siguientes**: investigar el motivo del error de descarga de hello en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-322">**Next steps**: Investigate why hello download failed on hello node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="b3db3-323">Validación de actualización</span><span class="sxs-lookup"><span data-stu-id="b3db3-323">Upgrade validation</span></span>
<span data-ttu-id="b3db3-324">**System.Hosting** notifica un error si se produce un error de validación durante la actualización de Hola o si hello actualización produce un error en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3db3-324">**System.Hosting** reports an error if validation during hello upgrade fails or if hello upgrade fails on hello node.</span></span>

* <span data-ttu-id="b3db3-325">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="b3db3-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="b3db3-326">**Propiedad**: prefijo de hello usa **FabricUpgradeValidation** y contiene la versión de actualización de Hola</span><span class="sxs-lookup"><span data-stu-id="b3db3-326">**Property**: Uses hello prefix **FabricUpgradeValidation** and contains hello upgrade version</span></span>
* <span data-ttu-id="b3db3-327">**Descripción**: puntos de error de toohello</span><span class="sxs-lookup"><span data-stu-id="b3db3-327">**Description**: Points toohello error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3db3-328">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3db3-328">Next steps</span></span>
[<span data-ttu-id="b3db3-329">Vista de los informes de estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b3db3-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="b3db3-330">¿Cómo tooreport y comprobación de estado de servicio</span><span class="sxs-lookup"><span data-stu-id="b3db3-330">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="b3db3-331">Supervisión y diagnóstico de los servicios localmente</span><span class="sxs-lookup"><span data-stu-id="b3db3-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="b3db3-332">Actualización de la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b3db3-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

