---
title: aaaAzure canal del servicio de Fabric Operational | Documentos de Microsoft
description: "Lista completa de los registros generados en clústeres de hello canal operativa de Azure Service Fabric."
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
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: 358782420ed62b202d6a89fe0f200b5ef0384c9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="operational-channel"></a>Canal operativo 

canal operativo Hola consta de registros de alto nivel acciones llevadas a cabo por Service Fabric en los nodos y el clúster. Cuando está habilitada "Diagnostics" para un clúster, Hola agente de diagnóstico de Azure se implementa en el clúster y de forma predeterminada está configurado tooread en registros de canal operativo Hola. Obtener más información acerca de la configuración de hello [agente de diagnóstico de Azure](service-fabric-diagnostics-event-aggregation-wad.md) configuración de diagnóstico de hello toomodify de su toopick de clúster más registros o los contadores de rendimiento. 

## <a name="operational-channel-logs"></a>Registros de canal operativo 

Esta es una lista completa de registros proporcionada por Service Fabric en canal operativo Hola. 

| EventId | Nombre | Origen (tarea) | Nivel |
| --- | --- | --- | --- |
| 25620 | NodeOpening | FabricNode | Informativo |
| 25621 | NodeOpenedSuccess | FabricNode | Informativo |
| 25622 | NodeOpenedFailed | FabricNode | Informativo |
| 25623 | NodeClosing | FabricNode | Informativo |
| 25624 | NodeClosed | FabricNode | Informativo |
| 25625 | NodeAborting | FabricNode | Informativo |
| 25626 | NodeAborted | FabricNode | Informativo |
| 29627 | ClusterUpgradeStart | CM | Informativo |
| 29628 | ClusterUpgradeComplete | CM | Informativo |
| 29629 | ClusterUpgradeRollback | CM | Informativo |
| 29630 | ClusterUpgradeRollbackComplete | CM | Informativo |
| 29631 | ClusterUpgradeDomainComplete | CM | Informativo |
| 23074 | ContainerActivated | Hospedaje | Informativo |
| 23075 | ContainerDeactivated | Hospedaje | Informativo |
| 29620 | ApplicationCreated | CM | Informativo |
| 29621 | ApplicationUpgradeStart | CM | Informativo |
| 29622 | ApplicationUpgradeComplete | CM | Informativo |
| 29623 | ApplicationUpgradeRollback | CM | Informativo |
| 29624 | ApplicationUpgradeRollbackComplete | CM | Informativo |
| 29625 | ApplicationDeleted | CM | Informativo |
| 29626 | ApplicationUpgradeDomainComplete | CM | Informativo |
| 18566 | ServiceCreated | FM | Informativo |
| 18567 | ServiceDeleted | FM | Informativo |

## <a name="next-steps"></a>Pasos siguientes

* Obtener más información sobre global [generación de eventos en el nivel de la plataforma de hello](service-fabric-diagnostics-event-generation-infra.md) en Service Fabric
* Modificar el [diagnósticos de Azure](service-fabric-diagnostics-event-aggregation-wad.md) más registros de configuración toocollect
* [Configuración de Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) toosee su canal operativo registros
