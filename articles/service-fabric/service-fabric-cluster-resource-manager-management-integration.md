---
title: "aaaService Administrador de recursos de clúster de tejido - integración de administración | Documentos de Microsoft"
description: "Información general de los puntos de integración de hello entre Hola, Administrador de recursos del clúster y administración de tejido de servicio."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 956cd0b8-b6e3-4436-a224-8766320e8cd7
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9a24c9de121fbe2e8e5e8e4d117e64686918936a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-integration-with-service-fabric-cluster-management"></a>Integración del Administrador de recursos de clúster con la administración de clústeres de Service Fabric
Hola, Administrador de recursos de clúster de servicio de Fabric no lleve a cabo actualizaciones en Service Fabric, pero está implicado. Hola primera forma Hola ayuda de administrador de recursos de clúster con la administración por seguimiento Hola deseado estado del clúster de Hola y servicios de hello dentro de él. Hola, Administrador de recursos del clúster envía informes de estado cuando no se pone clúster hello en la configuración deseada de Hola. Por ejemplo, si no hay suficientes Hola capacidad Administrador de recursos del clúster envía errores que indican el problema de Hola y advertencias de mantenimiento. Otra parte de la integración de tiene toodo con el funcionamiento de las actualizaciones. Hola, Administrador de recursos del clúster modifica ligeramente su comportamiento durante las actualizaciones.  

## <a name="health-integration"></a>Integración del mantenimiento
Hola, Administrador de recursos del clúster constantemente realiza un seguimiento de reglas de Hola que ha definido para colocar los servicios. También realiza un seguimiento Hola restantes capacidad para cada métrica en nodos de Hola y en clúster de Hola y en clúster de Hola como un todo. Si no es posible satisfacer esas reglas o si no hay capacidad suficiente, se emiten errores y advertencias de mantenimiento. Por ejemplo, si un nodo está por encima de hello y capacidad de administrador de recursos de clúster intentará situación de hello toofix moviendo los servicios. Si no se puede corregir la situación de hello emite una advertencia de estado que indica qué nodo es a través de la capacidad y para las métricas.

Otro ejemplo de advertencias de mantenimiento del Administrador de recursos de hello es infracciones de restricciones de posición. Por ejemplo, si ha definido una restricción de selección de ubicación (como `“NodeColor == Blue”`) y Hola, Administrador de recursos detecta una infracción de restricción, emite una advertencia de estado. Esto es cierto para restricciones personalizadas y Hola predeterminado (por ejemplo, restricciones de dominio de error y actualización del dominio de hello).

A continuación se muestra un ejemplo de un informe de mantenimiento de este tipo En este caso, el informe de mantenimiento de hello es para una de las particiones del servicio de sistema de Hola. mensaje de bienvenida de mantenimiento indica Hola réplicas de esa partición se empaquetan temporalmente en muy pocos dominios de actualización.

```posh
PS C:\Users\User > Get-WindowsFabricPartitionHealth -PartitionId '00000000-0000-0000-0000-000000000001'


PartitionId           : 00000000-0000-0000-0000-000000000001
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.PLB', Property='ReplicaConstraintViolation_UpgradeDomain', HealthState='Warning', ConsiderWarningAsError=false.

ReplicaHealthStates   :
                        ReplicaId             : 130766528804733380
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577821
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528854889931
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577822
                        AggregatedHealthState : Ok

                        ReplicaId             : 130837073190680024
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.PLB
                        Property              : ReplicaConstraintViolation_UpgradeDomain
                        HealthState           : Warning
                        SequenceNumber        : 130837100116930204
                        SentAt                : 8/10/2015 7:53:31 PM
                        ReceivedAt            : 8/10/2015 7:53:33 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer has detected a Constraint Violation for this Replica: fabric:/System/FailoverManagerService Secondary Partition 00000000-0000-0000-0000-000000000001 is
                        violating hello Constraint: UpgradeDomain Details: UpgradeDomain ID -- 4, Replica on NodeName -- Node.8 Currently Upgrading -- false Distribution Policy -- Packing
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Ok->Warning = 8/10/2015 7:13:02 PM, LastError = 1/1/0001 12:00:00 AM
```

