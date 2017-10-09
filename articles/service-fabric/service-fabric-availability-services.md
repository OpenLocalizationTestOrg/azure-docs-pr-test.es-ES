---
title: aaaAvailability de servicios de Service Fabric | Documentos de Microsoft
description: "Describe la detección de errores, la conmutación por error y la recuperación para los servicios"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 279ba4a4-f2ef-4e4e-b164-daefd10582e4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c443aadfe31a1413359b08d34c4b7dd5db4edd16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="availability-of-service-fabric-services"></a>Disponibilidad de los servicios de Service Fabric
En este artículo se ofrece una visión general de cómo Service Fabric mantiene la disponibilidad de un servicio.

## <a name="availability-of-service-fabric-stateless-services"></a>Disponibilidad de los servicios sin estado de Service Fabric
Los servicios de Service Fabric de Azure pueden ser con o sin estado. Un servicio sin estado es un servicio de aplicación que no tenga ningún [estado local](service-fabric-concepts-state.md) que necesita toobe altamente disponible y confiable.

Para crear un servicio sin estado, es necesario definir `InstanceCount`. recuento de instancias de Hello define número Hola de instancias del servicio sin estado Hola lógica de aplicación que debe estar ejecutándose en el clúster de Hola. Aumentar el número de Hola de instancias es Hola recomendada la forma de escalar horizontalmente un servicio sin estado.

Cuando se produce un error en una instancia de un estado con el nombre de servicio, se crea una nueva instancia en alguno de los nodos en clúster de hello elegible. Por ejemplo, una instancia de servicio sin estado podría producir error en el Nodo1 y crearse de nuevo en el Nodo5.

## <a name="availability-of-service-fabric-stateful-services"></a>Disponibilidad de los servicios con estado de Service Fabric
Un servicio con estado tiene algún estado asociado a él. En Service Fabric, un servicio con estado se modela como un conjunto de réplicas. Cada réplica es una instancia en ejecución de código de hello del servicio de Hola que también tiene una copia del estado de Hola para ese servicio. Operaciones de lectura y escritura se realizan en una réplica (llamada hello principal). Toostate de cambios de las operaciones de escritura son *replican* toohello otras réplicas del conjunto de réplicas de hello (denominado secundarias activas) y aplicar. 

Solo puede haber una réplica principal, pero puede haber varias réplicas secundarias activas. número de Hola de réplicas secundarias activas es configurable y un mayor número de réplicas puede tolerar un mayor número de errores de hardware y software simultáneo.

Si la réplica principal de hello deja de funcionar, Service Fabric realiza una de hello secundarias activas réplicas Hola nueva réplica principal. Esta réplica secundaria activa ya tiene la versión de Hola actualizado del estado de hello (a través de *replicación*), y se puede continuar con el procesamiento de lectura adicional y las operaciones de escritura.

Este concepto, de una réplica es un principal o secundaria activa, se conoce como Hola rol de réplica.

### <a name="replica-roles"></a>Roles de réplica
rol de Hola de una réplica es ciclo de vida de hello toomanage usado de estado de hello está administrado por esa réplica. Una réplica cuyo rol sea solicitudes de lectura de servicios principales. Hola principal también controla todas las solicitudes de escritura al actualizar su estado y replicar cambios de Hola. Estos cambios son toohello aplicado secundarias activas en el conjunto de réplicas de Hola. trabajo de Hola de una secundaria activa es cambios de estado de tooreceive que Hola réplica principal se ha replicado y actualizar la vista de estado de Hola.

> [!NOTE]
> Modelos de programación de nivel superior como [Reliable Actors](service-fabric-reliable-actors-introduction.md) y [servicios confiables](service-fabric-reliable-services-introduction.md) ocultar el concepto de Hola de rol de réplica del programador de Hola. En actores, noción de Hola de rol es innecesario, mientras en los servicios se ha simplificado en gran medida para la mayoría de los escenarios.
>

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre conceptos de Service Fabric, vea Hola siguientes artículos:

- [Escalado de aplicaciones de Service Fabric](service-fabric-concepts-scalability.md)
- [Creación de particiones de los servicios de Service Fabric](service-fabric-concepts-partitioning.md)
- [Definición y administración del estado](service-fabric-concepts-state.md)
- [Reliable Services](service-fabric-reliable-services-introduction.md)
