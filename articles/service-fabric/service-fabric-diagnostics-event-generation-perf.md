---
title: "aaaAzure supervisión del rendimiento de servicio de Fabric | Documentos de Microsoft"
description: "Obtenga información sobre los contadores de rendimiento para la supervisión y el diagnóstico de clústeres de Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a>Métricas de rendimiento

Las métricas deben ser recopilados toounderstand Hola rendimiento del clúster, así como aplicaciones de Hola que se ejecutan en él. Para los clústeres de Service Fabric, se recomienda recopilar Hola siguiendo los contadores de rendimiento.

## <a name="nodes"></a>Nodos

Para las máquinas de hello en el clúster, considere la posibilidad de recopilar Hola siguiendo los contadores de rendimiento toobetter comprender Hola carga de cada equipo y asegúrese de ajuste de escala en las decisiones de clúster correspondientes.

| Categoría de contador | Nombre del contador |
| --- | --- |
| Disco físico (por disco) | Prom. Longitud de la cola de lectura de disco |
| Disco físico (por disco) | Prom. Longitud de la cola de escritura de disco |
| Disco físico (por disco) | Prom. Segundos de disco/lecturas |
| Disco físico (por disco) | Prom. Segundos de disco/escrituras |
| Disco físico (por disco) | Lecturas de disco/s  |
| Disco físico (por disco) | Bytes de lectura de disco/s  |
| Disco físico (por disco) | Escrituras en disco/s |
| Disco físico (por disco) |  Bytes de escritura en disco/s |
| Memoria | MB disponibles |
| Archivo de paginación | % de uso |
| Proceso (total) | % de tiempo de procesador |
| Proceso (por servicio) | % de tiempo de procesador |
| Proceso (por servicio) | Id. de proceso |
| Proceso (por servicio) | Bytes privados |
| Proceso (por servicio) | Número de subprocesos |
| Proceso (por servicio) | Bytes virtuales |
| Proceso (por servicio) | Espacio de trabajo |
| Proceso (por servicio) | Espacio de trabajo privado |

## <a name="net-applications-and-services"></a>Aplicaciones y servicios .NET

Recopilar Hola después de contadores si va a implementar el clúster de .NET services tooyour. 

| Categoría de contador | Nombre del contador |
| --- | --- |
| Memoria CLR de .NET (por servicio) | Identificador del proceso |
| Memoria CLR de .NET (por servicio) | Número total de bytes confirmados |
| Memoria CLR de .NET (por servicio) | Número total de bytes reservados |
| Memoria CLR de .NET (por servicio) | Número de bytes en todos los montones |
| Memoria CLR de .NET (por servicio) | Número de colecciones de gen. 0 |
| Memoria CLR de .NET (por servicio) | Número de colecciones de gen. 1 |
| Memoria CLR de .NET (por servicio) | Número de colecciones de gen. 2 |
| Memoria CLR de .NET (por servicio) | % de tiempo del GC |

### <a name="service-fabrics-custom-performance-counters"></a>Contadores de rendimiento personalizados de Service Fabric

Service Fabric genera una cantidad considerable de contadores de rendimiento personalizados. Si tienes Hola SDK instalado, puede ver lista completa de hello en el equipo de Windows en la aplicación de Monitor de rendimiento (Inicio > Monitor de rendimiento). 

En las aplicaciones de hello están implementando tooyour clúster, si usas Reliable Actors, agregue countes de `Service Fabric Actor` y `Service Fabric Actor Method` categorías (vea [confiable actores diagnósticos del tejido servicio](service-fabric-reliable-actors-diagnostics.md)).

Si usa Reliable Services, del mismo modo tenemos las categorías de contadores `Service Fabric Service` y `Service Fabric Service Method` desde las cuales se deben recopilar los contadores. 

Si se usan colecciones confiables, se recomienda agregar hello `Avg. Transaction ms/Commit` de hello `Service Fabric Transactional Replicator` latencia de promedio de confirmación de hello toocollect por métrica de transacción.


## <a name="next-steps"></a>Pasos siguientes

* Obtenga más información sobre [generación de eventos en el nivel de la plataforma de hello](service-fabric-diagnostics-event-generation-infra.md) en Service Fabric
* Recopile las métricas de rendimiento mediante [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)
