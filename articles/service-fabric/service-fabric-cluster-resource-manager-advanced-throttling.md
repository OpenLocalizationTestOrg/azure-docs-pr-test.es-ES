---
title: "aaaThrottling en Administrador de recursos de clúster de Service Fabric Hola | Documentos de Microsoft"
description: "Obtenga información acerca de los aceleradores de hello tooconfigure proporcionadas por el servicio Administrador de recursos del clúster de tejido de Hola."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4a44678b-a5aa-4d30-958f-dc4332ebfb63
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f418536911d3e3814e78a4d9f057dfb867ca7c63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-hello-service-fabric-cluster-resource-manager"></a>Velocidad moderada Hola servicio Administrador de recursos del clúster de tejido
Incluso si Hola, Administrador de recursos del clúster que ha configurado correctamente, puede obtener interrumpa el clúster de Hola. ¿Por ejemplo, podría haber nodo y errores de dominio errores simultáneos - lo que sucedería si se produjo durante una actualización? Hola, Administrador de recursos del clúster siempre intenta toofix todo, consumiendo recursos del clúster de hello tratando de clúster de hello tooreorganize y corrección. Aceleradores ayudan a proporcionar una parada para que el clúster de hello puede utilizar los recursos toostabilize: nodos Hola vuelven, reparación de particiones de la red de hello, se implementan los bits corregidos.

toohelp con este tipo de situaciones, Hola, Administrador de recursos de clúster de tejido de servicio incluye varias limitaciones. Estas limitaciones son medidas bastante disruptivas. Generalmente no debe cambiarse sin realizar una planeación y pruebas rigurosas.

Si cambia los aceleradores del Administrador de recursos de clúster hello, debe ajustarlos carga real esperado de tooyour. Puede determinar que necesita toohave algunos limita en su lugar, incluso aunque esto signifique clúster Hola toma más toostabilize en algunas situaciones. Es necesario toodetermine Hola valores correctos para aceleradores pruebas. Aceleradores necesitan toobe tooallow lo suficientemente alto como Hola clúster toorespond toochanges en un intervalo de tiempo razonable, y baja suficiente tooactually evitar demasiado elevado consumo de recursos. 

La mayoría de los casos de Hola que hemos visto a los clientes usa aceleradores ha sido porque ya estaban en un entorno restringido de recursos. Algunos ejemplos serían ancho de banda de red limitado para los nodos individuales, o los discos que no están capaz de toobuild muchos réplicas con estado en paralelo debido a limitaciones de toothroughput. Sin aceleradores, las operaciones podrían sobrecargar estos recursos, que produce operaciones toofail o ser lenta. En estas situaciones, los clientes usan aceleradores y sabían que han ampliado la cantidad de Hola de tiempo que tardaría Hola clúster tooreach un estado estable. Los clientes también comprendían que podían terminar ejecutándose con una confiabilidad general menor mientras estaban con restricciones.


## <a name="configuring-hello-throttles"></a>Configuración de Hola de aceleradores

Tejido de servicio tiene dos mecanismos para la limitación de número de Hola de movimientos de réplica. mecanismo predeterminado de Hola que existían antes de Service Fabric 5.7 representa como un número absoluto de movimientos permitido de limitación. Esto no funciona con los clústeres de todos los tamaños. En concreto, para grandes clústeres Hola de manera predeterminada valor puede ser demasiado pequeño, ralentizar notablemente equilibrio incluso cuando sea necesario, al tiempo que tiene ningún efecto en clústeres más pequeños. Este mecanismo anterior ha sido reemplazada por la limitación de basadas en porcentajes, que se escala mejor con clústeres dinámicos en qué número de hello de servicios y nodos cambian con regularidad.

Hola aceleradores se basan en un porcentaje del número de Hola de réplicas en clústeres de Hola. Percetage según aceleradores Habilitar regla de hello expresar: "no se mueven más del 10% de las réplicas en un intervalo de 10 minutos", por ejemplo.

