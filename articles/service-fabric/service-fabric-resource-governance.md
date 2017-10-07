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
# <a name="resource-governance"></a>Regulador de recursos 

Cuando se ejecutan varios servicios en hello mismo nodo o el clúster, es posible que un servicio puede consumir más recursos privar a otros servicios. Este problema es tooas que se hace referencia hello-vecino. Service Fabric permite las reservas toospecify de desarrollador de Hola y límites por los recursos del servicio tooguarantee y limitar su uso de recursos. 

## <a name="resource-governance-metrics"></a>Métricas de regulación de recursos 

Service Fabric admite la regulación de recursos en función del [paquete de servicio](service-fabric-application-model.md). recursos de Hello asignados tooService paquete pueden dividirse aún más entre los paquetes de código. límites de recursos de Hello especificados también significan una reserva Hola de recursos de Hola. Service Fabric admite la determinación de CPU y memoria por cada paquete de servicio mediante la utilización de dos [métricas](service-fabric-cluster-resource-manager-metrics.md) integradas:

* CPU (nombre de la métrica `ServiceFabric:/_CpuCores`): un núcleo es un núcleo lógico que está disponible en el equipo de host de Hola y todos los núcleos en todos los nodos se ponderan Hola igual.
* Memoria (nombre de la métrica `ServiceFabric:/_MemoryInMB`): memoria se expresa en megabytes y se asigna memoria toophysical que está disponible en la máquina de Hola.

Solo las garantías de reserva de software son siempre - en tiempo de ejecución de hello rechaza la apertura del nuevo servicio se superan los recursos disponibles de paquetes. Sin embargo, si otro archivo ejecutable o contenedor se coloca en el nodo de hello, que pueden infringir las garantías de reserva original Hola.

Para estos dos métricas Hola [Administrador de recursos del clúster](service-fabric-cluster-resource-manager-cluster-description.md) realiza un seguimiento de la capacidad total en el clúster, carga de hello en cada nodo de clúster de hello, y, quedan recursos en clúster de Hola. Estos dos métricas es equivalente tooany otro usuario o una métrica personalizada y todas las características existentes pueden usarse con ellos:
* Puede ser clúster [equilibrada](service-fabric-cluster-resource-manager-balancing.md) según las métricas de toothese dos (comportamiento predeterminado).
* Puede ser clúster [desfragmentados](service-fabric-cluster-resource-manager-defragmentation-metrics.md) según las métricas de toothese dos.
* Para [describir un clúster](service-fabric-cluster-resource-manager-cluster-description.md), se puede establecer la capacidad de almacenamiento en búfer para estas dos métricas.

El [informe de carga dinámica](service-fabric-cluster-resource-manager-metrics.md) no es compatible con estas métricas, y las cargas para estas métricas se definen en el momento de la creación.

## <a name="cluster-set-up-for-enabling-resource-governance"></a>Configuración del clúster para habilitar la regulación de recursos

Capacidad debe definirse manualmente en cada tipo de nodo de clúster de hello como sigue:

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
La regulación de recursos solo se admite en servicios de usuario y no en todos los servicios de sistema. Al especificar la capacidad, algunos núcleos y la memoria deben dejarse desasignados para los servicios de sistema. Para obtener un rendimiento óptimo, Hola después de la configuración debe también activarse en el manifiesto de clúster de hello: 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a>Definición de la regulación de recursos 

Límites de regulación de recursos se especifican en el manifiesto de aplicación Hola (sección ServiceManifestImport) como se muestra en el siguiente ejemplo de Hola:

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
  
En este ejemplo, el paquete de servicio ServicePackageA Obtiene un núcleo en nodos de Hola donde se coloca. Este paquete de servicio contiene dos paquetes de código (CodeA1 y CodeA2), y ambos especifican hello `CpuShares` parámetro. proporción de Hola de CpuShares 512:256 divide core Hola a todos los paquetes de código de hello dos. Por lo tanto, en este ejemplo, CodeA1 obtiene dos tercios de un núcleo y CodeA2 Obtiene una tercera parte de un núcleo (y Hola una reserva de garantía de software del mismo). En caso de que cuando CpuShares no se especifican para los paquetes de código, Service Fabric divide núcleos Hola equitativamente entre ellos.

Límites de memoria están absolutos, por lo que ambos paquetes de código too1024 limitado MB de memoria (y una reserva de garantía de software del mismo Hola). Paquetes de código (contenedores o procesos) no son tooallocate capaz de más memoria que este límite e intentar toodo que se producirá una excepción de memoria insuficiente. Para toowork de cumplimiento del límite de recursos, todos los paquetes de código dentro de un paquete de servicio deben tener límites de memoria especificados.


## <a name="next-steps"></a>Pasos siguientes
* toolearn más sobre recursos Administrador de clústeres, lea esta [artículo](service-fabric-cluster-resource-manager-introduction.md).
* toolearn más información sobre el modelo de aplicación, paquetes de servicio, paquetes de código y cómo asignan las réplicas toothem lea esta [artículo](service-fabric-application-model.md).
