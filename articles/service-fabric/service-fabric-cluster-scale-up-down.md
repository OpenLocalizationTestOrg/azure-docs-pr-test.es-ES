---
title: "aaaScale un tejido de servicio de clúster o alejar | Documentos de Microsoft"
description: "Escalar un clúster de Service Fabric o alejar petición toomatch las reglas de escalado automático para cada conjunto de escalas de máquina de tipo/Virtual de nodo. Agregar o quitar el clúster de nodos tooa Service Fabric"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: aeb76f63-7303-4753-9c64-46146340b83d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: 37cfeaf80edc016cf6de017d1c2dc6fbcb8acc2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-in-or-out-using-auto-scale-rules"></a>Escalado o reducción horizontal de un clúster de Service Fabric usando reglas de escalado automático
Conjuntos de escalas de máquina virtual son un recurso de proceso de Azure que puede usar toodeploy y administrar una colección de máquinas virtuales como un conjunto. Cada tipo de nodo que se define en un clúster de Service Fabric está configurado como un conjunto de escalado de máquinas virtuales independiente. Cada tipo de nodo se puede escalar o reducir horizontalmente de forma independiente. Cada uno cuenta con diferentes conjuntos de puertos abiertos y puede tener distintas métricas de capacidad. Obtenga más información en hello [Service Fabric nodetypes](service-fabric-cluster-nodetypes.md) documento. Puesto que los tipos de nodos de Service Fabric hello en el clúster se realizan de conjuntos de escalas de máquina Virtual en hello back-end, debe tooset las reglas de escalado automático para cada conjunto de escalas de máquina de tipo/Virtual de nodo.

> [!NOTE]
> La suscripción debe tener suficiente tooadd núcleos Hola nuevas máquinas virtuales que componen este clúster. Actualmente no hay ninguna validación del modelo, por lo que se obtendrá un error en tiempo de implementación, si se produce cualquiera de los límites de cuota de Hola.
> 
> 

## <a name="choose-hello-node-typevirtual-machine-scale-set-tooscale"></a>Elija Hola escalas de máquina Virtual/tipo de nodo conjunto tooscale
Actualmente, no toospecify capaz de reglas de escalado automático de Hola para conjuntos de escalas de máquina Virtual mediante el portal de hello, por lo que nos permiten usar tipos de nodos de Azure PowerShell (1.0 +) toolist hello y, a continuación, agregue toothem de reglas de escalado automático.

lista de hello tooget de máquina Virtual de conjunto de escalado que componen el clúster, ejecute hello siguientes cmdlets:

```powershell
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Compute/VirtualMachineScaleSets

Get-AzureRmVmss -ResourceGroupName <RGname> -VMScaleSetName <Virtual Machine scale set name>
```

## <a name="set-auto-scale-rules-for-hello-node-typevirtual-machine-scale-set"></a>Establecer reglas de escalado automático para el conjunto de escalas de máquina Virtual/tipo de hello nodo
Si el clúster tiene varios tipos de nodo, a continuación, repita que esto para cada nodo tipos/Virtual escalas de máquina establece que desee tooscale (entrante o saliente). Tenga en número de nodos Hola de cuenta que debe tener antes de configurar la escala automática. un mínimo de nodos que necesita para el tipo de nodo principal de Hola Hola está controlado por el nivel de confiabilidad de hello que ha elegido. Más información sobre los [niveles de confiabilidad](service-fabric-cluster-capacity.md).

> [!NOTE]
> Ajuste de escala hacia abajo que no requiere herramientas tipo de nodo principal de Hola de número mínimo de hello realizar clúster Hola inestable o quede fuera de servicio. Esto podría dar lugar a pérdida de datos para las aplicaciones y servicios de sistema de Hola.
> 
> 

Actualmente característica de escalado automático de hello no está controlada por cargas de Hola que las aplicaciones pueden estar encontrando tooService tejido. Por lo que en este Hola tiempo Autoescala que obtendrá puramente está controlada por los contadores de rendimiento de Hola que se emiten por cada una de las instancias de conjunto de escala de máquina Virtual de Hola.  