valores de configuración de Hola de limitación basada en porcentaje son:

  - GlobalMovementThrottleThresholdPercentage - número máximo de movimientos permitido en clúster en cualquier momento, expresado como porcentaje del número total de réplicas en clúster de Hola. 0 indica sin límite. valor predeterminado de Hello es 0. Si no se especifican esta opción y el GlobalMovementThrottleThreshold, a continuación, hello más conservador límite se utiliza.
  - GlobalMovementThrottleThresholdPercentageForPlacement - número máximo de movimientos permitidos durante la fase de selección de ubicación de hello, expresado como porcentaje del número total de réplicas en clúster de Hola. 0 indica sin límite. valor predeterminado de Hello es 0. Si no se especifican esta opción y el GlobalMovementThrottleThresholdForPlacement, a continuación, hello más conservador límite se utiliza.
  - GlobalMovementThrottleThresholdPercentageForBalancing - número máximo de movimientos permitidas durante Hola equilibrio fase, expresado como porcentaje del número total de réplicas en clúster de Hola. 0 indica sin límite. valor predeterminado de Hello es 0. Si no se especifican esta opción y el GlobalMovementThrottleThresholdForBalancing, a continuación, hello más conservador límite se utiliza.

Al especificar el porcentaje de limitación de hello, especificaría 5% como 0,05. intervalo de saludo en el que se rigen estos aceleradores es hello GlobalMovementThrottleCountingInterval, que se especifica en segundos.


``` xml
<Section Name="PlacementAndLoadBalancing">
     <Parameter Name="GlobalMovementThrottleThresholdPercentage" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForPlacement" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForBalancing" Value="0" />
     <Parameter Name="GlobalMovementThrottleCountingInterval" Value="600" />
</Section>
```

a través de ClusterConfig.json para las implementaciones independientes o Template.json para los clústeres hospedados en Azure:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "GlobalMovementThrottleThresholdPercentage",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForPlacement",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForBalancing",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleCountingInterval",
          "value": "600"
      }
    ]
  }
]
```

### <a name="default-count-based-throttles"></a>Recuento predeterminado basado en limitaciones
Esta información se ofrece por si tiene clústeres anteriores o todavía se conservan estas configuraciones en clústeres que se han actualizado desde entonces. En general, se recomienda que estos se reemplazan con aceleradores de basadas en porcentajes del saludo anteriores. Limitación basada en el porcentaje se encuentra deshabilitado de forma predeterminada, estos aceleradores permanecen Hola aceleradores de forma predeterminada para un clúster hasta que se deshabilita y reemplazados por aceleradores basadas en porcentajes de Hola. 

  - GlobalMovementThrottleThreshold: esta configuración controla el número total de hello movimientos en el clúster de hello en algún tiempo. cantidad de Hola de tiempo se especifica en segundos como hello GlobalMovementThrottleCountingInterval. valor predeterminado de Hola para hello GlobalMovementThrottleThreshold es 1000 y valor predeterminado de Hola para hello GlobalMovementThrottleCountingInterval es 600.
  - MovementPerPartitionThrottleThreshold: esta configuración controla el número total de Hola de movimientos para cualquier partición de servicio a través de algún tiempo. cantidad de Hola de tiempo se especifica en segundos como hello MovementPerPartitionThrottleCountingInterval. valor predeterminado de Hola para hello MovementPerPartitionThrottleThreshold es 50 y valor predeterminado de Hola para hello MovementPerPartitionThrottleCountingInterval es 600.

configuración de Hola para estos aceleradores sigue Hola mismo patrón como Hola basadas en porcentajes de limitación.

## <a name="next-steps"></a>Pasos siguientes
- toofind out acerca de cómo Hola, Administrador de recursos del clúster administra y equilibra la carga en el clúster de hello, desproteger artículo hello en [equilibrio de carga](service-fabric-cluster-resource-manager-balancing.md)
- Hola, Administrador de recursos del clúster tiene muchas opciones para describir el clúster de Hola. toofind más información acerca de ellos, consulte este artículo en [que describe un clúster de Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