Esto es lo que nos dice este mensaje de mantenimiento:

1. Todas las réplicas de Hola por sí mismos son correctos: cada uno tiene AggregatedHealthState: correcto
2. actualmente se está infringe Hola restricción de distribución de la actualización del dominio. Esto significa que un dominio de actualización concreto tiene más réplicas de esta partición de lo que debería.
3. Qué nodo contiene infracción de hello réplica que producen Hola. En este caso es Hola nodo con el nombre de Hola "Node.8"
4. Si se está produciendo una actualización en esta partición ("Currently Upgrading -- false")
5. Hola directiva de distribución para este servicio: "Distribución directiva--empaquetado". Esto se rige por hello `RequireDomainDistribution` [directiva de colocación](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing). "Packing" indica que, en este caso, DomainDistribution _no_ era necesario, así que sabemos que no se especificó una directiva de colocación para este servicio. 
6. Cuándo se produjeron informe hello - 8/10/2015 7:13:02 P.M.

Información como este genera una alerta potencias que inician en toolet de producción sabe algo ha funcionado y también usa toodetect y detenga las actualizaciones incorrectas. En este caso, querríamos toosee si podemos averiguar por qué Hola, Administrador de recursos tenía toopack réplicas de hello en hello actualización del dominio. Normalmente empaquetado es transitorio porque nodos Hola Hola otros dominios de actualización se han hacia abajo, por ejemplo.

Supongamos que Hola, Administrador de recursos del clúster está intentando tooplace algunos servicios, pero no hay ninguna solución que funcione. Cuando no se puede colocar los servicios, suele funcionar es uno de hello siguientes motivos:

1. Una condición transitoria ha hecho que sea imposible tooplace esta instancia de servicio o la réplica correctamente
2. requisitos de ubicación del servicio de Hello son debe.

En estos casos, los informes de mantenimiento de Hola, Administrador de recursos del clúster ayudan a determinar por qué no se puede ubicar el servicio de Hola. Llamamos a esta secuencia de eliminación de restricción de Hola de proceso. Durante el proceso, sistema Hola le guía a través de restricciones de hello configurado que afecte a los registros y el servicio de hello lo que eliminan. Este modo, cuando los servicios no están capaz de toobe colocado, puede ver qué nodos se eliminaron y por qué.

## <a name="constraint-types"></a>Tipos de restricción:
Hablemos sobre cada una de las distintas restricciones de hello en los informes de estado. Verá las restricciones de toothese relacionados de mensajes de estado cuando no se puede colocar las réplicas.

* **ReplicaExclusionStatic** y **ReplicaExclusionDynamic**: estas restricciones indica que una solución se rechazó porque dos objetos de servicio de Hola misma partición toobe colocaría en hello mismo nodo. Esto no está permitido porque entonces el error de ese nodo afectaría demasiado a esa partición. ReplicaExclusionStatic y ReplicaExclusionDynamic son casi Hola realmente no importan mismas diferencias hello y reglas. Si está viendo una secuencia de eliminación de la restricción que contiene cualquier Hola restricción ReplicaExclusionStatic o ReplicaExclusionDynamic, Hola, Administrador de recursos del clúster se considera que hay suficientes nodos. Para ello, queda soluciones toouse estas ubicaciones no válidos que no están permitidos. Hello otras restricciones en la secuencia de hello normalmente nos indicará por qué nodos se se eliminan en primer lugar en Hola.
* **PlacementConstraint**: Si ve este mensaje, significa que se eliminaron, algunos nodos porque no coinciden con las restricciones de posición del servicio de Hola. Se realice un seguimiento a las restricciones de posición de hello configurada actualmente como parte de este mensaje. Esto es normal si tiene definida una restricción de colocación. Sin embargo, si restricción de selección de ubicación está provocando incorrectamente demasiadas toobe nodos eliminado es cómo verá.
* **NodeCapacity**: esta restricción significa que Hola Administrador de recursos del clúster no se pudo colocar réplicas de hello en hello indicado nodos, ya que podría poner a través de la capacidad.
* **Afinidad**: esta restricción indica que se no coloca réplica hello en nodos de hello afectado porque produciría una infracción de restricción de afinidad de Hola. Puede obtener más información sobre la afinidad en [este artículo](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md).
* **FaultDomain** y **UpgradeDomain**: esta restricción elimina nodos si colocar réplica Hola Hola indicado nodos causaría empaquetado en un error determinado o un dominio de actualización. Varios ejemplos hablar sobre esta restricción se presentan en el tema de hello en [las restricciones de dominio de error y de actualización y el comportamiento resultante](service-fabric-cluster-resource-manager-cluster-description.md)
* **PreferredLocation**: normalmente no debería verse esta restricción quitar nodos de solución de hello, ya que se ejecuta como una optimización de forma predeterminada. Hola preferido restricción de ubicación también está presente durante las actualizaciones. Durante la actualización es toomove usa servicios back-toowhere que estaban cuando se inició la actualización Hola.