Siga estas instrucciones [tooset la escala automática para cada conjunto de escalas de máquina Virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview.md).

> [!NOTE]
> En una escala hacia abajo del escenario, a menos que el tipo de nodo tiene un nivel de durabilidad de oro o plata debe hello toocall [cmdlet Remove-ServiceFabricNodeState](https://msdn.microsoft.com/library/azure/mt125993.aspx) con el nombre de nodo apropiado Hola.
> 
> 

## <a name="manually-add-vms-tooa-node-typevirtual-machine-scale-set"></a>Agregar manualmente las máquinas virtuales tooa nodo tipo/Virtual conjunto de escalas de máquina
Siga Hola/instrucciones de ejemplo Hola [Galería de plantillas de inicio rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) número de hello toochange de máquinas virtuales en cada Nodetype. 

> [!NOTE]
> Adición de máquinas virtuales lleva tiempo, por lo que tiene previsto Hola adiciones toobe instantáneo. Por lo que planear la capacidad de tooadd también en el tiempo, tooallow durante más de 10 minutos antes de que está disponible para las réplicas de Hola Hola capacidad VM / tooget de instancias que se colocan de servicio.
> 
> 

## <a name="manually-remove-vms-from-hello-primary-node-typevirtual-machine-scale-set"></a>Quitar manualmente las máquinas virtuales de conjunto de escalas de máquina Virtual/tipo de hello nodo principal
> [!NOTE]
> servicios del sistema de tejido de servicio de Hola se ejecutan en el tipo de nodo principal de hello en el clúster. Por lo que nunca se debe apagar o reducir el número de Hola de instancias de los tipos de ese nodo menor que el nivel de confiabilidad de hello garantiza. Consulte demasiado[Hola obtener más información sobre los niveles de confiabilidad aquí](service-fabric-cluster-capacity.md). 
> 
> 

Necesita tooexecute Hola siguientes pasos le indican una instancia de máquina virtual a la vez. Esto permite que los servicios del sistema hello (y los servicios con estado) toobe cierra correctamente en la instancia de máquina virtual de hello va a quitar y las réplicas nuevas creadas en otros nodos.

1. Ejecutar [Disable-ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) con nodo de intención 'RemoveNode' toodisable Hola va tooremove (instancia más alto de hello en ese tipo de nodo).
2. Ejecutar [ServiceFabricNode Get](https://msdn.microsoft.com/library/mt125856.aspx) toomake seguro de ese nodo Hola realmente ha pasado toodisabled. De lo contrario, espere hasta que el nodo de hello está deshabilitado. Este paso no puede saltarse.
3. Siga Hola/instrucciones de ejemplo Hola [Galería de plantillas de inicio rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange número de Hola de máquinas virtuales en una unidad en ese Nodetype. instancia de Hello quitado es instancia de máquina virtual más alto de Hola. 
4. Repita los pasos del 1 al 3 según sea necesario, pero nunca reducir el número de Hola de instancias en hello tipos de nodos principales menor que garantiza que el nivel de confiabilidad de Hola. Consulte demasiado[Hola obtener más información sobre los niveles de confiabilidad aquí](service-fabric-cluster-capacity.md). 

## <a name="manually-remove-vms-from-hello-non-primary-node-typevirtual-machine-scale-set"></a>Quitar manualmente las máquinas virtuales de nodo no es el principal tipo/Virtual conjunto de escalas de máquina de Hola
> [!NOTE]
> Para un servicio con estado, necesita un cierto número de nodos toobe siempre el estado de disponibilidad y conservar toomaintain de su servicio. En hello mínimo, necesitará el número de Hola de recuento de conjunto de nodos toohello igual destino réplica de partición de Hola/service. 
> 
> 

Necesita Hola ejecutar Hola después de una instancia VM de pasos a la vez. Esto permite toobe cerrar correctamente en hello instancia de máquina virtual que se va a quitar servicios del sistema hello (y los servicios con estado) y las nuevas réplicas crean where else.

1. Ejecutar [Disable-ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) con nodo de intención 'RemoveNode' toodisable Hola va tooremove (instancia más alto de hello en ese tipo de nodo).
2. Ejecutar [ServiceFabricNode Get](https://msdn.microsoft.com/library/mt125856.aspx) toomake seguro de ese nodo Hola realmente ha pasado toodisabled. Si no se espere a que el nodo de hello está deshabilitado. Este paso no puede saltarse.
3. Siga Hola/instrucciones de ejemplo Hola [Galería de plantillas de inicio rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange número de Hola de máquinas virtuales en una unidad en ese Nodetype. Esto quitará ahora la instancia de máquina virtual más alto de Hola. 
4. Repita los pasos del 1 al 3 según sea necesario, pero nunca reducir el número de Hola de instancias en hello tipos de nodos principales menor que garantiza que el nivel de confiabilidad de Hola. Consulte demasiado[Hola obtener más información sobre los niveles de confiabilidad aquí](service-fabric-cluster-capacity.md).

## <a name="behaviors-you-may-observe-in-service-fabric-explorer"></a>Comportamientos que se pueden observar en Service Fabric Explorer
Al escalar una una Hola clúster Service Fabric Explorer reflejará número Hola de nodos (instancias de conjunto de escalas de máquina Virtual) que forman parte del clúster de Hola.  Sin embargo, al escalar un clúster hacia abajo se verán Hola quitar nodo/instancia de máquina virtual aparece en mal estado a menos que llame a [ServiceFabricNodeState Remove cmd](https://msdn.microsoft.com/library/mt125993.aspx) con el nombre de nodo apropiado Hola.   

Aquí es explicación Hola este comportamiento.

nodos que se enumeran en el Explorador de Service Fabric Hello son un reflejo de los servicios del sistema de Service Fabric hello (FM específicamente) sabe de número de Hola de nodos Hola clúster tenido/tiene. Al escalar Hola conjunto de escalas de máquina Virtual, se eliminó Hola VM pero servicio de sistema de FM aún piensa que se devolverán ese nodo hello (que estaba asignado toohello máquina virtual que se ha eliminado). Por lo que Service Fabric Explorer continúa toodisplay ese nodo (aunque el estado de mantenimiento de hello puede ser error o desconocido).

En orden toomake seguro de que un nodo se quita cuando se quita una máquina virtual, tiene dos opciones:

1) Elegir un nivel de durabilidad de oro o plata (disponible próximamente) para los tipos de nodo de hello en el clúster, que proporciona Hola integración de la infraestructura. Que, a continuación, quitará automáticamente nodos Hola desde el estado de servicios (FM) del sistema al reducir verticalmente.
Consulte demasiado[Hola detalles sobre los niveles de durabilidad aquí](service-fabric-cluster-capacity.md)

2) Una vez que se ha reducido en instancia de máquina virtual de hello, necesita hello toocall [cmdlet Remove-ServiceFabricNodeState](https://msdn.microsoft.com/library/mt125993.aspx).

> [!NOTE]
> Clústeres de tejido de servicio requieren un cierto número de nodos toobe seguridad en todo el tiempo de hello en orden toomaintain disponibilidad y se conserva el estado - tooas que se hace referencia "mantenga el quórum". Por lo tanto, es normalmente unsafe tooshut hacia abajo de todas las máquinas de hello en clúster de Hola a menos que primero ha llevado a cabo una [una copia de seguridad completa del estado del](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Hola de lectura sigue tooalso Aprenda a planear la capacidad del clúster, actualizar a un clúster y servicios de creación de particiones:

* [Consideraciones de planeación de capacidad del clúster de Service Fabric](service-fabric-cluster-capacity.md)
* [Actualización de un clúster de Service Fabric](service-fabric-cluster-upgrade.md)
* [Partición de Reliable Services de Service Fabric](service-fabric-concepts-partitioning.md)

<!--Image references-->
[BrowseServiceFabricClusterResource]: ./media/service-fabric-cluster-scale-up-down/BrowseServiceFabricClusterResource.png
[ClusterResources]: ./media/service-fabric-cluster-scale-up-down/ClusterResources.png
