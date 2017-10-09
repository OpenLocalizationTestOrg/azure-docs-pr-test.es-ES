---
title: 'Cluster Resource Manager de Service Fabric: costo de movimiento | Microsoft Docs'
description: "Información general del costo de movimiento de los servicios de Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 65d4ac73efffcf7b25b1e95da6f9012a9238cb75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-movement-cost"></a>Costo del movimiento del servicio
Un factor que Hola Administrador de recursos de clúster de tejido de servicio tiene en cuenta al intentar toodetermine qué clúster de tooa toomake de cambios es el costo de Hola de esos cambios. noción de Hola de "costo" es sopesar con respecto a cuánto clúster Hola se puede mejorar. El costo se tiene en cuenta al mover los servicios por cuestiones de equilibrio, desfragmentación y otros requisitos. objetivo de Hello es toomeet requisitos de Hola Hola menos forma perjudiciales o costosa. 

Mover servicios supone unos costos mínimos de tiempo de CPU y ancho de banda de red. Para los servicios con estado, requiere copiar estado Hola de dichos servicios, consumiendo memoria adicional y disco. Minimizan los costos de Hola de soluciones que Hola Administrador de recursos de clúster de Azure Service Fabric aparece con la ayuda a garantizar que no se invierte en recursos del clúster de hello innecesariamente. Sin embargo, también prefiere no tooignore soluciones que podrían mejorar notablemente asignación Hola de recursos de clúster de Hola.

Hola, Administrador de recursos del clúster tiene dos maneras de calcular los costos y limita su acceso mientras lo intenta de clúster de hello toomanage. primer mecanismo de Hello simplemente está contando cada movimiento que sería. Si se generan dos soluciones con hello mismo equilibrar (puntuación), a continuación, Hola, Administrador de recursos de clúster prefiere Hola uno con hello menor coste (número total de movimientos).

Esta estrategia da buenos resultados. Pero, al igual que con cargas predeterminadas o estáticas, es poco probable que en cualquier sistema complejo todos los movimientos sean iguales. Algunas son probablemente toobe mucho más caro.

## <a name="setting-move-costs"></a>Establecimiento de los costos de movimiento 
Puede especificar el costo de movimiento de hello predeterminado para un servicio cuando se crea:

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

C#: 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

También puede especificar o actualizar MoveCost dinámicamente para un servicio después de que se ha creado el servicio de hello: 

PowerShell: 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

C#:

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a>Especificación de forma dinámica del costo de movimiento por réplica

Hello fragmentos de código anteriores son todos para especificar MoveCost para un servicio completo al mismo tiempo desde el propio servicio Hola exterior. Sin embargo, mover el costo es más útil es cuando cambia el costo de movimiento de Hola de un objeto de servicio específico sobre su duración. Puesto que Hola servicios por sí mismos, probablemente tiene Hola mejor idea de cómo costosos son toomove un momento dado, hay una API para tooreport servicios su propios movimiento individual de costo en tiempo de ejecución. 

C#:

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a>Impacto del costo de movimiento
El valor MoveCost tiene cuatro niveles: Zero (Cero), Low (Bajo), Medium (Medio) y High (Alto). MoveCosts son relativa tooeach otro, excepto cero. Cero costo de movimiento significa que el movimiento es gratuito y no debe contar con la puntuación de Hola de solución de Hola. Configuración de su movimiento costo tooHigh *no* garantiza que la réplica Hola permanece en un solo lugar.

<center>
![Costo de movimiento como un factor en la selección de réplicas para el movimiento][Image1]
</center>

MoveCost le ayuda a encontrar soluciones de Hola que causa Hola menor interrupción general y es más fácil tooachieve mientras todavía que llegan al saldo equivalente. Noción de un servicio de costo puede ser relativa toomany cosas. Hello factores más comunes para calcular el costo de movimiento son:

- cantidad de Hola de estado o los datos que el servicio de hello tiene toomove.
- costo de Hola de desconexión de los clientes. Mover una réplica principal es normalmente más elevado que el costo de Hola de mover una réplica secundaria.
- costo de Hola de interrumpir una operación en curso. Nivel de almacén de algunas operaciones en datos de Hola o las operaciones realizadas en la llamada de cliente de respuesta tooa son costosas. Después de un punto determinado, no desea toostop en caso de que no es necesario. Por lo tanto mientras la operación de hello está sucediendo, aumentar costo de movimiento de Hola de esta probabilidad de Hola de tooreduce de objeto de servicio que se desplaza. Cuando se realiza la operación de hello, establezca Hola costo atrás toonormal.

## <a name="enabling-move-cost-in-your-cluster"></a>Habilitación del costo de movimiento en el clúster
En orden para Hola más granular toobe MoveCosts tener en cuenta, MoveCost debe estar habilitada en el clúster. Sin esta configuración, se utiliza el modo de predeterminado de Hola de recuento de movimientos para calcular MoveCost y MoveCost informes se omiten.


ClusterManifest.xml:

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

a través de ClusterConfig.json para las implementaciones independientes o Template.json para los clústeres hospedados en Azure:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a>Pasos siguientes
- Administrador de recursos de clúster de tejido de servicio utiliza métricas toomanage consumo y la capacidad de clúster Hola. toolearn más información acerca de las métricas y cómo tooconfigure, visite [consumo de recursos de administración y carga de Service Fabric con métricas](service-fabric-cluster-resource-manager-metrics.md).
- toolearn acerca de cómo Hola, Administrador de recursos del clúster administra y equilibra la carga en el clúster de hello, visite [equilibrio su clúster de Service Fabric](service-fabric-cluster-resource-manager-balancing.md).

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
