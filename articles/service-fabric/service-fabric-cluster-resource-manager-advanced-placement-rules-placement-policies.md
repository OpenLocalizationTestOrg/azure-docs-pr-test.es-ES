---
title: "aaaService Administrador de recursos de clúster de tejido - directivas de colocación | Documentos de Microsoft"
description: "Información general sobre las reglas y directivas de colocación adicionales para los servicios de Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 5c2d19c6-dd40-4c4b-abd3-5c5ec0abed38
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: bb58642520085ab3000f3929cf9aea7a8f6e3070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="placement-policies-for-service-fabric-services"></a><span data-ttu-id="39e33-103">Directivas de colocación de servicios de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="39e33-103">Placement policies for service fabric services</span></span>
<span data-ttu-id="39e33-104">Las directivas de selección de ubicación son reglas adicionales que pueden ser la selección de ubicación de servicio de toogovern utilizado en algunos escenarios concretos y menos común.</span><span class="sxs-lookup"><span data-stu-id="39e33-104">Placement policies are additional rules that can be used toogovern service placement in some specific, less-common scenarios.</span></span> <span data-ttu-id="39e33-105">Algunos ejemplos de esos escenarios son:</span><span class="sxs-lookup"><span data-stu-id="39e33-105">Some examples of those scenarios are:</span></span>

- <span data-ttu-id="39e33-106">El clúster de Service Fabric abarca distancias geográficas, como varios centros de datos locales o regiones de Azure</span><span class="sxs-lookup"><span data-stu-id="39e33-106">Your Service Fabric cluster spans geographic distances, such as multiple on-premises datacenters or across Azure regions</span></span>
- <span data-ttu-id="39e33-107">El entorno abarca varias áreas de control geopolítica o legal, o algún otro caso donde tiene límites de directiva necesario tooenforce</span><span class="sxs-lookup"><span data-stu-id="39e33-107">Your environment spans multiple areas of geopolitical or legal control, or some other case where you have policy boundaries you need tooenforce</span></span>
- <span data-ttu-id="39e33-108">Existen consideraciones de rendimiento o latencia de comunicación debido a distancias toolarge o el uso de vínculos de red más lenta o menos confiable</span><span class="sxs-lookup"><span data-stu-id="39e33-108">There are communication performance or latency considerations due toolarge distances or use of slower or less reliable network links</span></span>
- <span data-ttu-id="39e33-109">Necesita tookeep ciertas cargas de trabajo se colocan como un mejor esfuerzo, con otras cargas de trabajo o de proximidad toocustomers</span><span class="sxs-lookup"><span data-stu-id="39e33-109">You need tookeep certain workloads collocated as a best effort, either with other workloads or in proximity toocustomers</span></span>

<span data-ttu-id="39e33-110">La mayoría de estos requisitos se alinea con el diseño físico de Hola de clúster de hello, representado como Hola dominios de error de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="39e33-110">Most of these requirements align with hello physical layout of hello cluster, represented as hello fault domains of hello cluster.</span></span> 

<span data-ttu-id="39e33-111">Hola avanzada de directivas de colocación que ayudan a solucionar que estos escenarios son:</span><span class="sxs-lookup"><span data-stu-id="39e33-111">hello advanced placement policies that help address these scenarios are:</span></span>

1. <span data-ttu-id="39e33-112">Dominios no válidos</span><span class="sxs-lookup"><span data-stu-id="39e33-112">Invalid domains</span></span>
2. <span data-ttu-id="39e33-113">Dominios requeridos</span><span class="sxs-lookup"><span data-stu-id="39e33-113">Required domains</span></span>
3. <span data-ttu-id="39e33-114">Dominios de preferencia</span><span class="sxs-lookup"><span data-stu-id="39e33-114">Preferred domains</span></span>
4. <span data-ttu-id="39e33-115">No permitir el empaquetado de réplicas</span><span class="sxs-lookup"><span data-stu-id="39e33-115">Disallowing replica packing</span></span>

