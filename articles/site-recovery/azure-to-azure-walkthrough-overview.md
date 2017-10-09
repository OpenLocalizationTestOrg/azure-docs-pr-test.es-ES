---
title: "aaaReplicate máquinas virtuales de Azure entre regiones de Azure | Documentos de Microsoft"
description: "Resume Hola pasos necesarios tooreplicate máquinas virtuales de Azure entre regiones de Azure con el servicio de Azure Site Recovery Hola Hola portal de Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>Replicación de máquinas virtuales de Azure entre regiones con Azure Site Recovery

>Este artículo proporciona información general de hello pasos necesarios tooreplicate Azure máquinas virtuales (VM) en una región de Azure tooAzure máquinas virtuales en una región distinta. 

>[!NOTE]
>
> La replicación de VM de Azure se encuentra en una versión preliminar en este momento.

Envíe los comentarios y preguntas en parte inferior de este artículo o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="step-1-review-architecture"></a>Paso 1: Revisión de la arquitectura

Antes de empezar la implementación, revise arquitectura del escenario de Hola y componentes de Hola que necesita toodeploy.

Vaya demasiado[paso 1: revisar la arquitectura de Hola](azure-to-azure-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Paso 2: revisión de los requisitos previos

Compruebe que haya Hola requisitos previos de Azure en sitios, incluida una suscripción, redes virtuales, cuentas de almacenamiento y requisitos de máquina virtual.

Vaya demasiado[paso 2: comprobar los requisitos previos y limitaciones](azure-to-azure-walkthrough-prerequisites.md)


## <a name="step-3-plan-networking"></a>Paso 3: Planeamiento de redes

Compruebe que la conectividad saliente está configurado en máquinas virtuales de Azure que desee tooreplicate y que se configuran las conexiones desde el entorno local.

Vaya demasiado[paso 4: planear las redes](azure-to-azure-walkthrough-network.md)



## <a name="step-4-create-a-vault"></a>Paso 4: Creación de un almacén 

Necesita tooset seguridad un tooorchestrate de almacén de servicios de recuperación y administrar la replicación y especificar la región de origen de Hola.

Vaya demasiado[paso 4: crear un almacén](azure-to-azure-walkthrough-vault.md)


## <a name="step-5-enable-replication"></a>Paso 5: Habilitamiento de la replicación


replicación de tooenable, configurar opciones de ubicación de destino, configurar una directiva de replicación y seleccione hello en las máquinas virtuales de Azure que desea tooreplicate. Después de habilitar esta opción, se produce la replicación inicial de hello máquina virtual.

Vaya demasiado[paso 5: habilitar la replicación](azure-to-azure-walkthrough-enable-replication.md)


## <a name="step-6-run-a-test-failover"></a>Paso 6: Ejecución de una conmutación por error de prueba

Después de que finalice la replicación inicial y replicación de datos se está ejecutando, puede ejecutar una toomake de conmutación por error de prueba seguro de que todo funciona según lo previsto.

Vaya demasiado[paso 6: ejecutar una prueba de conmutación por error](azure-to-azure-walkthrough-test-failover.md)


