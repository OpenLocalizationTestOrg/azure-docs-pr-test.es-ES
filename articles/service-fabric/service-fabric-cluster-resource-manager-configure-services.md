---
title: "configuración de métricas y la colocación de aaaSpecify en Azure microservicios | Documentos de Microsoft"
description: "Descripción de un servicio de Service Fabric mediante la especificación de métricas, restricciones de ubicación y otras directivas de ubicación."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 16e135c1-a00a-4c6f-9302-6651a090571a
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c633518b5dbf0c7b84e0d46c06bf1f92365d184d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-cluster-resource-manager-settings-for-service-fabric-services"></a>Configuración de Cluster Resource Manager para los servicios de Service Fabric
Hola, Administrador de recursos de clúster de tejido de servicio permite el control exhaustivo sobre las reglas de Hola que rigen a cada usuario individual con el nombre de servicio. Cada servicio que desee puede especificar reglas de cómo se debe asignar en clúster de Hola. Cada servicio con nombre también puede definir el conjunto de Hola de métricas que desea tooreport, incluida la importancia son toothat del servicio. La configuración de los servicios se divide en tres tareas distintas:

1. Configuración de restricciones de colocación
2. Configuración de métricas
3. Configuración de directivas de ubicación avanzadas (menos frecuentes)

## <a name="placement-constraints"></a>Restricciones de selección de ubicación
Las restricciones de posición son utilizado toocontrol qué nodos de clúster de hello realmente puede ejecutar un servicio en. Llama normalmente una determinada instancia de servicio o todos los servicios de un toorun determinado tipo restringido en un determinado tipo de nodo. Las restricciones de colocación son extensibles. Puede definir cualquier conjunto de propiedades por tipo de nodo y luego seleccionar para ellas restricciones al crear servicios. También puede cambiar las restricciones de colocación de un servicio mientras se ejecuta. Esto le permite toorespond toochanges en clúster de Hola o requisitos de hello del servicio de Hola. Hola propiedades de un nodo determinado también se pueden actualizar dinámicamente en clúster de Hola. Más información sobre las restricciones de posición y cómo tooconfigure ellos pueden encontrarse en [este artículo](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)

## <a name="metrics"></a>Métricas
Las métricas son conjunto de Hola de recursos que necesita un servicio con nombre determinado. La configuración de las métricas de un servicio incluye la cantidad de ese recurso que cada réplica con estado o instancia sin estado de ese servicio consume de forma predeterminada. Métricas también incluyen una ponderación que indica la importancia equilibrio esa métrica toothat servicio, en caso de compensaciones son necesarios.

## <a name="advanced-placement-rules"></a>Reglas de colocación avanzadas
Existen otros tipos de reglas de colocación que son útiles en escenarios menos comunes. A continuación, se indican algunos ejemplos:
- Restricciones que ayudan con los clústeres distribuidos geográficamente
- Determinadas arquitecturas de aplicaciones

Otras reglas de ubicación se configuran mediante correlaciones o directivas.

## <a name="next-steps"></a>Pasos siguientes
- Las métricas son cómo Hola, Administrador de recursos de clúster de tejido de servicio administra capacidad en clúster de Hola y consumo. toolearn más información acerca de las métricas y cómo tooconfigure, visite [este artículo](service-fabric-cluster-resource-manager-metrics.md)
- Afinidad es un modo en que puede configurar los servicios. No es muy común, pero si lo necesita puede encontrar información [aquí](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
- Hay muchas reglas de selección de ubicación diferentes que se pueden configurar en los escenarios adicionales de toohandle de servicio. Puede encontrar información sobre esas directivas de colocación diferentes [aquí](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)
- Desde el principio de Hola y [obtener un servicio Administrador de recursos del clúster de tejido de toohello de introducción](service-fabric-cluster-resource-manager-introduction.md)
- toofind out acerca de cómo Hola, Administrador de recursos del clúster administra y equilibra la carga en el clúster de hello, desproteger artículo hello en [equilibrio de carga](service-fabric-cluster-resource-manager-balancing.md)
- Hola, Administrador de recursos del clúster tiene muchas opciones para describir el clúster de Hola. toofind más información acerca de ellos, consulte este artículo en [que describe un clúster de Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