<span data-ttu-id="39e33-116">La mayoría de los siguientes controles de hello podría configurarse a través de propiedades de nodo y las restricciones de posición, pero algunos son más complicados.</span><span class="sxs-lookup"><span data-stu-id="39e33-116">Most of hello following controls could be configured via node properties and placement constraints, but some are more complicated.</span></span> <span data-ttu-id="39e33-117">toomake cosas más sencillas, Hola, Administrador de recursos de clúster de tejido de servicio proporciona estas directivas de selección de ubicación adicional.</span><span class="sxs-lookup"><span data-stu-id="39e33-117">toomake things simpler, hello Service Fabric Cluster Resource Manager provides these additional placement policies.</span></span> <span data-ttu-id="39e33-118">Las directivas de colocación se configuran por instancia de servicio con nombre previo.</span><span class="sxs-lookup"><span data-stu-id="39e33-118">Placement policies are configured on a per-named service instance basis.</span></span> <span data-ttu-id="39e33-119">También se pueden actualizar dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="39e33-119">They can also be updated dynamically.</span></span>

## <a name="specifying-invalid-domains"></a><span data-ttu-id="39e33-120">Especificación de dominios no válidos</span><span class="sxs-lookup"><span data-stu-id="39e33-120">Specifying invalid domains</span></span>
<span data-ttu-id="39e33-121">Hola **InvalidDomain** directiva de selección de ubicación le permite toospecify que un determinado dominio de error no es válido para un servicio específico.</span><span class="sxs-lookup"><span data-stu-id="39e33-121">hello **InvalidDomain** placement policy allows you toospecify that a particular Fault Domain is invalid for a specific service.</span></span> <span data-ttu-id="39e33-122">Resulta útil para garantizar que un servicio específico no se ejecute nunca en un área determinada, por ejemplo por motivos geopolíticos o relacionados con la directiva corporativa.</span><span class="sxs-lookup"><span data-stu-id="39e33-122">This policy ensures that a particular service never runs in a particular area, for example for geopolitical or corporate policy reasons.</span></span> <span data-ttu-id="39e33-123">Pueden especificarse varios dominios no válidos mediante distintas directivas.</span><span class="sxs-lookup"><span data-stu-id="39e33-123">Multiple invalid domains may be specified via separate policies.</span></span>