## <a name="blocklisting-nodes"></a>Lista de bloqueo de nodos
Otro de los informes de administrador de recursos de clúster mantenimiento mensaje Hola es cuando hay nodos blocklisted. La lista de bloqueo se puede considerar como una restricción temporal que se le aplica automáticamente. Los nodos entran en la lista de bloqueo cuando experimentan errores repetidos al iniciar instancias de ese tipo de servicio. Los nodos se incluyen en la lista de bloqueo por tipo de servicio. Un nodo puede estar en la lista de bloqueo para un servicio pero no para otro. 

Podrá ver blocklisting aparecer con frecuencia durante el desarrollo: algunos errores hace que su toocrash de host de servicio de inicio. Service Fabric intenta host de servicio de hello toocreate varias veces, y sigue ocurriendo el error Hola. Después de varios intentos, nodo de Hola obtiene blocklisted y Hola, Administrador de recursos de clúster intentará toocreate servicio de hello en otro lugar. Si la situación de ese error continúa en varios nodos, es posible que todos nodos válido Hola Hola clúster acabar bloquean. Blocklisting también puede quitar tantos nodos que no hay suficiente puede iniciar correctamente el escalado de hello servicio toomeet Hola deseado. Normalmente verá más errores o las advertencias del Administrador de recursos de clúster de hello, que indica que el servicio de Hola está por debajo de la réplica deseada de Hola o recuento de instancias, así como mensajes de estado que indica qué error hello es que está causando toohello blocklisting en primer lugar en Hola.

La lista de bloqueo no es una condición permanente. Después de unos minutos, nodo de Hola se quita de la lista de bloqueo de Hola y Service Fabric posible activar servicios de hello en ese nodo de nuevo. Si los servicios continúan toofail, nodo de hello es blocklisted para ese tipo de servicio de nuevo. 

### <a name="constraint-priorities"></a>Prioridades de restricción

> [!WARNING]
> No se recomienda cambiar las prioridades, además de que podría tener efectos adversos sobre su clúster. Hola información siguiente se proporciona como referencia de prioridades de restricción predeterminada de Hola y su comportamiento. 
>

Con todas estas restricciones, puede que se han pensando "Hola: creo que las restricciones de dominio de error son lo más importante de hello en mi sistema. En orden tooensure hello restricciones de dominio de error no se ha infringido, soy considera tooviolate otras restricciones. "

Las restricciones se pueden configurar con diferentes niveles de prioridad: Dichos componentes son:

   - "alta" (0)
   - "baja" (1)
   - "optimización" (2)
   - "desactivado" (-1). 
   
La mayoría de las restricciones de Hola se configura como restricciones de disco duras de forma predeterminada.

