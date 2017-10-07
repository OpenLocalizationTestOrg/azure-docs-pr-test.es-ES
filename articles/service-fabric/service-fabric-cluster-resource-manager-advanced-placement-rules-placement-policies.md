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
# <a name="placement-policies-for-service-fabric-services"></a>Directivas de colocación de servicios de Service Fabric
Las directivas de selección de ubicación son reglas adicionales que pueden ser la selección de ubicación de servicio de toogovern utilizado en algunos escenarios concretos y menos común. Algunos ejemplos de esos escenarios son:

- El clúster de Service Fabric abarca distancias geográficas, como varios centros de datos locales o regiones de Azure
- El entorno abarca varias áreas de control geopolítica o legal, o algún otro caso donde tiene límites de directiva necesario tooenforce
- Existen consideraciones de rendimiento o latencia de comunicación debido a distancias toolarge o el uso de vínculos de red más lenta o menos confiable
- Necesita tookeep ciertas cargas de trabajo se colocan como un mejor esfuerzo, con otras cargas de trabajo o de proximidad toocustomers

La mayoría de estos requisitos se alinea con el diseño físico de Hola de clúster de hello, representado como Hola dominios de error de clúster de Hola. 

Hola avanzada de directivas de colocación que ayudan a solucionar que estos escenarios son:

1. Dominios no válidos
2. Dominios requeridos
3. Dominios de preferencia
4. No permitir el empaquetado de réplicas

La mayoría de los siguientes controles de hello podría configurarse a través de propiedades de nodo y las restricciones de posición, pero algunos son más complicados. toomake cosas más sencillas, Hola, Administrador de recursos de clúster de tejido de servicio proporciona estas directivas de selección de ubicación adicional. Las directivas de colocación se configuran por instancia de servicio con nombre previo. También se pueden actualizar dinámicamente.

## <a name="specifying-invalid-domains"></a>Especificación de dominios no válidos
Hola **InvalidDomain** directiva de selección de ubicación le permite toospecify que un determinado dominio de error no es válido para un servicio específico. Resulta útil para garantizar que un servicio específico no se ejecute nunca en un área determinada, por ejemplo por motivos geopolíticos o relacionados con la directiva corporativa. Pueden especificarse varios dominios no válidos mediante distintas directivas.

<center>
![Ejemplo de dominio no válido][Image1]
</center>

Código:

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a>Especificación de dominios requeridos
Hola requiere la directiva de selección de ubicación de dominio requiere que el servicio de hello está presente sólo en el dominio especificado de Hola. Pueden especificarse varios dominios requeridos mediante directivas diferentes.

<center>
![Ejemplo de dominio requerido][Image2]
</center>

Código:

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a>Especificar un dominio preferido para las réplicas principales de Hola de un servicio con estado
Dominio principal preferido Hello especifica tooplace de dominio de error de Hola Hola principal en. Hola principal finaliza en este dominio cuando todo está correcto. Si el dominio de Hola o la réplica principal de Hola se produce un error o se apaga, Hola principal mueve toosome otra ubicación, lo ideal es que en hello mismo dominio. Si esta nueva ubicación no está en el dominio preferidos hello, Hola se desplaza del Administrador de recursos de clúster nuevo dominio preferidos toohello tan pronto como sea posible. Evidentemente, esta configuración solo tiene sentido para los servicios con estado. Esta directiva resulta útil principalmente en clústeres que están distribuidos entre regiones de Azure o entre varios centros de datos, pero tienen servicios que prefieren la colocación en una determinada ubicación. Mantener primarios cierre tootheir usuarios u otros servicios que ayuda a proporciona una menor latencia, especialmente para las lecturas, que se administran mediante los elementos de forma predeterminada.

<center>
![Dominios principales preferidos y conmutación por error][Image3]
</center>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a>Necesidad de la distribución de réplicas y prohibición del empaquetado
Las réplicas son _normalmente_ distribuidas a través de dominios de error y de actualización al clúster de hello es correcto. Sin embargo, hay casos donde más de una réplica para una partición determinada puede acabar empaquetada temporalmente en un solo dominio. Por ejemplo, supongamos que ese clúster hello tiene nueve nodos en tres dominios de error, fd: / 0, fd: / 1 y fd: / 2. Supongamos también que el servicio tiene tres réplicas. Supongamos que Hola nodos que se utiliza para las réplicas de fd: / 1 y fd: / 2 ha fallado. Normalmente Hola, Administrador de recursos del clúster preferiría otros nodos en los mismos dominios de error. En este caso, supongamos que debido a problemas de toocapacity ninguno de hello otros nodos en los dominios que son válidos. Si Hola, Administrador de recursos del clúster compila reemplazos de dichas réplicas, tendría toochoose nodos en fd: / 0. Sin embargo, esto _que_ crea una situación donde se infringe Hola restricciones de dominio de error. Empaquetado aumenta réplicas posibilidad de Hola que Hola conjunto de réplicas todo pudo dejan de funcionar o se pierdan. 

> [!NOTE]
> Para más información sobre las restricciones y las prioridades de restricción en general, consulte [este tema](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).
>

Si alguna vez vio un mensaje de estado como "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", es porque se topó con esta condición o algo parecido. Normalmente solo una o dos réplicas se empaquetan juntas temporalmente. Siempre que haya menos de un cuórum de réplicas en un dominio dado, está seguro. Empaquetado es poco frecuente, pero esto puede suceder y estas situaciones suelen ser transitorias ya que los nodos de hello vuelven a estar. Si nodos Hola queden hacia abajo y Hola, Administrador de recursos del clúster debe toobuild reemplazos, normalmente hay otros nodos disponibles en los dominios de error ideal de Hola.

Algunas cargas de trabajo sería preferible tener siempre el número de destino de Hola de réplicas, incluso si se empaquetan en menos dominios. Estas cargas de trabajo apuesta contra el número total de errores permanentes del dominio simultáneos y normalmente pueden recuperar el estado local. Otras cargas de trabajo en su lugar tardaría tiempo de inactividad de hello anterior a la corrección de riesgo o pérdida de datos. La mayoría de las cargas de trabajo de producción se ejecutan con más de tres réplicas, más de tres dominios de error y muchos nodos válidos por dominio de error. Por este motivo, el comportamiento predeterminado de Hola permite empaquetado de dominio de forma predeterminada. comportamiento predeterminado de Hello permite normal equilibrio y conmutación por error toohandle estos casos extremos, incluso si eso significa empaquetado de dominio temporal.

Si desea toodisable este tipo de empaquetado para una carga de trabajo determinada, puede especificar hello `RequireDomainDistribution` directiva en el servicio de Hola. Cuando se establece esta directiva, Hola, Administrador de recursos del clúster no garantiza ningún dos réplicas de hello misma partición que se ejecutan en hello mismo error o actualización de dominio.

Código:

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

¿Ahora, tendría ser posible toouse estas configuraciones para los servicios en un clúster que no se ha distribuido geográficamente? Aunque podría, no hay razones de peso para hacerlo. Hello las configuraciones de dominio necesarios, no válido y preferido deberían evitarse a menos que necesiten en escenarios de Hola. Que no tiene una carga de trabajo concreta toorun cualquier tooforce tootry de sentido en un único bastidor o tooprefer algún segmento de su clúster local frente a otro. Se deben distribuir diferentes configuraciones de hardware entre dominios de error y se deben controlar mediante propiedades de nodo y restricciones de colocación normales.

## <a name="next-steps"></a>Pasos siguientes
- Para más información sobre la configuración de servicios, vaya a [este vínculo](service-fabric-cluster-resource-manager-configure-services.md).

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