<span data-ttu-id="39e33-124"><center>
![Ejemplo de dominio no válido][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="39e33-124"><center>
![Invalid Domain Example][Image1]
</center></span></span>

<span data-ttu-id="39e33-125">Código:</span><span class="sxs-lookup"><span data-stu-id="39e33-125">Code:</span></span>

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="39e33-126">Powershell:</span><span class="sxs-lookup"><span data-stu-id="39e33-126">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a><span data-ttu-id="39e33-127">Especificación de dominios requeridos</span><span class="sxs-lookup"><span data-stu-id="39e33-127">Specifying required domains</span></span>
<span data-ttu-id="39e33-128">Hola requiere la directiva de selección de ubicación de dominio requiere que el servicio de hello está presente sólo en el dominio especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="39e33-128">hello required domain placement policy requires that hello service is present only in hello specified domain.</span></span> <span data-ttu-id="39e33-129">Pueden especificarse varios dominios requeridos mediante directivas diferentes.</span><span class="sxs-lookup"><span data-stu-id="39e33-129">Multiple required domains can be specified via separate policies.</span></span>

<span data-ttu-id="39e33-130"><center>
![Ejemplo de dominio requerido][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="39e33-130"><center>
![Required Domain Example][Image2]
</center></span></span>

<span data-ttu-id="39e33-131">Código:</span><span class="sxs-lookup"><span data-stu-id="39e33-131">Code:</span></span>

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

<span data-ttu-id="39e33-132">Powershell:</span><span class="sxs-lookup"><span data-stu-id="39e33-132">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a><span data-ttu-id="39e33-133">Especificar un dominio preferido para las réplicas principales de Hola de un servicio con estado</span><span class="sxs-lookup"><span data-stu-id="39e33-133">Specifying a preferred domain for hello primary replicas of a stateful service</span></span>
<span data-ttu-id="39e33-134">Dominio principal preferido Hello especifica tooplace de dominio de error de Hola Hola principal en.</span><span class="sxs-lookup"><span data-stu-id="39e33-134">hello Preferred Primary Domain specifies hello fault domain tooplace hello Primary in.</span></span> <span data-ttu-id="39e33-135">Hola principal finaliza en este dominio cuando todo está correcto.</span><span class="sxs-lookup"><span data-stu-id="39e33-135">hello Primary ends up in this domain when everything is healthy.</span></span> <span data-ttu-id="39e33-136">Si el dominio de Hola o la réplica principal de Hola se produce un error o se apaga, Hola principal mueve toosome otra ubicación, lo ideal es que en hello mismo dominio.</span><span class="sxs-lookup"><span data-stu-id="39e33-136">If hello domain or hello Primary replica fails or shuts down, hello Primary moves toosome other location, ideally in hello same domain.</span></span> <span data-ttu-id="39e33-137">Si esta nueva ubicación no está en el dominio preferidos hello, Hola se desplaza del Administrador de recursos de clúster nuevo dominio preferidos toohello tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="39e33-137">If this new location isn't in hello preferred domain, hello Cluster Resource Manager moves it back toohello preferred domain as soon as possible.</span></span> <span data-ttu-id="39e33-138">Evidentemente, esta configuración solo tiene sentido para los servicios con estado.</span><span class="sxs-lookup"><span data-stu-id="39e33-138">Naturally this setting only makes sense for stateful services.</span></span> <span data-ttu-id="39e33-139">Esta directiva resulta útil principalmente en clústeres que están distribuidos entre regiones de Azure o entre varios centros de datos, pero tienen servicios que prefieren la colocación en una determinada ubicación.</span><span class="sxs-lookup"><span data-stu-id="39e33-139">This policy is most useful in clusters that are spanned across Azure regions or multiple datacenters but have services that prefer placement in a certain location.</span></span> <span data-ttu-id="39e33-140">Mantener primarios cierre tootheir usuarios u otros servicios que ayuda a proporciona una menor latencia, especialmente para las lecturas, que se administran mediante los elementos de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="39e33-140">Keeping Primaries close tootheir users or other services helps provide lower latency, especially for reads, which are handled by Primaries by default.</span></span>

<span data-ttu-id="39e33-141"><center>
![Dominios principales preferidos y conmutación por error][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="39e33-141"><center>
![Preferred Primary Domains and Failover][Image3]
</center></span></span>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="39e33-142">Powershell:</span><span class="sxs-lookup"><span data-stu-id="39e33-142">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a><span data-ttu-id="39e33-143">Necesidad de la distribución de réplicas y prohibición del empaquetado</span><span class="sxs-lookup"><span data-stu-id="39e33-143">Requiring replica distribution and disallowing packing</span></span>
<span data-ttu-id="39e33-144">Las réplicas son _normalmente_ distribuidas a través de dominios de error y de actualización al clúster de hello es correcto.</span><span class="sxs-lookup"><span data-stu-id="39e33-144">Replicas are _normally_ distributed across fault and upgrade domains when hello cluster is healthy.</span></span> <span data-ttu-id="39e33-145">Sin embargo, hay casos donde más de una réplica para una partición determinada puede acabar empaquetada temporalmente en un solo dominio.</span><span class="sxs-lookup"><span data-stu-id="39e33-145">However, there are cases where more than one replica for a given partition may end up temporarily packed into a single domain.</span></span> <span data-ttu-id="39e33-146">Por ejemplo, supongamos que ese clúster hello tiene nueve nodos en tres dominios de error, fd: / 0, fd: / 1 y fd: / 2.</span><span class="sxs-lookup"><span data-stu-id="39e33-146">For example, let's say that hello cluster has nine nodes in three fault domains, fd:/0, fd:/1, and fd:/2.</span></span> <span data-ttu-id="39e33-147">Supongamos también que el servicio tiene tres réplicas.</span><span class="sxs-lookup"><span data-stu-id="39e33-147">Let's also say that your service has three replicas.</span></span> <span data-ttu-id="39e33-148">Supongamos que Hola nodos que se utiliza para las réplicas de fd: / 1 y fd: / 2 ha fallado.</span><span class="sxs-lookup"><span data-stu-id="39e33-148">Let's say that hello nodes that were being used for those replicas in fd:/1 and fd:/2 went down.</span></span> <span data-ttu-id="39e33-149">Normalmente Hola, Administrador de recursos del clúster preferiría otros nodos en los mismos dominios de error.</span><span class="sxs-lookup"><span data-stu-id="39e33-149">Normally hello Cluster Resource Manager would prefer other nodes in those same fault domains.</span></span> <span data-ttu-id="39e33-150">En este caso, supongamos que debido a problemas de toocapacity ninguno de hello otros nodos en los dominios que son válidos.</span><span class="sxs-lookup"><span data-stu-id="39e33-150">In this case, let's say due toocapacity issues none of hello other nodes in those domains were valid.</span></span> <span data-ttu-id="39e33-151">Si Hola, Administrador de recursos del clúster compila reemplazos de dichas réplicas, tendría toochoose nodos en fd: / 0.</span><span class="sxs-lookup"><span data-stu-id="39e33-151">If hello Cluster Resource Manager builds replacements for those replicas, it would have toochoose nodes in fd:/0.</span></span> <span data-ttu-id="39e33-152">Sin embargo, esto _que_ crea una situación donde se infringe Hola restricciones de dominio de error.</span><span class="sxs-lookup"><span data-stu-id="39e33-152">However, doing _that_ creates a situation where hello Fault Domain constraint is violated.</span></span> <span data-ttu-id="39e33-153">Empaquetado aumenta réplicas posibilidad de Hola que Hola conjunto de réplicas todo pudo dejan de funcionar o se pierdan.</span><span class="sxs-lookup"><span data-stu-id="39e33-153">Packing replicas increases hello chance that hello whole replica set could go down or be lost.</span></span> 

> [!NOTE]
> <span data-ttu-id="39e33-154">Para más información sobre las restricciones y las prioridades de restricción en general, consulte [este tema](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span><span class="sxs-lookup"><span data-stu-id="39e33-154">For more information on constraints and constraint priorities generally, check out [this topic](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span></span>
>

<span data-ttu-id="39e33-155">Si alguna vez vio un mensaje de estado como "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", es porque se topó con esta condición o algo parecido.</span><span class="sxs-lookup"><span data-stu-id="39e33-155">If you've ever seen a health message such as "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", then you've hit this condition or something like it.</span></span> <span data-ttu-id="39e33-156">Normalmente solo una o dos réplicas se empaquetan juntas temporalmente.</span><span class="sxs-lookup"><span data-stu-id="39e33-156">Usually only one or two replicas are packed together temporarily.</span></span> <span data-ttu-id="39e33-157">Siempre que haya menos de un cuórum de réplicas en un dominio dado, está seguro.</span><span class="sxs-lookup"><span data-stu-id="39e33-157">So long as there are fewer than a quorum of replicas in a given domain, you're safe.</span></span> <span data-ttu-id="39e33-158">Empaquetado es poco frecuente, pero esto puede suceder y estas situaciones suelen ser transitorias ya que los nodos de hello vuelven a estar.</span><span class="sxs-lookup"><span data-stu-id="39e33-158">Packing is rare, but it can happen, and usually these situations are transient since hello nodes come back.</span></span> <span data-ttu-id="39e33-159">Si nodos Hola queden hacia abajo y Hola, Administrador de recursos del clúster debe toobuild reemplazos, normalmente hay otros nodos disponibles en los dominios de error ideal de Hola.</span><span class="sxs-lookup"><span data-stu-id="39e33-159">If hello nodes do stay down and hello Cluster Resource Manager needs toobuild replacements, usually there are other nodes available in hello ideal fault domains.</span></span>

<span data-ttu-id="39e33-160">Algunas cargas de trabajo sería preferible tener siempre el número de destino de Hola de réplicas, incluso si se empaquetan en menos dominios.</span><span class="sxs-lookup"><span data-stu-id="39e33-160">Some workloads would prefer always having hello target number of replicas, even if they are packed into fewer domains.</span></span> <span data-ttu-id="39e33-161">Estas cargas de trabajo apuesta contra el número total de errores permanentes del dominio simultáneos y normalmente pueden recuperar el estado local.</span><span class="sxs-lookup"><span data-stu-id="39e33-161">These workloads are betting against total simultaneous permanent domain failures and can usually recover local state.</span></span> <span data-ttu-id="39e33-162">Otras cargas de trabajo en su lugar tardaría tiempo de inactividad de hello anterior a la corrección de riesgo o pérdida de datos.</span><span class="sxs-lookup"><span data-stu-id="39e33-162">Other workloads would rather take hello downtime earlier than risk correctness or loss of data.</span></span> <span data-ttu-id="39e33-163">La mayoría de las cargas de trabajo de producción se ejecutan con más de tres réplicas, más de tres dominios de error y muchos nodos válidos por dominio de error.</span><span class="sxs-lookup"><span data-stu-id="39e33-163">Most production workloads run with more than three replicas, more than three fault domains, and many valid nodes per fault domain.</span></span> <span data-ttu-id="39e33-164">Por este motivo, el comportamiento predeterminado de Hola permite empaquetado de dominio de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="39e33-164">Because of this, hello default behavior allows domain packing by default.</span></span> <span data-ttu-id="39e33-165">comportamiento predeterminado de Hello permite normal equilibrio y conmutación por error toohandle estos casos extremos, incluso si eso significa empaquetado de dominio temporal.</span><span class="sxs-lookup"><span data-stu-id="39e33-165">hello default behavior allows normal balancing and failover toohandle these extreme cases, even if that means temporary domain packing.</span></span>

<span data-ttu-id="39e33-166">Si desea toodisable este tipo de empaquetado para una carga de trabajo determinada, puede especificar hello `RequireDomainDistribution` directiva en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="39e33-166">If you want toodisable such packing for a given workload, you can specify hello `RequireDomainDistribution` policy on hello service.</span></span> <span data-ttu-id="39e33-167">Cuando se establece esta directiva, Hola, Administrador de recursos del clúster no garantiza ningún dos réplicas de hello misma partición que se ejecutan en hello mismo error o actualización de dominio.</span><span class="sxs-lookup"><span data-stu-id="39e33-167">When this policy is set, hello Cluster Resource Manager ensures no two replicas from hello same partition run in hello same fault or upgrade domain.</span></span>

<span data-ttu-id="39e33-168">Código:</span><span class="sxs-lookup"><span data-stu-id="39e33-168">Code:</span></span>

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

<span data-ttu-id="39e33-169">Powershell:</span><span class="sxs-lookup"><span data-stu-id="39e33-169">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

<span data-ttu-id="39e33-170">¿Ahora, tendría ser posible toouse estas configuraciones para los servicios en un clúster que no se ha distribuido geográficamente?</span><span class="sxs-lookup"><span data-stu-id="39e33-170">Now, would it be possible toouse these configurations for services in a cluster that was not geographically spanned?</span></span> <span data-ttu-id="39e33-171">Aunque podría, no hay razones de peso para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="39e33-171">You could, but there’s not a great reason too.</span></span> <span data-ttu-id="39e33-172">Hello las configuraciones de dominio necesarios, no válido y preferido deberían evitarse a menos que necesiten en escenarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="39e33-172">hello required, invalid, and preferred domain configurations should be avoided unless hello scenarios require them.</span></span> <span data-ttu-id="39e33-173">Que no tiene una carga de trabajo concreta toorun cualquier tooforce tootry de sentido en un único bastidor o tooprefer algún segmento de su clúster local frente a otro.</span><span class="sxs-lookup"><span data-stu-id="39e33-173">It doesn't make any sense tootry tooforce a given workload toorun in a single rack, or tooprefer some segment of your local cluster over another.</span></span> <span data-ttu-id="39e33-174">Se deben distribuir diferentes configuraciones de hardware entre dominios de error y se deben controlar mediante propiedades de nodo y restricciones de colocación normales.</span><span class="sxs-lookup"><span data-stu-id="39e33-174">Different hardware configurations should be spread across fault domains and handled via normal placement constraints and node properties.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39e33-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="39e33-175">Next steps</span></span>
- <span data-ttu-id="39e33-176">Para más información sobre la configuración de servicios, vaya a [este vínculo](service-fabric-cluster-resource-manager-configure-services.md).</span><span class="sxs-lookup"><span data-stu-id="39e33-176">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