Cambiar la prioridad de Hola de restricciones es poco habitual. Ha habido veces que las prioridades de restricción necesita toochange, por lo general toowork alrededor de algún otro error o comportamiento que influyó en el entorno de Hola. Generalmente flexibilidad de Hola de infraestructura de prioridad de restricción de hello ha trabajado muy bien, pero no se necesita a menudo. La mayoría de las veces de hello todo lo que se encuentra en sus prioridades predeterminadas. 

niveles de prioridad de Hello no significan que una restricción determinada _le_ se infringen, ni que siempre se cumplirá. Las prioridades de restricción definen el orden en el que se aplican las restricciones. Las prioridades de definen compensaciones hello cuando resulta imposible toosatisfy todas las restricciones. Normalmente se pueden satisfacer todas las restricciones de Hola a menos que haya pasando otra cosa en el entorno de Hola. Algunos ejemplos de escenarios que dará lugar a infracciones de tooconstraint son restricciones en conflicto, o un gran número de errores simultáneos.

En situaciones avanzadas, puede cambiar las prioridades de restricción de Hola. Por ejemplo, supongamos que desea que tooensure que siempre se infringirían afinidad cuando se emite la capacidad de los nodos toosolve necesarios. tooachieve esto, puede establecer la prioridad de Hola de restricción de afinidad Hola demasiado "soft" (1) y dejar Hola capacidad restricción se establece demasiado rígida"" (0).

valores de prioridad de Hello predeterminado para las distintas restricciones de Hola se especifican en hello después de configuración:

ClusterManifest.xml

```xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PlacementConstraintPriority" Value="0" />
            <Parameter Name="CapacityConstraintPriority" Value="0" />
            <Parameter Name="AffinityConstraintPriority" Value="0" />
            <Parameter Name="FaultDomainConstraintPriority" Value="0" />
            <Parameter Name="UpgradeDomainConstraintPriority" Value="1" />
            <Parameter Name="PreferredLocationConstraintPriority" Value="2" />
        </Section>
```

a través de ClusterConfig.json para las implementaciones independientes o Template.json para los clústeres hospedados en Azure:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PlacementConstraintPriority",
          "value": "0"
      },
      {
          "name": "CapacityConstraintPriority",
          "value": "0"
      },
      {
          "name": "AffinityConstraintPriority",
          "value": "0"
      },
      {
          "name": "FaultDomainConstraintPriority",
          "value": "0"
      },
      {
          "name": "UpgradeDomainConstraintPriority",
          "value": "1"
      },
      {
          "name": "PreferredLocationConstraintPriority",
          "value": "2"
      }
    ]
  }
]
```

## <a name="fault-domain-and-upgrade-domain-constraints"></a>Restricciones de dominio de error y dominio de actualización
Hola, Administrador de recursos del clúster que desee servicios tookeep reparten entre dominios de error y actualización. Esto modela como una restricción dentro del Administrador de recursos de clúster Hola motor. Para obtener más información sobre cómo se utilizan y su comportamiento específico, consulte el artículo de hello en [configuración de clúster](service-fabric-cluster-resource-manager-cluster-description.md#fault-and-upgrade-domain-constraints-and-resulting-behavior).

Hola, Administrador de recursos del clúster que tenga toopack algunas réplicas en un dominio de actualización en orden toodeal con actualizaciones, errores o a otras infracciones de restricción. Empaquetado en dominios de error o una actualización normalmente sólo se produce cuando hay varios errores o la renovación de otra en sistema de hello impide la selección de ubicación correcta. Si desea tooprevent empaquetado incluso durante estas situaciones, puede usar hello `RequireDomainDistribution` [directiva de colocación](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing). Sin embargo, considere detenidamente esta decisión, ya que puede afectar a la disponibilidad del servicio y a la confiabilidad, como efecto secundario.

Si el entorno de hello está configurado correctamente, todas las restricciones se respetan totalmente, incluso durante las actualizaciones. punto clave que se Hello es ese hello Administrador de recursos del clúster está supervisando de las restricciones. Cuando detecta una infracción inmediatamente lo notifica y trata de problema de hello toocorrect.

## <a name="hello-preferred-location-constraint"></a>Hola restricción de ubicación preferida
Hola PreferredLocation restricción es un poco diferente, porque tiene dos usos diferentes. Uno de los usos de esta restricción es durante las actualizaciones de aplicaciones. Hola, Administrador de recursos del clúster administra automáticamente esta restricción durante las actualizaciones. Es utilizado tooensure que, cuando actualiza están completos que réplicas devuelvan tootheir ubicaciones iniciales. Hola otros usos de hello PreferredLocation restricción son para hello [ `PreferredPrimaryDomain` directiva de colocación](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md). Ambas de estas optimizaciones y, por tanto, hello PreferredLocation restricción es Hola restricción establece demasiado "Optimización" de forma predeterminada.

## <a name="upgrades"></a>Actualizaciones
Hola, Administrador de recursos del clúster también ayuda a durante la aplicación y las actualizaciones de clúster, durante el cual tiene dos tareas:

* Asegúrese de que no se ponga en peligro reglas Hola de clúster de Hola
* intente ir de toohelp Hola actualización sin problemas

### <a name="keep-enforcing-hello-rules"></a>Mantener exigir reglas de Hola
Hola lo más importante toobe en cuenta es que aún se aplican reglas de hello: Hola estricta las restricciones como restricciones de posición y las capacidades - durante las actualizaciones. Las restricciones de selección de ubicación garantizan que sus cargas de trabajo se ejecuten solamente donde tengan permiso para ello, incluso durante las actualizaciones. Cuando los servicios presentan elevadas restricciones, las actualizaciones pueden tardar más. Al servicio de Hola o se está ejecutando en el nodo de hello está inactivo para una actualización puede haber algunas opciones para donde puede perder.

### <a name="smart-replacements"></a>Sustituciones inteligentes
Cuando se inicia una actualización, Hola, Administrador de recursos toma una instantánea de la organización actual de Hola de clúster de Hola. Como cada dominio de actualización se complete, trata de los servicios de hello tooreturn creados en esta organización original de tootheir de actualización del dominio. Este modo a lo sumo hay dos transiciones para un servicio durante la actualización de Hola. Hay un movimiento fuera del nodo de hello afectado y uno retroceder. Devolver hello toohow de clúster o un servicio que tenía antes de actualización de hello también garantiza la actualización de hello no afecta al diseño de Hola de clúster de Hola. 

### <a name="reduced-churn"></a>Renovación reducida
Otra cosa que se produce durante las actualizaciones es ese hello desactiva el Administrador de recursos del clúster de equilibrio. Impide equilibrio evita la actualización de toohello de reacciones innecesarias, lo mismo que mover servicios en los nodos que se vacían para la actualización de Hola. Si la actualización de hello en cuestión es una actualización de clúster, clúster completo hello no está equilibrado durante la actualización de Hola. Comprobaciones de restricciones permanecen activas, movimiento solo en función de hello equilibrio automático de métricas está deshabilitado.

### <a name="buffered-capacity--upgrade"></a>Capacidad de búfer y actualización
En general, es conveniente toocomplete actualización Hola aunque clúster hello es toofull restringida o cerrar. Administración de la capacidad de Hola de clúster de hello es incluso más importante durante las actualizaciones de lo habitual. Función hello número de dominios de actualización, entre 5 y 20 por ciento de capacidad debe migrarse como hello actualización pone en clúster de Hola. Ese trabajo ha toogo en algún lugar. Esto es donde Hola noción de [almacenado en búfer capacidades](service-fabric-cluster-resource-manager-cluster-description.md#buffered-capacity) es útil. La capacidad almacenada en búfer se respeta durante el funcionamiento normal. Hola, Administrador de recursos del clúster puede llenar nodos tootheir capacidad total (consumiendo búfer hello) durante las actualizaciones si es necesario.

## <a name="next-steps"></a>Pasos siguientes
* Desde el principio de Hola y [obtener un servicio Administrador de recursos del clúster de tejido de toohello de introducción](service-fabric-cluster-resource-manager-introduction.md)
